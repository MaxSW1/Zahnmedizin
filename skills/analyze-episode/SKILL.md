---
description: "Verarbeitet ein Podcast-/Video-Transkript vollständig: strukturieren, zusammenfassen, Hub updaten, Personen/Praxen erkennen, Web-Recherche."
allowed-tools: ["Read", "Write", "Edit", "Glob", "Grep", "WebSearch", "WebFetch", "Bash", "Task"]
---

# /analyze-episode

Vollständige Analyse eines Podcast-/Video-Transkripts.

## Aufruf

```
/analyze-episode Resource Analysis/_inbox/mein-transkript.md
/analyze-episode Pfad/zu/irgendeiner/datei.md
```

Max legt ein Transkript als Markdown-Datei ab (empfohlen: `Resource Analysis/_inbox/`, aber jeder Ort im Repo funktioniert) und gibt den Pfad an. Claude erledigt ALLES Weitere: Metadaten erfragen, Ordner erstellen, Transkript verschieben, analysieren.

## Workflow (Schritt für Schritt)

### Schritt 0 — Setup: Metadaten sammeln und Ordner erstellen (CLAUDE MACHT DAS)

Max muss KEINEN Ordner anlegen und KEINE Namenskonventionen kennen. Claude übernimmt das komplett.

**0a) Datei lesen und Typ erkennen:**

Claude liest die Input-Datei und prüft das YAML-Frontmatter:

**Fall A — Inbox-Episode (von `/get-podcast-url` erstellt):**
Wenn die Datei `type: inbox-episode` im Frontmatter hat, sind alle Metadaten bereits vorhanden:
- Podcast-Name, Episodennummer, Titel, Erscheinungsdatum, Gast → aus dem Frontmatter übernehmen
- Transkript-Text → aus der `## Transkript` Sektion extrahieren (alles nach dieser Überschrift)
- Screenshot-Dateiname → aus dem `screenshot`-Feld im Frontmatter (falls vorhanden)
- **Schritt 0b wird KOMPLETT ÜBERSPRUNGEN** — keine Nachfragen nötig
- Weiter mit Schritt 0c

**Fall B — Rohes Transkript (manuell abgelegt, kein Frontmatter oder anderer Typ):**
Claude liest das Transkript und versucht folgende Infos selbst zu ermitteln:
- **Podcast/Kanal-Name** (z.B. aus Intro: "Willkommen beim Praxisflüsterer")
- **Episodennummer** (z.B. "Folge 42", "Episode 15")
- **Episodentitel** (z.B. aus Intro oder Themenbeschreibung)
- **Erscheinungsdatum** (z.B. "aufgenommen im März 2023")
- Weiter mit Schritt 0b

**0b) Fehlende Infos bei Max nachfragen (NUR bei Fall B):**

Was Claude NICHT aus dem Transkript ermitteln konnte, fragt Claude bei Max nach. Beispiel:

> "Ich habe das Transkript gelesen. Folgendes konnte ich erkennen:
> - Podcast: Praxisflüsterer
> - Gast: Dr. Stefan Müller
>
> Folgendes brauche ich noch von dir:
> - Episodennummer? (oder keine, z.B. bei YouTube)
> - Erscheinungsdatum? (Monat und Jahr, z.B. 2023-06)
> - Kurzer Titel für die Episode? (z.B. 'Praxisbewertung')"

**WICHTIG**: Claude fragt ALLES auf einmal, nicht Stück für Stück. Und Claude fragt NUR was fehlt — was aus dem Transkript klar hervorgeht, wird nicht nachgefragt.

**0c) Episoden-Ordner erstellen:**

Claude erstellt den Ordner nach den Namenskonventionen:

| Situation | Ordnername | Beispiel |
|:----------|:-----------|:---------|
| Episode mit Nummer | `ep-NNN-titel-slug` | `ep-042-praxisbewertung` |
| Ohne Nummer (YouTube etc.) | `YYYY-MM-titel-slug` | `2024-03-mvz-aufbau` |
| Datums-Kollision | `YYYY-MM-DD-titel-slug` | `2024-05-12-dental-skalierung` |

Namensregeln (Claude wendet diese an, nicht Max):
- Keine Umlaute (ä→ae, ö→oe, ü→ue, ß→ss)
- Keine Leerzeichen (Bindestriche)
- Alles kleingeschrieben
- Akademische Titel weglassen im Ordnernamen

Vollständiger Pfad: `Resource Analysis/[Podcast-Name]/[episode-ordner]/`

**0d) Dateien verschieben:**

