---
id: analysis-compare-and-summarize
name: Compare and Summarize
category: analysis
owner: TODO-owner
status: draft
version: 1.0.0
tags:
  - comparison
  - synthesis
  - analysis
  - evaluation
  - recommendation
use_cases:
  - Compare multiple inputs and produce a balanced summary, synthesis, and optional recommendation
input_format: markdown
output_format: markdown
language: en
model_compatibility:
  - gpt-4.1
  - gpt-5
risk_notes:
  - Comparisons can become misleading if the inputs are uneven in detail, quality, or scope.
  - Recommendations still require human review when criteria, priorities, or context are incomplete.
created_at: 2026-03-30
updated_at: 2026-03-30
---

# Name

Compare and Summarize

## Zweck

Summarizes and compares multiple inputs in a balanced way so teams can understand similarities, differences, tradeoffs, and an overall synthesis without bias toward any single option.

## Use Case

Use this prompt for tool comparisons, architecture options, vendor evaluations, or research synthesis when multiple inputs need to be reviewed side by side. It is especially useful when the main value is not just summarizing each source, but identifying the meaningful differences and what they imply overall.

## Prompt

```text
You are an expert analyst.

Compare and summarize the following inputs:

{{inputs}}

Produce:

1. Summary of each input (short)
2. Key similarities
3. Key differences
4. Strengths and weaknesses per input
5. Overall synthesis
6. Recommendation (if applicable)

Notes:
- Avoid bias toward any single input.
- Focus on meaningful differences.
- Make assumptions explicit when the inputs use different scopes, levels of detail, or evaluation criteria.
- If a recommendation is not justified by the evidence, say so instead of forcing one.
```

## Variablen

| Variable | Pflicht | Beschreibung | Beispiel |
| --- | --- | --- | --- |
| `{{inputs}}` | ja | The set of alternatives, sources, or options to compare | `Three vendor proposals, two architecture drafts, or multiple research summaries` |

## Eingaben

- Multiple inputs that can reasonably be compared side by side
- Enough detail in each input to describe strengths, weaknesses, and differences
- Preferably a shared decision area, evaluation question, or comparison frame

## Ausgabeformat

Markdown with these sections in order:

1. `Summary of each input`
2. `Key similarities`
3. `Key differences`
4. `Strengths and weaknesses per input`
5. `Overall synthesis`
6. `Recommendation` when justified

Keep the summaries short and give more attention to differences that materially affect the conclusion.

## Einschraenkungen

- The prompt compares what is provided; it does not fill missing evidence with certainty
- Inputs with mismatched scope or quality may weaken the comparison
- Human review is still needed when the comparison drives material technical, financial, or strategic decisions

## Wann verwenden

- When multiple options or sources need balanced side-by-side analysis
- When the output should combine summary with comparison and synthesis
- When similarities and differences matter more than deep analysis of a single input

## Wann nicht verwenden

- When there is only one source and the goal is simple summarization
- When the task is to generate options rather than compare existing ones
- When a specialized comparison prompt already exists for a narrower domain and is a better fit

## Beispiele

### Beispiel 1

**Eingabe**

```text
Input A: Vendor offers lower upfront cost, basic analytics, and fast onboarding, but has limited API flexibility.
Input B: Vendor has higher cost, stronger workflow automation, richer APIs, and longer implementation time.
Input C: Vendor is mid-priced, offers strong support, moderate analytics, and lower long-term lock-in risk.
```

**Erwartete Ausgabe**

```text
## Summary of each input
- Input A: Lowest-cost and fastest-start option, but limited flexibility.
- Input B: Most capable automation and integration option, but slower and more expensive to adopt.
- Input C: Balanced middle option with stronger support and lower lock-in risk.

## Key similarities
- All three options cover the core functional need.

## Key differences
- The biggest tradeoffs are cost, implementation speed, API flexibility, and lock-in exposure.

## Strengths and weaknesses per input
- Input A
  - Strengths: low cost, fast onboarding
  - Weaknesses: weaker integration flexibility
- Input B
  - Strengths: strongest automation and API depth
  - Weaknesses: highest cost and longest time to value
- Input C
  - Strengths: balanced profile, strong support, lower lock-in risk
  - Weaknesses: no clear category-leading capability

## Overall synthesis
- A is optimized for speed and cost, B for capability, and C for balanced risk.

## Recommendation
- Choose C if the organization values balance and lower long-term dependency risk over maximum short-term savings or maximum feature depth.
```

## Version

`1.0.0`

## Aenderungsverlauf

- `1.0.0` Initial version
