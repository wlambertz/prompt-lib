# Naming Conventions

Prompt-Dateien werden nach einem einheitlichen Muster benannt:

```text
<category>-<short-purpose>-v<major>.md
```

Beispiel:

```text
documentation-api-changelog-v1.md
```

## Regeln

- Nur Kleinbuchstaben verwenden.
- Woerter mit Bindestrichen trennen.
- Keine Leerzeichen, Unterstriche oder Sonderzeichen verwenden.
- Der Name soll kurz, aber sprechend sein.
- Die Dateiendung ist immer `.md`.
- Die Kategorie muss einer gueltigen Hauptkategorie entsprechen.
- Die Major-Version wird im Dateinamen als `v1`, `v2`, `v3` usw. gefuehrt.

## Benennungslogik

Der Dateiname sollte in dieser Reihenfolge lesbar sein:

1. Kategorie
2. kurzer Zweck
3. Major-Version

Beispiele:

- `analysis-risk-review-v1.md`
- `coding-test-plan-v2.md`
- `communication-release-update-v1.md`

## Was ein guter Name leistet

Ein guter Name:

- beschreibt den primaeren Nutzen
- ist auch ohne Oeffnen der Datei verstaendlich
- grenzt sich von aehnlichen Prompts ab
- bleibt auch bei spaeteren Varianten stabil

## Was vermieden werden soll

Vermeide:

- generische Namen wie `prompt1.md`
- zu lange Dateinamen mit mehreren Nebenzwecken
- teaminterne Abkuerzungen ohne allgemein verstandene Bedeutung
- Mischkategorien im Dateinamen

## Versionierungsregel

- Kleinere inhaltliche Aenderungen aendern nicht den Dateinamen.
- Wenn sich der Prompt grundlegend aendert, wird eine neue Major-Datei angelegt.
- Die volle semantische Version wird im Dokumentinhalt und in den Metadaten gepflegt.
