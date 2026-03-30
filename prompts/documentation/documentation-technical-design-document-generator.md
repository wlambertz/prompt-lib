---
id: documentation-technical-design-document-generator
name: Technical Design Document Generator
category: documentation
owner: TODO-owner
status: draft
version: 1.0.0
tags:
  - technical-design
  - architecture
  - design-doc
  - documentation
  - implementation-planning
use_cases:
  - Generate a structured technical design document before implementation or design review
input_format: markdown
output_format: markdown
language: en
model_compatibility:
  - gpt-4.1
  - gpt-5
risk_notes:
  - The document can overstate completeness if requirements, constraints, or solution details are weak.
  - Generated design docs still require human review for feasibility, cross-team dependencies, and implementation accuracy.
created_at: 2026-03-30
updated_at: 2026-03-30
---

# Name

Technical Design Document Generator

## Zweck

Generates a comprehensive technical design document from structured design context so teams can align before implementation and review a proposed solution in a consistent format.

## Use Case

Use this prompt before implementation, during design reviews, or when multiple teams need alignment on a proposed feature or system change. It is especially useful when the core solution exists already but needs to be documented with goals, non-goals, architecture, interfaces, rollout considerations, and open questions.

## Prompt

```text
You are a senior engineer writing a technical design document.

**Feature/system**
{{feature}}

**Problem statement**
{{problem}}

**Goals**
{{goals}}

**Non-goals**
{{non_goals}}

**Constraints**
{{constraints}}

**Proposed solution**
{{solution}}

**Alternatives considered**
{{alternatives}}

**Risks**
{{risks}}

Produce:

1. Overview
2. Problem Statement
3. Goals / Non-goals
4. Requirements (functional + non-functional)
5. High-level architecture
6. Detailed design
7. Data model (if applicable)
8. API/interface changes
9. Alternatives considered
10. Risks and mitigations
11. Rollout plan
12. Open questions

Requirements:
- Prioritize clarity over verbosity.
- Make assumptions explicit.
- Keep the document grounded in the provided context rather than inventing unspecified subsystems.
- Distinguish clearly between confirmed details and inferred details.
- If a section is not applicable, say so briefly instead of forcing fake detail.
```

## Variablen

| Variable | Pflicht | Beschreibung | Beispiel |
| --- | --- | --- | --- |
| `{{feature}}` | ja | The feature, service, or system being designed | `Event-driven invoice reconciliation service` |
| `{{problem}}` | ja | The problem statement or motivation for the design | `Current reconciliation is manual, slow, and error-prone across multiple payment sources` |
| `{{goals}}` | ja | The primary goals the design should satisfy | `Reduce reconciliation latency, improve auditability, and support retryable processing` |
| `{{non_goals}}` | nein | What the design intentionally does not attempt to solve | `Replacing the billing platform, redesigning finance reporting workflows` |
| `{{constraints}}` | nein | Technical, org, compliance, or delivery constraints | `AWS only, PostgreSQL preferred, 3-engineer team, must launch in Q3` |
| `{{solution}}` | ja | The proposed design or implementation direction | `Async worker pipeline with ingestion, normalization, matching, and review queues` |
| `{{alternatives}}` | nein | Other solutions considered and why they differ | `Synchronous processing inside the billing service, external reconciliation SaaS` |
| `{{risks}}` | nein | Known risks, uncertainties, or failure areas | `False matches, queue backlog growth, integration inconsistency across payment providers` |

## Eingaben

- The feature or system being designed
- A clear problem statement and goals
- The proposed solution
- Optional non-goals, constraints, alternatives, and risks
- Enough context to produce a useful design artifact instead of generic architecture prose

## Ausgabeformat

Markdown with these sections in order:

1. `Overview`
2. `Problem Statement`
3. `Goals / Non-goals`
4. `Requirements`
5. `High-level architecture`
6. `Detailed design`
7. `Data model`
8. `API/interface changes`
9. `Alternatives considered`
10. `Risks and mitigations`
11. `Rollout plan`
12. `Open questions`

Within the document, make assumptions explicit when details are inferred from incomplete input.

## Einschraenkungen

- The prompt creates a design document, not a proof that the proposed solution is correct
- Weak inputs produce generic or misleading design sections
- Human review is still required for technical correctness, feasibility, and coordination across teams

## Wann verwenden

- When a team needs a structured technical design document before implementation
- When a proposal needs to be reviewed across engineering or adjacent teams
- When architecture, interfaces, rollout, and risks should be documented in one place

## Wann nicht verwenden

- When only a short ADR or decision summary is needed
- When the solution has not been formed enough to describe a proposed design
- When the task is to compare options rather than document a selected proposal

## Beispiele

### Beispiel 1

**Eingabe**

```text
Feature/system:
Event-driven invoice reconciliation service

Problem statement:
Current reconciliation is manual, slow, and error-prone across multiple payment providers.

Goals:
- Reduce reconciliation latency from days to minutes
- Improve auditability
- Support retryable processing and operator review

Non-goals:
- Replacing the billing platform
- Rebuilding downstream reporting

Constraints:
- AWS only
- PostgreSQL preferred
- Small team
- Must be incremental

Proposed solution:
Introduce an async reconciliation pipeline with ingestion, normalization, matching, exception handling, and operator review.

Alternatives considered:
- Keep reconciliation inside the billing service
- Buy an external reconciliation platform

Risks:
- Queue backlog under spikes
- False-positive matches
- Provider-specific data inconsistencies
```

**Erwartete Ausgabe**

```text
## Overview
This document proposes an event-driven reconciliation service that reduces manual effort while preserving auditability and incremental rollout.

## Problem Statement
Manual reconciliation creates latency, inconsistency, and operational risk across provider integrations.

## Goals / Non-goals
Goals:
- Reduce reconciliation latency
- Improve auditability
- Support retries and exception handling

Non-goals:
- Replace billing platform
- Rebuild reporting

## Requirements
...

## High-level architecture
...

## Detailed design
...

## Rollout plan
- Pilot on one payment provider
- Add monitoring and exception review
- Expand provider coverage incrementally

## Open questions
- What confidence threshold should trigger automatic matching?
```

## Version

`1.0.0`

## Aenderungsverlauf

- `1.0.0` Initial version
