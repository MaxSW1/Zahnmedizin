---
type: system-dokumentation
letzte-aktualisierung: 2026-03-10
---

# Knowledge-Management-System — Systemübersicht

Dieses Dokument beschreibt, wie das Wissensmanagement-System in diesem Repo funktioniert. Es dient als Referenz für Claude Code, um das System zu verstehen und korrekt damit zu arbeiten.

Für den vollständigen Implementierungsplan siehe: `Plans/Knowledge-System-Plan.md`

---

## Zweck des Systems

Max sammelt Wissen aus Podcasts und YouTube-Videos zum Thema Zahnmedizin-Unternehmertum (Praxisgründung, MVZ-Strukturen, Skalierung, Finanzen, Personal, etc.). Das System verarbeitet Transkripte und konsolidiert die Erkenntnisse in einem durchsuchbaren Knowledge-Hub.

Das Repo ist gleichzeitig ein **Obsidian-Vault** (Vault-Root = Repo-Root `farmerville/`). Alle Markdown-Dateien müssen Obsidian-kompatibel sein.

---

## Ordnerstruktur

```
Resource Analysis/
├── _inbox/                            # HIER legt Max Transkripte ab (Claude verschiebt sie)
├── _knowledge-hub/                    # Konsolidiertes Wissen nach Themen
│   ├── _hub-index.md                 # EINSTIEGSPUNKT: Übersicht aller Kategorien
│   ├── _hub-changelog.md             # Protokoll aller Struktur-Änderungen
│   ├── [kategorie].md                # Wissen zu einem Thema (einzelne Datei)
│   └── [kategorie]/                   # Oder als Ordner mit Sub-Themen (nach Splitting)
│       ├── _[kategorie]-moc.md       # Map of Content: Übersicht + Links
│       └── [sub-thema].md            # Einzelnes Sub-Thema mit Erkenntnissen
├── _system-overview.md               # DIESE DATEI
├── [Podcast-Name]/                    # Pro Quelle ein Ordner (von Claude erstellt)
│   └── [episode-ordner]/              # Pro Episode ein Ordner (von Claude erstellt)
│       ├── transkript.md              # Original (von Claude aus _inbox/ verschoben)
│       ├── transkript-strukturiert.md # Thematisch unterteilt (automatisch)
│       ├── [episodentitel-slug].md     # Zusammenfassung mit Episodentitel als Dateiname
│       ├── web-recherche.md           # Recherche zu Personen/Praxen (automatisch)
│       └── max-notizen.md             # Max' eigene Gedanken (manuell befüllt)
└── ...

Praxis-Konzepte/
├── _praxiskonzepte-index.md           # Übersicht aller Praxiskonzepte
├── _praxiskonzepte.base               # Obsidian Base: dynamische Praxis-Übersicht
├── Personen/                          # Personen-Verzeichnis
│   ├── _personen-index.md             # Übersicht aller Personen
│   ├── _personen.base                 # Obsidian Base: dynamische Personen-Übersicht
│   └── [vorname-nachname].md          # Profil pro Person
├── [Praxisname]/                      # Pro dokumentierter Praxis ein Ordner
│   └── profil.md                      # Profil: Geschäftsmodell, Skalierung, Learnings
└── ...
```

---

## Dateitypen und ihre Funktion

### Inbox-Dateien (temporär in `_inbox/`)

| Datei | Erstellt durch | Zweck |
|:------|:---------------|:------|
| `[podcast-slug]-ep-[NNN].md` | `/get-podcast-url` | Vorbereitete Episode mit Metadaten, Audio-URL, eingebettetem Screenshot und Transkript-Platzhalter. `type: inbox-episode` im Frontmatter. Wird von `/analyze-episode` erkannt und verarbeitet. |
| `[podcast-slug]-ep-[NNN]-screenshot.png` | `/get-podcast-url` | Screenshot der Episode (Bild-Asset). Per `![[...]]` in die Inbox-Markdown-Datei eingebettet. Wird von `/analyze-episode` in den Episoden-Ordner verschoben. |
| `[kanal-slug]-YYYY-MM-titel-slug.md` | `/get-youtube-url` | Vorbereitetes YouTube-Video mit Metadaten, YouTube-URL, eingebettetem Screenshot und Transkript-Platzhalter. `type: inbox-episode` im Frontmatter. Wird von `/analyze-episode` erkannt und verarbeitet. |
| `[kanal-slug]-YYYY-MM-titel-slug-screenshot.png` | `/get-youtube-url` | Screenshot des YouTube-Videos (Bild-Asset). Per `![[...]]` in die Inbox-Markdown-Datei eingebettet. Wird von `/analyze-episode` in den Episoden-Ordner verschoben. |

