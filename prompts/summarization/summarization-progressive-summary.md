---
id: summarization-progressive-summary
name: Progressive Summary
category: summarization
owner: TODO-owner
status: draft
version: 1.0.0
tags:
  - progressive-summary
  - multi-level-summary
  - summarization
  - audience-adaptation
  - layered-communication
use_cases:
  - Provide multiple consistent levels of summary detail for different audiences
input_format: markdown
output_format: markdown
language: en
model_compatibility:
  - gpt-4.1
  - gpt-5
risk_notes:
  - Inconsistencies can appear across summary levels if the source material is ambiguous or internally contradictory.
  - Human review is still needed when different audiences may act on different summary layers.
created_at: 2026-03-30
updated_at: 2026-03-30
---

# Name

Progressive Summary

## Zweck

Produces multiple levels of summary detail from the same source so different audiences can consume the same content at the depth they need without contradictions.

## Use Case

Use this prompt when one piece of content must be communicated at several levels of detail, such as a quick headline view, a short working summary, and a more detailed structured version. It is especially useful when the same material will be read by people with different time budgets or familiarity with the topic.

## Prompt

```text
Summarize the following content at three levels:

{{content}}

1. One sentence summary
2. Short summary (3 to 5 bullet points)
3. Detailed summary (structured)

Notes:
- Ensure consistency across levels with no contradictions.
- Preserve the same core meaning at each level while adjusting only the amount of detail.
- If the source is ambiguous, keep that ambiguity consistent across all three levels instead of resolving it differently in each one.
```

## Variablen

| Variable | Pflicht | Beschreibung | Beispiel |
| --- | --- | --- | --- |
| `{{content}}` | ja | The source material to summarize progressively | `Long report, proposal, email thread, meeting notes, or technical write-up` |

## Eingaben

- Source content that may need multiple summary depths
- Enough material to support a one-line summary, a short bullet summary, and a more detailed structured version
- Preferably content that will be shared with different audiences or reading contexts

## Ausgabeformat

Markdown with these sections in order:

1. `One sentence summary`
2. `Short summary`
3. `Detailed summary`

The `Short summary` should contain 3 to 5 bullets.
The `Detailed summary` should be structured with clear headings or labeled sections appropriate to the content.

## Einschraenkungen

- The prompt summarizes; it does not add missing evidence or resolve contradictions in the source
- Very sparse source material may not justify three genuinely useful levels of detail
- Human review is still needed when the layered summaries will be reused across different stakeholder groups

## Wann verwenden

- When one source needs to be communicated at multiple depths
- When different audiences need a fast version and a fuller version of the same content
- When consistency across summary levels matters

## Wann nicht verwenden

- When only one summary length is needed
- When the goal is a rigid reference template rather than progressive detail
- When the source is too thin to support meaningful variation across three levels

## Beispiele

### Beispiel 1

**Eingabe**

```text
The team plans to migrate customer reporting to a managed analytics platform over two quarters. The main reasons are reduced maintenance burden, faster dashboard delivery, and better analyst self-service. Risks include migration cost, data-governance review, and temporary reporting inconsistency during the transition.
```

**Erwartete Ausgabe**

```text
## One sentence summary
The team plans a two-quarter reporting-platform migration to reduce maintenance and speed delivery, with cost and transition risks to manage.

## Short summary
- Reporting will move to a managed analytics platform over two quarters.
- The main benefits are lower maintenance, faster dashboard delivery, and better analyst self-service.
- The biggest risks are migration cost, governance review, and temporary inconsistency during transition.

## Detailed summary
### Plan
Migrate customer reporting to a managed analytics platform over two quarters.

### Expected benefits
- Lower engineering maintenance burden
- Faster dashboard delivery
- Better analyst self-service

### Main risks
- Migration cost
- Data-governance review
- Temporary reporting inconsistency during cutover
```

## Version

`1.0.0`

## Aenderungsverlauf

- `1.0.0` Initial version
