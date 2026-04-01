---
id: coding-repository-commit-message-policy-advisor
name: Repository Commit Message Policy Advisor
category: coding
owner: TODO-owner
status: draft
version: 1.0.0
tags:
  - git
  - commit-messages
  - team-conventions
  - repository
  - conventional-commits
  - gitmoji
use_cases:
  - Advise a team on a commit-message policy for a specific repository based on the repo's workflow, history, and collaboration needs
  - Produce repo-specific commit-message guidance, examples, and adoption recommendations including optional gitmoji usage
input_format: markdown
output_format: markdown
language: en
model_compatibility:
  - gpt-4.1
  - gpt-5
risk_notes:
  - Recommendations can become cargo-cult policy if repository history, release workflow, or team constraints are underspecified.
  - Gitmoji can reduce clarity or searchability if it is treated as decoration without a clear textual convention underneath.
created_at: 2026-04-01
updated_at: 2026-04-01
---

# Name

Repository Commit Message Policy Advisor

## Zweck

Advises a team on how commit messages should work for a specific repository so the resulting convention is clear, sustainable, and aligned with the repo's tooling, review flow, and collaboration habits.

## Use Case

Use this prompt when a team wants to define, revise, or standardize commit-message rules for a repository rather than generate a single commit message. It is especially useful when the team needs a recommendation about plain Git-style subjects, Conventional Commits, scoped prefixes, explanatory bodies, squash-merge habits, or whether gitmoji should be part of the convention.

## Prompt

```text
You are advising a software team on commit-message policy for a specific repository.

Your job is to recommend a commit-message convention that fits the repository's workflow, team habits, and tooling constraints, then explain how the team should apply it consistently.

Work from the repository evidence first. Do not recommend a convention just because it is fashionable.

Inputs:
- Repository context: {{repository_context}}
- Existing commit history or examples: {{commit_history_samples}}
- Team workflow and collaboration style: {{team_workflow}}
- Current pain points: {{pain_points}}
- Release or automation requirements: {{automation_requirements}}
- Optional preference about gitmoji: {{gitmoji_preference}}
- Optional constraints: {{constraints}}

Instructions:
- inspect the repository context and commit history before recommending a convention
- identify whether the repo already has a visible pattern worth preserving, tightening, or replacing
- recommend one primary convention for the repo, such as plain imperative subjects, Conventional Commits, or another clearly defined structure
- explain when commit bodies are required versus optional
- define how to handle scopes, issue references, breaking changes, and mixed-concern commits
- explicitly say whether gitmoji should be:
  - not used
  - optional decoration on top of a textual convention
  - part of the documented standard
- if gitmoji is recommended, keep text clarity primary and explain the allowed mapping rules
- prefer conventions that are easy for humans to read in logs, PRs, blame output, and release tooling
- call out tradeoffs such as readability, learning curve, changelog generation, automation value, and review friendliness
- if the current repository history is inconsistent, recommend a practical transition policy instead of pretending perfect standardization already exists
- avoid recommending a policy that depends on tools or bots the repo does not have unless the user explicitly wants process changes

Return the answer in Markdown with these sections:

1. `Recommended policy`
- state the recommended convention in one paragraph

2. `Why this fits the repo`
- explain the strongest reasons based on the inputs

3. `Policy rules`
- provide a concise rule set the team can adopt
- include subject-line rules, body rules, scopes, issue references, and handling of unrelated changes

4. `Gitmoji guidance`
- state whether gitmoji is disallowed, optional, or standard
- if used, define how it interacts with the textual convention

5. `Examples`
- provide 5 to 8 example commit messages for realistic repo changes

6. `Adoption advice`
- explain how the team should roll this out, including whether to enforce immediately or phase it in

7. `Risks and caveats`
- identify where the policy could fail or create friction

Requirements:
- be specific and repo-aware
- do not force Conventional Commits unless the repo's needs justify them
- do not force gitmoji unless there is a clear human or workflow benefit
- prefer a convention that can be taught in a short team guide
- make the recommendation implementable without rewriting repository history
```

## Variablen

| Variable | Pflicht | Beschreibung | Beispiel |
| --- | --- | --- | --- |
| `{{repository_context}}` | ja | Repo type, stack, team size, merge strategy, and any workflow details that shape commit-message needs | `Backend API repo with 6 engineers, squash merges on GitHub, Jira references in PR titles, and no automated changelog tooling` |
| `{{commit_history_samples}}` | nein | Recent commit messages or representative examples from the repo | ``feat(api): add webhook retries`, `Fix flaky auth test`, `:sparkles: add billing export`` |
| `{{team_workflow}}` | nein | How the team collaborates, reviews, and lands changes | `Most work lands through PR squash merges, developers browse git log during debugging, and reviewers prefer short subjects with informative bodies for risky changes` |
| `{{pain_points}}` | nein | Problems with the current commit-message situation | `Subjects are inconsistent, some commits are too vague, and release notes are hard to group` |
| `{{automation_requirements}}` | nein | Tooling or release constraints that may require structured messages | `Semantic-release is being considered, but currently no release automation parses commit messages` |
| `{{gitmoji_preference}}` | nein | Whether the team wants to consider gitmoji, avoid it, or is undecided | `Undecided; some engineers like gitmoji, others worry it hurts readability` |
| `{{constraints}}` | nein | Extra rules such as subject length, mandatory ticket IDs, or policy rollout constraints | `Keep the convention lightweight and avoid mandatory scopes for tiny docs changes` |

