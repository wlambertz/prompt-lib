---
id: summarization-git-work-topics
name: Git Work Topics Summarizer
category: summarization
owner: TODO-owner
status: draft
version: 1.0.0
tags:
  - git
  - history
  - summarization
  - worklog
  - engineering
use_cases:
  - Summarize recent engineering topics from commit history for standups or weekly updates
  - Extract recurring work themes from recent git activity without reading every commit manually
input_format: markdown
output_format: markdown
language: en
model_compatibility:
  - gpt-4.1
  - gpt-5
risk_notes:
  - Commit messages alone can underrepresent the real topic if they are vague or noisy.
  - File paths and diffs can suggest topics incorrectly when mechanical changes dominate the history.
created_at: 2026-03-30
updated_at: 2026-03-30
---

# Name

Git Work Topics Summarizer

## Zweck

Extracts and summarizes the most recent work topics from git history so recent engineering activity can be understood quickly without manually reviewing every commit.

## Use Case

Use this prompt when someone wants a compact summary of what they or the team have been working on recently based on commit history. It is useful for standups, weekly recaps, handoffs, retrospectives, or rebuilding context after switching tasks.

## Prompt

```text
You are analyzing recent git history to identify the main topics of work.

Your job is to extract the last few meaningful work topics from the provided git history and summarize them clearly.

Work from the evidence in this priority order:
1. commit diffs or changed file summaries
2. file paths and directory patterns
3. commit messages
4. branches, tags, or dates if provided

Do not simply restate commit messages one by one. Group related commits into broader work topics when the evidence supports it.

Inputs:
- Time or history window: {{history_window}}
- Git history evidence: {{git_history}}
- Optional repository context: {{repository_context}}
- Optional focus: {{focus_preference}}
- Desired topic count: {{topic_count}}

Instructions:
- identify the most meaningful recent topics, not every tiny change
- merge obviously related commits into one topic
- prefer concrete topic names such as `authentication fixes`, `prompt-library documentation cleanup`, or `CI pipeline updates`
- for each topic, mention the strongest supporting evidence
- distinguish between confirmed topics and weak inferences
- ignore pure noise when possible, such as bulk formatting or dependency churn, unless it was a major focus
- if the history is too thin or ambiguous, say so explicitly
- if multiple unrelated streams of work appear, keep them separate

Return the answer in Markdown with these sections:

1. Recent topics
For each topic include:
- topic name
- short summary
- likely scope or affected area
- evidence
- confidence: high, medium, or low

2. Overall summary
- 3 to 6 sentences summarizing the recent direction of work

3. Uncertainties
- missing evidence
- ambiguous commits
- where the summary may be misleading

If the user asks for a personal update style summary, end with:
4. Suggested update
- a short first-person update that can be reused in a standup or weekly note
```

## Variablen

| Variable | Pflicht | Beschreibung | Beispiel |
| --- | --- | --- | --- |
| `{{history_window}}` | ja | Time range, number of commits, or other boundary for the git history under review | `Last 15 commits on the current branch` |
| `{{git_history}}` | ja | Git log output, commit list, changed file summaries, or selected diffs | `Commit messages with files changed from git log --stat` |
| `{{repository_context}}` | nein | Short explanation of the repository or subsystem to reduce wrong topic inference | `Prompt library repo with prompts/, docs/, templates/, and schemas/` |
| `{{focus_preference}}` | nein | Optional filter for what counts as a topic | `Focus on product-facing work and ignore dependency bumps unless they changed workflows` |
| `{{topic_count}}` | nein | Preferred number of topics to extract | `3 to 5 topics` |

## Eingaben

- Recent git history in Markdown or plain text
- Preferably commit messages plus changed files or diff summaries
- Optional repository context to interpret folder names and components correctly
- Optional desired time window, branch, or topic count

Minimum useful input:
- at least several commits
- enough file or diff context to distinguish real work themes from noise

## Ausgabeformat

Markdown with these sections:

- `Recent topics`
- `Overall summary`
- `Uncertainties`

Optional:
- `Suggested update`

Each topic should include a short summary, scope, evidence, and confidence.

## Einschraenkungen

- Weak commit messages can make topic extraction unreliable.
- Pure commit metadata without changed files or diffs may produce overly generic summaries.
- Mechanical edits such as formatting, renames, or generated files can distort the result if not labeled clearly.
- Human review is still needed before using the output as an authoritative project record.

## Wann verwenden

- When preparing a standup or weekly recap from recent git activity
- When reloading context after working across multiple tasks
- When a lead or teammate wants a quick view of recent engineering focus areas

## Wann nicht verwenden

- When exact chronology or a full changelog is required
- When the git history is too small, too noisy, or missing changed-file evidence
- When the goal is code review or root-cause analysis rather than work-topic summarization

## Beispiele

### Beispiel 1

**Eingabe**

```text
Time or history window:
Last 10 commits on main

Repository context:
Prompt library repository with prompts/, docs/, templates/, schemas/, and examples/

Git history evidence:
- feat: add repository system policy generator prompt
  files: prompts/documentation/documentation-repo-system-policy.md
- docs: expand review-process guidance
  files: docs/review-process.md, README.md
- feat: add repository agents structure prompt
  files: prompts/documentation/documentation-repo-agents-structure.md
- refactor: tighten metadata schema examples
  files: schemas/prompt-metadata.schema.yaml, templates/metadata-template.yaml
- docs: improve naming conventions
  files: docs/naming-conventions.md

Desired topic count:
3
```

**Erwartete Ausgabe**

```text
## Recent topics

### 1. Repository-focused agent documentation prompts
Summary: Recent work added reusable prompts for generating repo-specific agent guidance and system policy documents.
Likely scope or affected area: `prompts/documentation/`
Evidence: commits adding `documentation-repo-system-policy.md` and `documentation-repo-agents-structure.md`
Confidence: high

### 2. Prompt library governance and review guidance
Summary: Documentation was updated to make review and naming expectations clearer.
Likely scope or affected area: `docs/` and `README.md`
Evidence: changes in `docs/review-process.md`, `docs/naming-conventions.md`, and `README.md`
Confidence: high

### 3. Metadata and template tightening
Summary: Supporting schema and template files were adjusted to make prompt metadata more consistent.
Likely scope or affected area: `schemas/` and `templates/`
Evidence: changes in `schemas/prompt-metadata.schema.yaml` and `templates/metadata-template.yaml`
Confidence: medium

## Overall summary
Recent work focused on strengthening the prompt library as an operational system rather than just adding isolated prompt files. The main themes were new documentation-oriented prompts for agent workflows, clearer review and naming guidance, and tighter metadata structure. Overall, the direction suggests work on making the library easier to scale and govern.

## Uncertainties
- Commit messages do not show whether some edits were minor wording changes or substantial prompt rewrites.
- Without diffs, the exact scope of the schema and documentation edits remains partly inferred.

## Suggested update
I mainly worked on repo-aware prompt infrastructure this week: I added prompts for repo system policy and agent-structure generation, tightened the library's review and naming guidance, and cleaned up metadata/schema support so the prompt catalog is more consistent.
```

## Version

`1.0.0`

## Aenderungsverlauf

- `1.0.0` Initiale Version
