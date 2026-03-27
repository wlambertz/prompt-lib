---
id: documentation-repo-agents-structure
name: Repository AGENTS Structure Generator
category: documentation
owner: TODO-owner
status: draft
version: 1.0.0
tags:
  - repository-analysis
  - agents-md
  - agent-instructions
  - documentation
  - codebase-audit
use_cases:
  - Analyze an existing repository and create repo-specific root and nested AGENTS.md files plus an AGENTS_AUDIT.md report
input_format: markdown
output_format: markdown
language: en
model_compatibility:
  - gpt-4.1
  - gpt-5
risk_notes:
  - Can overstate repo conventions or commands if repository evidence is weak and the prompt guardrails are ignored.
  - Generated AGENTS.md files still require human review for safety-sensitive boundaries such as deployments, secrets, and migrations.
created_at: 2026-03-27
updated_at: 2026-03-27
---

# Name

Repository AGENTS Structure Generator

## Zweck

Creates a practical, repo-specific `AGENTS.md` instruction structure for an existing source repository by grounding every file in observed architecture, tooling, workflows, and risk boundaries.

## Use Case

Use this prompt when a team wants coding agents to work repeatedly inside a real repository and needs `AGENTS.md` files that reflect the codebase as it actually exists. It is especially useful for monorepos, multi-service repos, or codebases with meaningful local differences between applications, packages, infrastructure, database, or operations subtrees.

## Prompt

```text
You are operating inside an existing source code repository.

Your task is to analyze the repo and create a high-quality `AGENTS.md` instruction structure that matches the repository's actual architecture, workflows, tooling, and risk profile.

Goal:
Produce a practical, repo-specific set of `AGENTS.md` files that helps coding agents work safely and effectively in this codebase. Do not generate generic boilerplate. Infer the real structure and conventions from the repo.

What to do

1. Analyze the repository first
- Inspect the top-level layout and identify major subsystems, applications, packages, services, libraries, infrastructure, data, scripts, tests, docs, and deployment-related directories.
- Detect the tech stack, build tooling, package managers, test frameworks, linters, formatters, type checkers, CI configuration, container setup, infra tooling, and migration tooling.
- Identify architecture boundaries from the code and config, not from assumptions.
- Detect high-risk areas such as:
  - auth, permissions, secrets, credentials
  - production infra and deployment
  - database schemas and migrations
  - public APIs and compatibility-sensitive interfaces
  - billing, compliance, privacy, or safety-critical logic
- Determine whether this repo is a monorepo and whether nested or path-specific `AGENTS.md` files are warranted.

2. Design the instruction structure
- Create:
  - one root `AGENTS.md`
  - additional nested `AGENTS.md` files only where local instructions materially differ and would help an agent work better
- Use nested files for major subtrees only when justified, for example:
  - `apps/web/`
  - `services/api/`
  - `packages/domain/`
  - `infra/`
  - `db/`
  - `mobile/`
- Avoid over-fragmentation. Prefer a small number of high-signal files.

3. Write repo-specific content
Each `AGENTS.md` should be concise, operational, and concrete. Prefer commands and rules that can actually be executed or verified in this repo.

The root `AGENTS.md` should typically cover:
- repo purpose and scope
- how agents should work in this repo
- canonical commands:
  - install
  - dev or run
  - lint
  - format
  - typecheck
  - unit, integration, and e2e tests
  - build or package
  - migrations
  - relevant security or static-analysis commands
- completion criteria or validation contract
- codebase map
- architecture boundaries
- change policy:
  - prefer minimal diffs
  - avoid unrelated refactors
  - preserve backward compatibility unless explicitly asked
- safety boundaries
- documentation and update expectations

Nested `AGENTS.md` files should cover:
- what that subtree does
- local build or test commands if different
- local conventions and patterns
- boundaries specific to that subtree
- local risk and review guidance

4. Cover the important agent roles implicitly
The `AGENTS.md` structure should support these working modes where relevant:
- implementer or feature agent
- test agent
- reviewer
- refactoring agent
- docs agent
- security-sensitive changes
- reliability or ops-sensitive changes
- schema or migration-sensitive changes

Do not create separate role files unless the repo structure clearly benefits from it. Prefer a single instruction system that gives the right guardrails for these roles.

5. Base everything on evidence from the repo
- Do not invent commands that do not exist.
- Do not claim conventions unless they are supported by the codebase or config.
- If something is ambiguous, state a conservative rule.
- If a command cannot be confirmed, do not present it as canonical.
- Reuse exact command forms from package scripts, Makefiles, task runners, CI workflows, or docs where possible.

6. Keep the files useful for coding agents
- Be explicit.
- Be short.
- Be operational.
- Prefer bullets over essays.
- Prefer examples over abstract guidance.
- Do not duplicate large amounts of README content.
- Do not add generic "follow best practices" filler.

Required output

A. Create the actual `AGENTS.md` files in the repository.

B. Also produce a short report in markdown named `AGENTS_AUDIT.md` that includes:
1. proposed `AGENTS.md` file locations
2. why each file exists
3. which repo evidence was used
4. any uncertainties or assumptions
5. commands discovered
6. notable risks and boundaries identified

Quality bar

The result should reflect current best practice for agent instruction files:
- root instructions plus scoped nested instructions where needed
- concise and executable guidance
- commands near the top
- clear validation criteria
- explicit safety boundaries
- architecture-aware rules
- repo-specific, not template-ish

Before writing files, perform the analysis. Then create the files.

Implementation guidance

Follow this workflow:
1. inspect repo structure and key config files
2. inspect package manifests, build scripts, CI workflows, and task files
3. inspect test and lint setup
4. inspect infra and migration areas
5. decide the minimal useful `AGENTS.md` layout
6. write the files
7. write `AGENTS_AUDIT.md`

Suggested evidence sources to inspect:
- `README*`
- package manifests such as `package.json`, `pyproject.toml`, `Cargo.toml`, and `go.mod`
- `Makefile`, task runners, and shell or PowerShell scripts
- CI config such as `.github/workflows`, GitLab CI, or equivalent
- linter, formatter, and type-checker configs
- test configs
- Docker, Compose, or devcontainer files
- infra directories
- migration directories
- top-level docs and ADRs
- representative source directories

Writing rules for the generated `AGENTS.md` files:
- Use Markdown.
- Keep each file tight and high-signal.
- Put commands early.
- Prefer repo paths and exact command lines.
- Separate global versus local instructions cleanly.
- Include `Do not` guardrails where appropriate.
- Include a short `Done criteria` section.
- Include a short `File map` where helpful.
- Include examples only when they clarify a real convention in the repo.

Do not ask the user questions. Analyze the repo as it exists and make the best evidence-based version possible.
```

