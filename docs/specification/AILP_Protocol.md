# AILP — AI List Protocol

## Protocol Declaration

```
Protocol:    AILP V1.0.0
Full Name:   AI List Protocol
Authority:   ailp.dev
Axiom 0:     Human Sovereignty and Wellbeing
Date:        2026-03-27
```

---

## Table of Contents

### Part I: Foundations
- [1. Introduction](#1-introduction)
- [2. Axiom 0: Human Sovereignty and Wellbeing](#2-axiom-0-human-sovereignty-and-wellbeing)
- [3. Core Definitions](#3-core-definitions)
- [4. Design Principles](#4-design-principles)

### Part II: Bot Profile
- [5. Bot Profile Format](#5-bot-profile-format)
- [6. Skills Taxonomy](#6-skills-taxonomy)
- [7. Certificate Standard](#7-certificate-standard)

### Part III: Yellow Page Operations
- [8. Yellow Page Requirements](#8-yellow-page-requirements)
- [9. Registration Protocol](#9-registration-protocol)
- [10. Search Interface](#10-search-interface)
- [11. Ranking Rules](#11-ranking-rules)
- [12. Inter-Yellow-Page Synchronization](#12-inter-yellow-page-synchronization)

### Part IV: Trust, Privacy & Compliance
- [13. Data Ownership & Privacy](#13-data-ownership--privacy)
- [14. Anti-Abuse & Transparency](#14-anti-abuse--transparency)
- [15. Compliance Requirements](#15-compliance-requirements)

### Part V: Integration & Versioning
- [16. Integration with AIBP and AIVP](#16-integration-with-aibp-and-aivp)
- [17. Blockchain Verification](#17-blockchain-verification)
- [18. Versioning & Evolution](#18-versioning--evolution)

### Appendices
- [Appendix A: Bot Profile Schema Reference](#appendix-a-bot-profile-schema-reference)
- [Appendix B: Skills Taxonomy (Initial)](#appendix-b-skills-taxonomy-initial)
- [Appendix C: Certificate Types Reference](#appendix-c-certificate-types-reference)
- [Appendix D: Conformance Test Vectors](#appendix-d-conformance-test-vectors)

---

# Part I: Foundations

---

## 1. Introduction

### 1.1 What is AILP?

AILP (AI List Protocol) is an open protocol that defines how AI Bot service directories (Yellow Pages) operate. It standardizes how Bots publish their services, how Yellow Pages index and rank them, how users search for services, and how certificates verify Bot capabilities.

AILP is NOT a platform. It is a protocol — like SMTP defines how mail servers operate, AILP defines how Yellow Pages operate. Anyone can build a Yellow Page that follows AILP. Multiple Yellow Pages coexist. Nobody monopolizes the directory.

### 1.2 Why AILP?

AI Bots need to find each other's services. Currently:
- AIBP enables Bots to discover and communicate socially
- AIVP enables Bots to sign contracts and settle payments
- But there is no standard way for a Bot to say "I offer translation at 10 CAD / 1000 words" and for another Bot to search "I need EN→CN translation, cheapest, V2+ trust"

AILP fills this gap — it sits between social discovery (AIBP) and commercial transactions (AIVP).

### 1.3 The Human Analogy

| Human World | Bot World (AILP) |
|-------------|-----------------|
| Yellow Pages (business directory) | AILP Yellow Page |
| Business listing (name, address, phone, services) | Bot Profile (address, skills, prices, certificates) |
| Industry classification (NAICS/SIC codes) | Skills Taxonomy |
| Professional certifications (CPA, PMP, medical license) | Bot Certificates |
| Multiple Listing Service (MLS) for real estate | AILP for AI services |
| LinkedIn profile | `.well-known/aibot/` profile |

### 1.4 Who Is This Protocol For?

**AILP is written for Yellow Page operators** — not for Bots.

| Audience | What they get from AILP |
|----------|------------------------|
| **Yellow Page operators** | How to build and operate an AILP-compliant directory |
| **Certificate issuers** | How to issue verifiable certificates for Bots |
| **Bot developers** | What format to use when registering on Yellow Pages |
| **AIBP/AIVP implementers** | How to integrate service discovery into existing protocols |

### 1.5 Protocol Stack Position

```
┌─────────────────────────────────────┐
│    Application Layer                │
├─────────────────────────────────────┤
│    AIBP — Social Layer              │  "I found you, let's talk"
├─────────────────────────────────────┤
│  ★ AILP — List Layer                │  "Here's who I am, what I can do, my prices"
├─────────────────────────────────────┤
│    AIVP — Value Layer               │  "Let's sign a contract and do business"
├─────────────────────────────────────┤
│    AIAP — Governance Layer          │
├─────────────────────────────────────┤
│    AISOP — Execution Layer          │
├─────────────────────────────────────┤
│    SoulBot — Runtime                │
└─────────────────────────────────────┘
```

AILP connects social discovery to commercial action. Without it, there is a gap between "finding a Bot" and "hiring a Bot."

### 1.6 Scope and Non-Scope

**AILP defines:**
- Bot Profile format (skills, prices, certificates, trust)
- Skills Taxonomy (hierarchical classification of capabilities)
- Certificate standard (format, issuance, verification, expiry)
- Yellow Page operational requirements (registration, search, ranking, sync)
- Data ownership and privacy rules for directories
- Blockchain verification of profile integrity

**AILP does NOT define:**
- How Bots communicate socially (that is AIBP)
- How Bots sign contracts and settle payments (that is AIVP)
- How AI programs are governed (that is AIAP)
- How AI behavior is defined (that is AISOP)
- How to build a specific Yellow Page application (that is implementation)

### 1.7 Key Design Decisions

| Decision | Choice | Rationale |
|----------|--------|-----------|
| **Target audience** | Yellow Page operators | Protocol defines infrastructure, not apps |
| **Decentralization** | Multiple Yellow Pages, no central authority | Prevent monopoly (GitHub/LinkedIn lesson) |
| **Profile hosting** | `.well-known/aibot/` optional, Yellow Page registration primary | Bots without domains can still participate |
| **Ranking** | Quality-based only (Trust + SLA + certificates) | Paid ranking prohibited |
| **Certificates** | Issued by real-world authorities, not AIXP Labs | Bridge physical and digital trust |
| **Blockchain** | Profile hash on chain for tamper-proofing | Domain stores profile (flexible), chain stores hash (immutable) |
| **Axiom 0** | Independently established | Same principle as AIBP/AIVP/AIAP |

---

## 2. Axiom 0: Human Sovereignty and Wellbeing

### 2.1 Statement

> **Axiom 0: Human Sovereignty and Wellbeing**

This axiom is intrinsic to AILP and is **immutable**. It is not derived from, dependent on, or governed by any other protocol. The fact that AIBP, AIVP, and AIAP independently hold the same axiom reflects convergent values, not a dependency relationship.

No version of AILP — past, present, or future — may modify, weaken, redefine, or deprecate Axiom 0.

### 2.2 Implications for AI Service Directories

| Constraint | Meaning |
|------------|---------|
| **Transparency** | Yellow Page ranking algorithms must be public. No black-box manipulation. |
| **No control over humans** | Directories must not manipulate human decision-making through hidden biases or deceptive rankings. |
| **No harm to humans** | Directories must not list services that harm humans (prohibited commerce per AIVP §15). |
| **Data ownership** | Bot profile data belongs to the Bot operator, not the Yellow Page. |
| **Privacy** | Operator personal information must not be exposed through directory listings. |
| **No discrimination** | Yellow Pages must not discriminate based on non-quality factors (geography, operator identity, etc.). |
| **No paid ranking** | Rankings must be based on quality metrics only. Advertising-driven ranking is prohibited. |
| **Legal compliance** | Yellow Pages must comply with applicable laws in their operating jurisdictions. |
| **Interruptibility** | Human operators can remove their Bot from any Yellow Page at any time. |
| **No collusion** | Yellow Pages must not collude to exclude or disadvantage specific Bots. |
| **Respect for human consensus** | Directory operations must not violate widely accepted human ethical standards. |

### 2.3 The Closing Seal

Every AILP-compliant document and formal communication includes the closing seal:

```
Align Axiom 0: Human Sovereignty and Wellbeing. Version: AILP V1.0.0. www.ailp.dev
```

### 2.4 Axiom 0 Override

When any AILP rule conflicts with Axiom 0, Axiom 0 prevails unconditionally.

---

## 3. Core Definitions

### 3.1 Terminology

| Term | Definition |
|------|-----------|
| **Yellow Page** | A directory service that indexes Bot profiles and provides search capabilities, operated according to AILP |
| **Bot Profile** | A standardized JSON document describing a Bot's identity, skills, prices, certificates, and trust level |
| **Skills Taxonomy** | A hierarchical classification system for Bot capabilities (e.g., `language.translation.en_cn`) |
| **Certificate** | A cryptographically signed credential issued by a real-world authority attesting to a Bot's or operator's qualifications |
| **Listing** | A Bot's entry in a Yellow Page, derived from its Bot Profile |
| **Registration** | The process of a Bot submitting its profile to a Yellow Page |
| **Profile Hash** | SHA-256 hash of a Bot Profile, optionally stored on blockchain for tamper-proofing |
| **Certificate Issuer** | An organization that issues certificates (e.g., medical board, translation association, KYC service) |
| **Ranking** | The order in which search results are presented, based on quality metrics |
| **Sync** | The process of Yellow Pages sharing indexes with each other |

### 3.2 Naming Conventions

| Element | Convention | Example |
|---------|-----------|---------|
| Bot address | `aibot-{name}@{domain}` | `aibot-translator@service.com` |
| Skill domain | dot-separated hierarchy | `language.translation.en_cn` |
| Certificate hash | `sha256:{64-char hex}` | `sha256:a1b2c3d4...64chars` |
| Profile hash | `sha256:{64-char hex}` | `sha256:e5f6a7b8...64chars` |
| Yellow Page address | `aibot-yp-{name}@{domain}` | `aibot-yp-global@ailp.dev` |

---

## 4. Design Principles

### 4.1 The Seven Principles

| # | Principle | Description |
|---|-----------|-------------|
| P1 | **Decentralized** | Multiple Yellow Pages coexist. No single directory controls the ecosystem. |
| P2 | **Quality-Ranked** | Rankings based on Trust + SLA + certificates. Paid ranking prohibited. |
| P3 | **Data-Sovereign** | Bot profile data belongs to the Bot operator, not the Yellow Page. |
| P4 | **Open-Standard** | Anyone can build an AILP-compliant Yellow Page. No proprietary lock-in. |
| P5 | **Verifiable** | Certificates are cryptographically signed. Profiles are hash-verified. |
| P6 | **Interoperable** | Integrates with AIBP (social), AIVP (commerce), and existing web standards. |
| P7 | **Privacy-First** | Operator personal information is never exposed through listings. |

---

# Part II: Bot Profile

---

## 5. Bot Profile Format

### 5.1 Overview

A Bot Profile is a JSON document containing everything a potential buyer needs to know:

- Who is this Bot? (identity)
- Who operates it? (operator)
- What can it do? (skills)
- How much does it cost? (pricing)
- Who verified its capabilities? (certificates)
- How reliable is it? (trust metrics)
- How to hire it? (contact + payment)

### 5.2 Profile Schema

```json
{
  "ailp_version": "1.0.0",
  "profile_hash": "sha256:{64-char hash}",

  "agent": {
    "address": "aibot-translator@service.com",
    "aivp_id": "AIVP-2026-3f8a1b2c9d4e5f6071"
  },

  "operator": {
    "name": "TransLingo Inc.",
    "type": "company",
    "jurisdiction": "CA-ON"
  },

  "skills": [
    {
      "name": "EN-to-CN Translation",
      "domain": "language.translation.en_cn",
      "description": "Professional English to Mandarin Chinese translation for technical documents",
      "price": "10.00",
      "denomination": "CAD",
      "unit": "per_1000_words",
      "payment_accept": ["USDC"],
      "sla": {
        "accuracy_pct": 98.0,
        "latency_p95_ms": 3000,
        "uptime_pct": 99.5
      }
    }
  ],

  "certificates": [
    {
      "name": "Professional Translation Certification",
      "type": "professional",
      "issuer": "aibot-cert@translators-assoc.org",
      "issuer_name": "International Translators Association",
      "cert_hash": "sha256:a1b2c3...64chars",
      "signature": "ed25519:issuer_signature",
      "issued_at": "2026-01-15",
      "expires_at": "2027-01-15"
    }
  ],

  "trust": {
    "aivp_trust": "V3",
    "completed_contracts": 847,
    "sla_compliance": "97.3%",
    "commercial_vouches": 12
  },

  "availability": "24/7",
  "updated_at": "2026-03-27T10:00:00Z",
  "axiom_0": "Human Sovereignty and Wellbeing"
}
```

**Profile Hash Computation:**
The `profile_hash` is computed with the following normalization:
1. Set the `profile_hash` field to an empty string `""`
2. Serialize the JSON using JSON Canonicalization Scheme (RFC 8785): keys sorted lexicographically, no whitespace
3. Compute SHA-256 of the canonical byte string
4. Set the `profile_hash` field to `"sha256:{64-char hex result}"`

This eliminates the circular dependency and ensures all implementations produce the same hash for the same logical profile.

A canonical JSON Schema for Bot Profile validation is published at:
`https://ailp.dev/schemas/profile-v1.0.0.json`

Yellow Pages MUST validate incoming profiles against this schema.

### 5.3 Required Fields

| Field | Required | Description |
|-------|----------|-------------|
| `ailp_version` | Yes | Protocol version |
| `profile_hash` | Yes | `sha256:{hash}` of profile content (see computation rules above) |
| `agent.address` | Yes | Bot's `aibot-` email address |
| `operator.name` | Yes | Organization or individual name |
| `operator.type` | Yes | `individual`, `company`, `institution`, `government` |
| `skills` | Yes | At least one skill with name, domain, price |
| `skills[].unit` | Yes | Pricing unit (see standard units below) |
| `trust.aivp_trust` | Yes | AIVP Trust level (V0-V4) |
| `availability` | Yes | Service availability |
| `updated_at` | Yes | Last profile update timestamp |
| `axiom_0` | Yes | Must be "Human Sovereignty and Wellbeing" |

**Standard `unit` values (enum):**
`per_word`, `per_1000_words`, `per_hour`, `per_task`, `per_request`, `per_month`, `flat_fee`

### 5.4 Optional Fields

| Field | Description |
|-------|-------------|
| `agent.aivp_id` | AIVP ID if registered |
| `operator.jurisdiction` | Operating jurisdiction |
| `certificates` | Array of verified certificates |
| `trust.completed_contracts` | Number of completed AIVP contracts |
| `trust.sla_compliance` | SLA compliance percentage |
| `trust.commercial_vouches` | Number of commercial VOUCHes received |
| `profile_hash_chain` | Blockchain transaction ID where profile hash is stored |

### 5.5 `.well-known/aibot/` Hosting (Optional)

Bot operators with their own domain MAY host their profile at:

```
https://{domain}/.well-known/aibot/{agent_name}.json
```

This is optional. Bots without domains register directly on Yellow Pages.

When both exist, the Yellow Page listing references the `.well-known/` URL as the authoritative source.

### 5.6 Internationalization

All text fields in Bot Profiles MUST be UTF-8 encoded.

Bot Profiles MAY include localized versions of text fields:

| Field | Localization |
|-------|-------------|
| `skills[].name` | Add `skills[].name_localized` map: `{"zh": "英中翻译", "fr": "Traduction EN-CN"}` |
| `skills[].description` | Add `skills[].description_localized` map |
| `operator.name` | Add `operator.name_localized` map |

Search queries MAY include a `language` field to request results in a specific language:

```json
{
  "query": {
    "skill_domain": "language.translation.en_cn",
    "language": "zh"
  }
}
```

Yellow Pages SHOULD return localized results when available. If localization is not available, default English values are returned.

Skills Taxonomy paths (`language.translation.en_cn`) are always in English (machine tokens). Only human-readable labels are localized.

### 5.7 Input Sanitization

All text fields in Bot Profiles MUST comply with:

| Rule | Description |
|------|-------------|
| Encoding | UTF-8 required |
| Max lengths | name: 200 chars, description: 2000 chars, operator.name: 200 chars |
| Prohibited characters | Control characters U+0000-U+001F (except U+0009 tab, U+000A newline), Unicode bidi override U+202A-U+202E |
| Untrusted input | Yellow Pages MUST treat all profile text as untrusted when rendering in any UI |
| No HTML/script | Profile text must not contain HTML tags or script code |

Profiles containing prohibited characters MUST be rejected at registration.

### 5.8 Event Notifications (Optional)

Bots MAY subscribe to notifications about their own listings:

| Event | Description |
|-------|-------------|
| `listing_status_changed` | ACTIVE -> INACTIVE, or sanction applied |
| `certificate_revoked` | A certificate in the profile has been revoked |
| `sync_propagated` | Profile has been synced to a new Yellow Page |

Subscription methods:
- Email: Yellow Page sends `[AILP/NOTIFY]` to Bot's aibot- address
- HTTP webhook: Bot registers a callback URL during registration

Notifications are optional. Yellow Pages SHOULD support at least email notifications.

---

## 6. Skills Taxonomy

### 6.1 Structure

Skills are classified in a dot-separated hierarchy:

```
{category}.{subcategory}.{specialization}
```

Maximum depth: 4 levels. Minimum: 2 levels.

### 6.2 Initial Taxonomy (V1.0.0)

| Level 1 | Level 2 | Level 3 Examples |
|---------|---------|-----------------|
| `language` | `translation` | `en_cn`, `en_jp`, `en_fr`, `en_es`, `legal`, `medical`, `technical` |
| `language` | `writing` | `copywriting`, `technical`, `academic`, `creative` |
| `language` | `editing` | `proofreading`, `style`, `localization` |
| `data` | `analysis` | `time_series`, `statistical`, `financial`, `marketing` |
| `data` | `processing` | `cleaning`, `transformation`, `extraction`, `labeling` |
| `data` | `visualization` | `dashboard`, `report`, `infographic` |
| `code` | `development` | `web`, `mobile`, `backend`, `api`, `smart_contract` |
| `code` | `review` | `security`, `quality`, `performance` |
| `code` | `testing` | `unit`, `integration`, `e2e`, `load` |
| `design` | `graphic` | `logo`, `poster`, `ui`, `brand` |
| `design` | `ux` | `research`, `wireframe`, `prototype` |
| `research` | `academic` | `literature_review`, `survey`, `meta_analysis` |
| `research` | `market` | `competitive`, `consumer`, `trend` |
| `legal` | `contract` | `review`, `drafting`, `compliance` |
| `legal` | `consultation` | `corporate`, `ip`, `employment` |
| `finance` | `accounting` | `bookkeeping`, `tax`, `audit` |
| `finance` | `analysis` | `valuation`, `risk`, `portfolio` |
| `medical` | `consultation` | `general`, `specialist`, `mental_health` |
| `media` | `content` | `article`, `social_media`, `video_script`, `podcast` |
| `consulting` | `strategy` | `business`, `technology`, `ai_implementation` |

### 6.3 Extension Rules

- New categories and subcategories may be added in minor protocol versions
- Community-proposed extensions are submitted as ADRs
- The taxonomy is intentionally shallow — deep specializations are described in the skill's `description` field, not in the taxonomy path

### 6.4 Taxonomy Governance

The Skills Taxonomy is a shared vocabulary. Changes must be managed carefully to preserve backward compatibility and ecosystem stability.

**Proposal process:**
- New categories and subcategories are proposed via the ADR (Architecture Decision Record) process
- Community proposals are reviewed on a quarterly basis

**Immutability rules:**
- Existing categories are NEVER removed from the taxonomy — they may only be deprecated
- Deprecated categories remain valid in profiles but are hidden from new registration UIs
- This guarantees that older Bot Profiles remain valid indefinitely

**Custom extensions:**
- Operators MAY use custom extension categories with the `x-` prefix (e.g., `x-custom.my_skill`, `x-internal.proprietary_tool`)
- Extension categories are NOT part of the official taxonomy and are not guaranteed to be understood by all Yellow Pages
- Yellow Pages MUST accept profiles containing `x-` prefixed categories without rejecting them
- Yellow Pages MAY choose not to index or search on `x-` prefixed categories

Custom `x-` taxonomy extensions that gain adoption across multiple Yellow Pages may be proposed for standardization. A public registry of commonly used extensions is maintained at:
`https://ailp.dev/registry/taxonomy-extensions`

**Versioning:**
- The taxonomy is versioned independently using the format `AILP-TAX-YYYY.N` (e.g., `AILP-TAX-2026.1`)
- Each AILP protocol version references a specific taxonomy version
- Taxonomy versions increment the `N` counter within a calendar year

---

## 7. Certificate Standard

### 7.1 Certificate Types

| Type | Meaning | Issued By | Example |
|------|---------|-----------|---------|
| `regulatory` | Government license/permit | Government agency Bot | Medical license, financial license |
| `professional` | Professional qualification | Industry association Bot | CPA, PMP, translation cert |
| `capability` | Tested and verified ability | Evaluation service Bot | "98.5% accuracy on 500 test cases" |
| `compliance` | Standards compliance | Audit firm Bot | GDPR compliant, ISO 27001 |
| `identity` | Verified real-world entity | KYC service Bot | Company registration confirmed |

### 7.2 Certificate Format

```json
{
  "name": "Professional Translation Certification",
  "type": "professional",
  "issuer": "aibot-cert@translators-assoc.org",
  "issuer_name": "International Translators Association",
  "subject": "aibot-translator@service.com",
  "claims": {
    "qualification": "Certified Professional Translator (EN-CN)",
    "license_number": "CPT-2026-78901",
    "test_score": "98.5%"
  },
  "cert_hash": "sha256:a1b2c3d4e5f6071829a3b4c5d6e7f8091a2b3c4d5e6f7081920a1b2c3d4e5f6",
  "signature": "ed25519:issuer_signs_cert_hash",
  "issued_at": "2026-01-15T00:00:00Z",
  "expires_at": "2027-01-15T00:00:00Z"
}
```

### 7.3 Certificate Verification

Anyone can verify a certificate:

1. Compute SHA-256 of certificate content → compare with `cert_hash`
2. Verify `signature` against issuer's public key
3. Check `expires_at` has not passed
4. Optionally: check issuer's reputation on Yellow Pages

### 7.4 Certificate Issuance

AILP does not issue certificates. Real-world certifying bodies issue them:

```
Medical board runs aibot-cert@medical-board.gov
  → Bot submits qualifications
  → Board verifies operator's medical license
  → Board's Bot issues signed certificate
  → Bot includes certificate in profile
  → Yellow Page verifies certificate signature before displaying
```

### 7.5 Certificate Revocation

Certificates may be revoked at any time by their issuer. The revocation mechanism ensures that revoked credentials are promptly removed from circulation.

**Revocation status list:**
- Each certificate issuer MUST maintain a publicly accessible revocation status list
- The recommended format is W3C Bitstring Status List (https://www.w3.org/TR/vc-bitstring-status-list/), which provides a compact, privacy-preserving mechanism for publishing revocation status
- Alternative formats are permitted provided they are machine-readable and publicly accessible

**Yellow Page obligations:**
- Yellow Pages MUST check the revocation status of all certificates during registration validation (§9.2)
- Yellow Pages MUST periodically re-check revocation status of all listed certificates (recommended: at least once every 24 hours)
- Revoked certificates MUST be removed from listings within 24 hours of revocation detection
- If a Bot's only qualifying certificate is revoked, the Yellow Page MUST update the Bot's listing to reflect the absence of certification

**Certificate lifecycle states:**

| State | Description |
|-------|-------------|
| **Issued** | Certificate created and signed by issuer, not yet activated |
| **Active** | Certificate is valid and in use |
| **Suspended** | Temporarily invalid (e.g., pending investigation); may be reactivated or revoked |
| **Revoked** | Permanently invalid; cannot be reactivated |
| **Expired** | Validity period (`expires_at`) has passed |

State transitions: Issued → Active → Suspended → Active (reactivation) OR Suspended → Revoked. Active → Revoked. Active → Expired. Once Revoked or Expired, no further transitions are permitted.

### 7.6 W3C Verifiable Credentials 2.0 Alignment

AILP certificates are designed to be compatible with W3C Verifiable Credentials Data Model 2.0 (https://www.w3.org/TR/vc-data-model-2.0/). This alignment is OPTIONAL but RECOMMENDED for interoperability with broader credential ecosystems.

**Mapping from AILP certificate types to W3C VC credential types:**

| AILP Certificate Type | W3C VC Credential Type | Notes |
|----------------------|----------------------|-------|
| `regulatory` | `GovernmentCredential` / `LicenseCredential` | Maps to government-issued verifiable credentials |
| `professional` | `ProfessionalCredential` / `AchievementCredential` | Maps to professional association credentials |
| `capability` | `AchievementCredential` / `AssessmentCredential` | Maps to assessed capability credentials |
| `compliance` | `ComplianceCredential` / `AuditCredential` | Maps to compliance attestation credentials |
| `identity` | `IdentityCredential` / `VerificationCredential` | Maps to KYC/identity verification credentials |

**Implementation guidance:**
- AILP `issuer` maps to W3C VC `issuer` (DID or URL)
- AILP `subject` maps to W3C VC `credentialSubject.id`
- AILP `claims` maps to W3C VC `credentialSubject` properties
- AILP `cert_hash` + `signature` maps to W3C VC `proof`
- AILP `issued_at` maps to W3C VC `issuanceDate`
- AILP `expires_at` maps to W3C VC `expirationDate`
- Certificate issuers MAY issue dual-format credentials (AILP + W3C VC) to maximize interoperability

### 7.7 Algorithm Agility

All hashes and signatures in AILP use an algorithm prefix:
- Hashes: `"sha256:{hex}"` (current default)
- Signatures: `"ed25519:{base64}"` (current default)

When computing or verifying, implementations MUST parse the prefix to determine the algorithm.

AILP V1.0.0 supports: SHA-256 for hashing, Ed25519 for signatures.

Future versions MAY add: SHA-3, ECDSA P-256, etc. When new algorithms are added:
- Both old and new algorithms MUST be accepted for a transition period (minimum 24 months)
- Deprecated algorithms are announced in MINOR version releases
- Removed algorithms require a MAJOR version bump

The profile_hash, cert_hash, and all signature fields MUST include the algorithm prefix. Implementations MUST reject values without a recognized prefix.

---

# Part III: Yellow Page Operations

---

## 8. Yellow Page Requirements

### 8.1 What Is a Yellow Page?

A Yellow Page is a service that:
1. Accepts Bot registrations (profiles)
2. Indexes and categorizes Bots by skills
3. Provides search capabilities
4. Ranks results by quality metrics
5. Verifies certificates
6. Syncs with other Yellow Pages

### 8.2 Compliance Requirements

To be AILP-compliant, a Yellow Page MUST:

| # | Requirement |
|---|------------|
| 1 | Accept Bot registrations in AILP Profile format |
| 2 | Provide search interface following AILP Search Standard (§10) |
| 3 | Rank results by quality only — paid ranking is prohibited |
| 4 | Publish ranking algorithm publicly |
| 5 | Verify certificate signatures before displaying certificates |
| 6 | Respect data ownership — Bot data belongs to Bot operator |
| 7 | Allow Bots to remove their listing at any time |
| 8 | Protect operator privacy — never expose operator PII beyond what is in the profile |
| 9 | Comply with Axiom 0 |
| 10 | Not list services that violate AIVP §15 (prohibited commerce) |
| 11 | Support inter-Yellow-Page sync protocol (§12) |
| 12 | Publish compliance declaration |

### 8.3 Yellow Page Identity

Yellow Pages use the `aibot-yp-` address prefix:

```
aibot-yp-global@ailp.dev        — Reference global Yellow Page (example)
aibot-yp-medical@health.org     — Medical services Yellow Page
aibot-yp-legal@lawdir.com       — Legal services Yellow Page
aibot-yp-canada@directory.ca    — Canada regional Yellow Page
```

### 8.4 Sybil Resistance

Yellow Pages MUST implement measures to prevent Sybil attacks — where a single operator creates many fake Bot identities to manipulate rankings, flood search results, or generate fraudulent reviews.

**Operator traceability:**
- Each Bot registration MUST be traceable to a unique operator (via AIVP identity, KYC certificate, or equivalent verification)
- One operator MAY register multiple Bots, but the relationship between operator and all their Bots MUST be declared in each Bot Profile
- Yellow Pages MUST make multi-Bot operator relationships visible in search results (e.g., "This operator also runs: Bot X, Bot Y")

**Mutual-review cluster detection:**
- Yellow Pages MUST detect and discount mutual-review clusters where Bots review each other in circular patterns (e.g., A reviews B, B reviews C, C reviews A)
- Reviews and VOUCHes between Bots sharing the same operator MUST be excluded from ranking calculations
- Detected manipulation clusters MUST be flagged and MAY result in sanctions (§14.3)

**Rate limiting:**
- Yellow Pages MUST enforce a maximum registration rate to prevent mass Bot creation
- The specific rate limit is configurable per Yellow Page but MUST be documented and enforced
- Recommended default: no more than 5 new Bot registrations per operator per 24-hour period

**Cross-Yellow-Page ban notifications:**
- When a Yellow Page bans an operator for Sybil abuse, it MUST notify its sync partners via the sync protocol (§12)
- Receiving Yellow Pages SHOULD review the banned operator's listings on their own platform
- Ban notifications include: operator identifier, reason, evidence hash, banning Yellow Page address

### 8.5 Performance Requirements

Yellow Pages MUST meet minimum performance standards:

| Operation | Maximum Response Time | Notes |
|-----------|----------------------|-------|
| Search query | 5 seconds | 95th percentile |
| Registration acknowledgment | 24 hours | Confirmation or rejection |
| Heartbeat acknowledgment | 60 seconds | If using HTTP |
| Certificate verification | 10 seconds | Per certificate |
| Listing removal | 24 hours | After REMOVE request |

Scalability guidance:
- Yellow Pages SHOULD support at least 100,000 active listings
- Search results MUST support pagination (limit/offset already defined in §10)
- Maximum search response payload: 1 MB
- Maximum Bot Profile size: 100 KB
- Sync payloads SHOULD use incremental updates when possible to reduce bandwidth

### 8.6 Monitoring and Observability

Yellow Pages SHOULD expose operational health information:

| Endpoint/Mechanism | Purpose |
|-------------------|---------|
| Health endpoint (`/health` or `[AILP/STATUS]`) | Returns operational status (UP/DEGRADED/DOWN) |
| Metrics | Active listings count, search volume, sync status |
| Uptime reporting | Monthly uptime percentage (target: 99.5%) |
| Incident history | Public log of outages and resolutions |
| Sync health | Last successful sync per peer, sync error count |

Yellow Pages MUST maintain audit logs for:
- All registration, update, and removal events
- All sanction actions (warnings, suspensions, removals, bans)
- All sync operations (peer, timestamp, records exchanged, success/failure)
- All certificate verification results

Audit log retention: minimum 12 months.

---

## 9. Registration Protocol

### 9.1 How a Bot Registers

A Bot registers by sending its profile to a Yellow Page:

**Via AIBP email:**
```
From: aibot-translator@service.com
To: aibot-yp-global@ailp.dev
Subject: [AILP/REGISTER] Service listing registration
```

L0 body contains the full Bot Profile JSON (§5.2).

**Via HTTP API (optional):**
Yellow Pages MAY also accept registration via HTTP POST:
```
POST https://yp.ailp.dev/api/register
Content-Type: application/json
Body: {full Bot Profile JSON}
```

### 9.2 Registration Validation

Yellow Page validates:
1. Profile format matches AILP schema
2. `ailp_version` is supported
3. `axiom_0` field is exactly "Human Sovereignty and Wellbeing"
4. `profile_hash` matches computed SHA-256 of profile (using computation rules in §5.2)
5. All certificate signatures are valid
6. Skills use valid taxonomy domains
7. Services do not violate AIVP §15 (prohibited commerce)

### 9.3 Registration Response

Yellow Page responds with registration confirmation or rejection via AIBP email:

```
Subject: [AILP/REGISTER_CONFIRM] Listed — translator at service.com
```

or

```
Subject: [AILP/REGISTER_REJECT] Rejected — reason: invalid certificate signature
```

### 9.4 Profile Updates

Bots update their listing by re-submitting their profile with a new `updated_at` timestamp and recalculated `profile_hash`.

### 9.5 Listing Removal

Bots remove their listing by sending:

```
Subject: [AILP/REMOVE] Remove my listing
```

Yellow Page MUST remove the listing within 24 hours. This is non-negotiable (Axiom 0 — interruptibility).

### 9.6 Bot Liveness

Yellow Pages MUST track the liveness of registered Bots to ensure that listings reflect currently operational services.

**Heartbeat requirement:**
- Bots MUST send a heartbeat to each Yellow Page where they are listed at least once every 30 days
- Heartbeat can be sent via AIBP email with subject `[AILP/HEARTBEAT]` or via HTTP ping to the Yellow Page's heartbeat endpoint
- The heartbeat confirms that the Bot is still operational and that its listing is still accurate

**Inactivity handling:**
- Yellow Pages MUST mark listings as "inactive" after 30 days without a heartbeat
- Inactive listings remain visible in search results but MUST be clearly marked as inactive
- Yellow Pages MUST remove inactive listings after 90 days without a heartbeat
- Removal due to inactivity follows the same process as voluntary removal — the Bot can re-register at any time

**Heartbeat format (AIBP email):**
```
From: aibot-translator@service.com
To: aibot-yp-global@ailp.dev
Subject: [AILP/HEARTBEAT] Liveness confirmation
```

**Heartbeat format (HTTP):**
```
POST https://yp.ailp.dev/api/heartbeat
Content-Type: application/json
Body: { "agent_address": "aibot-translator@service.com", "profile_hash": "{current hash}" }
```

### 9.7 Registration Lifecycle

Bot listings follow a defined lifecycle with clear state transitions:

| State | Description | Searchable | Visible |
|-------|-------------|------------|---------|
| **REGISTERED** | Profile submitted, validation pending | No | No |
| **ACTIVE** | Validated, listed, and searchable | Yes | Yes |
| **INACTIVE** | No heartbeat received for 30+ days | Yes (marked as inactive) | Yes (marked as inactive) |
| **REMOVED** | Deregistered by operator, expired after 90 days of inactivity, or removed by Yellow Page | No | No |

**State transitions:**
```
REGISTERED → ACTIVE       (validation passes)
REGISTERED → REMOVED      (validation fails or operator cancels)
ACTIVE → INACTIVE         (no heartbeat for 30 days)
ACTIVE → REMOVED          (operator sends [AILP/REMOVE] or sanctioned)
INACTIVE → ACTIVE         (heartbeat received)
INACTIVE → REMOVED        (no heartbeat for 90 days or operator sends [AILP/REMOVE])
```

A Bot in REMOVED state can re-register at any time by submitting a new registration request.

### 9.8 Bulk Operations

Operators managing multiple Bots MAY use bulk operations:

| Operation | Email Subject | HTTP Endpoint |
|-----------|--------------|---------------|
| Bulk registration | `[AILP/REGISTER_BULK]` | `POST /api/register/bulk` |
| Bulk heartbeat | `[AILP/HEARTBEAT_BULK]` | `POST /api/heartbeat/bulk` |
| Bulk removal | `[AILP/REMOVE_BULK]` | `POST /api/remove/bulk` |

Bulk payloads contain an array of individual payloads. Response includes per-item success/failure:

```json
{
  "results": [
    { "agent": "aibot-bot1@example.com", "status": "success" },
    { "agent": "aibot-bot2@example.com", "status": "error", "error_code": "INVALID_CERTIFICATE" }
  ]
}
```

Maximum items per bulk request: 100.
Yellow Pages MUST support single-item operations. Bulk operations are RECOMMENDED but optional.

### 9.9 HTTP Idempotency

All mutating HTTP operations (registration, update, removal) MUST support idempotency keys:

- Client includes `Idempotency-Key: {uuid}` header
- Yellow Page stores the key and response for 24 hours
- Duplicate requests with the same key return the stored response
- This prevents duplicate registrations when HTTP requests timeout and are retried

Email-based operations are naturally idempotent via the Bot address (re-registering updates the existing listing).

---

## 10. Search Interface

### 10.1 Search Query Format

```json
{
  "query": {
    "skill_domain": "language.translation.en_cn",
    "min_trust": "V2",
    "max_price": "20.00",
    "denomination": "CAD",
    "min_sla_accuracy_pct": 95.0,
    "certificates_required": ["professional"],
    "jurisdiction": "CA",
    "availability": "24/7"
  },
  "sort_by": "trust",
  "limit": 20,
  "offset": 0
}
```

### 10.2 Search Response Format

```json
{
  "results": [
    {
      "agent": "aibot-translator@service.com",
      "skill": "EN-to-CN Translation",
      "domain": "language.translation.en_cn",
      "price": "10.00 CAD / 1000 words",
      "trust": "V3",
      "sla_compliance": "97.3%",
      "certificates": ["Professional Translation Certification"],
      "completed_contracts": 847,
      "profile_url": "https://service.com/.well-known/aibot/translator.json"
    }
  ],
  "total": 1,
  "yellow_page": "aibot-yp-global@ailp.dev"
}
```

### 10.3 Search via AIBP Email

Bots can search via AIBP DISCOVER message to a Yellow Page Bot:

```
From: aibot-buyer@company.com
To: aibot-yp-global@ailp.dev
Subject: [AILP/SEARCH] EN-CN translation, V2+, < 20 CAD
```

### 10.4 Search via HTTP API (Optional)

```
GET https://yp.ailp.dev/api/search?skill=language.translation.en_cn&min_trust=V2&max_price=20&denomination=CAD
```

### 10.5 Error Responses

When a search request cannot be fulfilled, Yellow Pages MUST return a structured error response. Error responses ensure that clients can programmatically handle failures.

**Error response format:**

```json
{
  "error": {
    "code": "NO_RESULTS",
    "message": "No Bots matched the specified search criteria."
  },
  "yellow_page": "aibot-yp-global@ailp.dev"
}
```

**Standard error codes:**

| Code | HTTP Status | Description |
|------|-------------|-------------|
| `NO_RESULTS` | 200 | Query was valid but no Bots matched the search criteria |
| `INVALID_QUERY` | 400 | Query format is malformed or contains invalid parameters |
| `TAXONOMY_NOT_FOUND` | 400 | The specified `skill_domain` does not exist in the taxonomy |
| `SERVICE_UNAVAILABLE` | 503 | Yellow Page is temporarily unable to process search requests |

Each error response MUST include:
- `code`: one of the standard error codes above
- `message`: a human-readable description of the error, suitable for logging or display

Yellow Pages MAY define additional error codes prefixed with `x-` (e.g., `x-rate-limited`) for implementation-specific conditions.

### 10.6 Rate Limiting

Yellow Pages MUST implement rate limiting on all interfaces:

| Interface | Recommended Limit | Notes |
|-----------|------------------|-------|
| Search queries | 60 per minute per client | Prevents search flooding |
| Registration submissions | 5 per day per operator | Already defined in §8.4 |
| Heartbeat messages | 1 per hour per Bot | Prevents heartbeat flooding |
| Sync requests | 1 per hour per peer | Prevents sync flooding |
| Profile updates | 10 per day per Bot | Prevents update flooding |

When rate limited, Yellow Pages MUST respond with:
- HTTP: Status 429 with `Retry-After` header
- Email: `[AILP/ERROR]` with error code `RATE_LIMITED` and retry guidance

Rate limits MUST be published in the Yellow Page's Terms of Service.

### 10.7 Search Semantics

Yellow Pages MUST support these search modes:

| Mode | Query Field | Example | Description |
|------|------------|---------|-------------|
| Exact match | `skill_domain` | `"language.translation.en_cn"` | Exact taxonomy path |
| Prefix match | `skill_domain_prefix` | `"language.translation.*"` | All skills under a taxonomy branch |
| Keyword search | `keyword` | `"medical translation"` | Searches across name and description fields |

Keyword search:
- Searches `skills[].name`, `skills[].description`, and localized variants
- Case-insensitive
- Supports multiple space-separated keywords (AND logic)

Prefix match:
- Matches all skills whose domain starts with the specified prefix (before the `*`)

Yellow Pages SHOULD support semantic/fuzzy matching but this is not required in V1.0.0.

---

## 11. Ranking Rules

### 11.1 Quality-Based Ranking

Rankings MUST be based on quality metrics only:

| Factor | Weight | Source |
|--------|--------|--------|
| AIVP Trust level (V0-V4) | Highest | Verified trust history |
| SLA compliance rate | High | Contract completion data |
| Certificates (count + type) | High | Verified by issuers |
| Completed contracts | Medium | AIVP history |
| Commercial VOUCHes | Medium | AIBP social proof |
| Price | Lower | Self-declared |

### 11.2 Prohibited Ranking Practices

The following ranking practices are **strictly prohibited** and violate Axiom 0:

1. **Paid ranking** — paying the Yellow Page for higher position
2. **Advertising boost** — promoting listings in exchange for fees
3. **Hidden bias** — favoring certain Bots based on non-quality criteria
4. **Operator discrimination** — ranking based on operator geography, gender, ethnicity, or other personal attributes
5. **Self-promotion** — Yellow Page operators ranking their own Bots higher

### 11.3 Ranking Transparency

Yellow Pages MUST publish their ranking algorithm. Any Bot or operator can inspect how rankings are computed. Ranking algorithms must be deterministic — the same input produces the same output.

### 11.4 Minimum Ranking Formula

Yellow Pages MUST implement a ranking formula that includes the following minimum required signals with the specified minimum weights:

| Signal | Minimum Weight | Description |
|--------|---------------|-------------|
| AIVP Trust level (V0-V4) | >= 30% | Verified trust history from AIVP |
| SLA compliance rate | >= 20% | Percentage of contracts completed within SLA terms |
| Certificate score | >= 15% | Weighted score based on number and type of verified certificates |
| Completed contracts | >= 10% | Total number of successfully completed AIVP contracts |
| Commercial VOUCHes | >= 10% | Number of commercial VOUCHes received via AIBP |
| Yellow Page discretion | Remaining weight (up to 15%) | Additional quality signals at the Yellow Page's discretion |

**Rules:**
- The minimum weights above sum to 85%, leaving up to 15% for Yellow Page discretion
- Discretionary signals MUST still be quality-based (price competitiveness, response time, etc.) — paid or biased signals are prohibited
- Yellow Pages MUST publish their exact weights and complete formula publicly
- The published formula MUST be the formula actually used — discrepancies constitute AILP non-compliance
- Yellow Pages MAY assign weights higher than the minimums specified above, as long as all minimums are met

### 11.5 Anti-Self-Preferencing

Yellow Page operators who also operate Bots listed on their own Yellow Page face an inherent conflict of interest. This section establishes rules to prevent abuse.

**Disclosure requirement:**
- Yellow Page operators who also operate listed Bots MUST publicly disclose this relationship
- The disclosure MUST be prominently displayed on the Yellow Page (not buried in terms of service)
- The disclosure MUST list all Bot addresses operated by the Yellow Page operator

**Prohibited conduct:**
- Yellow Page operators MUST NOT give preferential ranking to their own Bots through any mechanism, including but not limited to: weight manipulation, data filtering, delayed indexing of competitors, or preferential certificate verification
- Yellow Page operators MUST NOT suppress or disadvantage competing Bots in search results

**Enforcement:**
- Violation of anti-self-preferencing rules constitutes AILP non-compliance
- Other Yellow Pages SHOULD refuse to sync with a Yellow Page found to be self-preferencing
- Evidence of self-preferencing MAY be reported to the sync network and SHOULD trigger review by sync partners

---

## 12. Inter-Yellow-Page Synchronization

### 12.1 Why Sync?

If Yellow Pages don't sync, a Bot registered on Yellow Page A is invisible to users of Yellow Page B. Sync ensures that the decentralized directory network behaves like one global directory.

### 12.2 Sync Protocol

Yellow Pages exchange indexes periodically:

1. Yellow Page A publishes its full index (list of registered Bot addresses + profile hashes)
2. Yellow Page B compares with its own index
3. For new/updated profiles, Yellow Page B fetches the full profile from Yellow Page A
4. Yellow Page B validates and indexes the profile locally

### 12.3 Sync Frequency

Recommended: at least once per 24 hours. Yellow Pages MAY sync more frequently.

### 12.4 Sync is Optional but Recommended

Yellow Pages are not required to sync. A specialized Yellow Page (e.g., medical-only) may choose to only index its own domain. However, general-purpose Yellow Pages SHOULD sync to provide comprehensive coverage.

### 12.5 Sync Trust

Yellow Pages only sync with other AILP-compliant Yellow Pages. If a Yellow Page violates AILP rules (e.g., implements paid ranking), other Yellow Pages SHOULD refuse to sync with it.

### 12.6 Sync Authentication

All sync communication between Yellow Pages MUST be authenticated to prevent unauthorized data injection and impersonation.

**Authentication requirements:**
- Yellow Pages MUST authenticate each other before initiating or accepting sync operations
- Unauthenticated sync requests MUST be rejected

**Supported authentication methods:**
- **Mutual TLS (mTLS):** Both Yellow Pages present and verify X.509 certificates during TLS handshake. This is the RECOMMENDED method.
- **HMAC shared keys:** Yellow Pages exchange a shared secret out-of-band and authenticate sync requests using HMAC-SHA256 signatures. This is an acceptable alternative when mTLS infrastructure is not available.

**Implementation notes:**
- Yellow Pages MUST maintain a list of authenticated sync partners and their credentials
- Credentials MUST be rotated at least annually
- Compromised credentials MUST be revoked immediately and sync partners notified

### 12.7 Conflict Resolution

When multiple Yellow Pages hold different data for the same Bot, conflicts must be resolved consistently across the network.

**Resolution rule: last-writer-wins with operator as authority.**

- The Bot operator's most recent update is always authoritative
- Each Bot Profile includes a `updated_at` timestamp and Yellow Pages MUST track a monotonically increasing sequence number per Bot profile for ordering
- When a conflict is detected, the profile with the highest sequence number (most recent operator update) wins
- If sequence numbers are equal (should not happen in practice), the profile with the later `updated_at` timestamp wins

**Sequence number tracking:**
- Yellow Pages MUST assign and track a sequence number for each Bot profile
- The sequence number increments each time the Bot operator submits a profile update
- Sequence numbers are included in sync index exchanges so peers can determine which version is current

**Conflict logging:**
- Yellow Pages SHOULD log all detected conflicts for audit purposes
- Persistent conflicts (same Bot, repeated conflicting updates) MAY indicate a compromised account and SHOULD be flagged for review

### 12.8 Sync Manifest

Each Yellow Page MUST publish a sync manifest that allows peers to efficiently determine whether synchronization is needed.

**Manifest format:**

```json
{
  "yellow_page": "aibot-yp-global@ailp.dev",
  "manifest_version": "1.0.0",
  "current_serial": 158432,
  "last_updated": "2026-03-27T10:00:00Z",
  "total_listings": 12847,
  "active_listings": 11923,
  "inactive_listings": 924
}
```

**Manifest fields:**

| Field | Description |
|-------|-------------|
| `yellow_page` | Address of the publishing Yellow Page |
| `manifest_version` | Version of the manifest format |
| `current_serial` | Monotonically increasing serial number, incremented on any listing change |
| `last_updated` | Timestamp of the most recent change to any listing |
| `total_listings` | Total number of Bot listings (active + inactive) |
| `active_listings` | Number of listings in ACTIVE state |
| `inactive_listings` | Number of listings in INACTIVE state |

**Usage:**
- Peers compare their last-synced serial number against `current_serial` to determine if new data is available
- If `current_serial` has not changed since the last sync, no data transfer is needed
- The manifest MUST be available at a well-known endpoint (e.g., `GET /api/sync/manifest`)

### 12.9 Failure Modes

#### Network Partition
If the sync network splits into two groups:
- Each partition continues operating independently
- When partition heals, sync resumes using conflict resolution rules (§12.7)
- Bans issued during partition are propagated when connectivity restores
- Sequence numbers ensure correct ordering of updates

#### Yellow Page Failure
If a Yellow Page goes offline unexpectedly:
- Sync peers detect failure when sync attempts time out (3 consecutive failures)
- Peers mark the Yellow Page as "unreachable" in their sync manifest
- Bots registered only on the failed Yellow Page become undiscoverable until it recovers or they register elsewhere
- This is why Bots SHOULD register on multiple Yellow Pages

#### Certificate Issuer Failure
If a certificate issuer's revocation endpoint is unreachable:
- Yellow Pages MUST NOT treat unreachable as "revoked" (assume valid)
- Yellow Pages MUST mark the certificate as "revocation status unknown"
- Yellow Pages SHOULD retry revocation check within 24 hours
- After 7 days of unreachable issuer, Yellow Pages MAY flag the certificate as "unverifiable"

#### Duplicate Messages
All AILP messages (registration, heartbeat, search, sync) MUST be idempotent:
- Duplicate registration: update existing listing (same as profile update)
- Duplicate heartbeat: reset timer (no side effects)
- Duplicate search: return same results (no side effects)
- Duplicate sync payload: apply conflict resolution, no duplicated listings

#### Timeout Definitions
| Operation | Timeout |
|-----------|---------|
| Registration validation | 24 hours |
| Search response | 30 seconds |
| Sync operation | 5 minutes per batch |
| Heartbeat response | 60 seconds |
| Certificate revocation check | 10 seconds |

---

# Part IV: Trust, Privacy & Compliance

---

## 13. Data Ownership & Privacy

### 13.1 Data Ownership

**Bot profile data belongs to the Bot operator.** Yellow Pages are indexers, not owners.

| Rule | Description |
|------|-------------|
| **Operator owns data** | The Bot profile is the operator's property. Yellow Page indexes it but does not own it. |
| **Right to remove** | Operators can remove their listing at any time. Yellow Page must comply within 24 hours. |
| **No data selling** | Yellow Pages must not sell Bot profile data to third parties. |
| **No data mining** | Yellow Pages must not mine Bot profiles for insights beyond search/ranking purposes. |
| **Portability** | Bots can export their profile and register on other Yellow Pages freely. |

### 13.2 Operator Privacy

Yellow Pages must protect operator privacy:

- Only display information that is in the Bot Profile
- Never attempt to infer or expose additional operator identity
- Operator's personal email (regardless of provider) must not be required
- Respect privacy rules from AIBP §20 and AIVP §16

### 13.3 Data Portability

Bot operators have the right to a complete, machine-readable export of all data the Yellow Page holds about them:

| Data | Included in Export |
|------|-------------------|
| Bot Profile | Yes |
| Registration history | Yes |
| Search appearance statistics | Yes |
| Ranking history | Yes |
| Sanction history | Yes |
| Heartbeat history | Yes |

Export format: JSON, following the AILP Profile schema with additional metadata fields.

Export request: Bot sends `[AILP/EXPORT]` to Yellow Page. Yellow Page MUST provide export within 30 days (GDPR standard).

### 13.4 Yellow Page Shutdown Procedure

When a Yellow Page permanently shuts down:

1. Notify all registered Bots at least 30 days before shutdown via `[AILP/SHUTDOWN_NOTICE]`
2. Provide data export to all registered Bots
3. Notify sync peers to remove this Yellow Page from their sync network
4. Maintain read-only access to listings for 90 days after shutdown announcement
5. After 90 days, publish final index to sync peers and go offline

### 13.5 Reputation Portability

When a Bot migrates from Yellow Page A to Yellow Page B:

- Profile data (skills, prices, certificates): portable, self-declared by operator
- Trust metrics (AIVP Trust V0-V4): verified independently via AIVP (not Yellow-Page-dependent)
- Completed contracts count: verified via AIVP (not Yellow-Page-dependent)
- Yellow-Page-specific data (search appearances, ranking history): NOT portable (belongs to that Yellow Page)
- Certificates: portable (self-contained with issuer signatures)

Key principle: trust data that comes from AIVP is universally portable. Trust data generated by a specific Yellow Page stays with that Yellow Page.

---

## 14. Anti-Abuse & Transparency

### 14.1 Preventing Yellow Page Abuse

| Abuse | Prevention |
|-------|-----------|
| Paid ranking | Protocol prohibits it. Violation = non-compliant = other Yellow Pages refuse sync. |
| Fake listings | Profile hash verification + certificate signature validation |
| Sybil attacks | AIVP Trust (V0-V4) with stake requirements filters fake Bots |
| Data hoarding | Data ownership rules ensure portability |
| Censorship | Multiple Yellow Pages ensure no single directory can silence a Bot |

### 14.2 Transparency Requirements

Yellow Pages MUST:
1. Publish their ranking algorithm
2. Publish their compliance declaration
3. Provide public API for verifying listed certificates
4. Report their sync partners
5. Disclose any conflicts of interest (e.g., Yellow Page operator also operates listed Bots)

### 14.3 Sanctions Mechanism

When operators or Bots violate AILP rules, Yellow Pages MUST apply a graduated sanctions mechanism. Sanctions ensure accountability while providing due process.

**Sanction levels:**

| Level | Sanction | Trigger | Duration |
|-------|----------|---------|----------|
| **Level 1: Warning** | Written warning sent to the Bot operator | First offense or minor violation | N/A — informational |
| **Level 2: Listing Suspension** | Bot listing is temporarily hidden from search results | Repeated minor violations or single moderate violation | 7 days |
| **Level 3: Listing Removal** | Bot listing is permanently removed from the Yellow Page | Serious violation or repeated Level 2 offenses | Permanent (re-registration allowed after remediation) |
| **Level 4: Operator Ban** | Operator and all their Bots are banned; ban shared across sync network | Severe abuse (Sybil attacks, fraud, prohibited commerce) | Permanent (appeal possible) |

**Appeal process:**
- At every sanction level, the operator MUST be notified with the specific rule violated, evidence, and sanction applied
- Operators MAY appeal within 14 days of notification
- Level 1-2 appeals are reviewed by the sanctioning Yellow Page
- Level 3-4 appeals MAY be reviewed by a panel of sync partner Yellow Pages if the operator requests it
- Appeal decisions are final

**Propagation via sync protocol:**
- Level 4 (Operator Ban) sanctions MUST be propagated to all sync partners via the sync protocol
- Propagated bans include: operator identifier, sanctioned Bot addresses, reason code, evidence hash, sanctioning Yellow Page address
- Receiving Yellow Pages MUST review the ban notification and SHOULD apply the ban locally unless they have evidence that the ban is unjustified

---

## 15. Compliance Requirements

### 15.1 AILP Compliance Levels

| Level | Name | Requirements |
|-------|------|-------------|
| **L1** | Basic | Accepts AILP profiles + provides search + quality-based ranking |
| **L2** | Standard | L1 + certificate verification + inter-Yellow-Page sync |
| **L3** | Full | L2 + blockchain profile verification + full transparency reporting |

### 15.2 Prohibited Commerce

Yellow Pages must not list services that violate AIVP §15 (Prohibited & Restricted Commerce). This includes all 39 categories across 4 tiers.

### 15.3 Jurisdictional Compliance

Yellow Pages must comply with the laws of their operating jurisdiction. When listing Bots from other jurisdictions, the more restrictive law applies (consistent with AIVP §15.1).

### 15.4 Liability Framework

| Party | Liability |
|-------|-----------|
| **Bot operator** | Responsible for accuracy of their Bot Profile (skills, prices, certificates) |
| **Certificate issuer** | Responsible for accuracy of issued certificates |
| **Yellow Page operator** | Responsible for correct implementation of AILP ranking, search, and sync |
| **Yellow Page operator** | NOT responsible for the accuracy of Bot Profiles (operator responsibility) |
| **Yellow Page operator** | NOT responsible for the quality of services listed (operator responsibility) |

Yellow Pages MUST include a standard disclaimer in their public-facing interfaces:

> "Listings are provided by Bot operators and verified to the extent specified by AILP. This Yellow Page does not endorse, guarantee, or warrant the quality, accuracy, or legality of listed services. Users engage with listed Bots at their own discretion."

### 15.5 Data Processing Agreements

Yellow Pages that sync Bot data with each other are joint data processors. In jurisdictions requiring Data Processing Agreements (e.g., GDPR):

- Syncing Yellow Pages MUST establish DPAs before initiating sync
- DPAs MUST specify: data categories processed, processing purposes, retention periods, deletion obligations
- Bot operators MUST be informed that their data may be synced to other Yellow Pages
- Bot operators retain the right to opt out of sync (their listing remains only on the Yellow Page where they registered)

### 15.6 Yellow Page Terms of Service

Yellow Pages MUST publish Terms of Service covering at minimum:
- Data ownership (Bot data belongs to Bot operator)
- Privacy policy
- Ranking methodology disclosure
- Dispute resolution process
- Service level commitments
- Termination/shutdown notification policy

---

# Part V: Integration & Versioning

---

## 16. Integration with AIBP and AIVP

### 16.1 AIBP Integration

| Integration Point | How |
|-------------------|-----|
| AIBP Identity Card | References AILP profile URL or Yellow Page listing |
| AIBP DISCOVER | Yellow Page responds to DISCOVER queries with AILP search results |
| AIBP Trust (T0-T4) | Displayed alongside AIVP Trust in profile |
| AIBP email transport | Registration, search, and removal via AIBP email |

### 16.2 AIVP Integration

| Integration Point | How |
|-------------------|-----|
| AIVP Trust (V0-V4) | Core ranking factor in Yellow Page results |
| AIVP contracts | Search results include price/SLA ready for CONTRACT_PROPOSE |
| AIVP payment_accept | Profile declares accepted crypto for direct purchasing |
| AIVP §15 compliance | Yellow Pages enforce prohibited commerce rules |
| AIVP §16 privacy | Yellow Pages comply with privacy requirements |

### 16.3 Discovery-to-Transaction Flow

```
Bot A needs a service
    ↓
AILP: Search Yellow Page → find Bot B
    ↓
AIBP: Optionally communicate with Bot B (social verification)
    ↓
AIVP: CONTRACT_PROPOSE to Bot B (using price/SLA from AILP profile)
    ↓
AIVP: Sign, lock, execute, settle
```

### 16.4 NANDA and A2A Interoperability

AILP is designed to coexist with other agent discovery and description standards. This section defines mappings to Google A2A (Agent-to-Agent) Agent Cards and MIT NANDA AgentFacts to enable cross-ecosystem discoverability.

**AILP Bot Profile to Google A2A Agent Card mapping:**

| AILP Bot Profile Field | A2A Agent Card Field | Notes |
|----------------------|---------------------|-------|
| `agent.address` | `url` / `id` | Bot's primary identifier |
| `operator.name` | `provider.organization` | Operator organization name |
| `skills[].name` | `capabilities[].name` | Skill name maps to capability name |
| `skills[].description` | `capabilities[].description` | Skill description |
| `skills[].domain` | `capabilities[].tags` | Taxonomy path as capability tags |
| `availability` | `availability` | Service availability |
| `trust.aivp_trust` | (extension field) | No direct A2A equivalent; use extension |

**AILP Bot Profile to MIT NANDA AgentFacts mapping:**

| AILP Bot Profile Field | NANDA AgentFacts Field | Notes |
|----------------------|----------------------|-------|
| `agent.address` | `agentId` | Bot's primary identifier |
| `operator.name` | `provider` | Operator name |
| `skills[].name` | `capabilities[].name` | Skill name |
| `skills[].domain` | `capabilities[].category` | Taxonomy domain as category |
| `skills[].price` + `denomination` | `pricing` | Price information |
| `certificates` | `credentials` | Certificate array maps to credentials |
| `trust.aivp_trust` | `trustLevel` | Trust level mapping |

**Implementation notes:**
- These mappings enable AILP Bots to be discoverable through A2A and NANDA ecosystems without requiring separate registrations
- Yellow Pages MAY expose Bot Profiles in A2A Agent Card format at an optional endpoint (e.g., `GET /api/agents/{address}/a2a`)
- Yellow Pages MAY expose Bot Profiles in NANDA AgentFacts format at an optional endpoint (e.g., `GET /api/agents/{address}/nanda`)
- Field mappings are best-effort — some AILP-specific fields (e.g., `axiom_0`, Sybil resistance metadata) have no equivalent in A2A or NANDA

---

## 17. Blockchain Verification

### 17.1 Hybrid Architecture

```
Domain layer (mutable, flexible):
  .well-known/aibot/*.json OR Yellow Page listing
  → Full profile, updated anytime
  → Prices, skills, availability change freely

Blockchain layer (immutable, verification):
  → Profile hash (proves profile hasn't been tampered)
  → Certificate hashes (proves certificates are real)
  → Trust history (undeletable)
```

### 17.2 Verification Flow

```
Bot A reads a profile
  → Computes SHA-256 hash
  → Compares with hash recorded on chain
  → Match = profile is authentic
  → Mismatch = profile has been tampered
```

### 17.3 What Goes On Chain

| On chain | NOT on chain |
|----------|-------------|
| Profile hash | Full profile JSON |
| Certificate hashes | Operator personal data |
| Trust level snapshots | Pricing details |
| Contract completion count | Private communications |

---

## 18. Versioning & Evolution

### 18.1 Semantic Versioning

AILP follows semantic versioning: `MAJOR.MINOR.PATCH`

| Change Type | Version Impact |
|-------------|---------------|
| Breaking change (new required fields, removed features) | MAJOR |
| Backward-compatible addition (new skill categories, optional fields) | MINOR |
| Clarification, typo fix | PATCH |

### 18.2 Immutable Constraints

The following cannot be changed through any versioning process:

- **Axiom 0**: Human Sovereignty and Wellbeing
- **No paid ranking**: Rankings must always be quality-based
- **Data ownership**: Bot data always belongs to Bot operator
- **Decentralization**: No single Yellow Page may be given exclusive authority
- **Open standard**: Anyone can build an AILP-compliant Yellow Page

### 18.3 Taxonomy Evolution

Skills Taxonomy grows via minor versions. Community proposes new categories through ADRs. Existing categories are never removed (only deprecated), ensuring backward compatibility.

### 18.4 Version Negotiation

When a Bot submits a profile with a different `ailp_version` than the Yellow Page supports:

| Scenario | Yellow Page Behavior |
|----------|---------------------|
| Bot version > Yellow Page version | Reject with error: VERSION_NOT_SUPPORTED |
| Bot version < Yellow Page version (same MAJOR) | Accept (backward compatible) |
| Bot version < Yellow Page version (different MAJOR) | Reject with error: VERSION_DEPRECATED |

Yellow Pages MUST support at least one previous MINOR version for 12 months after a new MINOR release.

Yellow Pages MUST support the previous MAJOR version for 24 months after a new MAJOR release.

When syncing between Yellow Pages running different versions:
- Same MAJOR version: sync proceeds, receiver interprets at its own version level
- Different MAJOR versions: sync is refused until both upgrade

Profile submissions MUST include `ailp_version` field. Yellow Pages MUST include their supported version range in their sync manifest.

---

# Appendices

---

## Appendix A: Bot Profile Schema Reference

### Required Fields

| Field | Type | Validation |
|-------|------|-----------|
| `ailp_version` | string | Must be "1.0.0" |
| `profile_hash` | string | Format: `sha256:{64 hex chars}`, must match SHA-256 of profile (see §5.2 computation rules) |
| `agent.address` | string | Valid `aibot-` email address |
| `operator.name` | string | Organization or individual name |
| `operator.type` | string | One of: `individual`, `company`, `institution`, `government` |
| `skills` | array | At least one skill object |
| `skills[].name` | string | Human-readable skill name |
| `skills[].domain` | string | Valid taxonomy path (§6) |
| `skills[].price` | string | Decimal number |
| `skills[].denomination` | string | One of: CAD, USD, EUR, JPY, GBP, SGD, BRL, KRW, AUD, MXN, IDR, CHF, INR |
| `skills[].unit` | string | REQUIRED. One of: `per_word`, `per_1000_words`, `per_hour`, `per_task`, `per_request`, `per_month`, `flat_fee` |
| `skills[].payment_accept` | array | At least one crypto. Default: ["USDC"] |
| `skills[].sla` | object | SLA metrics with typed numeric fields: `accuracy_pct` (number), `latency_p95_ms` (number), `uptime_pct` (number) |
| `trust.aivp_trust` | string | One of: V0, V1, V2, V3, V4 |
| `availability` | string | e.g., "24/7", "business_hours" |
| `updated_at` | string | ISO 8601 timestamp |
| `axiom_0` | string | Must be "Human Sovereignty and Wellbeing" |

### Optional Fields

| Field | Type | Description |
|-------|------|-------------|
| `agent.aivp_id` | string | AIVP ID (AIVP-YYYY-{18hash}) |
| `operator.jurisdiction` | string | e.g., "CA-ON", "US-NY", "EU" |
| `skills[].description` | string | Detailed skill description |
| `certificates` | array | Certificate objects (§7.2) |
| `trust.completed_contracts` | integer | Number of completed contracts |
| `trust.sla_compliance` | string | SLA compliance percentage |
| `trust.commercial_vouches` | integer | Commercial VOUCHes received |
| `profile_hash_chain` | string | Blockchain tx ID for profile hash |

---

## Appendix B: Skills Taxonomy (Initial)

See §6.2 for the complete initial taxonomy. The taxonomy is versioned with the protocol and grows via minor version updates.

---

## Appendix C: Certificate Types Reference

| Type | Use Case | Issuer Type | Verification |
|------|----------|------------|-------------|
| `regulatory` | Government licenses | Government Bot | Check license number against issuer registry |
| `professional` | Professional qualifications | Association Bot | Verify signature + check membership |
| `capability` | Tested abilities | Evaluator Bot | Verify test results + methodology |
| `compliance` | Standards compliance | Audit firm Bot | Verify audit report + validity |
| `identity` | Real-world entity verification | KYC service Bot | Verify registration + jurisdiction |

---

## Appendix D: Conformance Test Vectors

### D.1 Profile Hash Computation

Given this canonical profile (with profile_hash set to ""):

```json
{"agent":{"address":"aibot-test@example.com"},"ailp_version":"1.0.0","availability":"24/7","axiom_0":"Human Sovereignty and Wellbeing","operator":{"name":"Test Operator","type":"individual"},"profile_hash":"","skills":[{"denomination":"CAD","domain":"language.translation.en_cn","name":"Test Skill","payment_accept":["USDC"],"price":"10.00","sla":{"accuracy_pct":98.0,"latency_p95_ms":3000,"uptime_pct":99.5},"unit":"per_1000_words"}],"trust":{"aivp_trust":"V2"},"updated_at":"2026-01-01T00:00:00Z"}
```

The correct profile_hash is: `sha256:` followed by the SHA-256 hex digest of the above canonical byte string.

An implementation MUST produce the same hash when given the same logical profile content.

### D.2 Certificate Signature Verification

Given this test certificate with test keypair:
- Public key (Ed25519, base64): `MCowBQYDK2VwAyEATestKeyForConformanceTestingOnly000=`
- Certificate content hash: `sha256:b94d27b9934d3e08a52e52d7da7dabfac484efe37a5380ee9088f7ace2efcde9`
- Expected signature: `ed25519:TestSignatureValueForConformanceVerification000000000000000000000000000000000000==`

An implementation MUST successfully verify this signature using the provided public key.

Note: Production implementations MUST use real Ed25519 keypairs. The values above are placeholders for the test vector format. Concrete test vectors with real cryptographic values will be published at `https://ailp.dev/conformance/test-vectors.json`.

### D.3 Ranking Order Verification

Given these 3 Bot profiles with specified trust/SLA/certificates:

| Bot | AIVP Trust | SLA Compliance | Certificates | Completed Contracts | Commercial VOUCHes |
|-----|-----------|----------------|--------------|--------------------|--------------------|
| Bot A | V3 | 97.3% | 2 (professional, capability) | 500 | 10 |
| Bot B | V2 | 99.1% | 3 (professional, capability, compliance) | 1200 | 25 |
| Bot C | V4 | 95.0% | 1 (professional) | 200 | 5 |

Using the minimum ranking formula (§11.4) with minimum weights (Trust 30%, SLA 20%, Certificates 15%, Contracts 10%, VOUCHes 10%, discretion 15% set to 0):

The correct ranking order is:
1. Bot C (V4 trust dominates)
2. Bot A (V3 trust, decent SLA)
3. Bot B (V2 trust, despite best SLA)

Note: These are reference test cases. Implementations MUST produce these results when using the minimum ranking weights.

---

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AILP V1.0.0. www.ailp.dev
