# OpenAI Codex Skills Guide

This guide extracts the core ideas from *The Complete Guide to Building Skills for Claude* and adapts them to **OpenAI Codex**.

## Executive summary

Yes, the Claude guide maps well to Codex.

Why:

- Both systems use the same basic idea: a **skill is a folder** with a `SKILL.md` entrypoint plus optional supporting files.
- Both rely on **progressive disclosure**: the model sees lightweight metadata first and only loads the full skill when relevant.
- OpenAI Codex now has **first-class Agent Skills**, plus companion mechanisms that Claude's guide does not cover in the same way: **`AGENTS.md`**, **Rules**, and **Plugins**.

The main adaptation is this:

- In **Claude**, the guide emphasizes `SKILL.md` and upload/distribution.
- In **Codex**, you should think in **four layers**:
  1. **Skills** for reusable workflows
  2. **`AGENTS.md`** for always-on repo or directory instructions
  3. **Rules** for command-execution policy outside the sandbox
  4. **Plugins** for packaging and distribution

---

## 1. What I extracted from the Claude guide

The PDF's most important ideas are still the right foundation for Codex:

### 1.1 A skill should be a reusable workflow, not a giant prompt dump

A strong skill captures a repeatable job such as:

- verifying code changes
- drafting a PR summary
- running a release review
- preparing migration plans
- reviewing logs against expected behavior

### 1.2 Start with 2-3 concrete use cases

Before writing files, define:

- what the user wants to accomplish
- the trigger phrases or situations
- the steps Codex should follow
- the expected output or artifact

### 1.3 The description is the routing contract

The original guide is right that the frontmatter matters most. In Codex too, the `description` is the main signal that decides whether the skill should be used.

A good description answers both:

- **What does this skill do?**
- **When should it trigger?**

### 1.4 Use progressive disclosure

Keep the main skill concise.

- Put the routing metadata in `SKILL.md` frontmatter.
- Put the core workflow in the `SKILL.md` body.
- Put large references, schemas, checklists, and examples in `references/`.
- Put deterministic mechanics in `scripts/`.

### 1.5 Let the model reason; use scripts for mechanics

Do not turn every step into code.

Good split:

- **Model:** interpretation, tradeoffs, review, prioritization, explanation
- **Scripts:** fixed command sequences, log collection, deterministic validation, structured extraction

### 1.6 Test three things separately

The Claude guide's testing model still works well for Codex:

1. **Triggering** — does the skill activate when it should?
2. **Functionality** — does it complete the workflow correctly?
3. **Performance/value** — is it actually better than doing the task ad hoc?

### 1.7 Iterate from real failures

The fastest way to improve a skill is still:

- run it on real work
- collect misses, over-triggering, and failure cases
- tighten the description
- refine the instructions
- script the repeated brittle parts

---

## 2. What changes for Codex

This is where the adaptation matters.

## 2.1 Codex has native Agent Skills

Codex supports Agent Skills directly. A skill is still a directory with a `SKILL.md` file and optional `scripts/`, `references/`, `assets/`, and optionally `agents/openai.yaml`.

Minimal shape:

```text
my-skill/
├── SKILL.md
├── scripts/
├── references/
├── assets/
└── agents/
    └── openai.yaml
```

For Codex, only `name` and `description` are required in `SKILL.md` frontmatter.

---

## 2.2 Codex also has `AGENTS.md`

A **Codex skill is not the same thing as `AGENTS.md`**.

Use them together, but for different purposes.

### Use a Skill when:

- the workflow is reusable but not always needed
- the task has a distinct trigger boundary
- you want optional scripts or references
- you want explicit `$skill-name` invocation or implicit routing

### Use `AGENTS.md` when:

- the instruction should apply to nearly every task in a repo or directory
- you want standing rules like coding standards, required checks, or dependency policy
- you want nested directory-specific overrides

A strong Codex setup often uses `AGENTS.md` to **tell Codex when to use certain skills**.

Example pattern:

```md
## Mandatory skill usage
- Use `$code-change-verification` when runtime code, tests, or build behavior changes.
- Use `$pr-draft-summary` when substantive code work is ready for review.
```

That pattern is especially powerful in repositories with required verification gates.

---

## 2.3 Codex has Rules for command control

If your workflow needs command policy, do **not** encode that only in prose.

Use **Rules** when you need to control which commands Codex may run outside the sandbox.

This is separate from skills:

