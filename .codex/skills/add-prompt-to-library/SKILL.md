---
name: add-prompt-to-library
description: Curate and add prompts to this prompt library. Use when the user wants to check whether a prompt already exists, decide if a prompt belongs in the library, propose category and filename, or scaffold a new prompt entry in the right location.
---

# Add Prompt To Library

Use this skill when the task is about curating a candidate prompt for this repository.

This skill is for:

- checking whether something similar already exists
- deciding whether a new prompt should be added, merged into an existing entry, or rejected
- proposing the best category, path, and filename
- scaffolding a new prompt file in `prompts/<category>/` when the user asked for addition and the prompt is worth adding

This skill is not for:

- broad repo cleanup unrelated to prompt curation
- rewriting the library taxonomy or contribution rules unless the user explicitly asks
- creating one-off prompts with no reusable value

## Required repo sources

Before making a recommendation, read the current repository guidance instead of restating it from memory:

- `README.md`
- `CONTRIBUTING.md`
- `docs/taxonomy.md`
- `docs/naming-conventions.md`
- `templates/prompt-template.md`
- `templates/metadata-template.yaml`
- `schemas/prompt-metadata.schema.yaml`

Also inspect existing content in:

- `prompts/`
- `examples/`

Use heuristic search first. Prefer `rg` for:

- filename overlap
- category overlap
- use-case overlap
- tag overlap
- prompt purpose overlap
- matching inputs or output format

## Default workflow

Follow this sequence in order.

### 1. Normalize the candidate

Turn the user request into a short prompt brief with:

- working title
- intended use case
- expected inputs
- expected outputs
- target audience or operator
- why it may be reusable

If the request is underspecified, state the missing details explicitly in the assessment. Do not invent a fully mature prompt idea from a vague one-line hint.

### 2. Search the library

Inspect the library for similar or overlapping prompts using heuristics only. Compare against:

- prompt filenames
- metadata in frontmatter
- use case wording
- prompt purpose
- input shape
- output shape
- nearby examples that could already cover the request

Always surface the closest existing candidates, even if they are only partial matches.

### 3. Classify the result

Choose exactly one recommendation:

- `add`
- `extend-existing`
- `reject`

Use these rules:

- `add`: the use case is reusable, well-scoped, and not already covered closely enough
- `extend-existing`: an existing prompt already covers the core use case and should be improved instead of duplicated
- `reject`: the prompt is too narrow, too weakly specified, outside the library purpose, or not worth the maintenance cost

### 4. Assign category and name

If the result is `add` or `extend-existing`, choose the best category from:

- `analysis`
- `coding`
- `communication`
- `documentation`
- `ideation`
- `summarization`

Then propose:

- the exact repository location
- the exact filename

Filename format must follow:

```text
<category>-<short-purpose>-v<major>.md
```

Rules:

- lowercase only
- hyphens only
- no spaces
- make the purpose human-readable
- use `v1` for new files unless the user is intentionally creating a new major version

### 5. Run the curator pass

After the primary recommendation, perform a second-pass curator review.

The curator pass is stricter than the primary pass. It checks:

- duplication risk
- category fit
- naming quality
- maintainability over time
- whether the prompt adds enough reusable value to justify future review and upkeep

Default behavior:

- simulate the curator pass as a separate section in the response
- only use a separate subagent if explicit delegation is available and appropriate

Curator decision rules:

- clear, high-fit cases may confirm the primary result quickly
- borderline cases should be treated conservatively
- the curator may veto a weak `add` recommendation

Read `references/curation-rubric.md` before writing the curator judgment.

### 6. Scaffold only when appropriate

If the user only asked for evaluation, stop after the recommendation.

If the user asked to add the prompt and the final recommendation is `add`, create one markdown file under `prompts/<category>/` with:

- YAML frontmatter based on `templates/metadata-template.yaml`
- required fields aligned to `schemas/prompt-metadata.schema.yaml`
- body sections based on `templates/prompt-template.md`
- an initial changelog entry

Do not create a separate metadata sidecar file in v1.

If the recommendation is `extend-existing`:

- do not create a new file by default
- name the target file to update
- explain what should be merged into it

If the recommendation is `reject`:

- do not scaffold
- explain whether the issue is duplication, low reuse, weak specification, or poor fit

## Output contract

Always respond with these sections and in this order:

### Recommendation

One of: `add`, `extend-existing`, `reject`

### Library Fit

One of: `high`, `medium`, `low`

### Confidence

One of: `high`, `medium`, `low`

### Similar Existing Entries

List the nearest matches with one-line reasons.

### Proposed Category

Name one category. If another category was plausible, mention it briefly here.

### Proposed Location

Exact repo path or exact existing file to extend.

### Proposed Filename

Exact filename for a new prompt, or `n/a` when not adding.

### Curator Opinion

A short, explicit judgment on whether this improves the library as a curated collection.

### Next Action

One of:

- scaffold new prompt
- extend existing file
- stop

## Scaffolding defaults

When creating a new file, use these defaults unless the user specifies otherwise:

- metadata lives in YAML frontmatter
- `status: draft`
- `version: 1.0.0`
- `language: de` if the request is in German, otherwise match the request language
- `owner`: use a clearly marked placeholder if no owner is given
- `created_at` and `updated_at`: use the current date
- examples should be concrete, not placeholder-only, whenever the request provides enough detail

Derive a stable prompt `id` from the filename stem without the `-v<major>` suffix when possible.

## Quality bar

Be conservative. This repository is curated, not a prompt dump.

Prefer `extend-existing` over `add` when the distinction is weak.
Prefer `reject` over creating low-value inventory.
Only scaffold when the prompt is reusable, specific enough to review, and materially improves the library.
