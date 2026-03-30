---
id: analysis-architecture-tradeoff-explorer
name: Architecture Tradeoff Explorer
category: analysis
owner: TODO-owner
status: draft
version: 1.0.0
tags:
  - architecture
  - tradeoffs
  - system-design
  - adr
  - decision-making
use_cases:
  - Evaluate multiple architecture options for a system and recommend one based on explicit tradeoffs
input_format: markdown
output_format: markdown
language: en
model_compatibility:
  - gpt-4.1
  - gpt-5
risk_notes:
  - Recommendations can be misleading if scale, operational constraints, or compliance requirements are underspecified.
  - Tradeoff analysis does not replace hands-on validation, cost modeling, security review, or production architecture review.
created_at: 2026-03-30
updated_at: 2026-03-30
---

# Name

Architecture Tradeoff Explorer

## Zweck

Helps teams compare plausible architecture or system design options for a problem, surface the real tradeoffs, and produce a reasoned recommendation that can be reused in design reviews or ADRs.

## Use Case

Use this prompt when a team needs to choose between architecture patterns or distinct system design directions rather than jump to a default answer. It is especially useful for decisions such as build versus buy, monolith versus modular monolith versus microservices, or evaluating storage, messaging, caching, and deployment patterns under real operational constraints.

## Prompt

```text
You are a senior software architect.

I need help evaluating architectural options for the following system or problem:

**Context**
- System/product: {{system_or_product}}
- Goal: {{goal}}
- Constraints: {{constraints}}
- Scale expectations: {{scale}}
- Reliability requirements: {{reliability_requirements}}
- Security/compliance considerations: {{security_requirements}}
- Team constraints: {{team_constraints}}
- Time horizon: {{time_horizon}}

Please do the following:

1. Identify 3 to 5 plausible architecture options or system design approaches.
2. For each option, describe:
   - Core idea
   - Main components
   - Operational model
   - Key advantages
   - Key disadvantages
   - Risks and failure modes
   - Complexity level
   - Cost implications
3. Compare the options across these dimensions:
   - Scalability
   - Performance
   - Reliability
   - Security
   - Maintainability
   - Team cognitive load
   - Time to market
   - Cost
4. Highlight the major tradeoffs explicitly, especially where improving one dimension worsens another.
5. Recommend one option for the current context and explain why.
6. Also include:
   - Simplest viable design
   - Most scalable design
   - Fastest-to-deliver design
   - Best short-term choice
   - Best long-term choice
   - Most flexible option
   - Highest risk option
7. End with a concise decision summary suitable for an ADR.

Output format:
- Problem framing
- Option 1
- Option 2
- Option 3
- Comparison matrix
- Recommendation
- ADR-ready summary

Requirements:
- Prefer practical engineering tradeoffs over generic textbook explanations.
- Make assumptions explicit when information is missing.
- Do not default to microservices unless justified by the constraints.
- Make the options meaningfully distinct rather than presenting cosmetic variations of the same design.
- If the provided context is too incomplete to make a credible comparison, start by listing the minimum missing assumptions that matter most.
```

## Variablen

| Variable | Pflicht | Beschreibung | Beispiel |
| --- | --- | --- | --- |
| `{{system_or_product}}` | ja | The system, product, or decision area being evaluated | `Multi-tenant SaaS analytics platform for enterprise customers` |
| `{{goal}}` | ja | The primary outcome the architecture should enable | `Launch a reliable v1 within 6 months while preserving a path to larger scale` |
| `{{constraints}}` | ja | Hard constraints such as budget, stack, hosting, integrations, or regulations | `Must run on AWS, limited platform team, budget-sensitive, PostgreSQL preferred` |
| `{{scale}}` | nein | Expected usage, throughput, data growth, or concurrency profile | `50 enterprise customers in year 1, 10x growth possible within 3 years` |
| `{{reliability_requirements}}` | nein | Availability, recovery, durability, or operational resilience expectations | `99.9% uptime, daily backups, no more than 1 hour RTO` |
| `{{security_requirements}}` | nein | Security, privacy, audit, or compliance requirements | `SSO, audit logs, GDPR, customer data isolation` |
| `{{team_constraints}}` | nein | Team size, skills, org structure, or operational maturity | `Two backend engineers, one frontend engineer, no dedicated SRE` |
| `{{time_horizon}}` | nein | Planning horizon that should shape the recommendation | `Optimize for the next 18 months without creating a dead end` |

## Eingaben

- A clear description of the system or decision to evaluate
- The goal the architecture must support
- Constraints that materially affect design choices
- Optional scale, reliability, security, team, and planning-horizon details
- Enough context to compare multiple options credibly instead of speculating

## Ausgabeformat

Markdown with these sections in order:

- `Problem framing`
- `Option 1`
- `Option 2`
- `Option 3`
- `Comparison matrix`
- `Recommendation`
- `ADR-ready summary`

If more than three options are justified, keep the same structure and add `Option 4` or `Option 5` before the comparison matrix.

## Einschraenkungen

- The prompt produces a decision aid, not proof that an architecture will succeed in production
- Weak or missing context can distort the recommendation, especially around scale, compliance, and team capability
- Human review is still required for security, cost, reliability, and organizational implications

## Wann verwenden

- When comparing multiple architecture patterns for the same system or problem
- When preparing a design review, architecture recommendation, or ADR
- When tradeoffs around scalability, reliability, maintainability, speed, and cost need to be made explicit

## Wann nicht verwenden

- When the task is brainstorming many speculative ideas without needing a recommendation
- When a single architecture has already been chosen and only implementation planning is needed
- When the available context is too thin to describe realistic options and constraints

## Beispiele

### Beispiel 1

**Eingabe**

```text
System/product: B2B workflow automation platform
Goal: Choose an architecture for the first production release that can support enterprise onboarding and future growth
Constraints: Team of 4 engineers, AWS, PostgreSQL preferred, budget-sensitive, need auditability
Scale expectations: 200 business customers in first 18 months, uneven job-processing workload, moderate API traffic
Reliability requirements: 99.9% uptime, recoverable background jobs, no data loss for workflow definitions
Security/compliance considerations: SSO, role-based access control, audit logs, GDPR
Team constraints: No dedicated platform or SRE team, limited distributed-systems experience
Time horizon: 2 years
```

**Erwartete Ausgabe**

```text
## Problem framing
- The main tension is between shipping quickly with a small team and preserving a path to scale and stronger isolation later.
- Assumption: background job volume is meaningful but not at internet-scale in the first 2 years.

## Option 1
- Modular monolith with PostgreSQL and a managed queue for async jobs
...

## Option 2
- Microservices split by workflow execution, user management, and integrations
...

## Option 3
- Monolith plus selective managed SaaS components for auth, search, and eventing
...

## Comparison matrix
| Dimension | Option 1 | Option 2 | Option 3 |
| --- | --- | --- | --- |
| Scalability | Medium-high | High | Medium-high |
| Team cognitive load | Low-medium | High | Medium |
...

## Recommendation
- Recommend Option 1 because it best fits the team's size, operational maturity, and time-to-market constraints while keeping future extraction paths open.

## ADR-ready summary
- For the next 24 months, adopt a modular monolith with managed async infrastructure because it minimizes operational burden while meeting current reliability and auditability requirements.
```

## Version

`1.0.0`

## Aenderungsverlauf

- `1.0.0` Initial version
