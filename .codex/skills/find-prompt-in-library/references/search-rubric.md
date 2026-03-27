# Search Rubric

Use this rubric before finalizing a recommendation.

## Strong fit

Treat a prompt as a strong fit when most of the following are true:

- the prompt solves the same core job the user described
- the required inputs are materially compatible
- the expected output shape is materially compatible
- the category and tags reinforce the fit instead of merely overlapping at a high level
- the `Wann verwenden` and `Wann nicht verwenden` sections support using it for this request

Strong fits can be recommended directly.

## Borderline fit

Treat a prompt as borderline when one of these is true:

- the category fits but the exact job is adjacent rather than matching
- the output shape is close but not clearly intended for this use
- the request shares wording with the prompt but not the actual workflow
- the prompt could help after significant reinterpretation

Borderline fits may appear as secondary alternatives, but only if they remain plausibly useful.

## Reject near matches

Reject a near match and prefer `no-suitable-match` when:

- the prompt would cause the user to use the wrong workflow
- the prompt expects different source material than the user has
- the prompt produces a different kind of deliverable than the user needs
- the fit depends mainly on one shared tag, category, or buzzword

Do not upgrade a weak fit just to avoid saying no.

## Recommend authoring

Recommend `$draft-prompt-for-library` only when all of these seem true:

- the missing use case appears recurring rather than one-off
- the task can be documented with stable inputs and outputs
- the gap looks meaningful enough to belong in a curated library

Do not recommend authoring when the request is too vague, too situational, or obviously outside the library's purpose.
