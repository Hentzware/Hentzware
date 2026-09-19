# Aptifold

<p align="center">
  <img src="Aptifold.png" alt="Aptifold" width="700" />
</p>

**Aptifold** ist ein KI-gestützter Bewerbungs-Manager für Windows. Er bündelt die Jobsuche an einer
Stelle: Bewerbungen verfolgen, Firmen und Kontakte pflegen, Stellenanzeigen übernehmen, Anschreiben
schreiben lassen, Vorstellungsgespräche üben.

Die Anwendung ist **Local-First** gebaut. Alle Bewerbungsdaten liegen in einer verschlüsselten
SQLite-Datenbank auf dem Rechner des Nutzers — der Desktop-Client ist die alleinige Quelle der
Wahrheit. Der Server führt nur die Benutzerkonten, rechnet die Credits ab und reicht KI-Anfragen an
den EU-Endpunkt weiter, ohne Inhalte zu speichern. Hochgeladene Dokumente werden als Text
weiterverarbeitet, die Originaldateien verlassen den Rechner nicht.

---

## Technologien

| Ebene | Technologie |
|---|---|
| Desktop-Client | .NET 10, WPF mit CommunityToolkit.Mvvm, LiveChartsCore |
| Lokale Datenhaltung | SQLite mit SQLCipher (verschlüsselt), EF Core |
| Server | ASP.NET Core 10 (Anmeldung, Credits, KI-Proxy), MariaDB |
| Admin-Panel | Angular 22 (TypeScript) |
| Browser-Erweiterung | Chrome Extension (MV3, TypeScript/Vite) |
| KI | Google Gemini über Vertex AI (EU-Endpunkt), Anthropic Claude |
| E-Mail | IMAP/SMTP mit eigenem Konto |
| Auslieferung | Velopack |
| Tests | xUnit, Moq, FluentAssertions, Testcontainers |

## Architektur

- **Local-First** — Bewerbungsdaten bleiben lokal und verschlüsselt; der Server hält nur Auth und
  Abrechnungs-Metadaten.
- **Fachgebiete statt Schichten** — je Bildschirm, den der Nutzer kennt, ein Ordner im Code; die
  Grenze verläuft zwischen Kern und Außenwelt, nicht zwischen Anwendung und Infrastruktur.
- **Architekturtests** — Projektkanten, Paketgrenzen und Fachgebietsgrenzen werden von einer eigenen
  Testsuite erzwungen, nicht von Konventionen.

## Features

### Bewerbungsmanagement

- **Bewerbungen verwalten** — Erstellen, Bearbeiten und Nachverfolgen aller Bewerbungen
- **Statusverfolgung** — von Entwurf über Interview und Assessment bis Zusage, Absage oder Ghosting
- **Kanban-Board** — alle Bewerbungen nach Status auf einen Blick
- **Prioritäten** — nach Dringlichkeit sortieren
- **Interaktions-Timeline** — chronologischer Verlauf aller Kontakte
- **Statushistorie** — lückenlose Dokumentation jeder Statusänderung

### KI-Funktionen

- **Anschreiben generieren** — individuelle Bewerbungsschreiben, als PDF nach DIN 5008
- **Lebenslauf-Analyse** — Abgleich des Lebenslaufs mit der Stellenausschreibung
- **Stellenanzeigen analysieren** — automatische Extraktion der relevanten Angaben
- **Interview-Coach** — Übungsfragen mit Bewertung der Antworten
- **Karriere-Chatbot** — Assistent für Fragen rund um die Bewerbung
- **Eigene KI-Anweisungen** — anpassbare Vorlagen für die Ergebnisse
- **Credits** — verbrauchsbasierte Abrechnung der KI-Nutzung, sichtbar in der App

### Stellensuche

- **Stellen-Scanner** — gespeicherte Suchen laufen im Hintergrund gegen Bundesagentur für Arbeit,
  Greenhouse und Arbeitnow
- **Browser-Clipper** — Stellenanzeigen direkt aus dem Browser in die App übernehmen

### Firmen, Kontakte, Dokumente

- **Firmendatenbank** — Arbeitgeber mit Branche, Standort und Bewertung
- **Kontaktverwaltung** — Recruiter und Ansprechpartner
- **Dokumentenverwaltung** — Lebensläufe und Anschreiben organisieren
- **E-Mail-Vorlagen** — Vorlagensammlung für die Kommunikation
- **Bewerbungsmappen** — Dokumente zu einer Bewerbung zusammenstellen

### Postfach & Termine

- **Postfach** — E-Mails per IMAP abrufen, Antworten per SMTP versenden
- **Zuordnung** — eingehende Nachrichten den Bewerbungen zuordnen
- **Termine** — Vorstellungsgespräche als .ics-Datei in den eigenen Kalender übernehmen
- **Erinnerungen** — Hinweise auf anstehende Termine und fällige Nachfassaktionen

### Sicherheit & Datenschutz

- Verschlüsselte lokale Datenbank (SQLCipher)
- JWT-Authentifizierung mit Refresh-Token-Rotation
- Rate-Limiting gegen Brute-Force
- KI-Proxy ohne Speicherung der übertragenen Inhalte
- DSGVO by Design: echtes Löschen statt Soft-Delete, pseudonymisiertes Logging

## Lizenz

Copyright Hentzware. Alle Rechte vorbehalten.