### Episoden-Dateien (pro Episode)

| Datei | Erstellt durch | Zweck |
|:------|:---------------|:------|
| `transkript.md` | Max (Upload) | Roh-Transkript, unverändert |
| `transkript-strukturiert.md` | `/analyze-episode` | In thematische Abschnitte unterteilt, mit `## Überschriften` für Obsidian-Verlinkung |
| `[episodentitel-slug].md` | `/analyze-episode` | Zusammenfassung mit Episodentitel als Dateiname (z.B. `3-trends-zahnaerzte-teil-1.md`). Hat `tiefe`-Feld: `gruendung-fokus` (sehr detailliert, Custom-Callouts) oder `management-fokus` (kompakt). Erkennbar am `type: episode-zusammenfassung` im Frontmatter. |
| `web-recherche.md` | `/analyze-episode` | Recherche-Ergebnisse zu Personen und Praxen aus dem Internet |
| `max-notizen.md` | `/analyze-episode` (Grundstruktur), Max (Inhalt) | Max' eigene Gedanken und Einschätzungen |

### Knowledge-Hub-Dateien

| Datei | Zweck |
|:------|:------|
| `_hub-index.md` | Zentraler Einstiegspunkt. Listet alle Kategorien mit kurzer Beschreibung. Claude liest IMMER zuerst diese Datei. |
| `_hub-changelog.md` | Protokolliert Struktur-Änderungen (neue Kategorien, Splitting, Merging, Link-Updates) |
| `[kategorie].md` | Einzelne Hub-Datei mit konsolidierten Erkenntnissen zu einem Thema |
| `_[kategorie]-moc.md` | Map of Content — entsteht nur nach Splitting, enthält Übersicht + Links zu Sub-Themen |
| `[sub-thema].md` | Einzelnes Sub-Thema nach Splitting, enthält Erkenntnisse + Quellenangaben |

### Praxiskonzept- und Personen-Dateien

| Datei | Zweck |
|:------|:------|
| `_praxiskonzepte-index.md` | Übersicht aller dokumentierten Praxen/Unternehmen |
| `_praxiskonzepte.base` | Obsidian Base: dynamische Praxis-Übersicht (selbstaktualisierend) |
| `_personen-index.md` | Übersicht aller dokumentierten Personen |
| `_personen.base` | Obsidian Base: dynamische Personen-Übersicht (selbstaktualisierend) |
| `[Praxisname]/profil.md` | Steckbrief einer Praxis: Geschäftsmodell, Skalierungsstrategie, Key Learnings |
| `[vorname-nachname].md` | Steckbrief einer Person: Expertise, Episoden, Web-Infos |

### Obsidian Base-Dateien (`.base`)

Bases sind dynamische Views, die sich automatisch aus Frontmatter-Properties aktualisieren. Sie ergänzen die Markdown-Indizes (nicht ersetzen).

| Datei | Zweck |
|:------|:------|
| `Resource Analysis/_episoden.base` | Alle Episoden sortiert/filterbar nach Quelle, Datum, Status |
| `Resource Analysis/_knowledge-hub/_hub-dashboard.base` | Hub-Kategorien mit Episode-Count und Aktualität |
| `Praxis-Konzepte/_praxiskonzepte.base` | Alle Praxiskonzepte als Karten-Ansicht |
| `Praxis-Konzepte/Personen/_personen.base` | Alle Personen mit Episoden-Count und Expertise |

---

## Die fünf Skills

### `/analyze-episode`

Verarbeitet ein Transkript vollständig. Max legt das Transkript in `Resource Analysis/_inbox/` ab (oder irgendwo im Repo) und ruft den Skill auf. Claude übernimmt alles: Metadaten ermitteln/nachfragen, Ordner erstellen, Transkript verschieben, analysieren.

Workflow:

0. **Setup** (Claude macht das): Transkript lesen → Metadaten extrahieren (Podcast, Episode, Datum, Titel) → fehlende Infos bei Max nachfragen → Episoden-Ordner erstellen → Transkript verschieben
1. Transkript normalisieren und strukturieren
2. Zeitliche Einordnung (relative → absolute Zeitangaben)
3. Zusammenfassung erstellen (mit Tiefe-Klassifikation: `gruendung-fokus` = sehr detailliert mit Custom-Callouts, `management-fokus` = kompakt)
4. Notiz-Datei erstellen (leer, für Max)
5. Personen und Praxen identifizieren
6. Web-Recherche zu Personen/Praxen
7. Knowledge-Hub aktualisieren (ANHÄNGEN, nicht überschreiben)
8. Hub-Struktur prüfen (Splitting/Merging nötig?)
9. Abschluss-Bericht an Max

