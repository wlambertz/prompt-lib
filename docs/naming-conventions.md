# Naming Conventions

Prompt-Dateien werden nach einem einheitlichen Muster benannt:

```text
<category>-<short-purpose>.md
```

Beispiel:

```text
documentation-api-changelog.md
```

## Regeln

- Nur Kleinbuchstaben verwenden.
- Woerter mit Bindestrichen trennen.
- Keine Leerzeichen, Unterstriche oder Sonderzeichen verwenden.
- Der Name soll kurz, aber sprechend sein.
- Die Dateiendung ist immer `.md`.
- Die Kategorie muss einer gueltigen Hauptkategorie entsprechen.
- Versionsangaben gehoeren nicht in den Dateinamen.

## Benennungslogik

Der Dateiname sollte in dieser Reihenfolge lesbar sein:

1. Kategorie
2. kurzer Zweck

Beispiele:

- `analysis-risk-review.md`
- `coding-test-plan.md`
- `communication-release-update.md`

## Was ein guter Name leistet

Ein guter Name:

- beschreibt den primaeren Nutzen
- ist auch ohne Oeffnen der Datei verstaendlich
- grenzt sich von aehnlichen Prompts ab
- bleibt auch bei spaeteren Versionen stabil

## Was vermieden werden soll

Vermeide:

- generische Namen wie `prompt1.md`
- zu lange Dateinamen mit mehreren Nebenzwecken
- teaminterne Abkuerzungen ohne allgemein verstandene Bedeutung
- Mischkategorien im Dateinamen

## Versionierungsregel

- Inhaltliche Aenderungen aendern den Dateinamen nicht.
- Grundlegende Aenderungen werden ueber die semantische Version und den Aenderungsverlauf nachverfolgt.
- Die volle semantische Version wird im Dokumentinhalt und in den Metadaten gepflegt.
- Parallele, inkompatible Varianten sollen nur als explizite Ausnahme und nicht als Standardkonvention angelegt werden.
