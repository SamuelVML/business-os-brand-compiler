# Business OS Brand Compiler

Evidence-driven compiler for turning a company's existing brand material into validated configuration for **Business OS Template**.

## Boundary

This repository interprets brand evidence. It does not own the Business OS runtime and does not deploy customer instances.

```
website / Figma / brand book / copy / assets / questionnaire
                         ↓
                   evidence layer
                         ↓
             extraction + interpretation
                         ↓
          normalized Brand Contract + provenance
                         ↓
                  validation/admission
                         ↓
            Business OS instance export
```

AI providers such as Claude are adapters behind the compiler contract. The contract is provider-neutral.

## Core rules

1. Extracted facts and model inferences are different evidence classes.
2. Every non-user-authored compiled value carries provenance and confidence.
3. Explicit customer/designer confirmation outranks inference.
4. Conflicting evidence is surfaced, not silently resolved.
5. Low-confidence required fields block automatic admission.
6. Secrets, customer operational data and unrelated PII are not brand inputs.
7. The compiler never mutates source evidence.
8. Output must validate against the Business OS instance contract before export.

## Planned structure

- `src/contracts` — canonical evidence, brand and export contracts.
- `src/ingest` — provider-neutral evidence ingestion.
- `src/providers` — Claude/manual/Figma/etc. adapters.
- `src/compiler` — evidence resolution and normalization.
- `src/validation` — conflicts, confidence and admission gates.
- `src/export` — Business OS Template export.
- `docs` — architecture, provider and governance specifications.

## Status

Contract-first foundation. No external AI provider is authoritative by itself.