### `/add-notes`

Max diktiert Notizen zu einer Episode direkt in Conductor. Der Skill:
- Erkennt die richtige Episode (anhand Nummer, Titel, Person oder Thema)
- Bereinigt das Diktat (Füllwörter raus, Sätze vervollständigen, Kern bewahren)
- Hängt die Notiz mit passender Überschrift an die `max-notizen.md` der Episode an
- Aktualisiert den Knowledge-Hub, falls Hub-relevante Erkenntnisse enthalten sind

### `/ask-knowledge`

Beantwortet Fragen anhand des gesammelten Wissens. Nutzt das 5-Stufen-Retrieval:
1. `_hub-index.md` → relevante Kategorien finden
2. Kategorie-Datei oder MOC → relevante Sub-Themen finden
3. Sub-Themen-Datei → konsolidiertes Wissen + Quellen
4. Episode-Zusammenfassung → mehr Kontext (nur bei Bedarf)
5. Transkript → Originaltext (nur wenn wirklich nötig)

### `/get-podcast-url`

Erstellt eine vorbereitete Inbox-Datei aus einem Podcast-Screenshot. Max fügt einen Screenshot der Episode bei (Spotify, Apple Podcasts, Podcast-Website etc.) und Claude:
1. Erkennt Podcast-Name, Episode-Titel, Datum, Gast, Beschreibung aus dem Screenshot
2. Sucht die direkte Audio-Download-URL (RSS-Feed, Podigee, Episode-Seite)
3. Speichert den Screenshot als Bild-Asset in `Resource Analysis/_inbox/`
4. Erstellt eine Markdown-Datei in `Resource Analysis/_inbox/` mit `type: inbox-episode` Frontmatter, allen Metadaten, Audio-URL, eingebettetem Screenshot (`![[...]]`) und `## Transkript` Platzhalter

**Workflow-Integration**: Max kopiert die Audio-URL in MacWhisper, fügt das fertige Transkript in die Inbox-Datei ein, und ruft `/analyze-episode` auf. Da alle Metadaten bereits im Frontmatter stehen, überspringt `/analyze-episode` die Nachfragephase komplett.

### `/get-youtube-url`

Erstellt eine vorbereitete Inbox-Datei aus einem YouTube-Screenshot. Max fügt einen Screenshot des YouTube-Videos bei und Claude:
1. Erkennt Kanal-Name, Video-Titel, Datum, Gast, Beschreibung, Kapitelmarken aus dem Screenshot
2. Sucht die YouTube-Video-URL per WebSearch
3. Speichert den Screenshot als Bild-Asset in `Resource Analysis/_inbox/`
4. Erstellt eine Markdown-Datei in `Resource Analysis/_inbox/` mit `type: inbox-episode` Frontmatter, allen Metadaten, YouTube-URL, eingebettetem Screenshot (`![[...]]`) und `## Transkript` Platzhalter

**Workflow-Integration**: Max kopiert die YouTube-URL in MacWhisper (oder nutzt YouTube-Untertitel), fügt das fertige Transkript in die Inbox-Datei ein, und ruft `/analyze-episode` auf. Da alle Metadaten bereits im Frontmatter stehen, überspringt `/analyze-episode` die Nachfragephase komplett. Das `podcast`-Feld wird mit dem YouTube-Kanal-Namen befüllt, da `/analyze-episode` dieses Feld für den Quellen-Ordner nutzt.

---

## Kernregeln

### Quellenangaben

Jede Information im Hub MUSS eine nachverfolgbare Quelle haben:

```markdown
> Quelle: [[Resource Analysis/Praxisflüsterer/ep-042-praxisbewertung/transkript-strukturiert#Ertragswertverfahren|Praxisflüsterer Ep.42 (Juni 2023)]]
```

- Obsidian-Wikilinks mit **vollem Pfad ab Vault-Root** (weil Dateinamen wie `transkript-strukturiert.md` in jeder Episode vorkommen)
- Erscheinungsdatum immer im Anzeigenamen
- Web-Recherche: `> Quelle: Web-Recherche (URL, recherchiert am DATUM)`
- Nie Informationen ohne Quelle in den Hub schreiben

