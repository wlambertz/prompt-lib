---
id: summarization-tldr-generator
name: TL;DR Generator
category: summarization
owner: TODO-owner
status: draft
version: 1.0.0
tags:
  - tldr
  - short-summary
  - summarization
  - quick-scan
  - compression
use_cases:
  - Produce an ultra-short summary for fast scanning of longer content
input_format: markdown
output_format: markdown
language: en
model_compatibility:
  - gpt-4.1
  - gpt-5
risk_notes:
  - Extreme compression can omit nuance, caveats, or secondary points.
  - Human review is still needed when short summaries could be mistaken for complete understanding.
created_at: 2026-03-30
updated_at: 2026-03-30
---

# Name

TL;DR Generator

## Zweck

Produces an ultra-short summary that preserves only the core meaning of longer content for very fast understanding.

## Use Case

Use this prompt for long texts, articles, emails, or Slack threads when the reader needs a quick scan rather than a full summary. It is especially useful when space or attention is limited and the output must stay extremely compact.

## Prompt

```text
Summarize the following content into:

1. One sentence TL;DR
2. Three bullet points capturing the essence

{{content}}

Constraints:
- Maximum 50 words total
- Preserve core meaning only

Notes:
- This is for fast scanning, not deep understanding.
- Omit secondary detail, examples, and supporting nuance unless they are essential to the core meaning.
- If the source is ambiguous, keep the summary cautious rather than overconfident.
```

## Variablen

| Variable | Pflicht | Beschreibung | Beispiel |
| --- | --- | --- | --- |
| `{{content}}` | ja | The source material to compress into a TL;DR plus three bullets | `Long email thread, article, or multi-message Slack discussion` |

## Eingaben

- Longer content such as articles, emails, threads, or documents
- Enough substance to identify a core message worth compressing
- Material where fast understanding matters more than detail retention

## Ausgabeformat

Markdown with:

1. One sentence `TL;DR`
2. Three bullet points

Keep the total output under 50 words.

## Einschraenkungen

- The prompt is intentionally lossy and should not be treated as a substitute for the full content
- Complex or ambiguous source material may not compress cleanly into 50 words
- Human review is still needed when omitted nuance could affect interpretation

## Wann verwenden

- When someone needs the essence of long content in seconds
- When the output must be extremely short and scannable
- When a fuller executive or structured summary would be too long

## Wann nicht verwenden

- When implications, risks, or recommended actions need to be preserved explicitly
- When the audience needs a structured reference rather than a compressed snapshot
- When the source content is too complex for a reliable ultra-short summary

## Beispiele

### Beispiel 1

**Eingabe**

```text
The product team discussed delaying the dashboard redesign by one sprint so engineering can stabilize the billing migration. Everyone agreed billing reliability is the current priority, but leadership still wants a visible roadmap update and a lightweight progress report for customers.
```

**Erwartete Ausgabe**

```text
TL;DR: The dashboard redesign is slipping one sprint so the team can prioritize billing migration stability.

- Billing reliability is the immediate priority.
- Leadership still wants a roadmap update.
- Customers need a lightweight progress report.
```

## Version

`1.0.0`

## Aenderungsverlauf

- `1.0.0` Initial version
