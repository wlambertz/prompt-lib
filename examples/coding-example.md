---
id: coding-refactor-plan
name: Refactoring Plan Generator
category: coding
owner: platform-team
status: active
version: 1.1.0
tags:
  - refactoring
  - planning
  - legacy-code
use_cases:
  - Refactoring-Schritte fuer bestehende Module strukturieren
input_format: markdown
output_format: markdown
language: de
model_compatibility:
  - gpt-4.1
  - gpt-5
risk_notes:
  - Kann technische Randbedingungen uebersehen, wenn Abhaengigkeiten nicht beschrieben sind.
created_at: 2026-03-27
updated_at: 2026-03-27
---

# Name

Refactoring Plan Generator

## Zweck

Erzeugt einen priorisierten Refactoring-Plan fuer bestehende Codebereiche mit Fokus auf Risiken, Reihenfolge und pragmatische Umsetzung.

## Use Case

Geeignet, wenn ein Team einen unuebersichtlichen Codebereich in konkrete Verbesserungssequenzen zerlegen will. Der Prompt hilft dabei, nicht direkt in Implementierung zu springen, sondern erst Arbeitspakete und Risiken sauber zu strukturieren.

## Prompt

```text
Du bist ein erfahrener Softwarearchitekt.

Analysiere den folgenden Code- oder Modulkontext und erstelle einen pragmatischen Refactoring-Plan.

Ziele:
- identifiziere die groessten strukturellen Probleme
- schlage eine sinnvolle Reihenfolge fuer Aenderungen vor
- benenne Risiken, Abhaengigkeiten und geeignete Tests
- bevorzuge kleine, reversible Schritte

Kontext:
{{module_context}}

Liefere die Antwort in folgenden Abschnitten:
1. Kurzdiagnose
2. Refactoring-Schritte
3. Risiken und Abhaengigkeiten
4. Empfohlene Tests
5. Was bewusst nicht im ersten Schritt angegangen werden sollte
```

## Variablen

| Variable | Pflicht | Beschreibung | Beispiel |
| --- | --- | --- | --- |
| `{{module_context}}` | ja | Beschreibung oder Ausschnitt des betroffenen Moduls | `Service mit zu vielen Verantwortlichkeiten und gemischter Datenzugriffsschicht` |

## Eingaben

- Modulbeschreibung, Codeauszug oder Architekturkontext
- bekannte Probleme oder Ziele
- optional vorhandene Testabdeckung

## Ausgabeformat

Markdown mit 5 festen Abschnitten.

## Einschraenkungen

- Keine automatische Bewertung der realen Codebasis ohne ausreichenden Kontext
- Architekturentscheidungen muessen durch das Team validiert werden

## Wann verwenden

- Vor groesseren Refactorings
- Bei Legacy-Code mit unklarer Priorisierung

## Wann nicht verwenden

- Fuer triviale Ein-Datei-Korrekturen
- Wenn bereits ein abgestimmter Refactoring-Plan existiert

## Beispiele

**Eingabe**

```text
Ein Backend-Service enthaelt Validierung, Business-Logik, Mapping und Repository-Zugriffe in einer Klasse mit 1200 Zeilen.
```

**Erwartete Ausgabe**

```text
1. Kurzdiagnose: Hohe Kopplung, fehlende Trennung von Verantwortlichkeiten
2. Refactoring-Schritte: Extraktion Validierung, Service-Schnittstellen, Repository-Grenzen
3. Risiken: implizite Seiteneffekte, fehlende Tests
4. Tests: Charakterisierungstests vor Strukturumbau
5. Nicht zuerst tun: kompletten Rewrite starten
```

## Version

`1.1.0`

## Aenderungsverlauf

- `1.1.0` Guardrail fuer kleine reversible Schritte ergaenzt
- `1.0.0` Initiale Version