### Zeitlicher Kontext

- Jede Episode hat ein Erscheinungsdatum im Frontmatter
- Relative Zeitangaben werden in absolute umgerechnet
- Bei Quellen älter als 2 Jahre: proaktiv darauf hinweisen
- Bei Widersprüchen: neuere Quelle steht oben, ältere darunter mit Obsidian-Callout `> [!warning] Zeitlicher Hinweis`
- Themen mit hoher zeitlicher Sensitivität (Marktpreise, Zinsen, Gehälter): Haltbarkeit nur 1-2 Jahre

### Obsidian-native Formatierung

Das System nutzt native Obsidian-Features:
- **Standard-Callouts**: `[!warning]` für Zeithinweise, `[!question]` für unklare Stellen, `[!example]-` für faltbare Transkript-Einbettungen
- **Custom-Callouts** (CSS in `.obsidian/snippets/custom-callouts.css`): `[!memorize]` (rot — Schlüsselzahlen), `[!concept]` (lila — Konzepte/Modelle), `[!speech]` (grün — Zitate), `[!expert]` (gold — Experten-Einordnung), `[!prereq]` (grau — Voraussetzungen), `[!diagram]` (teal — Diagramme). Werden primär in `gruendung-fokus`-Zusammenfassungen eingesetzt.
- **Nested Tags**: Hierarchische Tags wie `#finanzen/praxisbewertung` spiegeln die Hub-Kategorien wider
- **Embeds**: `![[...]]` bettet Transkript-Abschnitte in den Hub ein (immer in faltbare Callouts verpackt)
- **Bases**: `.base`-Dateien für dynamische, selbstaktualisierende Views (ersetzen NICHT die Markdown-Indizes)

### Dynamischer Hub (MOC-Splitting)

- Kategorien entstehen organisch aus dem Inhalt
- Wenn eine Hub-Datei >200 Zeilen hat oder 3+ Sub-Themen → Splitting in Ordner + MOC
- **Beim Splitting: alte Datei LÖSCHEN** (nicht neben dem Ordner stehen lassen)
- Alle Obsidian-Links in anderen Dateien aktualisieren
- Jede Änderung im `_hub-changelog.md` dokumentieren

### Namenskonventionen

- Episoden mit Nummer: `ep-NNN-titel-slug` (z.B. `ep-042-praxisbewertung`)
- Episoden ohne Nummer: `YYYY-MM-titel-slug` (z.B. `2024-03-mvz-aufbau`)
- Personen: `vorname-nachname.md` (ohne akademische Titel, ohne Umlaute)
- Keine Umlaute in Dateinamen (ä→ae, ö→oe, ü→ue, ß→ss)
- Keine Leerzeichen (Bindestriche verwenden)

---

## Fehlerbehandlung

- **Analyse-Abbruch**: Status auf `in-arbeit` setzen, erstellte Dateien behalten, bei Wiederaufruf Fortsetzung anbieten
- **Schlechte Transkript-Qualität**: Offensichtliche Fehler korrigieren, unsichere Stellen mit `[unklar]` markieren
- **Web-Recherche fehlgeschlagen**: Vermerken und normal weiterarbeiten (blockiert NIE die Analyse)
- **Fremdsprachige Transkripte**: Originalsprache beibehalten, alle anderen Dateien auf Deutsch

---

## Beziehung zwischen den Indizes

```
_hub-index.md (ZENTRALER EINSTIEG)
├── verlinkt auf → Hub-Kategorien / MOCs
├── verlinkt auf → _praxiskonzepte-index.md
└── verlinkt auf → _personen-index.md
```

Claude liest bei Fragen IMMER zuerst `_hub-index.md`. Von dort aus navigiert Claude zur passenden Kategorie, zum passenden Praxiskonzept oder zur passenden Person.

---

## YAML-Frontmatter

Jede Datei im System hat YAML-Frontmatter mit einem `type`-Feld. Die möglichen Typen:

