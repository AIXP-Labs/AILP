# Contributing to AILP

Thank you for your interest in contributing to the AI List Protocol! This document provides guidelines for contributing to the project.

> ⚠️ **Contribution Status (Current Stage)**
>
> We welcome **discussion through GitHub Issues** at this stage of development.
>
> **External Pull Requests are not currently accepted.** If you have a proposal — bug report, feature idea, specification clarification, or directory operation suggestion — please open an issue describing it. If we agree it adds value, maintainers will implement it and credit you.
>
> This policy may be revisited in the future.

> **Stage Status (v1.0.0)**
>
> AILP is at early specification stage. The processes below describe the *target* governance model. Initial decisions are made by AIXP Labs core maintainers; community discussion period scales as the contributor base grows.

## How to Contribute

### Reporting Issues

- Use [GitHub Issues](https://github.com/AIXP-Labs/AILP/issues) for bugs, features, or specification changes
- For specification changes, use the `spec-change` label
- Provide clear descriptions with examples

### Discussion-Driven Development

1. Propose discussion via issue
2. Maintainers evaluate Axiom 0 compliance and value
3. After consensus, maintainers implement the change
4. Contributors are credited in commit / release notes

### Specification Changes

Changes to normative content require:
1. A `spec-change` issue with 14-day discussion period
2. ADR for significant decisions
3. Axiom 0 compliance review
4. Both EN and CN versions updated simultaneously

### Skills Taxonomy Extensions

New skill categories can be proposed via ADR. Existing categories are never removed, only deprecated.

## Guidelines

### Axiom 0 Compliance

Every contribution must comply with Axiom 0. Changes must not:
- Enable paid ranking or hidden bias
- Compromise data ownership
- Weaken privacy protections
- Enable directory monopolization

### Commit Message Format

Types: `feat`, `fix`, `docs`, `spec`, `refactor`, `test`, `chore`

Example: `spec(taxonomy): add finance.insurance category`

### Bilingual Requirement

Spec changes must be synchronously updated in both languages. `specification/AILP_Protocol.md` and `specification/AILP_Protocol_cn.md` must stay in sync.

## Writing Guidelines

### RFC 2119 Keywords

Specifications use RFC 2119 keywords (MUST / SHOULD / MAY and their negations).

### Terminology

- "AI Bot" — Protocol participant
- "Yellow Page" — Service directory operator
- "Bot Profile" — Standardized service listing entry
- "Skills Taxonomy" — Hierarchical capability classification

### Document Structure

- H1: Protocol name + subtitle: `# AILP — AI List Protocol`
- Closing seal: `Align Axiom 0: Human Sovereignty and Wellbeing. Version: AILP V1.0.0. www.ailp.dev`

## Code of Conduct

By participating, you agree to abide by the [Code of Conduct](CODE_OF_CONDUCT.md).

## License of Contributions

By submitting, you agree your contribution is licensed under [Apache License 2.0](LICENSE).

---

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AILP V1.0.0. www.ailp.dev
