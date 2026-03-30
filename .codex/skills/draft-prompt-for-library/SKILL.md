---
name: draft-prompt-for-library
description: Draft and iterate reusable prompt entries for this prompt library. Use when the user wants to author, flesh out, or refine a library-worthy prompt idea into a template-compliant draft with frontmatter, body sections, a tentative category, and a tentative filename. Do not use for final add-versus-extend-versus-reject decisions or for vague ideas that still lack basic product intent.
---

# Draft Prompt For Library

Turn a reusable prompt idea into a reviewable draft that can be handed to `$add-prompt-to-library`.

This skill is the authoring stage, not the curator gate.

## Scope

Use this skill to:

- turn a raw prompt idea into a template-compliant draft
- iterate on wording, structure, variables, and examples
- prepare draft YAML frontmatter and draft prompt sections
- propose a tentative category and filename for later curator review
- identify missing details early when the prompt idea is too vague

Do not use this skill to:

- decide whether the prompt should be added, merged, or rejected
- treat duplicate detection as the primary task
- make the final call on category, path, or filename
- invent a stable reusable prompt when the request is still underspecified

## Required Repo Sources

Read these repository sources before drafting:

- `README.md`
- `CONTRIBUTING.md`
- `docs/taxonomy.md`
- `docs/naming-conventions.md`
- `docs/review-process.md`
- `templates/prompt-template.md`
- `templates/metadata-template.yaml`
- `schemas/prompt-metadata.schema.yaml`
- `examples/`

Read `references/authoring-checklist.md` before finalizing the draft.

## Default Workflow

Follow this sequence in order.

### 1. Normalize the idea

Turn the user request into a short author brief with:

- working title
- intended recurring use case
- target audience or operator
- expected inputs
- expected outputs
- constraints or failure modes already known

If the request is too vague to support a reusable prompt, stop and name the missing product intent explicitly.

### 2. Check for minimum reuse value

Confirm that the candidate appears reusable enough to draft:

- the task is recurring rather than one-off
- the expected inputs can be described concretely
- the expected output shape is reasonably stable
- the prompt can be documented with clear boundaries

This is only a drafting sanity check. Do not perform a curator-style add or reject decision here.

### 3. Draft the prompt structure

Create a complete draft that follows `templates/prompt-template.md` and includes:

- YAML frontmatter with all required metadata fields
- a clear name and purpose
- a usable prompt block with concrete variables
- realistic input and output expectations
- limitations, appropriate usage, and non-usage guidance
- at least one concrete example when the request provides enough detail

Prefer specific wording over generic prompt boilerplate.

### 4. Propose tentative placement

Choose the best tentative category from:

- `analysis`
- `coding`
- `communication`
- `documentation`
- `ideation`
- `summarization`

Then propose a tentative filename using:

```text
<category>-<short-purpose>.md
```

Treat both values as provisional until the curator skill confirms or changes them.

### 5. Run the author self-check

Use `references/authoring-checklist.md` to verify:

- all required sections are present
- all required metadata fields are present
- the draft has enough specificity to review
- the examples and risk notes are not placeholder-only
- any unresolved gaps are surfaced clearly

### 6. Prepare handoff to the curator

When the draft is strong enough for review, hand it off to `$add-prompt-to-library`.

The handoff must leave the curator with:

- a complete draft body
- complete draft metadata/frontmatter
- a tentative category
- a tentative filename
- any unresolved questions or assumptions called out explicitly

## Output Contract

Always respond with these sections and in this order:

### Draft Status

One of:

- `ready-for-curation`
- `needs-more-input`

### Prompt Brief

Summarize the draft target:

- working title
- recurring use case
- target operator
- expected inputs
- expected outputs

### Draft Metadata

Provide draft YAML frontmatter.

### Draft Prompt Entry

Provide the draft markdown entry that follows the repository template.

### Tentative Category

Name one category and briefly mention a plausible alternative only if it was close.

### Tentative Filename

Provide the proposed filename, or `n/a` when the draft is not ready.

### Open Gaps

List missing details that block a trustworthy reusable draft. Use `none` when the draft is ready for curation.

### Next Action

One of:

- `send to curator`
- `ask for more detail`

## Drafting Defaults

Use these defaults unless the user specifies otherwise:

- metadata lives in YAML frontmatter
- `status: draft`
- `version: 1.0.0`
- `language: de` if the request is in German, otherwise match the request language
- `owner`: use a clearly marked placeholder if no owner is given
- `created_at` and `updated_at`: use the current date
- derive `id` from the filename stem

## Quality Bar

Draft for review, not for automatic admission.

Be concrete, structured, and conservative:

- do not leave template placeholders in a supposedly ready draft
- do not hide missing requirements behind polished generic wording
- do not skip boundaries, examples, or risk notes just to make the draft look complete