| Type | Wo | Zweck |
|:-----|:---|:------|
| `inbox-episode` | `_inbox/` | Vorbereitete Episode von `/get-podcast-url` mit Metadaten + Audio-URL. Temporär — wird von `/analyze-episode` verarbeitet und gelöscht. |
| `episode-zusammenfassung` | Episoden-Ordner | Summary + Takeaways |
| `transkript-strukturiert` | Episoden-Ordner | Strukturiertes Transkript |
| `max-notizen` | Episoden-Ordner | Max' Gedanken |
| `web-recherche` | Episoden-Ordner | Internet-Recherche |
| `knowledge-hub` | `_knowledge-hub/` | Hub-Eintrag (Kategorie oder Sub-Thema) |
| `knowledge-hub-moc` | `_knowledge-hub/` | Map of Content nach Splitting |
| `hub-index` | `_knowledge-hub/` | Zentraler Index |
| `hub-changelog` | `_knowledge-hub/` | Änderungsprotokoll |
| `praxiskonzept` | `Praxis-Konzepte/[Name]/` | Praxis-Profil |
| `praxiskonzepte-index` | `Praxis-Konzepte/` | Übersicht aller Praxiskonzepte |
| `person` | `Praxis-Konzepte/Personen/` | Personen-Profil |
| `personen-index` | `Praxis-Konzepte/Personen/` | Übersicht aller Personen |
| `system-dokumentation` | `Resource Analysis/` | Diese Datei |

Zusätzlich: `.base`-Dateien (YAML, kein Frontmatter) für dynamische Obsidian-Views. Diese haben keinen `type`-Feld, da sie ein eigenes Format nutzen.

Vollständige Frontmatter-Schemas für jeden Typ: siehe `Plans/Knowledge-System-Plan.md`, Abschnitt 5.
Obsidian Base-Definitionen: siehe `Plans/Knowledge-System-Plan.md`, Abschnitt 15 (Obsidian-native Features).

---

## Dokumentations-Wartung (PFLICHT)

Dieses Dokument und die zugehörigen Referenzen MÜSSEN aktuell gehalten werden. Veraltete Doku ist schlimmer als keine Doku.

### Was wird aktuell gehalten?

| Dokument | Inhalt | Wann aktualisieren? |
|:---------|:-------|:--------------------|
| `CLAUDE.md` (Abschnitt Knowledge-System) | Kurzübersicht: Kernstruktur, Skills, Hauptregeln | Bei Änderungen an Kernstruktur, Skills oder Hauptregeln |
| `Resource Analysis/_system-overview.md` (diese Datei) | Vollständige Systemdoku | Bei JEDER System-Änderung |
| `Plans/Knowledge-System-Plan.md` | Implementierungsplan mit Details | Bei Änderungen an dort dokumentierten Regeln |

### Was ist eine "System-Änderung"?

**JA — Doku-Update nötig:**
- Neuer Skill hinzugefügt oder bestehender Skill geändert
- Neue Dateitypen eingeführt
- Workflow-Schritte geändert (Reihenfolge, neue Schritte, Schritte entfernt)
- Neue Regeln aufgestellt (z.B. neue Namenskonvention)
- Ordnerstruktur geändert (neue Ordner, umbenannte Ordner)
- Frontmatter-Schema geändert (neue Felder, entfernte Felder)
- Retrieval-Hierarchie geändert

**NEIN — Kein Doku-Update nötig:**
- Neue Episode analysiert (Routine)
- Neuer Hub-Eintrag geschrieben (Routine)
- Neue Kategorie im Hub angelegt (Routine — wird vom Hub-Index abgebildet)
- Hub-Kategorie gesplittet (Routine — wird vom Hub-Changelog abgebildet)
- Notizen bereinigt (Routine)
- Neues Personen- oder Praxisprofil erstellt (Routine)

### Wie wird aktualisiert?

Wenn Claude eine System-Änderung vornimmt, MUSS Claude im selben Arbeitsschritt:

1. Die Änderung umsetzen
2. `_system-overview.md` aktualisieren (diese Datei)
3. `CLAUDE.md` aktualisieren (nur wenn Kernstruktur/Skills/Hauptregeln betroffen)
4. `Plans/Knowledge-System-Plan.md` aktualisieren (nur wenn dort dokumentierte Details betroffen)
5. Das `letzte-aktualisierung` Datum im Frontmatter dieser Datei auf das aktuelle Datum setzen

**Das ist KEIN optionaler Schritt.** Wenn Claude eine System-Änderung macht aber die Doku nicht aktualisiert, ist das ein Fehler.

### Konsistenz-Check

Bei Unsicherheit, ob die Doku aktuell ist, kann Claude diese Prüfung durchführen:
- Stimmt die Ordnerstruktur in `_system-overview.md` mit der tatsächlichen Ordnerstruktur überein?
- Sind alle existierenden Skills in der Skill-Tabelle dokumentiert?
- Sind alle YAML-Frontmatter-Typen in der Typ-Tabelle aufgeführt?
- Stimmen die beschriebenen Workflow-Schritte mit den SKILL.md-Dateien überein?
