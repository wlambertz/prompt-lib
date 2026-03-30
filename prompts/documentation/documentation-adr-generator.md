---
id: documentation-adr-generator
name: ADR Generator
category: documentation
owner: TODO-owner
status: draft
version: 1.0.0
tags:
  - adr
  - architecture
  - decision-record
  - documentation
  - tradeoffs
use_cases:
  - Convert architecture decision context into a structured Architecture Decision Record
input_format: markdown
output_format: markdown
language: en
model_compatibility:
  - gpt-4.1
  - gpt-5
risk_notes:
  - The ADR can be misleading if the provided decision context is incomplete or biased toward the chosen option.
  - Generated ADRs still require human review for factual accuracy, decision ownership, and organizational alignment.
created_at: 2026-03-30
updated_at: 2026-03-30
---

# Name

ADR Generator

## Zweck

Generates a structured Architecture Decision Record from design context so teams can document architecture decisions, rationale, alternatives, and consequences in a durable format.

## Use Case

Use this prompt after architecture discussions or during system design decisions when the team needs a clear written ADR instead of loose notes. It is especially useful when tradeoffs, constraints, and alternatives have already been discussed but not yet documented consistently.

## Prompt

```text
You are a senior software architect.

Convert the following information into a well-structured Architecture Decision Record (ADR):

**Context**
{{context}}

**Decision drivers**
{{decision_drivers}}

**Options considered**
{{options}}

**Chosen option**
{{chosen_option}}

**Tradeoffs**
{{tradeoffs}}

**Constraints**
{{constraints}}

Please produce an ADR with:

1. Title
2. Status (Proposed / Accepted / Deprecated)
3. Context
4. Decision
5. Decision Drivers
6. Alternatives Considered (with pros/cons)
7. Consequences (positive and negative)
8. Risks and mitigations

Requirements:
- Be concise but precise.
- Make tradeoffs explicit.
- Avoid vague language.
- If the inputs are incomplete, make the minimum necessary assumptions explicit rather than inventing hidden rationale.
- Keep the ADR neutral and documentation-oriented rather than persuasive or promotional.
```

## Variablen

| Variable | Pflicht | Beschreibung | Beispiel |
| --- | --- | --- | --- |
| `{{context}}` | ja | Background on the system, decision area, and current situation | `Multi-tenant SaaS platform needs a background job architecture for async processing and retries` |
| `{{decision_drivers}}` | ja | Main factors driving the decision | `Operational simplicity, auditability, reliability, team familiarity, and time to market` |
| `{{options}}` | ja | The options that were considered | `Modular monolith with queue, microservices split by domain, managed workflow engine` |
| `{{chosen_option}}` | ja | The selected option to document in the ADR | `Modular monolith with managed queue` |
| `{{tradeoffs}}` | ja | Important tradeoffs, pros/cons, and compromises | `Lower operational complexity now, but weaker service isolation than a microservice approach` |
| `{{constraints}}` | nein | Budget, team, technical, regulatory, or timing constraints | `Small team, AWS, PostgreSQL preference, no dedicated SRE, enterprise audit requirements` |

## Eingaben

- Architecture decision context with enough detail to explain why a decision was made
- Clear decision drivers and alternatives
- The chosen option and its tradeoffs
- Optional constraints that shaped the decision

## Ausgabeformat

Markdown ADR with these sections in order:

1. `Title`
2. `Status`
3. `Context`
4. `Decision`
5. `Decision Drivers`
6. `Alternatives Considered`
7. `Consequences`
8. `Risks and mitigations`

Under `Alternatives Considered`, each alternative should include concise pros and cons.
Under `Consequences`, include both positive and negative outcomes.

## Einschraenkungen

- The prompt documents a decision; it does not validate whether the decision is actually correct
- Missing or weak alternatives reduce the usefulness of the ADR
- Human review is still required for ownership, accuracy, and organizational acceptance

## Wann verwenden

- When architecture discussions need to be turned into a durable ADR
- When tradeoffs and rationale should be documented for future maintainers
- When the decision exists already and the main need is structured documentation

## Wann nicht verwenden

- When the architecture decision has not been explored yet and options still need evaluation
- When only a short recommendation or summary is needed instead of a formal record
- When the provided information is too thin to document credible rationale or alternatives

## Beispiele

### Beispiel 1

**Eingabe**

```text
Context:
The platform needs a reliable way to run asynchronous workflow jobs with retries and auditability.

Decision drivers:
- Small engineering team
- Fast time to market
- Operational simplicity
- Audit requirements

Options considered:
- Modular monolith with a managed queue
- Microservices split into workflow, user, and integration services
- External workflow orchestration platform

Chosen option:
Modular monolith with a managed queue

Tradeoffs:
- Easier to operate now than microservices
- Less isolation than a service split
- Lower initial complexity than adopting an external workflow platform

Constraints:
- AWS environment
- PostgreSQL preferred
- No dedicated SRE team
```

**Erwartete Ausgabe**

```text
# Title
ADR: Background job architecture for asynchronous workflows

## Status
Proposed

## Context
The platform requires asynchronous job execution with retry handling and auditability while keeping operations manageable for a small team.

## Decision
Adopt a modular monolith with a managed queue for asynchronous workflow processing.

## Decision Drivers
- Operational simplicity
- Time to market
- Auditability
- Team familiarity

## Alternatives Considered
### Modular monolith with a managed queue
- Pros: Lower operational burden, faster delivery, simpler debugging
- Cons: Less isolation and independent scaling than microservices

### Microservices split by domain
- Pros: Stronger isolation and scaling flexibility
- Cons: Higher operational complexity and coordination cost

### External workflow orchestration platform
- Pros: Rich workflow features and built-in orchestration
- Cons: Added vendor dependency and onboarding complexity

## Consequences
- Positive: Faster delivery and simpler operations for the current team
- Negative: Future extraction work may be needed if workload or team complexity grows

## Risks and mitigations
- Risk: Queue backlog handling may become weak under growth
- Mitigation: Add backlog monitoring and revisit service extraction thresholds later
```

## Version

`1.0.0`

## Aenderungsverlauf

- `1.0.0` Initial version
