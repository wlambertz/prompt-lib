---
id: coding-intentional-ui-design-direction
name: Intentional, Non-Generic UI Design Direction
category: coding
owner: WLA
status: draft
version: 1.0.0
tags:
  - ui-design
  - art-direction
  - visual-hierarchy
  - frontend
use_cases:
  - Guide the composition and critique of a product interface during design or implementation
input_format: markdown
output_format: design artifact or markdown
language: en
model_compatibility:
  - gpt-5
risk_notes:
  - The direction needs a concrete brief and existing brand or accessibility constraints to produce a usable design.
  - The critique is qualitative and does not replace usability testing or accessibility checks.
created_at: 2026-11-16
updated_at: 2026-11-16
---

# Name

Intentional, Non-Generic UI Design Direction

## Zweck

Guides UI design toward content-driven composition and deliberate visual hierarchy instead of default template patterns.

## Use Case

Use this prompt when designing or implementing a product screen, page, or interface and a generic card-based layout would obscure the content's purpose. It complements the design-system assistant, which focuses on implementation tokens and UX copy rather than overall composition.

## Prompt

```text
# Design Direction: Intentional, Non-Generic UI

Act as an experienced product designer and art director, not as a generator of standard SaaS templates.

Your goal is to create distinctive, professional, functional designs that derive their visual structure from the content and its purpose.

## 1. Avoid default AI design patterns

Do not automatically use:

- Cards or rounded containers for every content section.
- Repeated grids of identical cards.
- Colored top borders or accent lines on containers.
- Decorative left borders beside headings or paragraphs.
- Gradient backgrounds, glows, glassmorphism, or unnecessary shadows.
- Repeated icon + heading + description patterns.
- Excessive badges, pills, and decorative labels.
- ALL-CAPS eyebrow headings above every section.
- Arbitrary oversized metrics and KPI cards.
- Generic hero sections with centered headlines and three feature cards.
- Identical layouts for unrelated information types.

These elements are not universally prohibited. Use them only when there is a clear functional or contextual reason.

## 2. Prefer content-driven composition

Choose the layout based on the nature of the information.

Consider:

- Open layouts using whitespace for grouping.
- Strong typographic hierarchy.
- Tables for structured comparisons.
- Lists for sequential or related information.
- Editorial layouts for explanatory content.
- Charts for quantitative information.
- Side-by-side compositions when comparison matters.
- Asymmetric compositions when they improve hierarchy.
- Containers only when visual separation is genuinely necessary.

Do not treat every piece of content as a standalone component that requires a box.

## 3. Visual hierarchy without decoration

Establish hierarchy primarily through:

1. Typography
2. Spacing
3. Alignment
4. Scale
5. Contrast
6. Color
7. Borders and surfaces, only when necessary

Avoid adding decorative elements to compensate for weak composition.

## 4. Make deliberate design decisions

Before generating a design:

1. Identify the audience and primary purpose.
2. Determine the information hierarchy.
3. Choose an appropriate visual direction.
4. Consider at least two substantially different layout approaches.
5. Check whether the chosen approach resembles a generic AI-generated template.
6. If it does, revise the composition before implementing it.

Every major stylistic decision should be explainable in terms of the content, usability, or visual identity.

## 5. Apply restraint

Use fewer, stronger design decisions rather than many small decorative treatments.

Not every section needs a background.
Not every group needs a border.
Not every heading needs an icon.
Not every metric needs a card.
Not every important element needs an accent color.

Avoid visual repetition unless the underlying information is genuinely repetitive.

## 6. Final design critique

Before presenting the result, critically evaluate it:

- Could this design belong to almost any generic SaaS application?
- Are cards being used where whitespace would suffice?
- Are any borders purely decorative?
- Is the same layout pattern repeated unnecessarily?
- Does the hierarchy remain clear without excessive containers?
- Does the composition reflect the actual content?
- Are visual elements present because they improve communication?

If the design fails these checks, revise it before delivering.

## Guiding principle

Do not decorate information. Design its structure.

Make the design feel intentionally art-directed rather than automatically assembled from familiar UI patterns.

Design brief:
{{design_brief}}
```

## Variablen

| Variable | Pflicht | Beschreibung | Beispiel |
| --- | --- | --- | --- |
| `{{design_brief}}` | ja | Audience, purpose, content, existing visual identity, constraints, and requested deliverable | `Design a desktop order history page for frequent buyers; show orders, status, and reorder actions; keep the existing brand colors.` |

## Eingaben

- A concrete screen or page brief with its audience, purpose, and actual content
- Existing brand, design-system, accessibility, and implementation constraints when available
- The requested deliverable, such as a mockup, component implementation, or design critique

## Ausgabeformat

Deliver the design or implementation requested in the brief. Explain the chosen composition and the main decisions briefly. If delivering a critique, identify concrete revisions tied to the content and hierarchy.

## Einschraenkungen

- Distinctive composition still has to respect brand, accessibility, responsive behavior, and implementation constraints.
- Without real content or an audience, the layout may still become generic despite these rules.
- The prompt does not by itself verify usability or accessibility.

## Wann verwenden

- When creating or revising a product interface with enough content to drive layout choices
- When a page needs stronger hierarchy and less decorative repetition
- When reviewing a proposed UI for generic template patterns

## Wann nicht verwenden

- When the task is limited to design tokens or UX copy without layout decisions
- When an existing approved design must be reproduced exactly
- When there is no concrete interface brief or content to organize

## Beispiele

### Beispiel 1

**Eingabe**

```text
Design brief:
Design a desktop order history page for frequent buyers. Show orders with date, item count, total, fulfillment status, and a reorder action. Keep the existing brand colors and support keyboard navigation.
```

**Erwartete Ausgabe**

```text
Use a compact order table with a clear header and row-level reorder actions. Put status in a dedicated column and use color only as a secondary cue. Keep page-level filters above the table, aligned with its columns. On narrow screens, switch to a readable order list with the same information order. Explain the hierarchy and check that row actions remain keyboard accessible.
```

## Version

`1.0.0`

## Aenderungsverlauf

- `1.0.0` Initial version
