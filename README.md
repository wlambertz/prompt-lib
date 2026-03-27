# Prompt Library

Eine kuratierte, versionierbare Prompt-Bibliothek fuer wiederkehrende, hochwertige Anwendungsfaelle. Dieses Repository ist fuer Teams gedacht, die Prompts nicht als lose Sammlung, sondern als wartbare Artefakte mit Kontext, Metadaten, Grenzen und Review-Prozess behandeln wollen.

## Ziel und Zweck

Die Bibliothek dient dazu, wiederverwendbare Prompts systematisch zu sammeln, zu verbessern und ueber laengere Zeit stabil nutzbar zu halten. Jeder Prompt wird als dokumentiertes Arbeitsartefakt verstanden, nicht nur als einzelner Textblock.

Ziele:

- wiederkehrende Aufgaben mit hochwertigen Prompt-Templates abdecken
- Prompts nach Anwendungsfall und Kategorie strukturieren
- Einsatzgrenzen, Risiken und Hinweise nachvollziehbar dokumentieren
- Aenderungen sauber versionieren
- Reviews und Weiterentwicklung im Team erleichtern

## Grundprinzipien

- Kuratiert statt gesammelt: Nur Prompts mit klarem Zweck, dokumentiertem Nutzen und realistischem Einsatzkontext werden aufgenommen.
- Templates statt Einmaltexte: Prompts sollen mit Variablen, Eingaben und Ausgabeerwartungen beschrieben werden.
- Kontext vor Copy-Paste: Zu jedem Prompt gehoeren Hinweise zu Grenzen, Risiken und geeigneten Einsatzsituationen.
- Evolvierbar statt statisch: Prompts werden ueber Versionen gepflegt und verbessert.
- Teamtauglich statt individuell: Benennung, Metadaten und Review-Kriterien sind standardisiert.

## Verzeichnisstruktur

```text
prompt-library/
|-- README.md
|-- CONTRIBUTING.md
|-- LICENSE
|-- .gitignore
|-- prompts/
|   |-- analysis/
|   |-- coding/
|   |-- communication/
|   |-- documentation/
|   |-- ideation/
|   `-- summarization/
|-- templates/
|   |-- prompt-template.md
|   `-- metadata-template.yaml
|-- schemas/
|   `-- prompt-metadata.schema.yaml
|-- docs/
|   |-- taxonomy.md
|   |-- naming-conventions.md
|   `-- review-process.md
`-- examples/
    |-- coding-example.md
    |-- summarization-example.md
    `-- communication-example.md
```

## Wie neue Prompts hinzugefuegt werden

1. Passende Kategorie in `prompts/` bestimmen.
2. Dateiname gemaess [docs/naming-conventions.md](docs/naming-conventions.md) waehlen.
3. Inhalt auf Basis von [templates/prompt-template.md](templates/prompt-template.md) anlegen.
4. Metadaten auf Basis von [templates/metadata-template.yaml](templates/metadata-template.yaml) ergaenzen.
5. Einsatzgrenzen, Variablen, Beispielnutzung und Versionshistorie dokumentieren.
6. Pull Request gegen die Qualitaetskriterien in [CONTRIBUTING.md](CONTRIBUTING.md) und [docs/review-process.md](docs/review-process.md) stellen.

## Metadatenformat

Jeder Prompt soll von strukturierten Metadaten begleitet werden. Die Metadaten koennen:

- als YAML-Block am Anfang einer Prompt-Datei gepflegt werden
- oder in einer separaten YAML-Datei nach derselben Struktur abgelegt werden

Beispiel:

```yaml
id: coding-refactor-plan
name: Refactoring Plan Generator
category: coding
owner: platform-team
status: active
version: 1.0.0
tags:
  - refactoring
  - planning
  - architecture
use_cases:
  - Bestehende Module in Refactoring-Schritte zerlegen
input_format: markdown
output_format: markdown
language: de
model_compatibility:
  - gpt-4.1
  - gpt-5
risk_notes:
  - Kann Abhaengigkeiten unterschaetzen, wenn der Input unvollstaendig ist.
created_at: 2026-03-27
updated_at: 2026-03-27
```

Die erwarteten Felder sind in [schemas/prompt-metadata.schema.yaml](schemas/prompt-metadata.schema.yaml) beschrieben.

## Review- und Pflegeprozess

Neue oder geaenderte Prompts werden leichtgewichtig, aber verbindlich geprueft:

- Ist der Zweck klar und von bestehenden Prompts abgrenzbar?
- Sind Eingaben, Variablen und Ausgabeerwartungen eindeutig beschrieben?
- Sind Grenzen, Risiken und ungeeignete Einsatzfaelle dokumentiert?
- Ist die Benennung konsistent und die Versionshistorie nachvollziehbar?

Der vollstaendige Ablauf steht in [docs/review-process.md](docs/review-process.md).

## Beispiel fuer gute Prompt-Dokumentation

Eine gute Prompt-Dokumentation enthaelt nicht nur den Prompt-Text selbst, sondern mindestens:

- klares Ziel und typischen Use Case
- erklaerte Variablen und erwartete Eingaben
- gewuenschtes Ausgabeformat
- Grenzen und Ausschlussfaelle
- mindestens ein konkretes Beispiel
- nachvollziehbare Versionsangabe mit Aenderungshinweisen

Beispieldateien:

- [examples/coding-example.md](examples/coding-example.md)
- [examples/summarization-example.md](examples/summarization-example.md)
- [examples/communication-example.md](examples/communication-example.md)

## Startempfehlung fuer Teams

- Zunaechst nur wenige, aber hochwertige Prompts aufnehmen.
- Dubletten vermeiden und bestehende Prompts eher erweitern als kopieren.
- Metadaten konsequent pflegen.
- Versionserhoehungen nur bei inhaltlich relevanten Aenderungen vornehmen.
- Regelmaessig ungenutzte oder veraltete Prompts ueberpruefen.
