---
name: find-prompt-in-library
description: Find the best existing prompt file in this prompt library for a concrete problem, task, or desired output. Use when the user wants to know whether the library already has a suitable prompt, which prompt fits best, or what nearby alternatives exist. Do not use to draft a new prompt, make final add-versus-extend-versus-reject curation decisions, or rewrite the library taxonomy.
---

# Prompt Librarian

Find the closest existing prompt entry in this repository without forcing weak matches.

This skill is retrieval and recommendation only. It does not draft new prompt entries or make curator admission decisions.

## Scope

Use this skill to:

- map a concrete problem or task to the best existing prompt file in `prompts/`
- return the top ranked match plus up to two nearby alternatives
- explain why a prompt fits or why none fits well enough
- recommend `$draft-prompt-for-library` only when a missing prompt would likely be reusable enough for the library

Do not use this skill to:

- write or revise prompt files
- decide `add`, `extend-existing`, or `reject` for library curation
- treat `examples/` or docs as library entries
- force a category-level or wording-only match when the actual job does not fit

## Required Repo Sources

Read these repository sources before searching:

- `README.md`
- `docs/taxonomy.md`
- `docs/naming-conventions.md`
- `schemas/prompt-metadata.schema.yaml`
- current files under `prompts/`

You may also inspect `examples/` to interpret the library's writing style and use-case patterns, but never return an example file as the selected prompt.

Read `references/search-rubric.md` before finalizing the recommendation.

## Default Workflow

Follow this sequence in order.

### 1. Normalize the request

Turn the user request into a short retrieval brief with:

- core job to be done
- expected input shape
- expected output shape
- likely category
- meaningful constraints or guardrails

If the request is vague, still extract the likely job, but preserve uncertainty explicitly instead of guessing a stronger fit than the evidence supports.

### 2. Search the library

Search `prompts/**/*.md` heuristically. Compare against:

- filename
- YAML frontmatter fields such as `name`, `category`, `tags`, `use_cases`, `input_format`, `output_format`, and `language`
- prompt body sections such as `Zweck`, `Use Case`, `Eingaben`, `Ausgabeformat`, `Wann verwenden`, and `Wann nicht verwenden`

Prefer `rg` and targeted file inspection over broad restatement.

Treat `examples/` and repo docs only as supporting context. They are not candidate matches.

### 3. Rank the candidates

Rank candidates in this order:

1. core use-case match
2. input and output fit
3. tags and category fit
4. wording overlap

Return at most three candidates, and only when each one is genuinely plausible for the user's task.

### 4. Refuse weak matches

Return `no-suitable-match` when:

- only the category overlaps
- the prompt's purpose differs materially from the user's job
- the expected inputs differ materially
- the expected output shape differs materially
- the match depends mostly on vague wording overlap

Do not recommend a prompt that would likely mislead the user into using the wrong workflow.

### 5. Decide authoring advice

When there is no suitable match:

- recommend `$draft-prompt-for-library` if the missing use case appears recurring, documentable, and library-worthy
- set authoring advice to `not needed` if the request appears one-off, too vague, or too narrow to justify a reusable library entry

Do not auto-draft or auto-curate a new prompt from this skill.

## Output Contract

Always respond with these sections and in this order:

### Recommendation

Provide the exact best prompt file path under `prompts/`, or `no-suitable-match`.

### Confidence

One of:

- `high`
- `medium`
- `low`

### Best Match Reason

Explain the strongest evidence for the recommendation in 2 to 4 concise sentences.

### Other Plausible Matches

List up to two additional prompt file paths with one-line reasons, or `none`.

### How To Use It

State briefly when the recommended prompt fits this request. If there is no exact match, write `n/a`.

### Why No Exact Match

Include this section only when the recommendation is `no-suitable-match`. State why nearby prompts fail the fit test.

### Authoring Advice

Use exactly one of:

- `not needed`
- `Use $draft-prompt-for-library to draft a reusable prompt for this gap.`

## Quality Bar

Be conservative.

- Prefer `no-suitable-match` over an attractive but misleading near match.
- Prefer a brief, evidence-based ranking over generic similarity language.
- Recommend authoring only when the missing use case looks stable enough to document as a reusable prompt.
