# Name

Kurzer, sprechender Name des Prompts.

## Zweck

Welches Problem loest der Prompt und welches Ergebnis soll er regelmaessig erzeugen?

## Use Case

Beschreibe den typischen Einsatzkontext in 2 bis 4 Saetzen.

## Prompt

```text
Rolle und Kontext:
{{role_context}}

Aufgabe:
{{task_description}}

Eingaben:
{{input_data}}

Anforderungen:
- {{requirement_1}}
- {{requirement_2}}
- {{requirement_3}}

Ausgabeformat:
{{output_expectation}}
```

## Variablen

| Variable | Pflicht | Beschreibung | Beispiel |
| --- | --- | --- | --- |
| `{{role_context}}` | ja | Fachliche Rolle oder Perspektive des Modells | `Du bist ein Senior Technical Writer.` |
| `{{task_description}}` | ja | Konkrete Aufgabe | `Erstelle eine API-Dokumentationszusammenfassung.` |
| `{{input_data}}` | ja | Eingabematerial, das verarbeitet werden soll | `Markdown-Notizen aus dem Review` |
| `{{requirement_1}}` | nein | Wichtige Zusatzanforderung | `Nutze nur Informationen aus dem Input.` |
| `{{output_expectation}}` | ja | Erwartete Struktur der Antwort | `Liefere eine Gliederung mit 5 Punkten.` |

## Eingaben

- Welche Eingaben werden erwartet?
- In welchem Format sollen sie vorliegen?
- Welche Mindestqualitaet ist noetig?

## Ausgabeformat

Beschreibe die gewuenschte Ausgabe moeglichst konkret, zum Beispiel:

- Markdown
- JSON
- Stichpunkte
- Tabelle
- strukturierte Zusammenfassung mit festen Abschnitten

## Einschraenkungen

- Welche Grenzen hat der Prompt?
- Welche Fehlerbilder treten bei schlechtem Input auf?
- Wo ist menschliche Pruefung zwingend noetig?

## Wann verwenden

- Wenn der Anwendungsfall wiederkehrend ist
- Wenn Eingaben in einem stabilen Format vorliegen
- Wenn das gewuenschte Ergebnis klar beschrieben werden kann

## Wann nicht verwenden

- Wenn der Input zu unvollstaendig oder widerspruechlich ist
- Wenn der Anwendungsfall fachlich ausserhalb des Prompt-Zwecks liegt
- Wenn eine frei explorative Antwort sinnvoller ist als ein Template

## Beispiele

### Beispiel 1

**Eingabe**

```text
{{example_input}}
```

**Erwartete Ausgabe**

```text
{{example_output}}
```
