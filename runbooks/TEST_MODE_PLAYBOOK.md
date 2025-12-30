# Test Mode Playbook

**Version:** 1.0.0  
**Effective:** 2025-12-24  
**Authority:** Founder + GPT/Claude consensus  
**Status:** ACTIVE

---

## Purpose

This playbook defines the operational boundaries, data handling requirements, and behavioral expectations when Xonaix Core operates in **TEST MODE**. It is designed to protect real users, ensure audit compliance, and prevent test artifacts from contaminating production.

---

## Mode Definitions

### TEST MODE

A system state where:
- Synthetic or explicitly marked test data is used
- Verbose error output is enabled
- All actions are logged at DEBUG level
- No real user PII is processed
- Failures are surfaced immediately (no silent recovery)

### PRODUCTION MODE

A system state where:
- Real user data may be processed
- Error output is controlled and sanitized
- Logging follows retention policies
- PII handling follows data classification rules
- Graceful degradation is permitted where safe

---

## Trust Posture Mapping

TEST MODE operates under explicitly defined trust postures as specified in:

```
foundation/specs/B-5.8.4/05.Nexus/TRUST_POSTURES.md
```

TEST MODE defaults to:

| Posture | Setting | Rationale |
|---------|---------|-----------|
| Transparency | **Maximum** | All internal state visible for debugging |
| Failure behavior | **Fail-closed** | Errors halt execution, never suppressed |
| Recovery | **No silent recovery** | All recovery actions logged and surfaced |
| Trust level | **Explicit distrust** | Assume all inputs are adversarial |

**Any deviation from these defaults must be documented in the test record.**

---

## Synthetic Data Requirements

### What is Synthetic Data?

Data that is:
- Artificially generated for testing purposes
- Contains no real user information
- Clearly marked as synthetic

### Requirements

1. **No real PII in test environments** — Ever. No exceptions.

2. **Synthetic data must be marked** — All synthetic records must include:
   - A `synthetic: true` flag or equivalent
   - A prefix/suffix identifier (e.g., `TEST_`, `_SYNTHETIC`)
   - Timestamp of generation

3. **Synthetic data sources must be documented** — How was it generated? By whom? When?

---

## Test Artifact Management

### Identification

Test artifacts MUST be identifiable by:

| Artifact Type | Identification Method |
|---------------|----------------------|
| Database records | `environment: test` field or `TEST_` prefix |
| Log files | Filename includes `_test_` or stored in `/test/` path |
| API responses | Header `X-Xonaix-Environment: test` |
| Files/exports | Filename includes `_TEST_` or `_SYNTHETIC_` |

### Purging

Test data MUST be purged:

| Trigger | Action |
|---------|--------|
| Test session ends | Ephemeral data deleted within 24 hours |
| Test cycle complete | All test artifacts archived or deleted within 7 days |
| Before production deploy | Verification that no test data exists in prod environment |

### Contamination Prevention

To prevent test data from contaminating production:

1. **Separate environments** — Test and production databases are physically separate
2. **No shared credentials** — Test credentials cannot access production
3. **Environment checks** — Code must verify environment before writes
4. **Audit on deploy** — Pre-deploy checklist includes test data verification

---

## Error Surfacing Policy

### In TEST MODE

| Error Type | Behavior |
|------------|----------|
| Validation errors | Full detail + stack trace |
| Business logic errors | Full detail + context |
| System errors | Full detail + stack trace + system state |
| Security errors | Full detail (no redaction in test) |

### In PRODUCTION MODE

| Error Type | Behavior |
|------------|----------|
| Validation errors | User-friendly message only |
| Business logic errors | User-friendly message + error code |
| System errors | Generic message + incident ID |
| Security errors | Minimal disclosure + silent alert |

---

## Log Retention Policy

| Environment | Log Level | Retention |
|-------------|-----------|-----------|
| TEST MODE | DEBUG | 7 days |
| TEST MODE | INFO+ | 30 days |
| PRODUCTION MODE | INFO+ | 90 days |
| PRODUCTION MODE | ERROR+ | 1 year |

### Log Content Rules

**In TEST MODE:**
- Full request/response bodies (if no real PII)
- Full stack traces
- Internal state dumps
- Performance metrics

**In PRODUCTION MODE:**
- Sanitized request/response (PII redacted)
- Error codes only (no stack traces to users)
- Aggregated metrics only
- Incident IDs for correlation

---

## Tester Onboarding Checklist

Before a tester accesses Xonaix Core in TEST MODE:

- [ ] Tester has signed NDA (if external)
- [ ] Tester understands this is TEST MODE (not production)
- [ ] Tester has received synthetic test credentials
- [ ] Tester knows how to report issues (GitHub, email, etc.)
- [ ] Tester understands data is synthetic and will be purged
- [ ] Tester has read relevant sections of B-5.8.4 specs (if technical)

---

## Incident Escalation During Testing

| Severity | Description | Response |
|----------|-------------|----------|
| **Low** | Minor UI issue, typo, cosmetic | Log in GitHub Issues |
| **Medium** | Functional bug, incorrect behavior | Log + notify Founder within 24h |
| **High** | Data integrity issue, security concern | Immediate Founder notification |
| **Critical** | System crash, potential vulnerability | Immediate halt + Founder notification |

### Escalation Contacts

| Role | Contact Method |
|------|----------------|
| Founder | Direct message (preferred) |
| Claude (AI) | Via Claude Code / chat |
| GPT (AI) | Via GPT chat |

---

## Test Record Requirements

Every test session SHOULD produce a record containing:

1. **Session metadata** — Date, tester, environment, duration
2. **Test scope** — What was tested
3. **Results** — Pass/fail, issues found
4. **Artifacts** — Links to logs, screenshots, exports
5. **Deviations** — Any deviations from standard trust postures

Records are stored in `xonaix-ops/docs/test-records/` (to be created when testing begins).

---

## Transition to Production

Before any component moves from TEST to PRODUCTION:

- [ ] All test data purged from target environment
- [ ] Environment variables set to production values
- [ ] Logging level reduced to INFO
- [ ] Error output sanitized
- [ ] Trust postures reviewed and adjusted
- [ ] Security review completed
- [ ] Founder sign-off obtained

---

## Change History

| Date | Version | Change |
|------|---------|--------|
| 2025-12-24 | 1.0.0 | Initial playbook established |

---

*This playbook is part of the Xonaix operational framework. Compliance protects users, testers, and the company.*

**The Xonaix Way: No debt. No shortcuts. Correctness first.**