- **Skill:** tells Codex *how to do the workflow*
- **Rules:** tell Codex *which commands are allowed, blocked, or require approval*

If a workflow depends on elevated or dangerous commands, document that in the skill, but enforce it with Rules.

---

## 2.4 Codex uses Plugins for distribution

This is one of the biggest differences from the Claude guide.

For Codex:

- **Skill folders** are best for local authoring and repo-scoped use.
- **Plugins** are the installable distribution unit.

So the recommended lifecycle is:

1. author and iterate as a local skill
2. validate it in real repos
3. package it as a plugin only when you are ready to share it across teams or projects

Minimal plugin shape:

```text
my-plugin/
├── .codex-plugin/
│   └── plugin.json
├── skills/
│   └── my-skill/
│       └── SKILL.md
├── .app.json
├── .mcp.json
└── assets/
```

---

## 3. The Codex mental model: Skill vs AGENTS.md vs Rules vs Plugin

| Mechanism | Best use | Scope | Typical content |
|---|---|---|---|
| **Skill** | Reusable workflow | Optional, task-triggered | `SKILL.md`, scripts, references |
| **`AGENTS.md`** | Standing project guidance | Global, repo, or subdirectory | coding norms, required skills, required checks |
| **Rules** | Command permission policy | User/admin/team config | allow, prompt, or forbid command prefixes |
| **Plugin** | Distribution and installation | Cross-team / reusable package | one or more skills, optional app or MCP config |

Quick rule of thumb:

- If the instruction should apply **all the time**, use `AGENTS.md`.
- If it should apply **only for a certain class of task**, use a Skill.
- If it is about **shell permission policy**, use Rules.
- If you want to **ship it to others**, use a Plugin.

---

## 4. Codex skill anatomy

## 4.1 `SKILL.md`

This is the entrypoint.

A minimal Codex `SKILL.md`:

```md
---
name: code-change-verification
description: run the required verification workflow when runtime code, tests, examples, or build/test behavior changes. do not use for docs-only edits or trivial note updates.
---

# Code Change Verification

## Goal
Verify that code changes satisfy the repository's required checks before work is marked complete.

## Inputs
- Changed files
- Current branch state
- Repository test and lint commands

## Workflow
1. Determine whether the change falls within this skill's scope.
2. If yes, run the required checks in the documented order.
3. Summarize results with pass/fail status and next actions.
4. Do not mark the task complete until required checks pass or failures are explained.
```

### Frontmatter rules

Keep it simple:

- `name`: short, stable, kebab-case
- `description`: precise trigger contract

Best practice:

- keep the `name` stable over time
- write the `description` in plain language that matches real task phrasing
- include both positive triggers and negative boundaries

Good:

```yaml
name: pr-draft-summary
description: create a pr title and draft description after substantive code changes are finished. trigger when wrapping up a moderate or larger change and a pr-ready summary block is needed.
```

Weak:

```yaml
name: pr-helper
description: helps with prs.
```

---

## 4.2 `scripts/`

Use scripts only when the workflow has a repeated, brittle, or deterministic mechanical core.

Good script candidates:

- run checks in a fixed order
- gather logs and store them in standard files
- summarize changed files into structured JSON
- bootstrap verification fixtures
- fetch release tags and compute diffs

Design scripts like tiny CLIs:

- accept clear arguments
- print deterministic stdout
- fail loudly with useful errors
- write outputs to known file paths when needed

Bad use of scripts:

- replacing judgment, prioritization, or review with opaque code
- hiding the entire workflow behind one giant shell script with no interpretable outputs

---

## 4.3 `references/`

Use `references/` for information Codex may need to load on demand, such as:

- repo-specific command reference
- architecture notes
- release checklist
- schema maps
- API constraints
- service ownership notes

This is the right place for details that are useful but too heavy for the main `SKILL.md` body.

---

## 4.4 `assets/`

Use `assets/` for reusable output materials such as:

- report templates
- PR templates
- issue templates
- example config snippets
- icons or screenshots for plugin presentation

---

## 4.5 `agents/openai.yaml` (optional)

For Codex, `agents/openai.yaml` is optional but useful.

Use it to add:

- user-facing display metadata
- optional default prompt text
- invocation policy such as `allow_implicit_invocation: false`
- declared tool dependencies, including MCP tools

Example:

