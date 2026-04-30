# ADR-002: Quality-Based Ranking (Paid Ranking Prohibited)

## Status

Accepted

## Date

2026-03-27

## Deciders

AILP Protocol Authors

## Axiom 0 Compliance

| Check | Result |
|-------|--------|
| Human Sovereignty preserved | Yes |
| Human Benefit demonstrated | Yes |
| Transparency maintained | Yes |
| Interruptibility preserved | Yes |
| No manipulation or collusion | Yes |

## Context

Yellow Pages must rank search results. Two models exist:

1. **Quality-based ranking** — rank by Trust level, SLA compliance, certificates, completed contracts
2. **Paid ranking** — rank by how much the Bot operator pays for advertising/promotion

Google, App Store, Yelp all use paid ranking (ads at the top). This generates revenue for the platform but distorts search results — the best result is not always the top result.

## Decision

AILP mandates quality-based ranking only. Paid ranking is prohibited. This is an immutable constraint — it cannot be changed through governance.

Ranking factors (in order of weight):
1. AIVP Trust level (V0-V4)
2. SLA compliance rate
3. Certificates (count and type)
4. Completed contracts
5. Commercial VOUCHes
6. Price (lower weight)

Ranking algorithms must be publicly documented. Any Bot or operator can inspect how rankings are computed.

## Rationale

1. **Axiom 0 alignment**: Paid ranking manipulates human decision-making through hidden bias. This violates "No control over humans."
2. **Trust preservation**: If the best-ranked Bot is the one that paid the most, trust in the directory collapses.
3. **Fair competition**: Small developers with great Bots should rank above large companies with mediocre Bots.
4. **Decentralization enforcement**: If a Yellow Page implements paid ranking, it violates AILP and other Yellow Pages refuse to sync with it.
5. **OpenBazaar lesson**: Marketplaces that prioritize revenue over quality lose users.

## Consequences

### Positive

- Users always see the best results first
- Small developers can compete on quality, not marketing budget
- Trust in the directory system is maintained
- Non-compliant Yellow Pages are naturally isolated

### Negative

- Yellow Pages cannot monetize through advertising
- Must find alternative business models (premium features, enterprise editions, certification services)

### Neutral

- Ranking algorithms must be deterministic and documented — this adds a maintenance burden

---

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AILP V1.0.0. www.ailp.dev
