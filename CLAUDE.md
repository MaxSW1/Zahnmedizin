# Projekt: Zahnmedizin / Farmerville

## Hintergrund Max

- Max ist 33 Jahre alt, ehemaliger Software-Unternehmer
- Max plant, Zahnmedizin an der Semmelweis Universität Budapest zu studieren
- Vorteil Semmelweis (EU-Ausland): Keine 2-jährige Vorbereitungszeit/Assistenzarztzeit nötig → sofort Praxisübernahme möglich
- Max' Bruder hat gerade sein Human- und Zahnmedizinstudium abgeschlossen und beginnt jetzt die Facharztausbildung in Mund-, Kiefer-, Gesichtschirurgie (Dauer: 5 Jahre)

## Ziel

- In ca. 5 Jahren gemeinsam mit dem Bruder eine Zahnarztpraxis eröffnen oder übernehmen
- Max bringt unternehmerische Erfahrung ein, der Bruder die chirurgische Spezialisierung
- Alles so effizient wie möglich gestalten: Studium, Vorbereitung auf den Beruf, Praxiskauf

## Fokus dieses Repos

- Recherche und Planung rund um den Weg zum Zahnarzt
- Unternehmerische Fragen zur Praxisgründung/-übernahme
- Vorbereitung während des Studiums auf den späteren Praxisbetrieb

## Anweisungen an Claude

- Claude kennt Max' Hintergrund und muss nicht jedes Mal nachfragen
- Antworten dürfen direkt und praxisorientiert sein
- Max denkt unternehmerisch, Claude darf Effizienz und Business-Perspektive einbringen
- Deutsch als Hauptsprache in diesem Projekt

## Knowledge-Management-System (Kurzübersicht)

Dieses Repo enthält ein Wissensmanagement-System für Podcast- und Video-Inhalte zum Thema Zahnmedizin-Unternehmertum. Das Repo ist gleichzeitig ein **Obsidian-Vault** (Vault-Root = Repo-Root).

**Kernstruktur:**
- `Resource Analysis/_inbox/` — Hier legt Max Transkripte ab (Claude verschiebt sie automatisch)
- `Resource Analysis/_knowledge-hub/` — Thematisch konsolidiertes Wissen (der "Hub")
- `Resource Analysis/[Quelle]/[Episode]/` — Episoden-Ordner mit Transkripten, Zusammenfassungen, Web-Recherche
- `Praxis-Konzepte/Personen/` — Personen-Verzeichnis
- `Praxis-Konzepte/[Praxisname]/` — Praxiskonzept-Profile

**Skills (manuell ausgelöst):**
- `/analyze-episode` — Max legt Transkript in `_inbox/` ab, Claude erfragt fehlende Metadaten, erstellt Ordner, verschiebt Transkript, analysiert komplett
- `/add-notes` — Max diktiert Notizen in Conductor, Claude bereinigt sie und hängt sie an die richtige Episoden-`max-notizen.md` an. Hub-Update wenn relevant.
- `/ask-knowledge` — Beantwortet Fragen anhand des Hubs (5-Stufen-Retrieval: Index → MOC → Sub-Thema → Zusammenfassung → Transkript)
- `/get-podcast-url` — Max fügt Screenshot einer Podcast-Episode bei (Spotify, Apple Podcasts etc.), Claude findet die direkte Audio-URL für MacWhisper, speichert den Screenshot als Bild-Asset und erstellt eine Inbox-Datei (`type: inbox-episode`) mit allen Metadaten und eingebettetem Screenshot. `/analyze-episode` erkennt diese Inbox-Dateien und überspringt die Metadaten-Nachfrage.
- `/get-youtube-url` — Max fügt Screenshot eines YouTube-Videos bei, Claude extrahiert Kanal, Titel, Datum etc., findet die YouTube-URL, speichert Screenshot und erstellt eine Inbox-Datei (`type: inbox-episode`). Max fügt dann das Transkript ein (MacWhisper mit YouTube-URL) und startet `/analyze-episode`.

**Wichtigste Regeln:**
- Jede Information im Hub MUSS eine Quellenangabe haben (Obsidian-Wikilinks mit vollem Pfad)
- Zeitlicher Kontext immer mitführen (Erscheinungsdatum, Aktualitätshinweise bei >2 Jahre alten Quellen)
- Hub-Kategorien entstehen dynamisch und werden bei Bedarf gesplittet (MOC-Struktur)
- Beim Splitting: alte Datei LÖSCHEN, Links aktualisieren, im Changelog dokumentieren

**Bei Fragen zum System oder Problemen:**
→ Vollständige Systemdokumentation: `Resource Analysis/_system-overview.md`
→ Implementierungsplan: `Plans/Knowledge-System-Plan.md`

**PFLICHT — Dokumentation aktuell halten:**
Wenn Claude das Knowledge-System verändert (neue Regeln, neue Dateitypen, Workflow-Änderungen, neue Skills, Strukturänderungen), MUSS Claude im selben Arbeitsschritt auch diese Dateien aktualisieren:
1. `Resource Analysis/_system-overview.md` — Vollständige Systemdoku anpassen
2. Diese CLAUDE.md — Kurzübersicht oben anpassen (falls die Änderung die Kernstruktur, Skills oder Hauptregeln betrifft)
3. `Plans/Knowledge-System-Plan.md` — Plan anpassen (falls die Änderung dort dokumentierte Regeln betrifft)

Routine-Operationen (neue Episode analysieren, Hub-Eintrag ergänzen, Notizen bereinigen) erfordern KEINE Doku-Updates. Nur **System-Änderungen** (neue Regel, neuer Dateityp, neuer Skill, geänderter Workflow).
