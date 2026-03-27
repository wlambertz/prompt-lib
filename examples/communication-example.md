---
id: communication-stakeholder-update
name: Stakeholder Update Draft
category: communication
owner: product-team
status: active
version: 1.0.0
tags:
  - stakeholder
  - updates
  - alignment
use_cases:
  - Sachliche Status-Updates fuer nicht-technische Stakeholder formulieren
input_format: markdown
output_format: markdown
language: de
model_compatibility:
  - gpt-4.1
  - gpt-5
risk_notes:
  - Kann unangenehme Risiken zu weich formulieren, wenn der Prompt nicht auf Klarheit besteht.
created_at: 2026-03-27
updated_at: 2026-03-27
---

# Name

Stakeholder Update Draft

## Zweck

Formuliert knappe, klare Status-Updates fuer Stakeholder mit Fokus auf Fortschritt, Risiken und naechste Schritte.

## Use Case

Geeignet, wenn Projektinformationen in eine adressatengerechte Nachricht fuer Management, Fachbereiche oder Kunden ueberfuehrt werden sollen, ohne technische Details zu ueberfrachten.

## Prompt

```text
Erstelle ein kurzes Stakeholder-Update auf Basis der folgenden Projektinformationen.

Anforderungen:
- sachlich und klar formulieren
- keine technischen Details ohne Relevanz fuer die Zielgruppe
- Fortschritt, Risiken und naechste Schritte getrennt darstellen
- Risiken nicht beschwichtigen

Projektinformationen:
{{project_status}}

Zielgruppe:
{{audience}}
```

## Variablen

| Variable | Pflicht | Beschreibung | Beispiel |
| --- | --- | --- | --- |
| `{{project_status}}` | ja | Statusnotizen oder Projektkontext | `Feature-Implementierung fertig, Rollout blockiert durch Freigabe` |
| `{{audience}}` | ja | Zielgruppe der Nachricht | `Bereichsleitung Vertrieb` |

## Eingaben

- Statusnotizen
- Zielgruppe
- optional gewuenschter Ton oder Laenge

## Ausgabeformat

Kurzer Markdown-Text mit den Abschnitten `Stand`, `Risiken`, `Naechste Schritte`.

## Einschraenkungen

- Keine politische oder rechtliche Freigabe
- Kritische Aussagen muessen vom verantwortlichen Team geprueft werden

## Wann verwenden

- Fuer regelmaessige Projektupdates
- Fuer knappe Management-Zusammenfassungen

## Wann nicht verwenden

- Fuer sensible Eskalationen ohne menschliche Freigabe
- Wenn juristisch abgestimmte Formulierungen noetig sind

## Beispiele

**Eingabe**

```text
Feature ist implementiert und intern getestet. Externer Rollout verschiebt sich um eine Woche wegen offener Compliance-Freigabe. Zielgruppe: Steering Committee.
```

**Erwartete Ausgabe**

```text
Stand: Implementierung und interne Tests sind abgeschlossen.
Risiken: Der externe Rollout verschiebt sich um eine Woche aufgrund einer offenen Compliance-Freigabe.
Naechste Schritte: Freigabe abschliessen und danach neuen Rollout-Termin bestaetigen.
```

## Version

`1.0.0`

## Aenderungsverlauf

- `1.0.0` Initiale Version
