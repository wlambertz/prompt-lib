---
id: summarization-executive-summary-generator
name: Executive Summary Generator
category: summarization
owner: TODO-owner
status: draft
version: 1.0.0
tags:
  - executive-summary
  - stakeholder-summary
  - decision-support
  - summarization
  - strategy
use_cases:
  - Produce a concise, decision-oriented summary of longer material for senior stakeholders
input_format: markdown
output_format: markdown
language: en
model_compatibility:
  - gpt-4.1
  - gpt-5
risk_notes:
  - Overcompression can hide nuance or important caveats when the source material is ambiguous or highly technical.
  - Executive summaries still require human review when the stakes are high or when omitted detail could change the decision.
created_at: 2026-03-30
updated_at: 2026-03-30
---

# Name

Executive Summary Generator

## Zweck

Produces a concise, decision-oriented summary for senior stakeholders who need the core context, implications, risks, and recommended action without reading the full source material.

## Use Case

Use this prompt for reports, strategy documents, technical proposals, or long analyses when the audience has limited time and mainly needs to understand what matters and what action to take. It is especially useful when the source material is detailed but the output must stay brief and decision-focused.

## Prompt

```text
You are an expert in executive communication.

Summarize the following content for a senior decision-maker:

{{content}}

Produce:

1. Context (1 to 2 sentences)
2. Key points (3 to 5 bullet points)
3. Implications (why this matters)
4. Risks / concerns
5. Recommended action

Constraints:
- Maximum 200 words
- No unnecessary detail
- Focus on decisions, not description

Notes:
- Assume the reader has very limited time and needs to act.
- Make the summary decision-oriented rather than explanatory.
- If the source material is ambiguous, reflect uncertainty briefly instead of inventing confidence.
```

## Variablen

| Variable | Pflicht | Beschreibung | Beispiel |
| --- | --- | --- | --- |
| `{{content}}` | ja | The report, proposal, analysis, or source material to summarize | `Six-page proposal comparing vendor migration options, projected costs, timeline, and operational risks` |

## Eingaben

- Source content such as a report, proposal, analysis, or strategy document
- Enough context in the source to identify implications, risks, and a plausible recommended action
- Preferably material that is longer or denser than the target executive summary

## Ausgabeformat

Markdown with these sections in order:

1. `Context`
2. `Key points`
3. `Implications`
4. `Risks / concerns`
5. `Recommended action`

Keep the full response within 200 words.

## Einschraenkungen

- The prompt summarizes existing material; it does not replace the underlying analysis
- If the source content lacks a clear recommendation basis, the output may remain necessarily tentative
- Human review is still needed when the summary will drive sensitive strategic, legal, or financial decisions

## Wann verwenden

- When a senior stakeholder needs a fast, decision-oriented summary of longer content
- When reports or proposals need to be condensed into an executive briefing
- When the main goal is to surface implications and next action rather than preserve full detail

## Wann nicht verwenden

- When the audience needs a detailed walkthrough instead of a compressed summary
- When the source material is too incomplete to support implications or a recommended action
- When the task is to persuade, announce, or communicate status rather than summarize existing content

## Beispiele

### Beispiel 1

**Eingabe**

```text
A technical proposal compares keeping the current reporting pipeline versus migrating to a managed analytics platform. The proposal highlights lower operational burden and faster feature delivery with the managed platform, but notes migration cost, vendor dependency, and data-governance review requirements. The current system is cheaper short term but slows delivery and creates recurring maintenance overhead. Leadership needs to decide whether to fund migration this quarter.
```

**Erwartete Ausgabe**

```text
## Context
Leadership must decide whether to fund a reporting-platform migration this quarter.

## Key points
- A managed analytics platform would reduce operational burden and speed feature delivery.
- The current pipeline is cheaper short term but continues to slow execution and consume engineering time.
- Migration introduces upfront cost, vendor dependency, and governance work.

## Implications
Delaying the move preserves short-term budget but likely extends delivery drag and maintenance overhead.

## Risks / concerns
Migration cost, vendor lock-in, and unresolved data-governance requirements.

## Recommended action
Approve migration planning now, contingent on governance sign-off and a phased rollout plan.
```

## Version

`1.0.0`

## Aenderungsverlauf

- `1.0.0` Initial version
