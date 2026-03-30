# Contributing

Dieses Repository ist eine kuratierte Bibliothek. Neue Inhalte werden nur aufgenommen, wenn sie wiederverwendbar, gut dokumentiert und klar von bestehenden Prompts abgrenzbar sind.

## Benennung neuer Prompts

Prompt-Dateien folgen dem Muster:

```text
<category>-<short-purpose>.md
```

Beispiele:

- `coding-refactor-plan.md`
- `summarization-meeting-notes.md`
- `communication-stakeholder-update.md`

Regeln:

- nur Kleinbuchstaben
- nur Bindestriche als Trenner
- keine Leerzeichen
- kurze, sprechende Namen
- Kategorien muessen zur Taxonomie in `docs/taxonomy.md` passen
- der Dateiname bleibt fuer denselben Prompt stabil

## Pflichtbestandteile jeder Prompt-Datei

Jede neue Prompt-Datei muss auf dem Template in `templates/prompt-template.md` basieren und diese Sektionen enthalten:

- Name
- Zweck
- Use Case
- Prompt
- Variablen
- Eingaben
- Ausgabeformat
- Einschraenkungen
- Wann verwenden
- Wann nicht verwenden
- Beispiele
- Version
- Aenderungsverlauf

Leere Platzhalter duerfen in Pull Requests nicht verbleiben.

## Erforderliche Metadaten

Jeder Prompt braucht die folgenden Metadaten:

- `id`
- `name`
- `category`
- `owner`
- `status`
- `version`
- `tags`
- `use_cases`
- `input_format`
- `output_format`
- `language`
- `model_compatibility`
- `risk_notes`
- `created_at`
- `updated_at`

Die Struktur ist in `templates/metadata-template.yaml` vorgegeben. Die erwarteten Typen und zulaessigen Werte stehen in `schemas/prompt-metadata.schema.yaml`.

## Neuer Prompt oder bestehender Prompt erweitern

Lege einen neuen Prompt nur an, wenn mindestens einer der folgenden Punkte zutrifft:

- der Anwendungsfall ist fachlich eigenstaendig
- das Ausgabeformat unterscheidet sich wesentlich
- die Eingaben oder Variablen sind grundlegend anders
- ein bestehender Prompt wuerde durch Erweiterung unnoetig breit oder unklar

Erweitere einen bestehenden Prompt, wenn:

- nur Beispiele, Formulierungen oder Guardrails verbessert werden
- der gleiche Kern-Use-Case genauer dokumentiert wird
- nur kleine Varianten fuer Modellverhalten oder Ausgabeformat noetig sind

Wenn unklar ist, ob ein neuer Prompt sinnvoll ist, gilt: erst zusammenfuehren, dann abspalten.

## Versionierung

Verwende semantisch lesbare Versionen im Inhalt und in den Metadaten:

- `major`: fuer grundlegende Verhaltensaenderungen, neue Struktur oder inkompatible Anpassungen
- `minor`: fuer erweiterte Beispiele, neue Hinweise oder verbesserte Formulierungen ohne geaenderten Kernzweck
- `patch`: fuer reine Korrekturen, Tippfehler oder redaktionelle Verbesserungen

Konvention:

- der Dateiname enthaelt keine Versionsangabe
- die inhaltliche Version in Datei und Metadaten kann `1.2.1` sein
- jede relevante Aenderung wird im Aenderungsverlauf dokumentiert
- nur in seltenen Ausnahmefaellen duerfen parallele, inkompatible Varianten als separate Dateien gefuehrt werden

## Pull-Request-Qualitaetskriterien

Ein Pull Request wird nur gemergt, wenn:

- der Prompt einen klaren, wiederkehrenden Nutzen adressiert
- keine offensichtliche Dublette vorhanden ist
- Metadaten vollstaendig und konsistent sind
- Variablen und Eingaben eindeutig dokumentiert sind
- Grenzen, Risiken und ungeeignete Einsatzsituationen benannt sind
- mindestens ein gutes Beispiel enthalten ist
- Dateiname, Kategorie und Versionierung den Konventionen entsprechen

## Pflege bestehender Prompts

Bestehende Prompts sollen regelmaessig ueberprueft werden auf:

- veraltete Modellannahmen
- zu breite oder unscharfe Formulierungen
- fehlende Beispiele
- wiederkehrende Fehlanwendungen
- ueberschneidungen mit neueren Prompts
