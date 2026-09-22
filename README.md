# Business OS Brand Compiler

Evidence-driven compiler for turning a company's existing brand material into validated configuration for **Business OS Template**.

## Boundary

This repository interprets brand evidence. It does not own the Business OS runtime and does not deploy customer instances.

## Canonical pipeline

```
website / Figma / brand book / copy / assets / questionnaire
                         ↓
                      EVIDENCE
                         ↓
                    PROVENANCE
                         ↓
          AUTHORITY + EVIDENCE CONFIDENCE
                         ↓
                   INTERPRETATION
                         ↓
             INTERPRETATION CONFIDENCE
                         ↓
                CONFLICT RESOLUTION
                         ↓
          NORMALIZED CANDIDATE CONTRACT
                         ↓
                   ADMISSION GATE
                         ↓
             APPROVED BRAND CONTRACT
                         ↓
               BUSINESS OS EXPORT
```

The ordering is intentional. Evidence is assessed before it is interpreted. The compiler must know where a fact came from, how authoritative that source is, and how reliable the evidence is before an interpretation layer may reason over it.

Interpretation has a separate confidence assessment. A high-authority source does not automatically make every interpretation drawn from it certain.

Only admitted values may enter the approved Brand Contract and be exported to Business OS.

AI providers such as Claude are adapters behind the compiler contract. The contract is provider-neutral.

## Evidence states

A compiled value must distinguish at least:

- **extracted** — explicitly present in source evidence.
- **inferred** — derived from one or more pieces of evidence.
- **suggested** — generated where authoritative evidence is absent.
- **designer-confirmed** — explicitly confirmed by an authorized designer.
- **customer-confirmed** — explicitly confirmed by the customer.

Confirmation changes authority; it does not rewrite or erase the underlying evidence trail.

## Authority

The default authority hierarchy is:

```
customer-confirmed
        ↓
designer-confirmed
        ↓
explicit official design-system rule
        ↓
explicit official brand-guideline rule
        ↓
consistent observed pattern
        ↓
AI inference
        ↓
AI suggestion
```

Recency, scope and explicit supersession must also be considered. Authority is not a license to silently discard conflicting evidence.

## Confidence

The compiler maintains two distinct confidence concepts:

1. **Evidence confidence** — confidence that the evidence was extracted/identified correctly and means what its provenance says it means.
2. **Interpretation confidence** — confidence in the conclusion derived from the admitted evidence set.

Neither score alone grants production authority.

## Conflict resolution

Conflicting evidence must be preserved and surfaced. Resolution may use authority, recency, scope and explicit supersession, but unresolved material conflicts must reach human review rather than being silently decided by a model.

Example:

```
2026 official Figma token → green → HIGH authority
legacy website CSS        → blue  → MEDIUM authority

Interpretation:
green probably supersedes blue

Interpretation confidence:
0.94

Admission:
human review if supersession is not explicit
```

## Admission

Admission is the governance boundary between proposed understanding and production configuration.

The admission gate may:

- auto-admit sufficiently authoritative, non-conflicting values;
- require human review;
- require customer/designer confirmation;
- reject malformed or unsupported values;
- block export when required fields remain unresolved.

Business OS consumes the **Approved Brand Contract**, never raw model output or an unreviewed candidate contract.

## Core rules

1. Extracted facts, interpretations and model suggestions are different evidence classes.
2. Provenance is established before interpretation.
3. Evidence authority/confidence and interpretation confidence are separate.
4. Every non-user-authored compiled value retains its evidence trail.
5. Explicit customer/designer confirmation outranks inference.
6. Conflicting evidence is surfaced, not silently resolved.
7. Low-confidence or materially conflicting required fields block automatic admission.
8. Secrets, customer operational data and unrelated PII are not brand inputs.
9. The compiler never mutates source evidence.
10. Only an Approved Brand Contract may be exported to Business OS.
11. Output must validate against the Business OS instance contract before export.

## Planned structure

- `src/contracts` — canonical evidence, provenance, candidate, approved brand and export contracts.
- `src/ingest` — provider-neutral evidence ingestion.
- `src/provenance` — source identity, authority, recency and evidence confidence.
- `src/providers` — Claude/manual/Figma/etc. adapters.
- `src/compiler` — interpretation and normalization.
- `src/conflicts` — conflict detection and resolution records.
- `src/admission` — human/automatic admission gates.
- `src/validation` — schema and Business OS compatibility validation.
- `src/export` — Business OS Template export.
- `docs` — architecture, provider and governance specifications.

## Status

Contract-first foundation. No external AI provider is authoritative by itself.
