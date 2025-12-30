# CI Pipeline Gotchas

**Repository:** xonaix-ops
**Scope:** xonaix-core CI under GitHub organization rulesets
**Last Updated:** 2025-12-24
**Origin:** Phase 0 baseline closure (B-5.8.4)

---

## Scope & Intent

This document captures **operational gotchas**—non-obvious CI, GitHub, and Rust tooling pitfalls encountered during Phase 0 baseline work.

This is **not** a specification. It is a runbook for engineers who will inevitably encounter these same failure modes and wonder why their CI is broken.

**Applies to:**
- xonaix-core repository
- GitHub Actions workflows
- GitHub organization rulesets
- Rust security and audit tooling

---

## Rust Security Tooling

### cargo-deny >= 0.14 Deprecated Keys

As of cargo-deny 0.14, several configuration keys were removed. Using them causes immediate failure with `error[deprecated]`.

**Removed keys in `[advisories]`:**
- `vulnerability`
- `unmaintained`
- `notice`

**Removed keys in `[licenses]`:**
- `unlicensed`
- `default`
- `copyleft`

**Before (broken):**
```toml
[advisories]
vulnerability = "deny"
unmaintained = "warn"
notice = "warn"

[licenses]
unlicensed = "deny"
default = "deny"
copyleft = "deny"
```

**After (working):**
```toml
[advisories]
db-path = "~/.cargo/advisory-db"
db-urls = ["https://github.com/rustsec/advisory-db"]
yanked = "deny"
# vulnerability, unmaintained, notice removed (cargo-deny 0.14+)
# Vulnerabilities denied by default; others use built-in defaults

[licenses]
confidence-threshold = 0.93
# unlicensed, default, copyleft removed (cargo-deny 0.14+)
# Relies on allow list; unlisted licenses denied by default

allow = [
    "MIT",
    "Apache-2.0",
    # ... your allowed licenses
    "LicenseRef-Proprietary",  # For your own crates
]
```

**Reference:** https://github.com/EmbarkStudios/cargo-deny/pull/611

### cargo-deny-action Version

**Use `v2`, not `v1`.**

The v1 action bundles an older cargo-deny that cannot parse CVSS 4.0 advisory formats. When the RustSec advisory database includes CVSS 4.0 entries, v1 fails with:

```
error: failed to load advisory database: parse error: unsupported CVSS version: 4.0
```

**Correct workflow configuration:**
```yaml
- name: Run cargo-deny
  uses: EmbarkStudios/cargo-deny-action@v2  # NOT v1
  with:
    command: check
    arguments: --all-features
```

---

## SBOM Generation

### Correct cargo-sbom Output Format

The `cargo-sbom` tool uses underscores and version suffixes in format names. The intuitive name does not work.

**Wrong:**
```yaml
run: cargo sbom --output-format cyclonedx_json > sbom.json
```

**Correct:**
```yaml
run: cargo sbom --output-format cyclone_dx_json_1_6 > sbom.json
```

**Available formats:**
- `spdx_json_2_3`
- `cyclone_dx_json_1_4`
- `cyclone_dx_json_1_5`
- `cyclone_dx_json_1_6`

The error message helpfully suggests the correct format, but only after failing.

---

## Gitleaks in GitHub Organizations

### GITLEAKS_LICENSE Requirement

For **GitHub organizations** (not personal accounts), gitleaks-action v2 requires a paid license.

**Error without license:**
```
[xonaix] is an organization. License key is required.
🛑 missing gitleaks license. Go grab one at gitleaks.io...
```

**Obtaining a license:**
1. Go to https://gitleaks.io
2. Purchase/obtain a license key
3. You will receive the key via email

### Where to Store the Secret

The secret can be stored at either level:

| Location | Path | Use Case |
|----------|------|----------|
| **Organization** | `github.com/organizations/{org}/settings/secrets/actions` | Multiple repos need it |
| **Repository** | `github.com/{org}/{repo}/settings/secrets/actions` | Single repo only |

**Secret name must be:** `GITLEAKS_LICENSE`

### Explicit Environment Passing

The secret must be **explicitly passed** to the action. It is not automatically available.

**Wrong (secret exists but not passed):**
```yaml
- name: Run Gitleaks
  uses: gitleaks/gitleaks-action@v2
  env:
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

**Correct:**
```yaml
- name: Run Gitleaks
  uses: gitleaks/gitleaks-action@v2
  env:
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
    GITLEAKS_LICENSE: ${{ secrets.GITLEAKS_LICENSE }}
