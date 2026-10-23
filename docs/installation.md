# Installation

Rechne mit rund 30 Minuten für die Einrichtung, plus Zeit zum Prüfen der Tipps.

## 1. Excel-Datei ablegen

1. Lade [`vorlage/Copilot-Znueni_Tipps.xlsx`](../vorlage/Copilot-Znueni_Tipps.xlsx) in eine SharePoint-Bibliothek hoch, zum Beispiel auf der Teamsite der IT unter `Dokumente/Copilot-Znüni/`.
   - Empfohlen ist SharePoint statt eines persönlichen OneDrive. So läuft der Flow auch bei Ferien oder Personalwechseln weiter.
   - Das Konto der Excel-Verbindung im Flow braucht Schreibrechte auf die Datei.
2. Fülle im Blatt **Einstellungen** die gelben Felder aus:

| Feld | Beschreibung |
| --- | --- |
| `Empfaenger` | Verteilerliste oder M365-Gruppe. Mehrere Adressen mit `;` trennen. Für den Test zuerst die eigene Adresse eintragen. |
| `Absender` | Optional. Zum Beispiel eine geteilte Mailbox `copilot@firma.ch`. Das Konto der Outlook-Verbindung braucht dafür die Berechtigung «Senden als». Leer lassen = Versand vom Konto der Verbindung. |
| `Absendername` | Grussformel unter der Mail. |
| `AdminMail` | Erhält Meldungen bei Fehlern und am Ende der Tippliste. |
| `FeedbackLink` | Optional. Teams-Kanal, Forms-Umfrage oder SharePoint-Seite. |
| `Betreffpraefix` | Erscheint im Betreff und im Kopf der Mail, z. B. «Copilot-Znüni». |
| `NurChatTipps` | `Ja`, wenn die Empfänger keine Copilot-Lizenz haben. Dann werden nur 15 der 42 Tipps versendet. |
| `Pausiert` | Bleibt vorerst auf `Ja`. So wird nichts versendet, bevor alles eingerichtet ist. |

3. Gehe die Tipps im Blatt **Tipps** durch:
   - Jeden Tipp einmal selbst ausprobieren.
   - Die Spalte **Hinweis** beachten.
   - Tipps zu Funktionen, die bei euch nicht freigegeben sind, auf `Aus` setzen.
   - Bei Bedarf Reihenfolge ändern oder eigene Tipps ergänzen (neue Zeilen innerhalb der Tabelle, `Nr` fortlaufend und eindeutig).

## 2. Flow importieren