- **Transkript**: Von seinem aktuellen Ort nach `Resource Analysis/[Podcast-Name]/[episode-ordner]/transkript.md` verschieben (per `git mv` falls getrackt, sonst per `mv`).
  - Bei `inbox-episode`: Nur den Transkript-Text (ab `## Transkript`) als `transkript.md` speichern. Die Inbox-Datei selbst wird NICHT verschoben — sie wird gelöscht nachdem der Transkript-Text extrahiert ist.
- **Screenshot** (nur bei `inbox-episode` mit `screenshot`-Feld): Die Screenshot-PNG aus `_inbox/` in den Episoden-Ordner verschieben (per `mv`). Der Dateiname bleibt gleich.

**0e) Re-Analyse prüfen:**

Falls der Ziel-Ordner bereits existiert und analysierte Dateien enthält (`transkript-strukturiert.md`, Zusammenfassungs-Datei etc.):
- Max fragen: "Diese Episode wurde bereits analysiert. Soll ich die bestehende Analyse überschreiben oder abbrechen?"
- Bei Status `in-arbeit`: Anbieten, die Analyse fortzusetzen statt neu zu starten

### Schritt 1 — Transkript normalisieren und strukturieren

Transkript-Format erkennen:
- Mit Zeitstempeln (`[00:12:34]`) → beibehalten als Referenz
- Mit Sprechernamen (`Host:`, `Gast:`) → beibehalten und nutzen
- Roh-Text ohne Struktur → Sprecher identifizieren wo möglich
- Bei schlechter Qualität (Spracherkennungsfehler): offensichtliche Fehler korrigieren, unsichere Stellen mit `[unklar]` markieren

Ergebnis als `transkript-strukturiert.md` im Episoden-Ordner speichern mit:
- YAML-Frontmatter (type: transkript-strukturiert)
- Thematische Abschnitte mit `## Überschriften` (damit Obsidian-Links auf Abschnitte funktionieren)

```yaml
---
type: transkript-strukturiert
quelle: [Podcast/Kanal-Name]
episode: [Nummer oder null]
erschienen: [YYYY-MM]
analysiert: [YYYY-MM-DD]
sprecher: ["Host", "Gast-Name"]
abschnitte: [Anzahl]
hat-zeitstempel: [true/false]
sprache: [de/en/etc.]
---
```

### Schritt 2 — Zeitliche Einordnung

Relative Zeitbezüge im strukturierten Transkript annotieren:
- "aktuell", "dieses Jahr", "gerade" → `[Stand: Q1 2023]`
- "letztes Jahr" → konkretes Jahr berechnen basierend auf Erscheinungsdatum
- "vor drei Jahren" → konkretes Jahr berechnen

### Schritt 3 — Zusammenfassung erstellen

**3a) Tiefe-Klassifikation bestimmen:**

Vor dem Schreiben der Zusammenfassung MUSS Claude den Episode-Fokus klassifizieren:

| Klassifikation | Kriterien | Frontmatter-Wert |
|:---------------|:----------|:-----------------|
| **Gründung-Fokus** | Episode behandelt Praxisgründung, Finanzierung, Rentabilität, Aufbau, Übernahme, Investitionsmodelle, Standortwahl, oder Praxisbewertung | `tiefe: gruendung-fokus` |
| **Management-Fokus** | Episode behandelt laufenden Praxisbetrieb, Abrechnung, aktuelle Konzepte, wie Zahnärzte Geld verdienen, Team-Führung, Patientenkommunikation | `tiefe: management-fokus` |

**3b) Zusammenfassung schreiben:**

Zusammenfassungs-Datei im Episoden-Ordner erstellen. **Dateiname = Episodentitel-Slug** (NICHT `zusammenfassung.md`), z.B. `3-trends-zahnaerzte-teil-1.md`, `die-visionaere-alldent-gruender.md`. Slug-Regeln: kleingeschrieben, keine Umlaute, Bindestriche statt Leerzeichen, keine akademischen Titel. YAML-Frontmatter:

```yaml
---
type: episode-zusammenfassung
status: komplett
quelle: [Podcast/Kanal-Name]
episode: [Nummer oder null]
titel: "[Episodentitel]"
url: "[YouTube-URL oder Podcast-URL, falls bekannt]"
erschienen: [YYYY-MM]
analysiert: [YYYY-MM-DD]
personen: ["Person 1", "Person 2"]
praxen: ["Praxis 1"]
kategorien: ["kategorie-1", "kategorie-2"]
tags: [kategorie/sub-thema, ...]
zeitlich-sensitiv: ["Thema 1"]
aliases: ["Ep.42", "Kurzname"]
tiefe: [gruendung-fokus|management-fokus]
---
```

