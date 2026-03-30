---
id: ideation-constraints-driven-innovation
name: Constraints-Driven Innovation
category: ideation
owner: TODO-owner
status: draft
version: 1.0.0
tags:
  - ideation
  - innovation
  - constraints
  - brainstorming
  - concept-generation
use_cases:
  - Generate a broad set of ideas that stay credible under hard real-world constraints
input_format: markdown
output_format: markdown
language: en
model_compatibility:
  - gpt-4.1
  - gpt-5
risk_notes:
  - Ideas can become superficial or repetitive if the constraints are vague, contradictory, or too generic.
  - The prompt can improve idea quality under constraints, but it does not validate business viability, technical feasibility, or market demand.
created_at: 2026-03-30
updated_at: 2026-03-30
---

# Name

Constraints-Driven Innovation

## Zweck

Uses tight constraints as a creative forcing function to generate ideas that are both inventive and grounded in real limits.

## Use Case

Use this prompt when a team wants to explore solution ideas without ignoring hard constraints such as budget, regulations, time, channel limits, platform boundaries, or resource scarcity. It is especially useful when unconstrained brainstorming tends to produce ideas that are imaginative but not actionable.

## Prompt

```text
You are an innovation facilitator.

I want to generate ideas under these constraints:

- Problem area: {{problem_area}}
- Hard constraints: {{hard_constraints}}
- Nice-to-have outcomes: {{desired_outcomes}}

Generate 12 ideas that work within these constraints.

For each idea, include:
- One-line description
- Why it fits the constraints
- What makes it interesting
- Main drawback

Then identify:
- 3 most realistic ideas
- 3 boldest ideas
- 1 idea that is both practical and differentiated

Requirements:
- Treat the hard constraints as real design boundaries, not suggestions.
- Make the ideas meaningfully different from each other rather than presenting small variations.
- Prefer ideas that are plausible in the stated context over generic brainstorming output.
- If the constraints conflict or are underspecified, state the most important assumptions before listing ideas.
```

## Variablen

| Variable | Pflicht | Beschreibung | Beispiel |
| --- | --- | --- | --- |
| `{{problem_area}}` | ja | The domain, challenge, or opportunity space to ideate within | `Reducing food waste in small urban grocery stores` |
| `{{hard_constraints}}` | ja | Non-negotiable limits that the ideas must respect | `No mobile app, budget under $20k, must launch in 8 weeks, no new hardware` |
| `{{desired_outcomes}}` | nein | Valuable outcomes or qualities that would improve the result if achievable | `High customer participation, visible differentiation, easy staff adoption` |

## Eingaben

- A clear problem area or innovation target
- Concrete hard constraints that materially shape what is possible
- Optional desirable outcomes to help rank ideas without weakening the hard constraints
- Enough context to distinguish practical ideas from unrealistic ones

## Ausgabeformat

Markdown with these sections in order:

- `Assumptions` when needed
- `Idea 1` through `Idea 12`
- `Most realistic ideas`
- `Boldest ideas`
- `Practical and differentiated pick`

Each idea section should contain the four required bullets:
- `One-line description`
- `Why it fits the constraints`
- `What makes it interesting`
- `Main drawback`

## Einschraenkungen

- The prompt generates candidate ideas, not validated solutions
- Weak constraints lead to weak differentiation and lower-value output
- Human review is still needed to assess feasibility, desirability, and execution risk

## Wann verwenden

- When hard constraints should shape ideation instead of being applied after brainstorming
- When teams need a mix of realistic and bold options within a bounded problem space
- When standard brainstorming keeps producing ideas that are too expensive, too slow, or too vague

## Wann nicht verwenden

- When the goal is to evaluate or rank a fixed set of existing options rather than generate new ones
- When constraints are missing and broad exploratory ideation is more appropriate
- When the task requires a detailed implementation or business case rather than early-stage concepts

## Beispiele

### Beispiel 1

**Eingabe**

```text
Problem area: Improve member engagement for a local public library
Hard constraints: No custom mobile app, no increase in headcount, budget under $10,000, must use existing website and email tools
Nice-to-have outcomes: More repeat visits, stronger community participation, visible differentiation from nearby libraries
```

**Erwartete Ausgabe**

```text
## Idea 1
- One-line description: Launch a monthly themed email challenge with simple in-branch and online participation.
- Why it fits the constraints: Uses existing email and website tools, needs no new app, and can be run by current staff.
- What makes it interesting: Turns routine outreach into recurring community participation.
- Main drawback: Engagement may plateau without strong editorial consistency.

...

## Most realistic ideas
- Email challenge series
- Staff-curated neighborhood reading maps
- Member spotlight recommendation loop

## Boldest ideas
- Community-created local history archive sprint
- Library passport across partner venues
- Time-boxed civic problem-solving clubs

## Practical and differentiated pick
- Staff-curated neighborhood reading maps because it is low-cost, easy to pilot, and creates a distinctive local identity.
```

## Version

`1.0.0`

## Aenderungsverlauf

- `1.0.0` Initial version
