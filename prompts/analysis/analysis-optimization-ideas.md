---
id: analysis-optimization-ideas
name: Optimization Ideas
category: analysis
owner: TODO-owner
status: draft
version: 1.0.0
tags:
  - optimization
  - improvement
  - prioritization
  - effort-impact
  - operations
use_cases:
  - Generate and prioritize improvement ideas for a system or process across speed, cost, quality, or reliability goals
input_format: markdown
output_format: markdown
language: en
model_compatibility:
  - gpt-4.1
  - gpt-5
risk_notes:
  - Recommendations can be weak if the current pain points or constraints are too vague.
  - Idea prioritization does not replace measurement, experimentation, or operational validation.
created_at: 2026-03-30
updated_at: 2026-03-30
---

# Name

Optimization Ideas

## Zweck

Generates practical improvement ideas for a system or process, groups them by effort and impact, and prioritizes the most promising actions.

## Use Case

Use this prompt when a team wants to improve speed, reduce cost, raise quality, or increase reliability without jumping straight into implementation. It is especially useful when there are visible pain points, limited capacity, and a need to distinguish quick wins from strategic investments.

## Prompt

```text
You are an optimization advisor.

I want to improve this system/process:

- System/process: {{system}}
- Current pain points: {{pain_points}}
- Optimization goal: {{optimization_goal}}
- Constraints: {{constraints}}

Please generate:
1. 12 optimization ideas
2. Categorize them into:
   - Low effort / high impact
   - Medium effort / medium impact
   - High effort / strategic impact
3. For each idea, include:
   - Expected benefit
   - Tradeoff introduced
   - Prerequisites
4. Recommend a prioritized top 5

Requirements:
- Keep the ideas tied to the stated optimization goal rather than generic improvements.
- Make the ideas materially different from each other.
- Be explicit about the tradeoff each idea introduces instead of assuming pure upside.
- If the context is underspecified, state the most important assumptions before generating ideas.
```

## Variablen

| Variable | Pflicht | Beschreibung | Beispiel |
| --- | --- | --- | --- |
| `{{system}}` | ja | The system, workflow, or process to improve | `Customer support ticket triage workflow` |
| `{{pain_points}}` | ja | The current issues, bottlenecks, or inefficiencies | `Slow routing, repeated manual tagging, inconsistent prioritization, missed SLAs` |
| `{{optimization_goal}}` | ja | The main dimension to improve | `Reduce response time without adding headcount` |
| `{{constraints}}` | nein | Limits around budget, tooling, staffing, risk, or timing | `Must use current helpdesk platform, no new hires this quarter, low change tolerance during peak season` |

## Eingaben

- A specific system or process
- Clear pain points or bottlenecks
- A defined optimization goal such as speed, cost, quality, or reliability
- Optional constraints that shape what is realistic

## Ausgabeformat

Markdown with these sections in order:

- `Assumptions` when needed
- `Low effort / high impact`
- `Medium effort / medium impact`
- `High effort / strategic impact`
- `Prioritized top 5`

For each idea, include:
- `Idea`
- `Expected benefit`
- `Tradeoff introduced`
- `Prerequisites`

## Einschraenkungen

- The prompt suggests optimization directions, not guaranteed outcomes
- Poorly described pain points lead to shallow prioritization
- Human review is still needed to validate feasibility, sequencing, and actual impact

## Wann verwenden

- When a system or process has visible inefficiencies and the team needs structured improvement options
- When effort-versus-impact tradeoffs matter as much as idea generation
- When the output should help with prioritization rather than just brainstorming

## Wann nicht verwenden

- When the task is open-ended innovation with no concrete pain points or improvement goal
- When a detailed implementation plan is needed instead of a prioritized options list
- When optimization decisions require hard production metrics that are not available yet

## Beispiele

### Beispiel 1

**Eingabe**

```text
System/process: Customer support ticket triage workflow
Current pain points: Slow routing, repeated manual tagging, inconsistent prioritization, missed SLA warnings
Optimization goal: Reduce response time and improve consistency without increasing headcount
Constraints: Must stay within the current helpdesk platform, minimal budget, low appetite for major process changes this quarter
```

**Erwartete Ausgabe**

```text
## Low effort / high impact
- Idea: Introduce rule-based auto-tagging for the most common ticket categories
  - Expected benefit: Faster routing and less repetitive manual work
  - Tradeoff introduced: Rules may misclassify edge cases
  - Prerequisites: Historical category review and rule tuning

...

## Prioritized top 5
1. Rule-based auto-tagging
2. SLA risk flagging dashboard
3. Clear triage playbook for common issue types
4. Queue ownership by issue family
5. Weekly review of misrouted tickets
```

## Version

`1.0.0`

## Aenderungsverlauf

- `1.0.0` Initial version
