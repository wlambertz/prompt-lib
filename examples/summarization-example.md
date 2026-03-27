---
id: summarization-meeting-brief
name: Meeting Brief Summarizer
category: summarization
owner: operations-team
status: active
version: 1.0.0
tags:
  - meetings
  - summary
  - action-items
use_cases:
  - Meeting-Notizen in kurze, handlungsorientierte Zusammenfassungen ueberfuehren
input_format: markdown
output_format: markdown
language: de
model_compatibility:
  - gpt-4.1
  - gpt-5
risk_notes:
  - Kann implizite Entscheidungen ueberbetonen, wenn Notizen mehrdeutig sind.
created_at: 2026-03-27
updated_at: 2026-03-27
---

# Name

Meeting Brief Summarizer

## Zweck

Verdichtet Meeting-Notizen in eine kurze Zusammenfassung mit Entscheidungen, offenen Punkten und naechsten Schritten.

## Use Case

Geeignet fuer Team- oder Projektmeetings, in denen aus laengeren Rohnotizen eine verteilbare Kurzfassung entstehen soll. Fokus ist nicht Vollstaendigkeit, sondern eine belastbare Handlungsuebersicht.

## Prompt

```text
Fasse die folgenden Meeting-Notizen in einer knappen, klaren Arbeitszusammenfassung zusammen.

Anforderungen:
- trenne zwischen Entscheidungen, offenen Fragen und naechsten Schritten
- uebernimm keine Informationen, die nicht im Input vorkommen
- markiere Unsicherheiten explizit
- formuliere praezise und ohne Floskeln

Input:
{{meeting_notes}}
```

## Variablen

| Variable | Pflicht | Beschreibung | Beispiel |
| --- | --- | --- | --- |
| `{{meeting_notes}}` | ja | Rohnotizen oder Transkript-Auszug | `Diskussion ueber Rollout-Termin und offene Blocker` |

## Eingaben

- Meeting-Notizen, Stichpunkte oder Transkript

## Ausgabeformat

Markdown mit den Abschnitten `Entscheidungen`, `Offene Fragen`, `Naechste Schritte`.

## Einschraenkungen

- Keine Rekonstruktion fehlender Inhalte
- Bei unklaren Verantwortlichkeiten muessen Menschen nachschaerfen

## Wann verwenden

- Nach internen Abstimmungen
- Fuer verteilbare Kurzfassungen

## Wann nicht verwenden

- Wenn ein vollstaendiges Protokoll erforderlich ist
- Wenn juristisch oder regulatorisch exakte Formulierungen noetig sind

## Beispiele

**Eingabe**

```text
Rollout nicht vorziehen. QA braucht noch drei Tage. Sarah klaert das Monitoring. Unklar bleibt, ob Kunde A im ersten Batch ist.
```

**Erwartete Ausgabe**

```text
Entscheidungen: Rollout wird nicht vorgezogen.
Offene Fragen: Gehoert Kunde A zum ersten Batch?
Naechste Schritte: QA finalisiert in drei Tagen; Sarah klaert Monitoring.
```

## Version

`1.0.0`

## Aenderungsverlauf

- `1.0.0` Initiale Version
