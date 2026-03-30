---
id: communication-persuasive-message
name: Persuasive Message
category: communication
owner: TODO-owner
status: draft
version: 1.0.0
tags:
  - persuasion
  - communication
  - stakeholder-buy-in
  - advocacy
  - proposal
use_cases:
  - Craft a persuasive message tailored to a specific audience and recommendation, including objection handling and channel variants
input_format: markdown
output_format: markdown
language: en
model_compatibility:
  - gpt-4.1
  - gpt-5
risk_notes:
  - Persuasive framing can become manipulative or misleading if the supporting reasons are weak or selective.
  - Human review is still needed for sensitive requests involving politics, compensation, legal exposure, or public messaging.
created_at: 2026-03-30
updated_at: 2026-03-30
---

# Name

Persuasive Message

## Zweck

Crafts a persuasive message that is tailored to a specific audience, grounded in their priorities, and proactive about likely objections.

## Use Case

Use this prompt for internal proposals, change advocacy, budget or resource requests, and stakeholder buy-in efforts when the goal is to move an audience toward a recommendation or action. It is especially useful when the same core argument needs both a fuller message and shorter channel-specific versions.

## Prompt

```text
You are a strategic communicator.

Help me write a persuasive message.

**Goal**
{{goal}}

**Audience**
{{audience}}

**Current situation**
{{situation}}

**Recommendation**
{{recommendation}}

**Supporting reasons**
{{reasons}}

**Likely objections**
{{objections}}

Please produce:
1. A persuasive message tailored to the audience
2. A version optimized for email
3. A shorter version suitable for chat or Slack

Constraints:
- Be respectful and credible
- Address likely objections proactively
- Focus on audience priorities, not just my own
- Do not overstate certainty or invent evidence
- Keep the message persuasive without sounding defensive or manipulative
```

## Variablen

| Variable | Pflicht | Beschreibung | Beispiel |
| --- | --- | --- | --- |
| `{{goal}}` | ja | The outcome or action the message should achieve | `Get approval for an additional backend engineer` |
| `{{audience}}` | ja | The audience to persuade | `Engineering director`, `Finance partner`, `Cross-functional leadership team` |
| `{{situation}}` | ja | The current context that creates the need for persuasion | `Delivery timelines are slipping because one engineer is covering platform work and roadmap work simultaneously` |
| `{{recommendation}}` | ja | The proposed action, decision, or position | `Approve hiring one additional backend engineer this quarter` |
| `{{reasons}}` | ja | The strongest supporting reasons for the recommendation | `Reduced delivery risk, better incident coverage, and improved roadmap predictability` |
| `{{objections}}` | nein | The audience's likely concerns or objections | `Budget pressure, hiring freeze concerns, and uncertainty about workload duration` |

## Eingaben

- The persuasion goal
- The target audience
- Current situation and recommendation
- Supporting reasons and likely objections
- Enough context to tailor the message credibly to what the audience cares about

## Ausgabeformat

Markdown with these sections in order:

1. `Persuasive message`
2. `Email version`
3. `Chat/Slack version`

Each version should stay aligned to the same core recommendation while adapting tone and length to the channel.

## Einschraenkungen

- The prompt improves persuasive communication; it does not validate the factual basis of the argument
- Weak reasons or missing audience context will weaken the message quality
- Human review is still needed when the message could create formal commitments, escalations, or reputational risk

## Wann verwenden

- When trying to build support for a recommendation or request
- When likely objections need to be addressed without becoming combative
- When the same core message needs both long-form and short-form versions

## Wann nicht verwenden

- When the goal is neutral reporting rather than persuasion
- When the message must be legally or politically reviewed line by line
- When there is not enough evidence to support a credible recommendation

## Beispiele

### Beispiel 1

**Eingabe**

```text
Goal:
Get approval for one additional backend engineer

Audience:
Engineering director

Current situation:
The team is covering roadmap work, production support, and migration tasks with too little backend capacity.

Recommendation:
Approve hiring one additional backend engineer this quarter.

Supporting reasons:
- Reduce delivery risk
- Improve incident coverage
- Stabilize roadmap predictability

Likely objections:
- Budget pressure
- Concern that the workload spike may be temporary
```

**Erwartete Ausgabe**

```text
## Persuasive message
We should add one backend engineer this quarter because current capacity is constraining both delivery reliability and incident resilience. This is not just a speed issue; it is a risk-management issue that affects roadmap predictability and operational stability.

## Email version
Subject: Request to add one backend engineer this quarter
...

## Chat/Slack version
We need one additional backend engineer this quarter to reduce delivery and support risk. Current capacity is stretched across roadmap work, migrations, and incident response, and the cost of delay is likely to exceed the cost of the hire.
```

## Version

`1.0.0`

## Aenderungsverlauf

- `1.0.0` Initial version
