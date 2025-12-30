# Workstation Golden State Contract

**Version:** 1.0.1  
**Effective:** 2025-12-24  
**Authority:** Founder + GPT/Claude consensus  
**Status:** ACTIVE

---

## Purpose

This contract establishes the **minimum required state** for any development workstation used to build, test, or release Xonaix Core. The companion inventory document (`WORKSTATION_INVENTORY.md`) serves as the reference implementation.

Compliance with this contract is mandatory. Deviations must be documented and approved.

---

## Applicability & Scope

This contract applies to:

- **The Founder**
- **Any future contributors with commit access**
- **Any machine used to build, test, or release `xonaix-core`**

CI is authoritative for enforcement where possible; local verification is mandatory before first commit.

---

## Mandatory Tools

The following tools MUST be installed and functional:

### Rust Toolchain

| Tool | Minimum Version | Verification |
|------|-----------------|--------------|
| rustc | 1.92.0 | `rustc --version` |
| cargo | 1.92.0 | `cargo --version` |
| clippy | (bundled) | `cargo clippy --version` |
| rustfmt | (bundled) | `cargo fmt --version` |
| rust-analyzer | (bundled) | `rustup component list --installed` |

### Cargo Tools

| Tool | Purpose | Verification |
|------|---------|--------------|
| cargo-nextest | Fast test runner | `cargo nextest --version` |
| cargo-audit | Vulnerability scanning | `cargo audit --version` |
| cargo-deny | License/advisory compliance | `cargo deny --version` |

### Security Tools

| Tool | Purpose | Verification |
|------|---------|--------------|
| gitleaks | Secret detection | `gitleaks version` |
| trivy | Vulnerability scanning | `trivy --version` |

### Version Control

| Tool | Purpose | Verification |
|------|---------|--------------|
| git | Source control | `git --version` |
| gh | GitHub CLI | `gh --version` |

---

## Version Pinning Policy

1. **`rust-toolchain.toml` is authoritative** — The version specified in `xonaix-core/rust-toolchain.toml` is the required Rust version.

2. **Upgrades require justification** — Rust toolchain upgrades must be:
   - Tested against CI
   - Documented in a PR
   - Approved by Founder

3. **Downgrades are prohibited** — Using an older toolchain than specified is not permitted.

---

## Security Tool Policy

1. **Security tools may not be removed** without explicit Founder approval.

2. **Security tools must be current** — Keep gitleaks and trivy updated to latest stable.

3. **SSH key policy** — Passphrase-less SSH keys are permitted on single-user, non-mobile, disk-encrypted development workstations.

4. **Pre-commit verification** — Before any commit to `xonaix-core`, verify:
   - `cargo clippy` passes
   - `cargo fmt --check` passes
   - `gitleaks detect --source .` reports no findings

---

## Environment Parity

**Local environment parity with CI is required; CI failures override local success.**

This means:
- If CI fails but local passes, the code is **not ready**
- "Works on my machine" is not a valid defense
- CI configuration is the source of truth

---

## Deviation Policy

Any deviation from this contract MUST be:

1. **Documented** — Written explanation of what and why
2. **Temporary** — With a remediation plan
3. **Approved** — By Founder (Phase 0) or designated reviewer (Phase 1+)

Undocumented deviations are grounds for rejecting PRs.

---

## Verification Requirement

Before first commit to any Xonaix repository:

1. Run `Verify-XonaixWorkstation.ps1`
2. All checks must pass (warnings acceptable, failures not)
3. Screenshot or log output retained for audit if requested

---

## Audit Trail

The following must be retained:

| Item | Location | Retention |
|------|----------|-----------|
| Workstation inventory | `xonaix-ops/runbooks/WORKSTATION_INVENTORY.md` | Permanent |
| Verification logs | Local (on request) | 90 days minimum |
| Secret rotation records | Secure notes | Permanent |

---

## Enforcement

| Phase | Enforcement |
|-------|-------------|
| Phase 0 | Founder self-enforces; honor system |
| Phase 1+ | CI gates + PR review |
| External contributors | Must demonstrate compliance before access |

---

## Change History

| Date | Version | Change |
|------|---------|--------|
| 2025-12-24 | 1.0.0 | Initial contract established |
| 2025-12-24 | 1.0.1 | Added SSH key policy for passphrase-less keys |

---

*This contract is part of the Xonaix governance framework. Compliance is not optional.*

**The Xonaix Way: No debt. No shortcuts. Correctness first.**
