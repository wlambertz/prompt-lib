---
id: analysis-key-insights-extractor
name: Key Insights Extractor
category: analysis
owner: TODO-owner
status: draft
version: 1.0.0
tags:
  - insights
  - analysis
  - research
  - interpretation
  - synthesis
use_cases:
  - Extract the most important insights, non-obvious findings, and open questions from source material
input_format: markdown
output_format: markdown
language: en
model_compatibility:
  - gpt-4.1
  - gpt-5
risk_notes:
  - Insight extraction can become shallow or biased if the source content is weak, ambiguous, or highly technical without context.
  - The prompt interprets meaning from material, so human review is still needed when conclusions may affect high-stakes decisions.
created_at: 2026-03-30
updated_at: 2026-03-30
---

# Name

Key Insights Extractor

## Zweck

Extracts the most important insights from content by focusing on meaning, implications, surprising findings, and unresolved questions rather than restating what was said.

## Use Case

Use this prompt for research papers, reports, meeting transcripts, or market analyses when the goal is to identify what actually matters in the material. It is especially useful when a plain summary would repeat obvious points instead of surfacing interpretation, novelty, or gaps.

## Prompt

```text
You are an analytical reader.

From the following content:

{{content}}

Extract:

1. 5 to 10 key insights
2. For each insight:
   - Explanation (1 to 2 sentences)
   - Why it matters
3. Surprising or non-obvious findings
4. Missing information or open questions

Notes:
- Focus on meaning, not repetition.
- Avoid restating obvious points.
- Prefer insights that change interpretation, priorities, or understanding.
- If the material is incomplete or ambiguous, make uncertainty explicit rather than filling gaps with assumptions.
```

## Variablen

| Variable | Pflicht | Beschreibung | Beispiel |
| --- | --- | --- | --- |
| `{{content}}` | ja | The source material to interpret and extract insights from | `Research summary on customer churn drivers, interview notes, and supporting usage metrics` |

## Eingaben

- Source content such as research papers, reports, transcripts, or market analysis
- Enough substance in the material to support interpretation beyond simple summary
- Preferably material where hidden patterns, implications, or unknowns matter

## Ausgabeformat

Markdown with these sections in order:

1. `Key insights`
2. `Surprising or non-obvious findings`
3. `Missing information or open questions`

Under `Key insights`, provide 5 to 10 insights.
For each insight, include:
- `Insight`
- `Explanation`
- `Why it matters`

## Einschraenkungen

- The prompt highlights interpretation, not exhaustive coverage of the source
- Thin or low-quality inputs may produce generic insights
- Human review is still needed to validate whether the extracted insights are fair, complete, and decision-relevant

## Wann verwenden

- When the goal is to understand the most meaningful takeaways from dense material
- When non-obvious findings and unresolved questions matter as much as summary
- When a standard summary would be too descriptive and not analytical enough

## Wann nicht verwenden

- When a short stakeholder-ready summary is needed instead of analytical insight extraction
- When the source material is too sparse to support interpretation
- When the task is to rewrite or communicate the content rather than analyze it

## Beispiele

### Beispiel 1

**Eingabe**

```text
A market analysis on collaboration software adoption shows that buyers increasingly prioritize workflow integration over standalone feature depth. Interview notes suggest that security concerns remain table stakes rather than differentiators, while onboarding friction is a major source of churn. The report also notes that smaller customers adopt faster but expand less reliably than enterprise accounts.
```

**Erwartete Ausgabe**

```text
## Key insights
- Insight: Integration quality appears to be a stronger buying driver than raw feature breadth.
  - Explanation: The analysis suggests buyers care more about how tools fit existing workflows than about isolated capability depth.
  - Why it matters: Product and go-to-market priorities may need to shift toward ecosystem fit rather than feature expansion.

- Insight: Onboarding friction is likely a bigger commercial risk than baseline security positioning.
  - Explanation: Security is treated as expected, while onboarding problems are tied more directly to churn behavior.
  - Why it matters: Investment in activation and early user experience may yield more retention impact than additional security messaging.

## Surprising or non-obvious findings
- Smaller customers adopt faster, but that speed does not translate cleanly into durable expansion.

## Missing information or open questions
- Which specific onboarding frictions are most predictive of churn?
- Does the integration preference vary by customer segment or company size?
```

## Version

`1.0.0`

## Aenderungsverlauf

- `1.0.0` Initial version
