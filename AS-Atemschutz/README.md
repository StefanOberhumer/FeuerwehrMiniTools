# AS-Sammelstelle & AS-Überwachung

Zwei schlanke Web-Werkzeuge für den **Atemschutz-Einsatz der Feuerwehr**:

| Datei(ausprobieren) | Zweck | Stand |
|---|---|---|
| [`AS-Sammelstelle.html`](https://StefanOberhumer.github.io/FeuerwehrMiniTools/AS-Atemschutz/AS-Sammelstelle.html) | Atemschutz-Sammelstelle: Personen zu Trupps zusammenstellen, Abmarsch und Rückmeldung erfassen, Warteschlange anzeigen | V 1.04 |
| [`AS-Ueberwachung.html`](https://StefanOberhumer.github.io/FeuerwehrMiniTools/AS-Atemschutz/AS-Ueberwachung.html) | Atemschutz-Überwachung: Luftvorrat je Person, Druckkontrollen, Alarm bei ½ Einsatzzeit und Reserve | V 1.04 |

Jede App ist **eine einzige HTML-Datei** und braucht weder Installation noch Server oder Internet. Datei herunterladen, im Browser öffnen, fertig.

---

## Gemeinsame Eigenschaften

- **Eine Datei, keine Abhängigkeiten:** HTML, CSS und JavaScript stecken in der Datei. Sie läuft offline in jedem aktuellen Browser (Chrome, Edge, Firefox, Safari).
- **Für Tablets gebaut:** große Schaltflächen und keine Funktionen, die nur mit der Maus erreichbar sind. Dunkelmodus folgt der Systemeinstellung.
- **Kein Internet nötig:** kein Upload, kein irgendwas... Tut was es tun soll.
- **Daten bleiben lokal:** Gespeichert wird nur im `localStorage` des Browsers, nichts verlässt das Gerät.
- **Selbstlernende Vorschläge:** Feuerwehr, Namen, Abschnitt/Auftrag und Funk werden während der Eingabe aus dem aktuellen Einsatz vorgeschlagen, auch am Touch-Gerät.
- **Zwei Ansichten:** *Übersicht* (große Kacheln, z. B. für einen zweiten Bildschirm) und *Tabelle* (alle Details, druckbar). Mehrere Browser-Tabs bleiben synchron.
- **Export/Import:** Einsätze lassen sich als JSON-Datei sichern und auf einem anderen Gerät wieder einlesen.
- **Einsätze verwalten:** anlegen, bearbeiten, abschließen (danach schreibgeschützt), löschen (mit Angebot zum vorherigen Export). Offene Einsätze stehen oben.

---

## AS-Sammelstelle

Die Sammelstelle sammelt eintreffende Atemschutzträger, bildet daraus Trupps und schickt sie in die Einsatzabschnitte.

- **Trupp anlegen:** Truppname (Pflicht, eindeutig), laufende Nummer (automatisch), Personen mit Feuerwehr, Anmeldezeit.
- **Abmarsch:** Uhrzeit, Einsatzabschnitt, Funkverbindung.
- **Rückmeldung:** Uhrzeit der Rückkehr. Der Trupp kann danach neu angemeldet werden.
- **Status** wird automatisch abgeleitet: *wartend → im Einsatz → zurück*.
- **Übersicht für Wartende und Leitung:** Warteschlange und Trupps im Einsatz, mit Buttons für Abmarsch und Rückmeldung direkt an jedem Trupp.
- **Zeitwarnung:** Ist ein Trupp länger als 45 Minuten im Einsatz, wird er gelb und später rot markiert.

---

## AS-Überwachung

Die Überwachung rechnet für jeden Trupp im Einsatz mit, wie lange der Luftvorrat reicht, und alarmiert rechtzeitig.

### Erfassung
- Je Person **Anfangsdruck** und **Gerät/Flasche**: 6 l / 300 bar (Standard), 4 l / 200 bar oder 2 × 6 l / 300 bar.
- Plausibilitätsprüfung des Anfangsdrucks (270–300 bar bzw. 180–200 bar bei 4 l). Abweichungen werden markiert, aber nicht gesperrt.
- Auftrag/Aufgabe, Funkverbindung, Start- und Endzeit (sekundengenau, mit „Jetzt“-Button).
- **Enddruck je Person** beim Beenden des Trupps (Pflicht, nie höher als der Anfangsdruck).

### Berechnung
- Luftmenge = Flaschenvolumen × Druck. Die **letzten 50 bar sind Reserve** und werden nie verplant.
- Maßgeblich ist die Person mit der **geringsten nutzbaren Luftmenge**. Kommuniziert wird in bar.
- Verbrauch standardmäßig **50 l/min**, je Einsatz einstellbar.
- Daraus ergeben sich die erwartete Einsatzzeit und die Zeitpunkte:
  - **1. Druckkontrolle** nach ⅓,
  - **½ Einsatzzeit – Rückweg** nach der Hälfte,
  - **2. Druckkontrolle** nach ⅔,
  - **Reserve erreicht** am Ende.
- **Jede Druckablesung rechnet neu**, außerdem wird der Ist-Verbrauch angezeigt. Eine Ablesung ist der niedrigste gemeldete Druck im Trupp (ohne Person). Sie kann nie höher sein als die vorige, das schützt vor Tippfehlern.

### Alarme
- Vorwarnung 1 Minute vor jedem Ereignis. In der letzten Minute läuft der Countdown in Sekunden.
- Bei Alarm ertönt ein **Warnton, der alle 15 Sekunden wiederholt** wird, solange ein Alarm ansteht. Mit 🔔/🔕 lässt er sich ein- und ausschalten.
- **½ Einsatzzeit – Rückweg:** Ist die Zeit erreicht, kann der Alarm um 1–5 Minuten verschoben werden (wird in den Notizen protokolliert), oder „Rückweg angetreten“ wird bestätigt.

### Ausdruck
Die Tabelle ist druckoptimiert und listet für jeden Trupp alle Druckablesungen auf.

---

## Benutzung

1. Die gewünschte HTML-Datei herunterladen (oder das Repository klonen).
2. Die Datei doppelklicken bzw. im Browser öffnen. Am Tablet: Datei lokal speichern und mit dem Browser öffnen.
3. **Neuer Einsatz** → Trupps anlegen → loslegen.

> **Wichtig:** Die Daten liegen nur in diesem Browser auf diesem Gerät. Löschen der Browserdaten oder ein privates Fenster bedeutet Datenverlust. Nach dem Einsatz deshalb **exportieren**.

> **Hinweis zu den Zeitfeldern:** Die Eingabefelder für Datum und Uhrzeit zeichnet der Browser selbst, in seiner *Anzeigesprache*. Ist der Browser auf Englisch eingestellt, erscheinen sie im englischen Format (AM/PM), auch wenn die übrige Seite deutsch formatiert ist.

---

## Haftungsausschluss

Diese Werkzeuge sind **Hilfsmittel** und ersetzen weder die Atemschutzüberwachung nach den geltenden Vorschriften und Dienstanweisungen noch die Verantwortung der Einsatzkräfte. Alle Berechnungen sind Schätzungen auf Basis angenommener Verbrauchswerte. Der tatsächliche Verbrauch kann deutlich abweichen. Maßgeblich sind immer die abgelesenen Druckwerte und die Entscheidung vor Ort.

---

## Entwicklung

- Kein Build, keine Tests, keine Abhängigkeiten: einfach die HTML-Datei bearbeiten und im Browser neu laden.
- Syntaxprüfung: den `<script>`-Block extrahieren und `node --check` darauf ausführen.
- Die beiden Apps sind bewusst parallel aufgebaut und sollen später eventuell zusammengeführt werden.

---

© FF Haselbach [BR-AT] / Stefan Oberhumer