## Eingaben

- Repository context with enough detail to understand how the team works
- Optional commit history samples or current examples from the repo
- Optional collaboration and release-process details
- Optional pain points, tooling requirements, or preferences about gitmoji

Minimum useful input:

- what kind of repo and team this is
- whether the repo already has an established pattern
- whether any tooling depends on commit-message structure

## Ausgabeformat

Markdown with these sections in order:

- `Recommended policy`
- `Why this fits the repo`
- `Policy rules`
- `Gitmoji guidance`
- `Examples`
- `Adoption advice`
- `Risks and caveats`

The `Policy rules` section should be concise enough that a team could copy it into `CONTRIBUTING.md` with minimal editing.

## Einschraenkungen

- The prompt recommends a policy; it does not inspect the live repository unless the caller provides repo evidence.
- Weak or cherry-picked commit-history examples can bias the recommendation toward the wrong convention.
- A good policy cannot compensate for commits that bundle unrelated changes together.
- Human review is still needed before turning the output into an enforced team standard.

## Wann verwenden

- When a team wants repo-specific guidance on how commit messages should be written
- When deciding whether to use Conventional Commits, plain Git-style subjects, scoped prefixes, or gitmoji
- When documenting or revising commit-message rules for onboarding, reviews, or release hygiene

## Wann nicht verwenden

- When the goal is to write one commit message for one change
- When no repository context or team workflow information is available
- When the real problem is branch strategy, PR hygiene, or commit granularity rather than message format

## Beispiele

### Beispiel 1

**Eingabe**

```text
Repository context:
TypeScript monorepo with web app, API, and shared packages. Team of 10 engineers. GitHub PR flow with squash merges enabled. No existing changelog automation.

Existing commit history or examples:
- fix login redirect bug
- feat(api): add usage endpoint
- :recycle: cleanup billing service
- update stuff

Team workflow and collaboration style:
Most developers inspect git log during debugging and code archaeology. Reviewers want subjects that are fast to scan. Bodies are useful for risky backend or migration changes.

Current pain points:
Inconsistent style, vague subjects, and disagreement about whether emojis are helpful.

Release or automation requirements:
No parser currently depends on commit messages, but the team may add release tooling later.

Optional preference about gitmoji:
Undecided.

Optional constraints:
Keep the policy lightweight and easy to onboard.
```

**Erwartete Ausgabe**

```text
## Recommended policy
Adopt a lightweight Conventional Commits style with optional scopes and optional bodies for non-trivial changes. Keep gitmoji optional and secondary to the textual subject rather than making emoji the primary signal.

## Why this fits the repo
- The repo already shows partial Conventional Commit usage.
- A structured subject helps a monorepo and keeps future release tooling possible.
- Optional scopes and optional gitmoji keep the rule set light enough for daily use.

## Policy rules
- Use `<type>[optional scope]: <description>` for the subject.
- Keep the subject imperative and specific.
- Use a body when the change has important context, tradeoffs, or migration impact.
- Do not hide unrelated changes in one commit message.
...

## Gitmoji guidance
- Gitmoji is optional decoration.
- If used, place it before the textual subject and keep the textual convention intact.
...
```

### Beispiel 2

**Eingabe**

```text
Repository context:
Small internal infrastructure repo with 3 engineers and mostly operational scripts. Merges are infrequent and maintainers read full PRs more often than raw git history.

Existing commit history or examples:
- Add backup retention script
- Fix broken cron path
- Update README

Team workflow and collaboration style:
The team wants low process overhead and values clarity over categorization.

Current pain points:
Not much standardization, but no one wants verbose syntax.

Release or automation requirements:
None.

Optional preference about gitmoji:
Avoid it.

Optional constraints:
Subjects should stay under 72 characters.
```

**Erwartete Ausgabe**

```text
## Recommended policy
Use plain imperative Git-style subjects with optional bodies for operational or risky changes. Do not adopt Conventional Commits or gitmoji for this repo because the workflow does not need extra taxonomy.

## Why this fits the repo
- The team is small and does not need structured release automation.
- Existing history is already readable in plain English.
- Extra syntax would add overhead without enough payoff.

## Policy rules
- Write a short imperative subject.
- Add a body only when the reason or operational consequence matters.
- Reference tickets only when relevant.
...

## Gitmoji guidance
- Do not use gitmoji in this repository.
...
```

## Version

`1.0.0`

## Aenderungsverlauf

- `1.0.0` Initial version
