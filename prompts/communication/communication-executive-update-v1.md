---
id: communication-executive-update
name: Executive Update
category: communication
owner: TODO-owner
status: draft
version: 1.0.0
tags:
  - executive-communication
  - stakeholder-update
  - status-reporting
  - leadership
  - project-update
use_cases:
  - Turn raw project status, progress, and issues into a concise executive-facing update
input_format: markdown
output_format: markdown
language: en
model_compatibility:
  - gpt-4.1
  - gpt-5
risk_notes:
  - The update can become misleading if achievements, risks, or needed decisions are incomplete or biased.
  - Human review is still needed before sending updates tied to sensitive commitments, escalations, or governance decisions.
created_at: 2026-03-30
updated_at: 2026-03-30
---

# Name

Executive Update

## Zweck

Turns raw status notes into a concise executive-facing update that emphasizes implications, support needed, and next steps rather than operational detail.

## Use Case

Use this prompt for weekly leadership updates, project status summaries, steering committee communication, or stakeholder reporting when senior readers need a brief, high-signal update. It is especially useful when project teams have raw notes but need a confident, neutral executive summary.

## Prompt

```text
You are an expert in executive communication.

I need to communicate a project or initiative update to senior stakeholders.

**Context**
- Project/initiative: {{project}}
- Audience: {{audience}}
- Reporting period: {{period}}
- Achievements: {{achievements}}
- Current status: {{status}}
- Risks/issues: {{risks}}
- Decisions needed: {{decisions_needed}}
- Next steps: {{next_steps}}

Please produce:
1. A concise executive summary
2. Current status in plain language
3. Key achievements
4. Risks or blockers
5. Decisions or support needed
6. Next steps

Constraints:
- Keep it brief and high signal
- Focus on implications, not operational detail
- Use confident, neutral language
- Do not soften real risks or blockers
- If no decisions are needed, say that clearly instead of inventing asks
```

## Variablen

| Variable | Pflicht | Beschreibung | Beispiel |
| --- | --- | --- | --- |
| `{{project}}` | ja | The project, initiative, or program being reported on | `Billing migration program` |
| `{{audience}}` | ja | The senior stakeholder audience | `Executive leadership team` |
| `{{period}}` | nein | The reporting period covered by the update | `Week of March 24 to March 28` |
| `{{achievements}}` | ja | The main accomplishments during the reporting period | `Completed internal testing, finalized migration checklist, and launched pilot onboarding` |
| `{{status}}` | ja | The current overall state in plain terms | `On track overall, but external rollout depends on compliance approval` |
| `{{risks}}` | nein | Risks, blockers, or unresolved issues | `Compliance sign-off remains open and could delay rollout by one week` |
| `{{decisions_needed}}` | nein | Escalations, approvals, or support required from leadership | `Confirm whether pilot customers can be onboarded before full compliance completion` |
| `{{next_steps}}` | nein | Immediate next actions for the team | `Close compliance review, finalize rollout date, and prepare customer communications` |

## Eingaben

- Project or initiative name
- Audience and reporting period
- Achievements, current status, and current risks
- Optional decisions needed and next steps
- Enough context to express implications clearly without inventing detail

## Ausgabeformat

Markdown with these sections in order:

1. `Executive summary`
2. `Current status`
3. `Key achievements`
4. `Risks or blockers`
5. `Decisions or support needed`
6. `Next steps`

Keep the tone concise, neutral, and executive-appropriate.

## Einschraenkungen

- The prompt improves communication quality; it does not validate the underlying project facts
- Weak or incomplete raw inputs can produce overconfident updates
- Human review is still needed before sharing externally or with senior governance groups

## Wann verwenden

- When leadership needs a concise project or initiative update
- When raw status notes need to be translated into executive language
- When implications and support needed matter more than detailed operational narrative

## Wann nicht verwenden

- When a detailed project report is required instead of an executive update
- When the message is a sensitive escalation requiring tightly reviewed wording
- When there is too little concrete information to support a credible status update

## Beispiele

### Beispiel 1

**Eingabe**

```text
Project/initiative: Billing migration program
Audience: Steering committee
Reporting period: This week
Achievements: Completed internal testing, finalized migration checklist, and prepared customer support guidance
Current status: On track overall, but rollout timing still depends on compliance approval
Risks/issues: Compliance sign-off remains open and may delay production rollout by one week
Decisions needed: None at this time
Next steps: Close compliance review, confirm rollout date, and prepare customer communications
```

**Erwartete Ausgabe**

```text
## Executive summary
The billing migration remains broadly on track, with rollout timing dependent on final compliance approval.

## Current status
Core preparation work is complete, but production launch is still gated by compliance sign-off.

## Key achievements
- Internal testing completed
- Migration checklist finalized
- Customer support guidance prepared

## Risks or blockers
- Compliance approval remains open and could delay rollout by one week

## Decisions or support needed
- None at this time

## Next steps
- Close compliance review
- Confirm rollout date
- Prepare customer communications
```

## Version

`1.0.0`

## Aenderungsverlauf

- `1.0.0` Initial version