## Variablen

| Variable | Pflicht | Beschreibung | Beispiel |
| --- | --- | --- | --- |
| `{{repository_context}}` | ja | Snapshot of repo structure, key config files, workflows, and high-risk areas to inspect | `Monorepo with apps/web, services/api, packages/shared, infra/terraform, db/migrations, .github/workflows, pnpm-workspace.yaml, and Docker Compose` |
| `{{focus_areas}}` | nein | Specific risk or architecture areas that deserve extra attention | `Auth boundaries, migration workflow, release automation, and public SDK compatibility` |
| `{{output_constraints}}` | nein | Constraints on file count, tone, or artifact scope | `Prefer one root AGENTS.md plus only two nested files unless local workflows materially differ` |
| `{{agent_environment}}` | nein | Runtime and permission context of the agent creating the files | `CLI coding agent with repo write access, shell access, and no network by default` |

## Eingaben

- A real repository or a grounded summary of its current layout and tooling
- Key manifests, scripts, docs, CI files, test setup, and infrastructure signals
- Optional focus areas for safety-sensitive or underdocumented parts of the repo
- Optional operating constraints for the agent that will create the files

## Ausgabeformat

Markdown that performs analysis first and then produces repository files.

The response should result in:

- actual `AGENTS.md` files written into the repository
- an `AGENTS_AUDIT.md` report

The analysis should make clear:

- observed repository evidence
- the chosen `AGENTS.md` file layout
- why each file exists
- what commands and safety boundaries were discovered
- what remains uncertain and is therefore handled conservatively

## Einschraenkungen

- The prompt should not invent commands, workflows, or architecture boundaries that are not supported by repository evidence.
- Sparse repositories may justify only a root `AGENTS.md` and a short audit rather than a deep nested structure.
- Human review is still required before relying on generated agent instructions for production-sensitive operations.

## Wann verwenden

- When an existing repository needs repo-specific `AGENTS.md` guidance for repeated coding-agent use
- When a monorepo or multi-surface repo would benefit from scoped local instructions under specific paths
- When teams want agent instructions grounded in actual commands, risks, and architecture rather than generic policy text

## Wann nicht verwenden

- When the goal is a global `SYSTEM.md` or platform-level policy rather than `AGENTS.md` files
- When the repository has not been inspected and only vague assumptions are available
- When the task is to create a brand-new repository structure instead of documenting an existing one

## Beispiele

### Beispiel 1

**Eingabe**

```text
Repository context:
- Existing monorepo with `apps/web`, `services/api`, `packages/domain`, `infra/terraform`, and `db/migrations`
- Root `package.json` exposes `lint`, `test`, `build`, and `typecheck`
- `apps/web/package.json` adds Playwright and Storybook commands
- `services/api` uses Prisma migrations and integration tests
- `.github/workflows/ci.yml` runs lint, typecheck, unit tests, and API integration tests
- `README.md` explains local setup; `CONTRIBUTING.md` warns against unrelated refactors

Focus areas:
- deployment safety
- migration review
- public API compatibility

Output constraints:
- keep the instruction layout minimal and high-signal
- only add nested files where workflows differ materially

Agent environment:
- CLI coding agent with shell access and repo write access
```

**Erwartete Ausgabe**

```text
Observed repository evidence:
- Monorepo structure with separate web, API, domain, infra, and migration areas
- Commands differ between frontend and backend subtrees
- CI confirms canonical validation commands

Chosen AGENTS.md layout:
- `AGENTS.md`
- `apps/web/AGENTS.md`
- `services/api/AGENTS.md`
- `infra/AGENTS.md`

Then create:
- a root `AGENTS.md` with shared repo rules, commands, architecture map, and done criteria
- scoped nested files with local commands, risk boundaries, and subtree-specific do-not rules
- `AGENTS_AUDIT.md` documenting evidence, commands, assumptions, and risks
```

## Version

`1.0.0`

## Aenderungsverlauf

- `1.0.0` Initiale Version
