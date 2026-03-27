# Review Process

Der Review-Prozess soll leichtgewichtig bleiben, aber eine verlaessliche Mindestqualitaet sicherstellen.

## Ziel des Reviews

Jeder Prompt soll vor der Aktivierung geprueft werden auf:

- Klarheit des Zwecks
- Wiederverwendbarkeit
- Abgrenzung zu bestehenden Prompts
- Vollstaendigkeit der Dokumentation
- realistische Grenzen und Risiken

## Review-Stufen

### 1. Autorenselbstcheck

Vor dem Pull Request prueft die Autorin oder der Autor:

- Ist der Anwendungsfall wiederkehrend und nicht einmalig?
- Ist die Kategorie korrekt?
- Sind alle Pflichtsektionen ausgefuellt?
- Sind Metadaten vollstaendig und plausibel?
- Gibt es mindestens ein realistisches Beispiel?

### 2. Fachlicher Review

Eine zweite Person oder das verantwortliche Team prueft:

- ob der Prompt den beschriebenen Zweck tatsaechlich adressiert
- ob Variablen und Eingaben klar genug beschrieben sind
- ob Grenzen und Fehlanwendungen realistisch benannt sind
- ob der Prompt eine echte Luecke schliesst und keine Dublette ist

### 3. Statusentscheidung

Empfohlene Statuswerte:

- `draft`: in Arbeit, noch nicht reviewt
- `review`: bereit zur Begutachtung
- `active`: freigegeben fuer regulare Nutzung
- `deprecated`: noch vorhanden, aber nicht mehr empfohlen
- `archived`: nur noch aus Dokumentationsgruenden vorhanden

## Pull-Request-Checkliste

Ein PR sollte folgende Fragen mit Ja beantworten:

- Ist der Prompt fuer andere Personen im Team verstaendlich?
- Ist die Ausgabeerwartung konkret genug?
- Ist klar beschrieben, wann der Prompt nicht genutzt werden soll?
- Ist die Version korrekt gepflegt?
- Ist die Aenderung im Verlauf dokumentiert?

## Pflege nach dem Merge

Auch aktive Prompts sollen regelmaessig ueberprueft werden:

- bei wiederholten Fehlanwendungen
- bei groesseren Modellwechseln
- wenn sich Eingabeformate im Umfeld aendern
- wenn neue, bessere Varianten entstehen

## Empfohlener leichter Rhythmus

- bei neuen Prompts: Review vor Aktivierung
- bei aktiven Prompts: quartalsweise Sichtung oder anlassbezogen
- bei selten genutzten Prompts: ggf. deprecaten statt weiter pflegen
