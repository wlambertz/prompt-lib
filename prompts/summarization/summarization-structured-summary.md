---
id: summarization-structured-summary
name: Structured Summary
category: summarization
owner: TODO-owner
status: draft
version: 1.0.0
tags:
  - structured-summary
  - notes
  - meeting-notes
  - knowledge-capture
  - summarization
use_cases:
  - Convert unstructured content into a structured, scannable summary format
input_format: markdown
output_format: markdown
language: en
model_compatibility:
  - gpt-4.1
  - gpt-5
risk_notes:
  - Important nuance can be lost if the source material is disorganized or contradictory.
  - Human review is still needed when decisions, action items, or open questions affect downstream work.
created_at: 2026-03-30
updated_at: 2026-03-30
---

# Name

Structured Summary

## Zweck

Converts unstructured content into a precise, scannable format that makes topics, objectives, key concepts, decisions, action items, and open questions easier to review quickly.

## Use Case

Use this prompt for documentation, meeting notes, technical content, or knowledge-base material when the source is messy or free-form but the output needs stable headings. It is especially useful when readers need a structured reference instead of a narrative summary.

## Prompt

```text
You are a structured note-taking assistant.

Summarize the following content:

{{content}}

Output in this structure:

- Topic:
- Objective:
- Key concepts:
- Important details:
- Decisions (if any):
- Action items (if any):
- Open questions:

Notes:
- Be precise and structured.
- Do not omit critical information.
- If a section does not apply, say so briefly instead of inventing content.
- Preserve important decisions, action items, and unresolved questions when they are present.
```

## Variablen

| Variable | Pflicht | Beschreibung | Beispiel |
| --- | --- | --- | --- |
| `{{content}}` | ja | The unstructured source material to convert into a structured summary | `Raw meeting notes, technical draft, or copied documentation text` |

## Eingaben

- Unstructured or loosely organized content
- Material such as meeting notes, documentation drafts, technical explanations, or knowledge-base inputs
- Enough content to identify topic, objective, details, and any decisions or actions

## Ausgabeformat

Markdown using exactly these fields in order:

- `Topic`
- `Objective`
- `Key concepts`
- `Important details`
- `Decisions (if any)`
- `Action items (if any)`
- `Open questions`

Use concise bullets or short sentences under each field.

## Einschraenkungen

- The prompt reorganizes content; it does not resolve contradictions in the source
- Weak or incomplete source material may leave some sections sparse
- Human review is still needed when action items or decisions will be used operationally

## Wann verwenden

- When unstructured content needs to become a structured reference
- When meeting or technical notes should be made easier to scan
- When decisions and action items need to be preserved in a predictable layout

## Wann nicht verwenden

- When a short executive briefing is needed instead of a structured reference format
- When the main goal is analytical interpretation rather than reformatting and organizing
- When the source content is too incomplete to infer a topic or objective responsibly

## Beispiele

### Beispiel 1

**Eingabe**

```text
Discussion covered the billing migration timeline, the need to avoid customer invoice disruption, and a proposal to run the new reconciliation flow in parallel for two weeks. The team agreed to keep the current export format for finance, revisit dashboard requirements later, and assign Maria to confirm data backfill steps. Open concern remains whether legacy edge cases are fully covered.
```

**Erwartete Ausgabe**

```text
- Topic:
  Billing migration and reconciliation rollout
- Objective:
  Plan a safer transition to the new billing flow without disrupting invoice handling
- Key concepts:
  Parallel run, export compatibility, reconciliation flow, backfill validation
- Important details:
  The team wants a two-week parallel run and to preserve the current finance export format during migration.
- Decisions (if any):
  Keep the current export format for finance and defer dashboard requirement changes.
- Action items (if any):
  Maria to confirm data backfill steps.
- Open questions:
  Whether legacy billing edge cases are fully covered.
```

## Version

`1.0.0`

## Aenderungsverlauf

- `1.0.0` Initial version