**URL-Feld**: Wenn die Episode von `/get-youtube-url` oder `/get-podcast-url` kommt, steht die URL bereits im Inbox-Frontmatter → übernehmen. Bei manuell abgelegten Transkripten: Max nach der URL fragen (optional). In Obsidian wird das `url`-Feld als klickbarer Link in den Properties angezeigt.

**Bei `gruendung-fokus` — SEHR detaillierte Zusammenfassung:**

Diese Episoden sind Max' Kerninteresse. Jede relevante Zahl, jedes Modell, jedes Beispiel MUSS erfasst werden. Struktur:

1. `> [!abstract] Executive Summary` — 4-6 Sätze mit den wichtigsten Zahlen (Rentabilität, Investitionsvolumen etc.)
2. `> [!tip] Key Takeaways für Max` — 8-12 Bullet Points, jeder mit **fetter Kernzahl/Kernaussage**
3. **Thematische Abschnitte** mit folgenden Custom-Callouts:
   - `> [!memorize]` (rot) — **Schlüsselzahlen und Fakten** die man sich merken muss (z.B. "30% Rentabilität", "0,47% Insolvenzquote", Investment-Spannen, Faustregeln). JEDE wichtige Zahl bekommt ein eigenes Memorize-Callout.
   - `> [!concept]` (lila) — **Wichtige Konzepte und Modelle** (z.B. "Goodwill-Transfer-Modell", "Profit-Center-Denken", "Teilzeit-Tetris"). Erklärt das Modell so, dass es ohne Transkript verständlich ist.
   - `> [!expert]` (gold) — **Experten-Einschätzungen und Einordnungen für Max** (z.B. Implikationen für Max' Gründungsplanung, Vergleiche mit anderen Branchen)
   - `> [!speech]` (grün) — **Direkte Zitate** die besonders aussagekräftig sind
4. **Eigene Abschnitte** für: Rentabilität/Risiko, Investitionsmodelle, Controlling-Metriken, Praxisbewertung
5. Jeder Abschnitt MUSS eine Quellenangabe mit Wikilink haben
6. **Trennlinien (`---`)** zwischen den Hauptabschnitten für visuelle Klarheit

Ziel: Max soll die Zusammenfassung lesen und SOFORT alle relevanten Zahlen, Modelle und Implikationen für seine Gründung finden — ohne das Transkript öffnen zu müssen.

**Bei `management-fokus` — Kompakte Zusammenfassung:**

1. `> [!abstract] Executive Summary` — 3-4 Sätze
2. `> [!tip] Key Takeaways` — 5-8 Bullet Points
3. Thematische Abschnitte — kurz und auf den Punkt
4. Custom-Callouts NUR wo besonders relevante Zahlen oder Konzepte auftauchen
5. Quellenangaben mit Wikilinks

Inhalt allgemein:
- Bei fremdsprachigem Transkript: Zusammenfassung auf Deutsch

### Schritt 4 — Notiz-Datei erstellen

`max-notizen.md` im Episoden-Ordner erstellen — nur Frontmatter + eine Hauptüberschrift, **keine thematischen Unter-Überschriften**:

```yaml
---
type: max-notizen
quelle: [Podcast/Kanal-Name]
episode: [Nummer oder null]
erstellt: [YYYY-MM-DD]
bereinigt: false
roh-version: null
---

# Notizen: [Episodentitel]

```

### Schritt 5 — Personen und Praxen identifizieren

- Alle genannten Personen und Praxen auflisten
- **Duplikat-Check**: VOR dem Erstellen neuer Profile immer `Praxis-Konzepte/Personen/_personen-index.md` und `Praxis-Konzepte/_praxiskonzepte-index.md` lesen + bestehende `aliases`-Felder prüfen
- Existierendes Profil → ergänzen (Episoden-Array erweitern, neue Infos hinzufügen)
- Neues Profil → erstellen unter `Praxis-Konzepte/Personen/vorname-nachname.md` bzw. `Praxis-Konzepte/[Praxisname]/profil.md`
- Indizes aktualisieren

**Personen-Profil Frontmatter:**
```yaml
---
type: person
name: "Dr. Stefan Müller"
rolle: "Gründer & Geschäftsführer"
unternehmen: "Dental21"
episoden: ["Praxisflüsterer/ep-042"]
expertise: ["MVZ-Aufbau", "Skalierung"]
web-recherche-datum: [YYYY-MM-DD]
aliases: ["Stefan Müller", "Dr. Müller"]
---
```

**Praxiskonzept-Profil Frontmatter:**
```yaml
---
type: praxiskonzept
praxis: "Dental21"
gruender: "Dr. Stefan Müller"
standorte: ["Berlin", "München"]
rechtsform: MVZ
spezialisierung: ["Allgemeinzahnheilkunde", "Implantologie"]
gruendungsjahr: 2018
episoden: ["Praxisflüsterer/ep-042"]
info-stand: [YYYY-MM]
web-recherche-datum: [YYYY-MM-DD]
aliases: ["Dental 21", "Dental21 GmbH"]
---
```

### Schritt 6 — Web-Recherche

Zu jeder identifizierten Person und Praxis automatisch recherchieren:
- Hintergrund, Karriere, Veröffentlichungen
- Aktuelle Entwicklungen bei Praxis/Unternehmen
- Andere Interviews/Auftritte (Querverweise)

**Fallback-Strategie**: WebFetch zuerst versuchen → bei Fehler automatisch WebSearch nutzen.

Ergebnisse als `web-recherche.md` im Episoden-Ordner speichern:

```yaml
---
type: web-recherche
quelle: [Podcast/Kanal-Name]
episode: [Nummer oder null]
personen: ["Person 1"]
praxen: ["Praxis 1"]
recherche-datum: [YYYY-MM-DD]
quellen-count: [Anzahl]
---
```

**WICHTIG**: Web-Recherche-Fehler blockieren NIE die restliche Analyse. Bei Fehlern vermerken und weiterarbeiten.

### Schritt 7 — Knowledge-Hub aktualisieren

1. `Resource Analysis/_knowledge-hub/_hub-index.md` lesen → relevante Kategorien identifizieren
2. Erkenntnisse in die passenden Hub-Dateien unter `Resource Analysis/_knowledge-hub/` ANHÄNGEN (nie überschreiben)
3. Wenn ein Thema nirgends passt → neue Kategorie vorschlagen und in `Resource Analysis/_knowledge-hub/` anlegen
4. Jeder Hub-Eintrag MUSS eine Quellenangabe haben:

```markdown
> Quelle: [[Resource Analysis/Podcast/episode/transkript-strukturiert#Abschnitt|Podcast Ep.42 (Juni 2023)]]
```

5. Zeitliche Einordnung bei allen Einträgen mitführen
6. Bei Widersprüchen zu bestehenden Einträgen: Neuere Quelle oben, ältere darunter mit `> [!warning] Zeitlicher Hinweis`

### Schritt 8 — Hub-Struktur prüfen

- Wird eine Hub-Datei zu groß (>200 Zeilen) oder hat 3+ Sub-Themen? → Splitting in Ordner + MOC
- Überlappen zwei Kategorien stark? → Zusammenlegung vorschlagen
- **Beim Splitting**: Alte Datei LÖSCHEN, alle Obsidian-Links per Grep suchen und aktualisieren, in `Resource Analysis/_knowledge-hub/_hub-changelog.md` dokumentieren
- `Resource Analysis/_knowledge-hub/_hub-index.md` Frontmatter aktualisieren (kategorien-count, episoden-total)

### Schritt 9 — Abschluss-Bericht

Am Ende eine Zusammenfassung an Max ausgeben:

```
Episode analysiert: [Quelle] [Episode] - [Titel] ([Datum])
Transkript verschoben nach: Resource Analysis/[Podcast]/[episode-ordner]/
Transkript strukturiert ([X] Abschnitte)
Zusammenfassung erstellt
Hub aktualisiert: [Kategorien] ([X] Kategorien)
Praxiskonzept erkannt: [Name] → [Pfad] (oder: Kein Praxiskonzept erkannt)
Person(en) erkannt: [Name(n)] → [Pfad(e)] (oder: Keine neuen Personen)
Web-Recherche: [X] Quellen gefunden (oder: Fehlgeschlagen/Keine Ergebnisse)
Max-Notizen: max-notizen.md erstellt (leer, wartet auf Max)
```

## Fehlerbehandlung

- **Sehr langes Transkript (>50.000 Wörter)**: In Abschnitten verarbeiten. Falls Context-Limit erreicht: Status `in-arbeit` setzen, bisherige Ergebnisse speichern, Max informieren.
- **Schlechte Qualität**: Offensichtliche Fehler korrigieren, `[unklar]` für unsichere Stellen. Nur eindeutige Informationen in Zusammenfassung und Hub übernehmen.
- **Keine Sprecher identifizierbar**: Als `Sprecher 1`, `Sprecher 2` etc. labeln.
- **Fremdsprachiges Transkript**: Originalsprache im strukturierten Transkript beibehalten. Zusammenfassung, Hub-Einträge und alle anderen Dateien auf Deutsch.
- **Abbruch**: Status `in-arbeit` setzen, erstellte Dateien NICHT löschen. Bei erneutem Aufruf Fortsetzung anbieten.
