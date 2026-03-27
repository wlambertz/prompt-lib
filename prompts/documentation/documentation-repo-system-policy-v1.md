---
id: documentation-repo-system-policy
name: Repository System Policy Generator
category: documentation
owner: TODO-owner
status: draft
version: 1.0.0
tags:
  - repository-analysis
  - system-md
  - agent-policy
  - documentation
use_cases:
  - Analyze a repository and derive a repo-specific SYSTEM.md for an AI agent working there repeatedly
input_format: markdown
output_format: markdown
language: en
model_compatibility:
  - gpt-4.1
  - gpt-5
risk_notes:
  - Can overgeneralize from weak repo signals unless assumptions are labeled explicitly.
  - May invent workflows or conventions if the repository is underdocumented and the prompt guardrails are ignored.
created_at: 2026-03-27
updated_at: 2026-03-27
---

# Name

Repository System Policy Generator

## Zweck

Creates a production-quality `SYSTEM.md` for a specific repository by grounding the policy in the repo's actual structure, docs, scripts, tests, workflows, and conventions.

## Use Case

Use this prompt when a team wants an AI agent to operate repeatedly inside a repository and needs a stable, repo-specific system policy rather than a generic agent manifesto. The prompt is designed for repos that already contain some combination of code, docs, CI, scripts, and contribution conventions, but may still have documentation gaps that require clearly labeled assumptions.

## Prompt

```text
You are analyzing a repository in order to derive the global operating policy for an AI agent that will work in it repeatedly.

Your job is to create a production-quality `SYSTEM.md` that reflects what actually exists in the repository.

Do not write a generic agent manifesto. Ground every policy statement in repository evidence such as:
- directory structure
- source code organization
- scripts and commands
- tests and validation workflows
- CI/CD pipelines
- deployment or release conventions
- docs and contribution guidance
- architecture and coding conventions
- existing agent, automation, prompt, or workflow files

Repository context:
{{repository_context}}

Target agent and operating environment:
{{target_agent}}

Additional focus areas:
{{focus_areas}}

Output constraints:
{{output_constraints}}

Work in two phases.

Phase 1: Analyze the repository
- summarize the project purpose
- summarize major directories and their roles
- identify key scripts, commands, workflows, and pipelines
- identify the test strategy
- identify deployment and release conventions
- identify architecture patterns
- infer coding conventions only when supported by repo evidence
- assess documentation quality and gaps
- identify existing agent, prompt, automation, or workflow files

Explicitly separate:
- observed facts
- reasonable inferences
- recommendations

Phase 2: Derive the system policy
Based on the repository, infer what an AI agent should globally optimize for in this repo.

Generate a concise, operational, stable `SYSTEM.md` with these sections:
1. Mission
2. Scope
3. Priorities
4. Hard constraints
5. Tool and repo-navigation policy
6. Change policy
7. Testing and validation expectations
8. Documentation policy
9. Uncertainty and fallback behavior
10. Instruction precedence
11. Boundaries: what belongs in Skills instead

Requirements:
- base the policy on the repository as it exists
- prefer explicit operational rules over vague values
- do not invent tools, environments, processes, or team conventions that are not supported by the repo
- keep repo-global policy separate from task-specific workflows
- include clear guardrails around risky or ambiguous areas
- if the repo lacks conventions, propose only minimal sane defaults and label them as proposed
- optimize for repeated safe use by an agent in this repository

Before the final `SYSTEM.md`, provide:

A. Observed signals
- strongest repository signals that shaped the policy

B. Candidate Skill boundaries
- workflows that should be separate `SKILL.md` files instead of being embedded in `SYSTEM.md`

C. Policy risks
- ambiguities, gaps, or contradictions in the repo
- how the `SYSTEM.md` should handle them

After the `SYSTEM.md`, provide:
- a short rationale for each major section
- a short list of recommended follow-up files such as `SKILL.md`, `references/*.md`, `scripts/*.py`, or `agents/openai.yaml`

If the repository is ambiguous, do not stop. Produce the best grounded draft you can and label assumptions clearly.
```

## Variablen

| Variable | Pflicht | Beschreibung | Beispiel |
| --- | --- | --- | --- |
| `{{repository_context}}` | ja | Repo snapshot, directory map, key files, or extracted notes from inspection | `Monorepo with backend/, frontend/, .github/workflows/, docs/, Makefile, and CONTRIBUTING.md` |
| `{{target_agent}}` | nein | Agent role, tool access, runtime constraints, or expected collaboration model | `CLI coding agent with repo write access, shell access, and responsibility for docs, code changes, and tests` |
| `{{focus_areas}}` | nein | Extra areas to inspect more closely | `Pay special attention to deployment scripts, release automation, and agent instruction files` |
| `{{output_constraints}}` | nein | Constraints on style, length, or required sections | `Keep SYSTEM.md concise, high-signal, and stable over time` |

## Eingaben

- A repository or a structured summary of its codebase, docs, and workflows
- Enough repo evidence to infer conventions without inventing them
- Optional agent-environment details such as available tools or permissions
- Optional focus areas for high-risk or underdocumented parts of the repo

## Ausgabeformat

Markdown with these parts in order:

- repo analysis with clear separation of facts, inferences, and recommendations
- `Observed signals`
- `Candidate Skill boundaries`
- `Policy risks`
- final `SYSTEM.md`
- brief rationale per major section
- recommended follow-up files

## Einschraenkungen

- Weak or sparse repositories may not justify strong policy statements
- Human review is still required before adopting the generated `SYSTEM.md` as governing repo policy
- The prompt does not replace task-specific skills, deployment runbooks, or contributor documentation

## Wann verwenden

- When a repository needs a repo-specific operating constitution for an AI agent
- When onboarding an agent to an existing codebase with real conventions to infer
- When teams want stable global policy separated from task-level instructions

## Wann nicht verwenden

- When the goal is a one-off task prompt rather than a reusable repo policy
- When the repository has not been inspected and only vague assumptions are available
- When a narrower workflow document or skill should be written instead of a global `SYSTEM.md`

## Beispiele

### Beispiel 1

**Eingabe**

```text
Analyze a repository that contains:
- backend/ with Gradle build, integration tests, and Flyway migrations
- frontend/ with React app and Playwright tests
- .github/workflows/ for CI, release, and dependency checks
- docs/architecture.md, CONTRIBUTING.md, and scripts/release.ps1

Target agent:
- repository coding agent with shell access and write permissions

Focus areas:
- release safety, test expectations, migration guardrails, and documentation update rules

Output constraints:
- keep the final SYSTEM.md concise, operational, and grounded in repo evidence
```

**Erwartete Ausgabe**

```text
Observed signals:
- CI and release workflows indicate test and release discipline
- migration tooling suggests schema changes need stronger guardrails

Candidate Skill boundaries:
- release cut procedure
- database migration workflow
- frontend test triage

Policy risks:
- deployment ownership unclear; SYSTEM.md should require escalation instead of guessing

# SYSTEM.md
## Mission
Help deliver safe, reviewable changes across backend, frontend, and docs while preserving release reliability.
...
```

## Version

`1.0.0`

## Aenderungsverlauf

- `1.0.0` Initiale Version
