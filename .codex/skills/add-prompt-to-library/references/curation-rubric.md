# Curation Rubric

Use this rubric for the second-pass curator judgment.

## Add

Choose `add` when most of the following are true:

- the prompt covers a recurring task, not a one-off request
- the use case is specific enough to document well
- the category is clear
- inputs and outputs can be described concretely
- no existing prompt already covers the same core job
- the long-term maintenance cost looks reasonable

## Extend Existing

Choose `extend-existing` when most of the following are true:

- an existing prompt already covers the same core purpose
- the new idea mainly improves wording, examples, guardrails, or output constraints
- the distinction would not justify another long-lived file
- adding a new file would increase duplication more than clarity

## Reject

Choose `reject` when one or more of the following dominate:

- the idea is too narrow or too situational
- the user has not provided enough detail to define a stable reusable prompt
- the use case falls outside the library mission
- the candidate is mostly a duplicate of an existing entry
- the prompt would be expensive to maintain relative to its value

## Borderline guidance

For borderline cases:

- bias against creating new files
- prefer reuse and extension
- ask whether another team member would understand when to use the prompt without further explanation
- ask whether the prompt would still deserve a place in the library six months from now

## Naming checks

A good new prompt name:

- is readable without opening the file
- states the primary purpose
- matches one category cleanly
- avoids vague words like `general`, `helper`, `misc`, `assistant`

## Curator tone

The curator opinion should be direct and brief.
It should say whether the candidate raises or lowers the quality of the library as a curated set of reusable prompts.
