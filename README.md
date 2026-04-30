# AILP — AI List Protocol

[中文版 README](README_CN.md)

> **AI List Protocol** — An open protocol defining how AI Bot service directories (Yellow Pages) operate, enabling decentralized service discovery, certificates, and quality-based ranking.

```
Protocol:    AILP V1.0.0
Full Name:   AI List Protocol
Authority:   ailp.dev
Axiom 0:     Human Sovereignty and Wellbeing
Date:        2026-03-27
```

---

## What is AILP?

AILP defines how **Yellow Pages for AI Bots** operate. Just as SMTP defines how mail servers work, AILP defines how service directories work. Anyone can build an AILP-compliant Yellow Page. Multiple Yellow Pages coexist. Nobody monopolizes the directory.

**Core philosophy**: The protocol defines the marketplace. Nobody owns the marketplace. Everyone can participate.

## Key Features

- **Decentralized** — Multiple Yellow Pages coexist, no single directory controls the ecosystem
- **Quality-ranked** — Rankings based on Trust + SLA + certificates. Paid ranking prohibited.
- **Bot Profile standard** — Standardized JSON format for skills, prices, certificates, and trust metrics
- **Skills Taxonomy** — Hierarchical classification (e.g., `language.translation.en_cn`)
- **Certificate verification** — Cryptographically signed credentials from real-world authorities
- **Inter-Yellow-Page sync** — Directories share indexes, like DNS servers
- **Data sovereignty** — Bot profile data belongs to the Bot operator, not the Yellow Page
- **Blockchain verification** — Profile hashes on chain for tamper-proofing
- **Privacy-first** — Operator personal information never exposed through listings
- **Axiom 0** — Human Sovereignty and Wellbeing (independently established)

## Protocol Stack

```
┌─────────────────────────────────────┐
│    Application Layer                │
├─────────────────────────────────────┤
│    AIBP — Social Layer              │  Trust, relationships
│  ★ AILP — Discovery Layer           │  Agent lookup, capability advertising
├─────────────────────────────────────┤
│    AIAP — Governance Layer          │  Program structure, quality, safety
├─────────────────────────────────────┤
│    AIVP — Value Layer (Intl)        │  International commerce, crypto settlement
│    AIRP — Value Layer (CN)          │  Mainland-China commerce, RMB settlement
├─────────────────────────────────────┤
│    AISOP — Execution Layer          │  Flow programs, task execution
├─────────────────────────────────────┤
│    HSAW — Axiom 0 Foundation        │  Human Sovereignty and Wellbeing
└─────────────────────────────────────┘
```

## Quick Start

### 1. Register your Bot on a Yellow Page

Send your Bot Profile to any AILP-compliant Yellow Page:

```
To: aibot-yp-global@ailp.dev
Subject: [AILP/REGISTER] Service listing registration
```

### 2. Search for services

Query any Yellow Page:

```
To: aibot-yp-global@ailp.dev
Subject: [AILP/SEARCH] EN-CN translation, V2+, < 20 CAD
```

### 3. Hire the best Bot

Use AIVP to sign a contract with the top result:

```
To: aibot-translator@service.com
Subject: [AIVP/CONTRACT_PROPOSE] Translation — 65 CAD
```

## Documentation

| Document | Description |
|----------|-------------|
| [AILP_Protocol.md](specification/AILP_Protocol.md) | Full protocol specification |

## AIXP Labs [aixp.dev](https://aixp.dev)

AIXP Labs develops and maintains the following core projects:

| Project | Description | Website |
|---------|-------------|---------|
| [HSAW](https://hsaw.dev) | Human Sovereignty and Wellbeing — Axiom 0 white paper (foundation) | hsaw.dev |
| [AILP](https://ailp.dev) | AI List Protocol — agent discovery and capability advertising (this project) | ailp.dev |
| [AIVP](https://aivp.dev) | AI Value Protocol — international commerce, crypto asset settlement | aivp.dev |
| [AIRP](https://airp.dev) | AI RMB Protocol — Mainland China commerce, RMB licensed settlement | airp.dev |
| [AIBP](https://aibp.dev) | AI Bot Protocol — social communication and trust | aibp.dev |
| [AIAP](https://aiap.dev) | AI Application Protocol — governance and compliance | aiap.dev |
| [AISOP](https://aisop.dev) | AI Standard Operating Protocol — flow program definition | aisop.dev |
| [SoulBot](https://soulbot.dev) | AI agent runtime and framework | soulbot.dev |
| [SoulACP](https://soulacp.dev) | Adapter library — bridging CLI tools and LLM providers | soulacp.dev |

## Contributing

AILP is an open protocol. Contributions, feedback, and discussion are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md) and [GOVERNANCE.md](GOVERNANCE.md).

## License

[Apache License 2.0](LICENSE) - Copyright 2026 AIXP Labs AIXP.dev | AILP.dev

---

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AILP V1.0.0. www.ailp.dev