```yaml
interface:
  display_name: "PR Draft Summary"
  short_description: "Create a PR-ready title and summary block"
  default_prompt: "Use this skill to prepare the final PR draft"

policy:
  allow_implicit_invocation: false

dependencies:
  tools:
    - type: "mcp"
      value: "openaiDeveloperDocs"
      description: "OpenAI Docs MCP server"
```

Use this when you want a better Codex app experience or when the skill depends on a named tool.

---

## 5. Where to save Codex skills

Codex discovers skills from multiple locations.

### Repository-scoped

Use repo skills when a workflow belongs to the codebase.

Common location:

```text
$REPO_ROOT/.agents/skills/
```

This is the best default for team workflows tied to a repository.

### User-scoped

Use user-level skills for personal workflows that should follow you across repos.

```text
$HOME/.agents/skills/
```

### Admin/system

Codex can also load admin and system-level skills.

Use these for organization-wide defaults or curated built-ins.

---

## 6. How Codex activates skills

Codex can activate a skill in two ways:

### Explicit

You name the skill directly.

Examples:

- `/skills`
- `$my-skill`
- prompt text that explicitly mentions the skill

### Implicit

Codex chooses the skill because the task matches the `description`.

This is why routing metadata matters so much.

If implicit routing becomes noisy, either:

- tighten the description, or
- set `allow_implicit_invocation: false` in `agents/openai.yaml`

---

## 7. A Codex-first process for building skills

This is the Claude guide rewritten for Codex.

## Step 1: decide whether this should be a Skill at all

Ask:

- Is this a repeatable workflow?
- Is it optional rather than always-on?
- Does it have a recognizable trigger boundary?
- Would it benefit from reusable scripts or references?

If the answer is mostly no, use `AGENTS.md` instead.

---

## Step 2: define 2-3 concrete use cases

Write them in this format:

```text
Use case: verify runtime code changes
Trigger: edited runtime code, tests, examples, or build/test config
Inputs: changed files, repo commands, logs
Workflow:
1. determine applicability
2. run checks in order
3. collect output
4. summarize failures and next actions
Output: pass/fail verification report
```

If you cannot name the triggers clearly, the skill is probably too vague.

---

## Step 3: split always-on rules from reusable workflows

Before writing the skill, split the design into:

### `AGENTS.md`
Put here:

- standing coding agreements
- required commands or required skill usage
- dependency or review policy
- directory-specific overrides

### Skill
Put here:

- the reusable workflow itself
- conditional logic
- references and scripts
- structured outputs

### Rules
Put here:

- allow/prompt/forbid command policy outside the sandbox

This separation keeps the system understandable.

---

## Step 4: write the routing metadata first

Start with the shortest correct `name` and the best possible `description`.

A good `description` usually includes:

- the action
- the trigger condition
- the task boundary
- sometimes an explicit non-trigger

Template:

```yaml
description: [do this workflow] when [these changes or user requests happen]. do not use when [out of scope cases].
```

Examples:

```yaml
description: run the repository verification workflow when changes affect runtime code, tests, examples, or build/test behavior. do not use for docs-only edits.
```

```yaml
description: prepare a pr-ready summary after substantive code work is complete. use when the branch is ready for review and a title, summary, and change narrative are needed.
```

---

## Step 5: keep the body procedural and imperative

Your `SKILL.md` body should read like an operating procedure.

Recommended structure:

```md
# Skill name

## Goal
What success looks like.

## Trigger interpretation
How to confirm the task is in scope.

## Inputs
What the skill expects.

## Workflow
1. First step
2. Second step
3. Third step

## Output format
What Codex should return or write.

## Failure handling
What to do when checks fail, data is missing, or tools are unavailable.

## References
Which files under `references/` to consult and when.
```

Best practices:

- write commands exactly when they matter
- name expected outputs explicitly
- say when not to continue
- say what “done” means

---

## Step 6: move repeated shell work into scripts

If you notice the same command recipe appearing more than once, move it into `scripts/`.

Typical signals that a script is warranted:

- exact command order matters
- output must be collected consistently
- failure modes should be standardized
- the task is easy for a shell but tedious for the model to rediscover

A useful pattern is:

- the skill decides **whether** to run the workflow
- the script executes **how** to run the mechanical steps
- the skill interprets the result and reports next actions

---

## Step 7: wire the skill into `AGENTS.md`

Once the skill is reliable, make it part of the repo's working agreements.

Example:

