# Konzept: Copilot-Adoption mit täglichen Häppchen

## Ausgangslage

Nach der Einführung von Microsoft 365 Copilot zeigt sich oft dasselbe Bild:
- Viele nutzen Copilot nur für wenige Dinge, meist in Teams und Outlook.
- Funktionen in Word, Excel, PowerPoint oder die Copilot-Suche bleiben unbekannt.
- Lizenzen werden bezahlt, aber kaum genutzt.

Einmalige Schulungen helfen, verblassen aber schnell. Neue Funktionen kommen laufend dazu, und im Alltag fehlt die Zeit, sich selbst darüber zu informieren.

Das Copilot-Znüni setzt deshalb auf **Microlearning**: jeden Arbeitstag ein Tipp, der in höchstens fünf Minuten ausprobiert ist. Die Idee stammt aus dem Projekt [Copilot Yoga](https://github.com/sir-benniboy/copilotyoga), das laut einer Copilot-Admin-Schulung auch bei Microsoft Schweiz intern eingesetzt wurde.

## Ziele

1. **Nutzung verbreitern:** Mitarbeitende kennen und nutzen Copilot in mehreren Apps, nicht nur in einer.
2. **Gute Gewohnheiten aufbauen:** besser prompten, Antworten prüfen, Datenschutz beachten.
3. **Lizenzwert steigern:** Die Active Rate der Copilot-Lizenzen steigt messbar.
4. **Feedback sammeln:** Die IT erfährt, welche Anwendungsfälle im Unternehmen funktionieren und wo es hakt.

## Prinzipien

- **Kurz:** ein Tipp, ein Nutzen, höchstens fünf Minuten.
- **Sofort ausprobierbar:** Prompt zum Kopieren und Link direkt in die App.
- **Vom Einfachen zum Komplexen:** zuerst Prompt-Grundlagen und Copilot Chat, dann Office-Apps, am Schluss Agents.
- **Ehrlich:** Grenzen benennen («Vertrauen, aber prüfen»), keine überzogenen Versprechen.
- **Freiwillig und ohne Tracking:** keine Lesebestätigungen, keine Auswertung pro Person.

## Zielgruppen und Varianten

| Zielgruppe | Einstellung | Umfang |
| --- | --- | --- |
| Mitarbeitende mit Microsoft 365 Copilot-Lizenz | `NurChatTipps = Nein` | 42 Tipps, rund 8,5 Wochen |
| Mitarbeitende mit Copilot Chat (ohne Zusatzlizenz) | `NurChatTipps = Ja` | 15 Tipps, rund 3 Wochen |

Für beide Gruppen gleichzeitig braucht es zwei Kopien von Excel-Datei und Flow, je mit eigener Verteilerliste. Der Status der Tipps wird pro Datei geführt.

Bei Chat-Usern sind Tipps zu Premium-Funktionen nicht nur unnütz, sondern frustrierend («Wieso kann ich das nicht?»). Deshalb lohnt sich die Trennung.

## Ablauf

| Zeitpunkt | Was | Wer |
| --- | --- | --- |
| 4 Wochen vorher | Tipps prüfen, auf eigene Beispiele anpassen, Feedbackkanal einrichten | Copilot-Verantwortliche, Champions |
| 3 Wochen vorher | Baseline aus den Usage Reports sichern (siehe Messung) | IT |
| 2 Wochen vorher | Ankündigung per Mail oder Intranet | Kommunikation, IT |
| 1 Woche vorher | Testlauf mit Pilotgruppe (Champions), letzte Korrekturen | IT |
| Start (Montag) | Erster Tipp, Begrüssungspost im Teams-Kanal | IT |
| Wöchentlich | Feedback sichten, Fragen im Kanal beantworten, Tipps bei Bedarf anpassen | Champions, IT |
| Halbzeit | Kurzer Zwischenstand im Kanal, z. B. beliebtester Tipp | IT |
| Ende | Abschlussmail mit Feedback-Umfrage | IT |
| 4 Wochen danach | Auswertung und Entscheid über eine nächste Runde | Copilot-Verantwortliche |

Vorlagen für Ankündigung, Start und Abschluss stehen in [`kommunikation.md`](kommunikation.md).

## Rollen

- **Copilot-Verantwortliche/r (Owner):** verantwortet Inhalte, Zeitplan und Auswertung. In kleinen Firmen oft dieselbe Person wie der Admin.
- **Admin:** richtet Flow und Datei ein und erhält Fehlermeldungen (`AdminMail`).
- **Champions:** einige technikaffine Mitarbeitende aus verschiedenen Abteilungen. Sie testen die Tipps vorab, steuern eigene Beispiele bei und beantworten Fragen im Kanal.
- **Helpdesk:** kennt den Zeitplan, damit Fragen zu den Tipps richtig eingeordnet werden.

Gibt es ein Copilot Center of Excellence, gehört das Znüni dorthin.

## Erfolg messen

Das Znüni selbst erhebt bewusst keine Daten. Die Wirkung misst ihr mit den vorhandenen Microsoft-Werkzeugen:

| Kennzahl | Quelle | Vergleich |
| --- | --- | --- |
| Aktive Copilot-User und Active Rate | M365 Admin Center → Berichte → Nutzung → Microsoft 365 Copilot | Baseline vs. Ende vs. 4 Wochen danach |
| Nutzung pro App (Teams, Outlook, Word, Excel, PowerPoint …) | gleicher Bericht | Steigt die Nutzung in Apps, zu denen Tipps versendet wurden? |
| Nutzung von Copilot Chat | Bericht Copilot Chat | für Chat-Zielgruppe |
| Nutzung der Agents | Bericht Agents | nach den Agent-Tipps |
| Detaillierte Adoption pro Abteilung | Copilot Dashboard (Viva Insights) | Schwellwerte für Anonymisierung beachten |
| Zufriedenheit, beliebteste Tipps | Feedback-Umfrage am Ende | qualitativ |

Ablauf der Messung:
- **Baseline vor dem Start sichern** (Screenshot oder Export), weil die Berichte nur kurze Zeiträume zeigen.
- **Ziel vorher festlegen**, zum Beispiel: Active Rate von 55 % auf 70 %, Copilot-Nutzung in Word bei mindestens 40 % der lizenzierten User.
- **Benchmarks mit Vorsicht** verwenden: Werte anderer Firmen sind nur bedingt vergleichbar.

## Inhalte pflegen

Ein guter Tipp:
- hat einen konkreten Nutzen im ersten Satz,
- kommt mit höchstens drei bis vier Schritten aus,
- enthält einen Prompt, der mit wenigen Anpassungen funktioniert (Platzhalter in `[eckigen Klammern]`),
- verweist auf eure eigenen Begriffe, Dateien oder Abläufe, wo möglich,
- wurde vorher im eigenen Tenant getestet.

Eigene Tipps lohnen sich besonders zu:
- häufigen Aufgaben in euren Abteilungen,
- internen Agents, die die IT bereitstellt,
- neuen Funktionen aus dem Message Center.

## Datenschutz und Governance

- Der Flow liest und schreibt nur die Excel-Datei und versendet Mails an die konfigurierte Adresse.
- Es werden keine personenbezogenen Daten verarbeitet und keine Öffnungs- oder Klickraten erfasst.
- Die Mails enthalten keine externen Bilder oder Tracking-Pixel.
- Tipps zu Funktionen, die nicht freigegeben sind (Bildgenerierung, Agents, andere KI-Modelle), werden vorher auf `Aus` gesetzt.
- Der Tipp «Ist mein Copilot geschützt?» kann mit der internen KI-Richtlinie verlinkt werden.

## Erweiterungsideen

- Zusätzlich oder statt Mail in einem **Teams-Kanal** posten (Aktion «Nachricht in einem Chat oder Kanal posten»)
- **SharePoint-Liste** statt Excel, für grössere Teams mit mehreren Redaktoren
- **Feiertagskalender** als zusätzliche Tabelle, damit der Flow an Feiertagen automatisch aussetzt
- **Mehrsprachig** (DE, FR, IT) mit je einer Spalte pro Sprache und einer Verteilerliste pro Sprachregion
- **Ein Tipp pro Woche** statt pro Tag, für eine zweite, längere Runde mit vertieften Themen
