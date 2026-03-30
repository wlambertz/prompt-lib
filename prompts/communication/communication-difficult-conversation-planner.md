---
id: communication-difficult-conversation-planner
name: Difficult Conversation Planner
category: communication
owner: TODO-owner
status: draft
version: 1.0.0
tags:
  - communication
  - feedback
  - conflict
  - conversation-planning
  - management
use_cases:
  - Prepare for sensitive or high-stakes conversations with tact, clarity, and constructive framing
input_format: markdown
output_format: markdown
language: en
model_compatibility:
  - gpt-4.1
  - gpt-5
risk_notes:
  - Poorly framed inputs can lead to advice that underestimates emotional, cultural, or organizational context.
  - Human judgment is still required for sensitive personnel, legal, or safety-related matters.
created_at: 2026-03-30
updated_at: 2026-03-30
---

# Name

Difficult Conversation Planner

## Zweck

Helps prepare for sensitive or high-stakes conversations and turn raw observations into constructive, actionable feedback by improving framing, reducing defensiveness, and keeping the message clear and constructive.

## Use Case

Use this prompt when preparing to give difficult feedback, address misalignment, reset expectations, or escalate issues diplomatically. It is especially useful when the goal is not only to say something hard, but to do it in a way that improves the chance of a productive outcome, including feedback situations where raw observations need to be turned into constructive language.

## Prompt

```text
You are an experienced manager and communication coach.

Help me prepare for a difficult conversation.

**Situation**
{{situation}}

**Person/role**
{{person}}

**What I need to communicate**
{{message}}

**What I want to achieve**
{{desired_outcome}}

**Potential sensitivities**
{{sensitivities}}

Please provide:
1. A recommended framing for the conversation
2. Suggested opening lines
3. Key points to communicate
4. Phrases to avoid
5. Likely reactions and how to respond
6. A calm, professional version of the message
7. A more direct version
8. A softer version
9. Suggested follow-up questions
10. A version that emphasizes collaboration and next steps

Constraints:
- Be direct but respectful
- Reduce defensiveness
- Optimize for clarity and constructive resolution
- Do not encourage manipulation, humiliation, or escalation for its own sake
- If the situation suggests HR, legal, or safety involvement, note that clearly
- Focus on observable behavior and impact rather than personal criticism
```

## Variablen

| Variable | Pflicht | Beschreibung | Beispiel |
| --- | --- | --- | --- |
| `{{situation}}` | ja | The situation or context behind the conversation | `Repeated missed deadlines are creating tension across the team` |
| `{{person}}` | ja | The person or role involved | `Senior engineer`, `Direct report`, `Peer manager`, `Cross-functional stakeholder` |
| `{{message}}` | ja | What needs to be communicated, including raw observations when relevant | `I need to address the impact of the missed deadlines and reset expectations` |
| `{{desired_outcome}}` | ja | What a constructive outcome would look like | `Agree on clearer commitments and a recovery plan` |
| `{{sensitivities}}` | nein | Emotional, political, personal, or contextual sensitivities to account for | `They feel under pressure already and may hear this as a personal criticism` |

## Eingaben

- Situation and person or role involved
- The message that needs to be delivered
- The desired outcome
- Optional sensitivities or context that may affect tone and response

## Ausgabeformat

Markdown with these sections in order:

1. `Recommended framing`
2. `Suggested opening lines`
3. `Key points to communicate`
4. `Phrases to avoid`
5. `Likely reactions and how to respond`
6. `Calm, professional version of the message`
7. `More direct version`
8. `Softer version`
9. `Suggested follow-up questions`
10. `Collaboration and next steps version`

Keep the guidance practical, respectful, and focused on constructive resolution.

## Einschraenkungen

- The prompt supports preparation; it does not replace real-world judgment during the conversation
- It cannot fully model interpersonal history, power dynamics, or legal sensitivity from limited input
- Human review is still needed for HR-sensitive, legal, or safety-related situations

## Wann verwenden

- When a difficult conversation needs preparation before speaking live or writing a message
- When reducing defensiveness matters as much as being clear
- When the goal is constructive resolution rather than venting or blame

## Wann nicht verwenden

- When the issue requires immediate HR, legal, or security escalation instead of coaching
- When you need a persuasive advocacy message rather than a difficult interpersonal conversation plan
- When the input is too vague to understand what must actually be communicated

## Beispiele

### Beispiel 1

**Eingabe**

```text
Situation:
A direct report has missed multiple agreed deadlines, and other team members are now carrying extra work.

Person/role:
Direct report

What I need to communicate:
I need to address the pattern clearly and explain its impact on the team.

What I want to achieve:
Agree on clearer commitments, surface any blockers, and reset expectations.

Potential sensitivities:
They have seemed stressed recently and may interpret the conversation as a sign they are failing.
```

**Erwartete Ausgabe**

```text
## Recommended framing
Frame the conversation around impact, expectations, and support rather than personal judgment.

## Suggested opening lines
- I want to talk about the pattern we have seen around recent deadlines and how it is affecting the team.
- My goal here is to be clear about the impact and also understand what is getting in the way.

## Key points to communicate
- The missed deadlines have created downstream pressure for others.
- The issue is the recurring pattern, not a single isolated miss.
- We need a more reliable way to set and meet commitments.

## Phrases to avoid
- You are unreliable.
- Everyone is frustrated with you.

## Likely reactions and how to respond
- If they become defensive, acknowledge the pressure they may be feeling and return to specific examples and desired next steps.

## Calm, professional version of the message
I want to address the recent pattern of missed deadlines because it is starting to affect team coordination and workload balance. My goal is to understand what is contributing to it and agree on a more reliable plan going forward.
```

## Version

`1.0.0`

## Aenderungsverlauf

- `1.0.0` Initial version