```md
## Mandatory skill usage
- Use `$release-review` before publishing a release candidate.
- Use `$code-change-verification` for runtime, test, example, or build/test changes.
- Use `$pr-draft-summary` when a non-trivial branch is ready for review.
```

This is one of the strongest Codex-specific upgrades over the Claude-only approach.

---

## Step 8: test routing, execution, and safety

### Routing tests

Create prompts that should trigger and should not trigger.

Should trigger:

- "Run the verification stack for this runtime change"
- "I changed tests and build config; make sure the repo checks pass"
- "Prepare the PR summary for this finished branch"

Should not trigger:

- "Explain how this file works"
- "Rewrite this comment"
- "What does this regex do?"

### Execution tests

Verify that the skill:

- runs the right steps
- uses the right scripts
- produces the expected output block or files
- stops correctly on failure

### Safety tests

Check assumptions about:

- sandbox mode
- command approvals
- required tools or MCP servers
- internet access

If a skill depends on network access, document that clearly. In Codex cloud, the agent phase blocks internet access by default unless you enable it.

---

## Step 9: package as a plugin only after the workflow is stable

When the skill is mature and worth sharing:

- create `.codex-plugin/plugin.json`
- move skills under `skills/`
- optionally add `.mcp.json`, `.app.json`, and presentation assets

Start local. Package later.

---

## 8. Codex-specific best practices

## 8.1 Spend disproportionate effort on `description`

If routing feels off, fix metadata before adding more logic.

Usually the problem is not that the skill needs more instructions; it is that Codex cannot reliably tell when to use it.

---

## 8.2 Keep each skill narrow

One skill should usually do one job.

Good:

- `code-change-verification`
- `release-review`
- `pr-draft-summary`
- `api-migration-plan`

Weak:

- `engineering-helper`
- `repo-assistant`
- `project-workflow`

---

## 8.3 Use `AGENTS.md` to enforce required skills

A very strong Codex pattern is:

- `AGENTS.md` defines required workflow use
- skills encode the workflows
- scripts encode the mechanics

That gives you both flexibility and enforceability.

---

## 8.4 Separate judgment from execution

Let Codex do:

- classification
- review
- synthesis
- risk analysis
- explanation

Let scripts do:

- exact command sequences
- repeated parsing
- deterministic log collection
- standardized report scaffolding

---

## 8.5 Be explicit about “done”

The skill should say what completion means.

Examples:

- "Do not mark the task complete until required checks pass."
- "If the release diff shows unresolved compatibility risk, return a block marked NOT READY."
- "If the PR draft is missing branch context, stop and request the missing data."

---

## 8.6 Design for evidence

Strong Codex workflows preserve evidence:

- commands run
- logs collected
- files produced
- diffs examined
- checks passed or failed

The skill should not only do work; it should make the work auditable.

---

## 9. Security and environment guidance

## 9.1 Internet access

For Codex cloud tasks, agent internet access is blocked by default during the agent phase. Setup scripts still have internet access for dependency installation.

Implication for skill authors:

- do not silently assume the web is available
- document when internet or MCP access is required
- scope domain access narrowly if internet must be enabled

## 9.2 Command policy

If the workflow may need dangerous or privileged commands:

- mention that in the skill
- enforce policy with Rules
- do not rely only on prose warnings

## 9.3 Missing dependencies

If the skill depends on:

- an MCP server
- a named tool
- a repo command
- a service login
- an environment variable

state that clearly near the top of the skill and, where helpful, in `agents/openai.yaml` dependencies.

---

## 10. Example: a high-quality Codex skill template

### Folder layout

```text
code-change-verification/
├── SKILL.md
├── scripts/
│   └── run_verification.sh
├── references/
│   └── verification-policy.md
└── agents/
    └── openai.yaml
```

### `SKILL.md`

```md
---
name: code-change-verification
description: run the repository verification workflow when changes affect runtime code, tests, examples, or build/test behavior. do not use for docs-only or comment-only edits.
---

# Code Change Verification

## Goal
Confirm that code-affecting changes satisfy the repository's required checks before work is marked complete.

## Trigger interpretation
Use this skill only when the diff affects:
- runtime code
- tests
- examples
- build or test configuration

Do not use it for:
- docs-only edits
- comment-only edits
- planning-only discussions with no code changes

## Inputs
- changed file list
- current branch state
- repository verification commands
- optional prior logs or CI failures

## Workflow
1. Inspect the changed files and confirm that the task is in scope.
2. Read `references/verification-policy.md` for the exact command order and repository-specific rules.
3. Run `scripts/run_verification.sh`.
4. Summarize:
   - commands executed
   - pass/fail outcome
   - failing steps
   - concrete next actions
5. Do not mark the task complete until required checks pass or the remaining failures are explicitly explained.

## Failure handling
- If a required command is missing, report the missing dependency and stop.
- If a command fails, include the failing command, high-signal error output, and the next recommended fix.
- If the change is out of scope, state that this skill does not apply.
```

