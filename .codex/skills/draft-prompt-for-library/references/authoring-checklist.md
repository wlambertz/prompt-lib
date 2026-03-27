# Authoring Checklist

Use this checklist before handing a prompt draft to `$add-prompt-to-library`.

## Required Prompt Sections

The draft entry must include all sections from `templates/prompt-template.md`:

- `Name`
- `Zweck`
- `Use Case`
- `Prompt`
- `Variablen`
- `Eingaben`
- `Ausgabeformat`
- `Einschraenkungen`
- `Wann verwenden`
- `Wann nicht verwenden`
- `Beispiele`
- `Version`
- `Aenderungsverlauf`

Do not leave placeholder-only content in the final draft.

## Required Metadata Fields

The YAML frontmatter must include all required fields from `templates/metadata-template.yaml` and `schemas/prompt-metadata.schema.yaml`:

- `id`
- `name`
- `category`
- `owner`
- `status`
- `version`
- `tags`
- `use_cases`
- `input_format`
- `output_format`
- `language`
- `model_compatibility`
- `risk_notes`
- `created_at`
- `updated_at`

## Metadata Constraints

Apply these schema-level checks:

- `id` must match `^[a-z0-9]+(-[a-z0-9]+)*$`
- `category` must be one of `analysis`, `coding`, `communication`, `documentation`, `ideation`, `summarization`
- `status` must be one of `draft`, `review`, `active`, `deprecated`, `archived`
- `version` must match semantic versioning in `x.y.z` form
- `tags`, `use_cases`, `model_compatibility`, and `risk_notes` must each contain at least one item
- `created_at` and `updated_at` should use `YYYY-MM-DD`
- `status: active` is not appropriate for a fresh author draft

## Author Self-Check

Mirror the author self-check from `docs/review-process.md` before sending the draft onward:

- Is the use case recurring and not one-off?
- Is the category plausible?
- Are all required sections filled in?
- Are metadata complete and plausible?
- Is there at least one realistic example?

## Handoff Readiness

The draft is ready for curator review only when:

- the prompt purpose is specific enough that another reviewer can judge reuse value
- the inputs, variables, and output format are concrete
- the limitations and failure modes are named plainly
- the tentative filename is readable and follows `docs/naming-conventions.md`
- any unresolved assumptions are called out explicitly instead of hidden in prose
