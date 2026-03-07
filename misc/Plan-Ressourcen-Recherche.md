# Plan: Ressourcen-Recherche "Zahnarztpraxis gründen & maximalen Umsatz erzielen"

## Ziel

Eine umfassende, strukturierte Markdown-Datei mit den besten deutschsprachigen Ressourcen für Max' Weg zur eigenen Zahnarztpraxis. Fokus auf das deutsche System (KZV, GOZ/BEMA, deutsche Regulierung).

---

## WICHTIG: Anforderungen an jede Ressource

**Jede einzelne Ressource MUSS folgende Informationen enthalten:**

- **Name/Titel** der Ressource
- **Direkter Link zur Primärquelle** (Website, Amazon, Spotify, YouTube etc.) – PFLICHT!
- **Kurze Beschreibung** (1-2 Sätze: Was bietet die Ressource konkret?)
- **Relevanz-Tags** (z.B. `Gründung`, `Abrechnung`, `Marketing`, `Führung`, `Implantologie`)
- **Empfehlungsgrad** nach folgendem Schema:
  - ⭐ = Nützlich, aber nicht essenziell
  - ⭐⭐ = Empfehlenswert, guter Mehrwert
  - ⭐⭐⭐ = Must-Have, wird branchenweit empfohlen oder ist Standardwerk

> Ressourcen OHNE funktionierenden Link werden NICHT aufgenommen.

---

## Kategorien der Recherche

### 1. Bücher
- Praxisgründung & Praxisübernahme
- BWL & Betriebswirtschaft für Zahnärzte
- Abrechnung (GOZ, BEMA)
- Marketing für Zahnarztpraxen
- Führung & Personalmanagement
- Steuern & Recht für Heilberufe

### 2. Podcasts
- Dental-Business & Praxismanagement
- Unternehmertum für Zahnärzte
- Abrechnung & Finanzen
- Interviews mit erfolgreichen Praxisgründern

### 3. YouTube-Kanäle
- Praxisgründung & Business-Tipps
- Umsatzstarke Behandlungen (Implantologie, Aligner, Ästhetik)
- Abrechnung & GOZ-Optimierung
- Dental-Industrie & Trends

### 4. Messen & Kongresse
- Große Dental-Messen (IDS, Fachdental etc.)
- Fachkongresse (DGI, DGZMK etc.)
- Business-Events für Praxisgründer
- Regionale Fortbildungsveranstaltungen

### 5. Online-Kurse & Fortbildungen
- Abrechnungskurse (GOZ/BEMA)
- Implantologie-Curricula
- Marketing & Praxismanagement-Kurse
- Zertifikatslehrgänge

### 6. Blogs, Portale & Online-Communities
- Fachportale (ZWP, zm-online etc.)
- Foren & Communities für Zahnärzte
- Newsletter & Online-Magazine
- Social-Media-Gruppen

### 7. Berater, Netzwerke & Organisationen
- Praxisberater (spezialisiert auf Zahnärzte)
- Steuerberater für Heilberufe
- Berufsverbände & Kammern
- Gründer-Netzwerke für Zahnärzte

### 8. Software & Tools
- Praxisverwaltungssoftware (PVS)
- Abrechnungssoftware
- Buchhaltung & Steuer-Tools
- Terminmanagement & Patientenkommunikation
- Praxismarketing-Tools (SEO, Social Media, Bewertungsportale)

### 9. Finanzierung & Fördermittel
- Banken mit Spezialisierung auf Heilberufe (Deutsche Apothekerbank, KfW etc.)
- Förderprogramme für Praxisgründer
- Finanzierungsmodelle (Praxisübernahme vs. Neugründung)
- Versicherungen für Zahnärzte (Berufshaftpflicht, Praxisausfallversicherung etc.)

---

## Ausführungsanweisung für Claude

### Ablauf der Recherche

Die Recherche wird **kategoriewise mit separaten Agents** durchgeführt:

1. **Pro Kategorie ein eigener Agent** – Jede der 9 Kategorien wird von einem dedizierten Agent recherchiert
2. **Sequenzielle Abarbeitung** – Die Kategorien werden nacheinander abgearbeitet (1 → 2 → 3 → ... → 9)
3. **Zwischenergebnis pro Kategorie** – Jeder Agent schreibt seine Ergebnisse in eine eigene Markdown-Datei:
   - `Recherche/01-Buecher.md`
   - `Recherche/02-Podcasts.md`
   - `Recherche/03-YouTube-Kanaele.md`
   - `Recherche/04-Messen-Kongresse.md`
   - `Recherche/05-Online-Kurse-Fortbildungen.md`
   - `Recherche/06-Blogs-Portale-Communities.md`
   - `Recherche/07-Berater-Netzwerke-Organisationen.md`
   - `Recherche/08-Software-Tools.md`
   - `Recherche/09-Finanzierung-Foerdermittel.md`
4. **Zusammenfassung** – Nach Abschluss aller Kategorien werden alle Einzelergebnisse in ein Gesamtdokument zusammengeführt:
   - `Recherche/GESAMT-Ressourcen-Recherche.md`

### Anweisungen an jeden Agent

- Verwende `WebSearch` um relevante Ressourcen zu finden
- Verifiziere jeden Link mit `WebFetch` (bei 403-Fehler: `WebSearch` als Fallback)
- Nutze zusätzlich das **Chrome-Browser-Plugin** (`mcp__claude-in-chrome`), um Webseiten direkt zu öffnen, zu durchsuchen und Inhalte zu verifizieren – besonders hilfreich bei Seiten, die WebFetch blockieren, oder um Preise, Bewertungen und Details direkt auf den Zielseiten abzulesen
- Halte dich strikt an das Ressourcen-Format (siehe oben)
- Finde mindestens **5-10 Ressourcen pro Kategorie** (Qualität vor Quantität)
- Bevorzuge aktuelle Ressourcen (2023-2026)
- Fokus auf deutschsprachige Ressourcen und das deutsche Gesundheitssystem
- Keine Duplikate über Kategorien hinweg