1. Öffne [make.powerautomate.com](https://make.powerautomate.com) und wähle oben rechts die richtige Umgebung (meist die Standardumgebung).
2. **Meine Flows → Importieren → Paket importieren (Legacy)**.
3. Lade [`flow/Copilot-Znueni_Flow.zip`](../flow/Copilot-Znueni_Flow.zip) hoch.
4. Unter **Ressourcen im Paket überprüfen**:
   - Beim Flow «Copilot-Znüni» bleibt **Neu erstellen** stehen.
   - Bei **Excel Online (Business)** und **Office 365 Outlook** jeweils auf **Während des Imports auswählen** klicken und eine bestehende Verbindung wählen oder neu erstellen.
5. **Importieren** klicken.

> Wenn der Import fehlschlägt, kannst du den Flow anhand von [`flow-aufbau.md`](flow-aufbau.md) auch von Hand nachbauen.

## 3. Excel-Aktionen verbinden

Die Datei ist in jedem Tenant eine andere. Deshalb müssen vier Aktionen nach dem Import auf deine Datei zeigen. Öffne den Flow zum Bearbeiten:

| Aktion | Ort im Flow | Tabelle |
| --- | --- | --- |
| `Einstellungen_lesen` | Ausfuehren | `tblEinstellungen` |
| `Offene_Tipps_lesen` | Ausfuehren | `tblTipps` |
| `Tipp_als_gesendet_markieren` | Ausfuehren → Tipp_vorhanden → Ja | `tblTipps` |
| `Automatisch_pausieren` | Ausfuehren → Tipp_vorhanden → Nein | `tblEinstellungen` |

Bei jeder Aktion:
1. **Speicherort** (SharePoint-Site), **Dokumentbibliothek**, **Datei** und **Tabelle** wählen.
2. Danach prüfen, ob die übrigen Felder noch gesetzt sind. Wurden sie beim Wechsel der Tabelle zurückgesetzt, trage sie neu ein:

| Aktion | Feld | Wert |
| --- | --- | --- |
| `Einstellungen_lesen` | Schlüsselspalte / Schlüsselwert | `Id` / `1` |
| `Offene_Tipps_lesen` | Filterabfrage | `Status eq 'Offen'` |
| `Tipp_als_gesendet_markieren` | Schlüsselspalte | `Nr` |
| | Schlüsselwert (Ausdruck) | `trim(coalesce(outputs('Tipp')?['Nr'],''))` |
| | Status | `Gesendet` |
| | GesendetAm (Ausdruck) | `formatDateTime(convertFromUtc(utcNow(),'W. Europe Standard Time'),'dd.MM.yyyy')` |
| `Automatisch_pausieren` | Schlüsselspalte / Schlüsselwert | `Id` / `1` |
| | Pausiert | `Ja` |

3. **Speichern**. Der Flow-Prüfer sollte keine Fehler mehr anzeigen.

## 4. Testen

1. In der Excel-Datei: `Empfaenger` = eigene Adresse, `Pausiert` = `Nein`.
2. Im Flow: **Testen → Manuell → Testen → Flow ausführen**. Der manuelle Test funktioniert an jedem Tag, auch am Wochenende.
3. Prüfen:
   - Ist die Mail angekommen, und sieht sie in Outlook Desktop, im Web und auf dem Smartphone gut aus?
   - Steht beim ersten Tipp in der Excel-Datei nun `Gesendet` und das heutige Datum?
4. Den getesteten Tipp wieder auf `Offen` setzen und `GesendetAm` leeren.
5. Optional: `Pausiert` = `Ja`, einen Test ausführen und prüfen, dass nichts versendet wird.

## 5. Go-live

1. Ankündigen, siehe [`kommunikation.md`](kommunikation.md).
2. Am Vortag des Starts: `Empfaenger` auf die Verteilerliste setzen und `Pausiert` = `Nein`.
3. Der erste Tipp kommt am nächsten Werktag um 08:45 Uhr.

Eine andere Uhrzeit stellst du im Trigger `Wochentags_um_0845` ein.

## Häufige Probleme

| Problem | Ursache und Lösung |
| --- | --- |
| Es kommt keine Mail, der Lauf ist aber erfolgreich | `Pausiert` steht auf `Ja`, oder es gibt keinen Tipp mehr mit Status `Offen` (bzw. keinen Chat-Tipp bei `NurChatTipps = Ja`). |
| Fehler bei `Einstellungen_lesen` | Datei oder Tabelle falsch gewählt, Tabelle umbenannt oder in der Spalte `Id` steht nicht `1`. |
| Fehler beim Versand mit `Absender` | Dem Konto der Outlook-Verbindung fehlt die Berechtigung «Senden als» für die Absenderadresse. |
| Geänderte Tipps werden nicht berücksichtigt | Der Excel-Connector sieht Änderungen manchmal mit einigen Minuten Verzögerung. Datei speichern und schliessen. |
| Ein Tipp wird doppelt versendet | Die Spalte `Nr` ist nicht eindeutig. Jede Nummer darf nur einmal vorkommen. |
| Excel-Datei ist gesperrt | Der Connector kann nicht schreiben, solange die Datei im Desktop-Excel exklusiv geöffnet ist. Excel im Browser oder Co-Authoring verwenden. |
