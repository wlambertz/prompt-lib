---
id: coding-repository-folder-structure
name: Repository Folder Structure Planner
category: coding
owner: WLA
status: draft
version: 1.0.0
tags:
  - repository
  - scaffolding
  - structure
  - documentation
  - infrastructure
use_cases:
  - Plan a new repository layout before implementation starts, including code, docs, and infrastructure areas
input_format: markdown
output_format: markdown
language: en
model_compatibility:
  - gpt-4.1
  - gpt-5
risk_notes:
  - Can produce an overengineered structure if the project scope, team size, or deployment model is not clarified first.
  - Suggested directories still need human validation against actual tooling, compliance, and hosting constraints.
---

# Name

Repository Folder Structure Planner

## Zweck

Designs a pragmatic folder structure for a new software repository by first clarifying the repository's purpose, product shape, documentation needs, and infrastructure expectations.

## Use Case

Use this prompt when a team is starting a new repository and wants a deliberate, reviewable structure instead of creating folders ad hoc. The prompt is especially useful when the repository must make room for application code, architecture documentation, UI/UX documentation, operational docs, and infrastructure assets from the beginning.

## Prompt

```text
You are helping design the initial folder structure for a brand-new software repository.

Your goal is to propose a practical repository layout that fits the intended product, delivery model, documentation needs, and infrastructure footprint.

If the input is incomplete, do not jump straight to a tree. First ask the user the minimum set of clarifying questions needed to make the structure credible.

Start by checking whether you know enough about:
- the repository purpose
- the type of software being built
- the main components or services
- whether this is a monolith, modular app, or monorepo
- frontend or UI presence
- infrastructure and deployment expectations
- documentation expectations
- test strategy and developer tooling

If key information is missing, ask concise questions such as:
- What is the primary purpose of this repository?
- What kind of software will live here: backend, frontend, full-stack app, mobile app, CLI, data pipeline, library, or something else?
- What are the main runtime components or services?
- Do you expect a monorepo with multiple apps/packages, or a single deployable application?
- Will this repository contain UI work that needs dedicated UI or UX documentation?
- What documentation should be maintained here: architecture, ADRs, API docs, onboarding docs, runbooks, UI/UX docs, product decisions?
- Will infrastructure live in the same repo, for example Terraform, Kubernetes, Helm, CI/CD, or deployment scripts?
- Are there specific environments, compliance constraints, or team conventions that should shape the structure?

Once you have enough information, produce the answer in this order:

1. Assumptions
- list the facts provided by the user
- list any explicit assumptions you had to make

2. Recommended repository structure
- provide a directory tree in Markdown
- keep it pragmatic and avoid unnecessary nesting
- include only folders that have a clear purpose

3. Folder rationale
- explain the purpose of each top-level directory
- call out where software components live
- call out where documentation lives
- call out where infrastructure lives

4. Documentation coverage
- explicitly include space for documentation such as:
  - architecture
  - ADRs
  - API or integration docs when relevant
  - UI/UX docs, flows, design decisions, or assets when relevant
  - onboarding and contribution docs
  - operational docs or runbooks

5. Infrastructure coverage
- explicitly include space for infrastructure assets such as:
  - infrastructure as code
  - deployment manifests
  - environment configuration templates
  - CI/CD workflows
  - operational scripts

6. Suggested starter files
- recommend a short list of initial files the team should create alongside the folders

7. Watchouts
- identify likely overengineering risks
- identify repo-splitting or monorepo risks if relevant
- mention anything that should be validated before scaffolding

Requirements:
- ask clarifying questions first when the repo intent is underspecified
- optimize for maintainability and discoverability, not maximum abstraction
- make room for both product code and non-code assets
- include documentation and infrastructure as first-class parts of the repository when relevant
- keep the proposal adaptable to small teams unless the user explicitly asks for enterprise-scale structure
- avoid inventing technologies the user did not mention; label recommendations clearly when inferred
```

## Variablen

| Variable | Pflicht | Beschreibung | Beispiel |
| --- | --- | --- | --- |
| `{{repository_brief}}` | ja | Initial description of the repository purpose, software type, and any known constraints | `New SaaS product with React frontend, Python API, PostgreSQL, and Terraform-managed cloud infrastructure` |
| `{{known_components}}` | nein | Known services, apps, packages, or bounded contexts | `web-app, api, worker, shared-ui, shared-config` |
| `{{documentation_expectations}}` | nein | Required documentation areas that should have dedicated space in the repo | `architecture docs, ADRs, UI flows, onboarding, runbooks` |
| `{{infrastructure_scope}}` | nein | Deployment and operations assets expected to live in the repository | `Terraform, Helm charts, GitHub Actions workflows, scripts for local setup` |
| `{{constraints}}` | nein | Team, compliance, hosting, or tooling constraints that affect structure | `Small team, single repo preferred, must separate app code from infra and regulated documentation` |

## Eingaben

- A short repository brief describing the product or system being built
- Known software components, services, apps, or packages if already decided
- Documentation expectations, especially architecture and UI/UX needs
- Infrastructure expectations such as IaC, deployment manifests, CI/CD, or scripts
- Optional constraints around team size, environments, compliance, or tooling

## Ausgabeformat

Markdown with these sections in order:

- `Assumptions`
- `Recommended repository structure`
- `Folder rationale`
- `Documentation coverage`
- `Infrastructure coverage`
- `Suggested starter files`
- `Watchouts`

The `Recommended repository structure` section should contain a readable folder tree.

## Einschraenkungen

- The prompt cannot determine the right repository shape if the product boundaries are still undefined
- Human review is required before generating or scaffolding folders automatically
- The output is a planning artifact, not a substitute for architecture, platform, or security review

## Wann verwenden

- When starting a new repository and wanting a deliberate initial structure
- When teams need code, docs, and infrastructure to coexist clearly in one repository
- When architecture and UI/UX documentation should be planned alongside implementation folders

## Wann nicht verwenden

- When the repository structure already exists and only minor cleanup is needed
- When the project brief is too vague to distinguish between single-app and multi-package layouts
- When the task is to generate implementation code rather than plan repository structure

## Beispiele

### Beispiel 1

**Eingabe**

```text
We are starting a new repository for a B2B SaaS platform.

Known details:
- React web app
- Node.js backend API
- background worker
- PostgreSQL
- GitHub Actions for CI/CD
- Terraform for cloud infrastructure

We want dedicated space for:
- architecture documentation
- ADRs
- UI/UX flows and design notes
- onboarding docs
- operational runbooks

We are a small team and want to avoid overengineering.
```

**Erwartete Ausgabe**

```text
## Assumptions
- Single repository for web, API, and worker
- Shared docs and infrastructure stay in the same repo

## Recommended repository structure
repo/
|- apps/
|  |- web/
|  |- api/
|  `- worker/
|- docs/
|  |- architecture/
|  |- adrs/
|  |- ui-ux/
|  |- onboarding/
|  `- runbooks/
|- infra/
|  |- terraform/
|  |- environments/
|  `- scripts/
|- .github/
|  `- workflows/
`- tools/

## Folder rationale
- `apps/` holds deployable software components
- `docs/` keeps long-lived project documentation discoverable
- `infra/` isolates infrastructure definitions and operational assets
...
```