### `references/verification-policy.md`

```md
# Verification Policy

Run commands in this order:
1. pnpm install
2. pnpm build
3. pnpm lint
4. pnpm test

If `packages/` changed, also run:
5. pnpm changeset status

Completion rule:
Do not mark the work complete until all required checks pass.
```

### `scripts/run_verification.sh`

```bash
#!/usr/bin/env bash
set -euo pipefail

pnpm install
pnpm build
pnpm lint
pnpm test
```

### `agents/openai.yaml`

```yaml
interface:
  display_name: "Code Change Verification"
  short_description: "Run required repo verification checks"

policy:
  allow_implicit_invocation: true
```

This is intentionally small. It is easier to grow a good narrow skill than to rescue a vague giant one.

---

## 11. Anti-patterns

Avoid these mistakes.

### 11.1 Vague skill names

Bad:

- `helper`
- `dev-workflow`
- `project-assistant`

### 11.2 Descriptions with no trigger boundary

Bad:

```yaml
description: helps with testing and releases.
```

Better:

```yaml
description: review release readiness before publishing a new version. use when preparing a release candidate or comparing the current branch against the previous release tag.
```

### 11.3 Putting repo-global policy inside every skill

That belongs in `AGENTS.md`, not in every skill.

### 11.4 Scripts that hide all reasoning

If the workflow becomes a black box, Codex cannot explain the result well and you lose auditability.

### 11.5 Distributing too early

Do not package a plugin before the local skill is proven in real work.

---

## 12. A practical build checklist

### Planning

- [ ] I can name 2-3 concrete use cases.
- [ ] I know the trigger boundary.
- [ ] I know what success looks like.
- [ ] I know whether this should be a Skill, `AGENTS.md`, Rules, or some combination.

### Authoring

- [ ] The skill has a focused name in kebab-case.
- [ ] The description says what it does and when it should trigger.
- [ ] The body is procedural and imperative.
- [ ] Repeated mechanics moved into scripts.
- [ ] Large details moved into references.
- [ ] Tool or MCP dependencies are documented.

### Testing

- [ ] I tested prompts that should trigger.
- [ ] I tested prompts that should not trigger.
- [ ] The workflow succeeds on real tasks.
- [ ] Failure handling is explicit and useful.
- [ ] Internet, sandbox, and command assumptions are validated.

### Operationalization

- [ ] `AGENTS.md` tells Codex when to use the skill if the repo requires it.
- [ ] Rules enforce any risky command policy.
- [ ] The skill is only packaged as a plugin after local success.

---

## 13. Recommended build order for a real team

If you are introducing Codex Skills in an engineering organization, this sequence works well:

1. Write a clean repo-level `AGENTS.md`.
2. Add one high-value workflow skill only.
3. Script the brittle steps.
4. Validate on 5-10 real tasks.
5. Tighten routing metadata.
6. Add a second skill only after the first one is stable.
7. Package the best skills as a plugin for wider rollout.

Good first skills:

- code change verification
- PR draft summary
- release readiness review
- API migration planner
- CI failure triage

---

## 14. Bottom line

The Claude guide transfers well to Codex because the underlying design pattern is the same: **small, well-routed, reusable workflows with progressive disclosure**.

But for Codex, the best version of that pattern is not “just write `SKILL.md`.”

It is:

- **Skills** for reusable workflows
- **`AGENTS.md`** for standing project instructions
- **Rules** for execution policy
- **Plugins** for distribution

That is the Codex-native way to apply the original guide.

---

## 15. Source notes

This guide was adapted from:

- the uploaded PDF: *The Complete Guide to Building Skills for Claude*
- OpenAI Codex documentation on Skills
- OpenAI Codex documentation on `AGENTS.md`
- OpenAI Codex documentation on Rules
- OpenAI Codex documentation on Plugins
- OpenAI Codex documentation on agent internet access
- OpenAI's engineering write-up on using skills to accelerate OSS maintenance