```

### Required Workflow Permissions

Gitleaks scans PR commits via the GitHub API. The default `GITHUB_TOKEN` permissions are insufficient.

**Error without permissions:**
```
RequestError [HttpError]: Resource not accessible by integration
status: 403
'x-accepted-github-permissions': 'pull_requests=read'
```

**Required job-level permissions:**
```yaml
gitleaks:
  name: Secret Detection
  runs-on: ubuntu-latest
  permissions:
    contents: read
    pull-requests: read  # Required for PR commit scanning
  steps:
    - uses: actions/checkout@v4
      with:
        fetch-depth: 0
    - name: Run Gitleaks
      uses: gitleaks/gitleaks-action@v2
      env:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        GITLEAKS_LICENSE: ${{ secrets.GITLEAKS_LICENSE }}
```

---

## GitHub Rulesets vs Branch Protection

### These Are Different Systems

GitHub has **two** branch protection mechanisms that look similar but are configured separately and have different capabilities.

| Feature | Branch Protection | Repository Rulesets |
|---------|-------------------|---------------------|
| Configuration path | `/settings/branches` | `/settings/rules` or `/rules/{id}` |
| API endpoint | `/branches/{branch}/protection` | `/rulesets` |
| Bypass mechanism | "Allow specified actors to bypass" | "Bypass list" with granular control |
| Status checks | Case-insensitive (legacy) | **Case-sensitive** |
| Scope | Single branch pattern | Multiple branch patterns |

### Status Check Names Are Case-Sensitive in Rulesets

This is the most common failure mode. Rulesets enforce **exact string matching** on status check names.

**Example failure:**
- Ruleset requires: `check`, `clippy`, `fmt`, `test`
- CI produces: `Check`, `Clippy`, `Format`, `Test`
- Result: **Merge blocked** ("4 of 4 required status checks are expected")

**Diagnosis:**
```bash
# Check what your CI actually produces
gh pr view {number} --json statusCheckRollup --jq '.statusCheckRollup[].name'

# Check what the ruleset expects
gh api repos/{owner}/{repo}/rulesets/{id} --jq '.rules[] | select(.type=="required_status_checks") | .parameters.required_status_checks[].context'
```

**Fix:** Update the ruleset to match exact CI job names, or rename CI jobs to match the ruleset.

### Admin Bypass May Not Work

Rulesets can be configured with `current_user_can_bypass: "never"`, which blocks even organization owners.

**To allow bypass:**
1. Go to the ruleset configuration
2. Add yourself (or a team) to the "Bypass list"
3. Or temporarily set "Enforcement status" to "Disabled"

---

## Lessons Learned

### Why This Pain Surfaced in Phase 0

Phase 0 was the first time we:
- Pushed to protected branches in an organization context
- Ran the full CI matrix on real PRs
- Exercised GitHub's security tooling requirements

This pain was **expected and correct**. The alternative—discovering these issues during feature development or in production—would have been far more expensive.

### Why This Is Actually Good

The fact that:
- CI caught configuration errors immediately
- Rulesets enforced merge discipline
- Tooling failed loudly with actionable errors

...is evidence that the governance model is working. These are the exact failure modes that catch real problems later.

### Why Document It

Without this document, a future engineer will:
1. Encounter the same cryptic error
2. Spend 30-60 minutes debugging
3. Fix it locally
4. Not document it
5. The next engineer repeats steps 1-4

This runbook breaks that cycle.

---

## Quick Reference

```yaml
# Complete working gitleaks job
gitleaks:
  name: Secret Detection
  runs-on: ubuntu-latest
  permissions:
    contents: read
    pull-requests: read
  steps:
    - uses: actions/checkout@v4
      with:
        fetch-depth: 0
    - name: Run Gitleaks
      uses: gitleaks/gitleaks-action@v2
      env:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        GITLEAKS_LICENSE: ${{ secrets.GITLEAKS_LICENSE }}

# Complete working cargo-deny job
deny:
  name: Cargo Deny
  runs-on: ubuntu-latest
  steps:
    - uses: actions/checkout@v4
    - name: Run cargo-deny
      uses: EmbarkStudios/cargo-deny-action@v2
      with:
        command: check
        arguments: --all-features

# Complete working SBOM job
sbom:
  name: Generate SBOM
  runs-on: ubuntu-latest
  steps:
    - uses: actions/checkout@v4
    - uses: dtolnay/rust-toolchain@stable
    - run: cargo install cargo-sbom
    - run: cargo sbom --output-format cyclone_dx_json_1_6 > sbom.json
```

---

## Changelog

| Date | Change | Author |
|------|--------|--------|
| 2025-12-24 | Initial creation from Phase 0 learnings | Claude Code |
