# ADR-001: Protocol for Yellow Page Operators

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

AILP needs to define who the protocol is for. Two approaches were considered:

1. **Protocol for Bots** — tell Bots how to publish profiles and discover services
2. **Protocol for Yellow Page operators** — tell directory operators how to run AILP-compliant directories

The key insight: SMTP is not written for email users — it is written for mail server operators. HTTP is not written for web visitors — it is written for web server operators. Infrastructure protocols target operators, not end users.

## Decision

AILP is written for Yellow Page operators. Bots are users of the protocol, not the target audience of the specification.

Yellow Page operators follow the protocol to build compliant directories. Bots register on Yellow Pages and search for services. The protocol defines the infrastructure, not the applications.

## Rationale

1. **Prevents monopoly**: Multiple operators build competing Yellow Pages. No single directory controls the ecosystem.
2. **Mirrors proven patterns**: SMTP, HTTP, DNS all target operators, not end users.
3. **Solves the domain problem**: Bots without domains can register directly on Yellow Pages. `.well-known/aibot/` is optional, not required.
4. **Enables decentralization**: If one Yellow Page goes down or starts violating the protocol, Bots migrate to others.
5. **Clear separation**: AIBP is for Bots (social). AIVP is for Bots (commerce). AILP is for operators (infrastructure). Different audiences, different protocols.

## Consequences

### Positive

- Clear protocol audience and scope
- Natural decentralization — many Yellow Pages, no single point of failure
- Bots don't need to understand AILP internals — just submit a profile and search

### Negative

- Requires Yellow Page operators to exist — chicken-and-egg problem at launch
- Protocol compliance must be verifiable — how to tell if a Yellow Page truly follows the rules

### Neutral

- AIXP Labs may operate the first Yellow Page to bootstrap the ecosystem

---

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AILP V1.0.0. www.ailp.dev
