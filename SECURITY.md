# Security Policy

## Reporting a Vulnerability

AILP is a protocol specification. Vulnerabilities in the protocol design — such as mechanisms that could be exploited to manipulate rankings, forge certificates, conduct Sybil listing attacks, or violate data ownership — are taken seriously.

### How to Report

- **GitHub**: Open a [Security Advisory](https://github.com/AIXP-Labs/AILP/security/advisories/new) (private)
- **Title**: `[AILP-SECURITY] Brief description`

### Response Timeline

| Action | Timeline |
|--------|----------|
| Acknowledgment | Within 48 hours |
| Initial assessment | Within 7 days |
| Resolution plan | Within 30 days |
| Public disclosure | After fix, or 90 days |

### Scope

In scope:
- Ranking manipulation vectors (bypassing quality-based ranking)
- Certificate forgery or verification bypass
- Sybil listing attacks (fake Bot registrations)
- Data ownership violations (Yellow Page claiming Bot data)
- Sync protocol exploits (poisoning inter-Yellow-Page sync)
- Privacy boundary circumvention
- Axiom 0 bypass mechanisms

Out of scope:
- Specific Yellow Page implementation bugs (report to the implementer)
- General email/DNS security issues
- AIBP/AIVP protocol issues (report to those projects)

---

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AILP V1.0.0. www.ailp.dev
