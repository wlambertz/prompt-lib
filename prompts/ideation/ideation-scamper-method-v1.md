---
id: ideation-scamper-method
name: SCAMPER Method
category: ideation
owner: TODO-owner
status: draft
version: 1.0.0
tags:
  - ideation
  - scamper
  - brainstorming
  - innovation
  - framework
use_cases:
  - Use the SCAMPER framework to generate structured idea variations for a product, process, or system
input_format: markdown
output_format: markdown
language: en
model_compatibility:
  - gpt-4.1
  - gpt-5
risk_notes:
  - Outputs can become formulaic if the topic or goal is too vague.
  - The framework generates idea directions, but it does not validate feasibility, demand, or implementation cost.
created_at: 2026-03-30
updated_at: 2026-03-30
---

# Name

SCAMPER Method

## Zweck

Applies the SCAMPER framework to generate structured idea variations across seven lenses so teams can explore a topic more systematically than with free-form brainstorming.

## Use Case

Use this prompt when a team wants to improve or rethink an existing product, process, or system by deliberately exploring substitutions, combinations, adaptations, removals, and reversals. It is especially useful when generic ideation is too loose and a repeatable framework is needed to force breadth.

## Prompt

```text
Apply the SCAMPER method to this topic:

- Product/process/system: {{topic}}
- Goal: {{goal}}
- Constraints: {{constraints}}

For each SCAMPER dimension, generate ideas:

- Substitute
- Combine
- Adapt
- Modify
- Put to another use
- Eliminate
- Reverse

For each section:
- Give 3 ideas
- Highlight the strongest one
- Briefly explain why it may be valuable

Then summarize:
- Top 5 ideas overall
- Top 2 easiest to test
- Top 2 highest upside ideas

Requirements:
- Keep the ideas grounded in the stated goal and constraints.
- Make the three ideas within each SCAMPER dimension meaningfully different from each other.
- If the topic is underspecified, state the minimum assumptions required before generating ideas.
- Prefer practical and specific ideas over generic innovation language.
```

## Variablen

| Variable | Pflicht | Beschreibung | Beispiel |
| --- | --- | --- | --- |
| `{{topic}}` | ja | The product, process, or system to be explored with SCAMPER | `Internal employee onboarding process` |
| `{{goal}}` | ja | The improvement goal or innovation target | `Reduce onboarding time while improving new-hire clarity and completion rates` |
| `{{constraints}}` | nein | Limits that the ideas should respect | `No extra headcount, minimal software spend, must fit current HR tooling` |

## Eingaben

- A specific product, process, or system
- A clear goal so the SCAMPER ideas have direction
- Optional constraints to keep the ideas realistic
- Enough context to avoid purely abstract suggestions

## Ausgabeformat

Markdown with these sections in order:

- `Assumptions` when needed
- `Substitute`
- `Combine`
- `Adapt`
- `Modify`
- `Put to another use`
- `Eliminate`
- `Reverse`
- `Top 5 ideas overall`
- `Top 2 easiest to test`
- `Top 2 highest upside ideas`

Within each SCAMPER section:
- list 3 ideas
- identify the strongest idea
- briefly explain why that strongest idea may be valuable

## Einschraenkungen

- The SCAMPER method works best when improving or reframing something concrete rather than inventing from a blank slate
- Weak topic framing produces shallow or repetitive ideas
- Human review is still needed to assess feasibility, prioritization, and execution risk

## Wann verwenden

- When a structured ideation framework is more useful than open-ended brainstorming
- When improving an existing product, process, or system
- When teams want broad exploration across multiple transformation lenses

## Wann nicht verwenden

- When the task is to compare a fixed set of existing options rather than generate new ideas
- When the topic is too vague or there is no clear goal for improvement
- When a different ideation method is preferred because constraints or prioritization are more important than framework coverage

## Beispiele

### Beispiel 1

**Eingabe**

```text
Product/process/system: Internal employee onboarding process
Goal: Reduce onboarding time while improving clarity for new hires
Constraints: No new full-time hires, low budget, must work with current HR systems and documentation tools
```

**Erwartete Ausgabe**

```text
## Substitute
1. Replace long orientation calls with short role-specific video briefings
2. Replace static checklist emails with a guided onboarding hub
3. Replace generic documentation bundles with first-week role packs
Strongest idea: Guided onboarding hub
Why it may be valuable: It reduces confusion by centralizing steps, ownership, and timing.

## Combine
...

## Top 5 ideas overall
- Guided onboarding hub
- Manager welcome kit plus first-week schedule template
- Peer buddy integration into current workflow tools
- Role-based documentation starter packs
- Pre-day-one access checklist automation

## Top 2 easiest to test
- Role-based documentation starter packs
- Manager welcome kit plus first-week schedule template

## Top 2 highest upside ideas
- Guided onboarding hub
- Pre-day-one access checklist automation
```

## Version

`1.0.0`

## Aenderungsverlauf

- `1.0.0` Initial version
