# Knowledge-System-Plan: Wissensmanagement

## Übersicht

Dieser Plan beschreibt das vollständige Wissensmanagement-System für dieses Repo. Er dient als Spezifikation, die Claude Code Schritt für Schritt umsetzen kann — von der Ordnerstruktur über die SKILL.md-Dateien bis zu den Templates.

## Kontext

Max baut ein Wissensmanagement-System in diesem Repo auf. Er hört sich regelmäßig Podcasts und schaut YouTube-Videos zum Thema Zahnmedizin-Unternehmertum an (Praxisgründung, MVZ-Strukturen, Mitarbeiterführung, profitable Bereiche, Skalierung, etc.). Das Problem: Zu viel Wissen geht verloren, weil man sich nicht alles merken kann.

Das Repo wird auch als **Obsidian-Vault** genutzt. Alle Markdown-Dateien müssen Obsidian-kompatibel sein. Der Vault-Root ist das Repo-Root (`farmerville/`).

**Übergeordnetes Ziel**: Alles sammeln und strukturieren, was Max hilft, eine erfolgreiche Zahnarztpraxis aufzubauen und zu skalieren.

---

## Was das System leisten soll

### 1. Episoden-Upload & automatische Verarbeitung

Max legt ein Transkript als Markdown-Datei in `Resource Analysis/_inbox/` ab (oder irgendwo im Repo — jeder Ort funktioniert). Dann ruft Max den Skill auf: `/analyze-episode Resource Analysis/_inbox/mein-transkript.md`

Max muss KEINEN Ordner anlegen und KEINE Namenskonventionen kennen. Claude übernimmt das komplett.

**Was der Skill der Reihe nach tut:**

0. **Setup — Metadaten sammeln und Ordner erstellen** (Claude macht das):
   - Transkript lesen und Metadaten extrahieren (Podcast-Name, Episodennummer, Titel, Erscheinungsdatum)
   - Was Claude nicht findet → bei Max nachfragen (ALLES auf einmal, nicht Stück für Stück)
   - Episoden-Ordner erstellen nach Namenskonventionen (siehe Abschnitt ›Namenskonventionen‹)
   - Transkript aus `_inbox/` in den Episoden-Ordner verschieben als `transkript.md`
   - Re-Analyse prüfen: Falls Ziel-Ordner schon existiert → Max fragen ob überschreiben oder abbrechen

1. **Transkript-Format erkennen und normalisieren**: Transkripte kommen in verschiedenen Formaten:
   - Mit Zeitstempeln (`[00:12:34]`) → beibehalten als Referenz
   - Mit Sprechernamen (`Host:`, `Gast:`) → beibehalten und nutzen
   - Roh-Text ohne Struktur → Claude identifiziert Sprecher wo möglich
   - Bei schlechter Qualität (Spracherkennungsfehler): offensichtliche Fehler korrigieren, unsichere Stellen mit `[unklar]` markieren
   - Das normalisierte Transkript wird als `transkript-strukturiert.md` gespeichert

2. **Transkript strukturieren**: In thematische Abschnitte unterteilen mit klaren Überschriften (als `## Abschnitt-Name`), sodass jeder Abschnitt per Obsidian-Link referenzierbar ist

3. **Zeitliche Einordnung**: Aussagen mit relativen Zeitbezügen ("aktuell", "dieses Jahr", "gerade", "momentan") werden mit dem konkreten Zeitraum annotiert (z.B. "der aktuelle Markt [Stand: Q1 2023]")

4. **Zusammenfassung erstellen**: Executive Summary + Key Takeaways, immer mit Erscheinungsdatum im Header. Bei fremdsprachigem Transkript: Zusammenfassung auf Deutsch.

5. **Notiz-Datei erstellen**: Vorbereitete Markdown-Datei für Max' eigene Gedanken (Grundstruktur mit Headings basierend auf den Themen der Episode, aber leerem Inhalt)

6. **Personen & Praxen identifizieren**: Erkennen, ob eine Praxis vorgestellt oder Person interviewt wird (Details siehe Abschnitte ›Praxiskonzepte-Referenz‹ und ›Personen- & Web-Recherche‹)

7. **Web-Recherche durchführen**: Zu identifizierten Personen und Praxen (Details siehe Abschnitt ›Personen- & Web-Recherche‹). Falls die Web-Recherche fehlschlägt: Vermerken und mit der restlichen Analyse fortfahren. Web-Recherche darf die Analyse NICHT blockieren.

8. **Knowledge-Hub aktualisieren**: Relevante Erkenntnisse in die Hub-Dateien eintragen (ANHÄNGEN, nicht überschreiben), mit zeitlicher Einordnung und Quellenangaben

9. **Struktur-Check**: Prüfen, ob die Hub-Struktur noch passt oder angepasst werden muss (Details siehe Abschnitt ›Dynamischer Knowledge-Hub‹)

10. **Abschluss-Bericht ausgeben**: Am Ende der Analyse gibt Claude eine Zusammenfassung an Max aus:
    ```
    Episode analysiert: Praxisflüsterer Ep.42 - Praxisbewertung (Juni 2023)
    Transkript verschoben nach: Resource Analysis/Praxisfluesterer/ep-042-praxisbewertung/
    Transkript strukturiert (14 Abschnitte)
    Zusammenfassung erstellt
    Hub aktualisiert: finanzen, praxiskonzepte (2 Kategorien)
    Praxiskonzept erkannt: Dental21 → Concepts/Dental21/profil.md
    Person erkannt: Dr. Stefan Müller → Concepts/Personen/stefan-mueller.md
    Web-Recherche: 4 Quellen gefunden
    Max-Notizen: max-notizen.md erstellt (leer, wartet auf Max)
    ```

### 2. Quellenreferenzierung (Obsidian-Wikilinks)

**Kernprinzip**: Jede Information im Knowledge-Hub muss nachverfolgbar sein - wie Fußnoten in einer Doktorarbeit.

**WICHTIG - Obsidian-Pfade**: Da Dateinamen wie `transkript-strukturiert.md` in JEDER Episode vorkommen, müssen Wikilinks den **vollen Pfad ab Vault-Root** verwenden, damit Obsidian die richtige Datei findet.

**Format im Knowledge-Hub:**
```markdown
### Praxiswert-Berechnung nach Ertragswertverfahren

Das Ertragswertverfahren basiert auf dem durchschnittlichen Gewinn der letzten 3 Jahre...
[Detaillierte Erklärung der Erkenntnis]

> Quelle: [[Resource Analysis/Praxisflüsterer/ep-042-praxisbewertung/transkript-strukturiert#Ertragswertverfahren|Praxisflüsterer Ep.42 (Juni 2023)]]
```

**Zeitstempel sind immer Teil der Quellenangabe** - das `(Juni 2023)` am Ende zeigt sofort, wie aktuell die Information ist.

**So funktioniert es in Obsidian:**
- `[[Voller/Pfad/zur/Datei#Überschrift|Anzeigename]]` erzeugt einen klickbaren Link
- Max klickt auf die Quelle → Obsidian springt direkt zur Stelle im strukturierten Transkript
- Max kann sofort verifizieren, ob die Information korrekt wiedergegeben ist
- Backlinks in Obsidian zeigen umgekehrt: "Welche Hub-Einträge referenzieren diese Episode?"

**Regeln für Quellenangaben:**
- Jeder inhaltliche Absatz im Knowledge-Hub MUSS eine Quellenangabe haben
- Wenn mehrere Episoden die gleiche Erkenntnis bestätigen, werden ALLE Quellen aufgeführt
- Max' eigene Notizen: `> Quelle: [[Resource Analysis/.../max-notizen|Max' Notizen zu Ep.42]]`
- Web-Recherche: `> Quelle: Web-Recherche (URL, recherchiert am DATUM)`
- Nie Informationen ohne Quelle in den Hub schreiben

### 3. Zeitlicher Kontext & Aktualitätsgewichtung

**Kernprinzip**: Informationen verändern sich über die Zeit. Der Zahnmedizin-Markt 2022 ist nicht der Markt 2026. Das System muss das abbilden.

**Zeitliche Einordnung bei der Analyse:**
- Jede Episode hat ein Erscheinungsdatum im YAML-Frontmatter (`erschienen: 2023-06`)
- Wenn im Podcast gesagt wird "aktuell sind die Praxispreise hoch" → wird annotiert als "Praxispreise hoch [Stand: Q2 2023]"
- Relative Zeitangaben ("letztes Jahr", "vor drei Jahren") werden in absolute umgerechnet basierend auf dem Erscheinungsdatum

**Zeitliche Sensitivität nach Themenbereich:**

Nicht alle Themen altern gleich schnell. Claude unterscheidet:

| Sensitivität | Themenbeispiele | Haltbarkeit |
|:------------|:----------------|:------------|
| **Hoch** - veraltet schnell | Marktpreise, Zinsen, Regulierung, KV-Richtlinien, Gehälter, Förderprogramme | 1-2 Jahre |
| **Mittel** - verändert sich | Personalmarkt, Marketing-Kanäle, Technologie, Patientenverhalten | 2-4 Jahre |
| **Niedrig** - bleibt stabil | Führungsprinzipien, Praxisorganisation, Behandlungskonzepte, Skalierungsstrategien | 5+ Jahre |

**Widersprüche zwischen Episoden:**

Wenn zwei Episoden sich widersprechen, IMMER den zeitlichen Kontext einbeziehen:

```markdown
### Praxispreise in Deutschland

**Neuere Einschätzung (2024):** Der Markt hat sich abgekühlt, Praxispreise sind um ~15% gesunken.
> Quelle: [[Resource Analysis/.../ep-089/transkript-strukturiert#Marktentwicklung|Praxisflüsterer Ep.89 (März 2024)]]

**Frühere Einschätzung (2022):** Praxispreise auf Allzeithoch, Verkäufermarkt.
> Quelle: [[Resource Analysis/.../ep-042/transkript-strukturiert#Marktlage|Praxisflüsterer Ep.42 (Juni 2022)]]

> [!warning] Zeitlicher Hinweis
> Diese Aussagen widersprechen sich. Die neuere Information (2024) spiegelt die aktuelle Marktlage wider. Die ältere Information (2022) zeigt den historischen Kontext.
```

**Regeln für zeitliche Gewichtung:**
- Neuere Informationen werden als relevanter eingestuft, BESONDERS bei hoch-sensitiven Themen
- Ältere Informationen werden NICHT gelöscht, sondern als historischer Kontext erhalten
- Bei Widersprüchen: Neuere Quelle steht oben, ältere darunter mit Obsidian-Callout `> [!warning] Zeitlicher Hinweis`
- Claude weist Max bei Fragen proaktiv darauf hin, wenn die verfügbaren Infos älter als 2 Jahre sind

### 4. Dynamischer Knowledge-Hub (NICHT statisch)

**Kernprinzip**: Die Kategorien sind NICHT fest vorgegeben. Sie entstehen organisch aus dem Inhalt und entwickeln sich weiter.

**Wie Kategorien entstehen und sich entwickeln:**

1. **Start**: Der Hub startet leer. Die ersten 3-5 Episoden formen die initialen Kategorien basierend auf den tatsächlichen Inhalten.

2. **Bei jeder neuen Episode** prüft `/analyze-episode` automatisch:
   - Passt der Inhalt in bestehende Kategorien? → Dort eintragen
   - Gibt es ein Thema, das nirgends hinpasst? → Neue Kategorie vorschlagen und anlegen
   - Wird eine Kategorie zu breit/überladen? → Sub-Kategorien vorschlagen (Splitting)
   - Überlappen zwei Kategorien stark? → Zusammenlegung vorschlagen (Merging)

3. **Struktur-Evolution protokollieren**: Änderungen an der Hub-Struktur werden in `_hub-changelog.md` dokumentiert, damit nachvollziehbar bleibt, warum was umstrukturiert wurde.

4. **Leitfrage** für jede Kategorisierung: "Hilft diese Struktur Max dabei, schnell die Information zu finden, die er braucht, um eine erfolgreiche Praxis aufzubauen und zu skalieren?"

**MOC-Struktur (Map of Content) für Skalierung:**

Statt einer einzelnen riesigen Datei pro Thema verwendet der Hub eine MOC-Struktur, aber erst wenn nötig:

```
_knowledge-hub/
├── _hub-index.md              # Top-Level-Übersicht: alle Kategorien + Beschreibung
├── _hub-changelog.md          # Protokoll der Struktur-Änderungen
├── finanzen.md                # Startet als EINE Datei
├── finanzen/                  # Wenn Splitting nötig: finanzen.md wird GELÖSCHT...
│   ├── _finanzen-moc.md       # ...und der Inhalt hierhin migriert (MOC + Links)
│   ├── praxisbewertung.md     # Sub-Thema mit allen Erkenntnissen dazu
│   ├── finanzierung.md        # Sub-Thema
│   └── roi-analyse.md         # Sub-Thema
└── [neue-kategorie]/          # Entsteht dynamisch
    └── ...
```

**Regeln für die MOC-Struktur:**
- Jede Kategorie startet als EINE Datei (z.B. `finanzen.md`)
- Sobald eine Datei zu groß wird (>200 Zeilen) oder 3+ deutliche Sub-Themen hat → automatisch in Ordner + MOC + Sub-Dateien splitten
- **WICHTIG: Beim Splitting wird die ursprüngliche Datei (z.B. `finanzen.md`) GELÖSCHT.** Der Inhalt wird in die MOC-Datei und die Sub-Themen-Dateien migriert. Es darf NICHT gleichzeitig `finanzen.md` und `finanzen/` existieren, da dies zu mehrdeutigen Obsidian-Links führt.
- Die MOC-Datei (`_finanzen-moc.md`) enthält nur eine Übersicht + Links zu den Sub-Themen
- Sub-Themen-Dateien enthalten die eigentlichen Erkenntnisse mit Quellenangaben
- Beim Splitting: Alle bestehenden Obsidian-Links in anderen Dateien müssen aktualisiert werden (per Grep alle Verweise suchen und anpassen). Jede Link-Änderung im `_hub-changelog.md` dokumentieren.

### 5. YAML-Frontmatter auf jeder Datei

Jede Markdown-Datei im System bekommt YAML-Frontmatter. Das ermöglicht:
- **Obsidian Graph View**: Verbindungen zwischen Episoden, Themen und Konzepten visualisieren
- **Obsidian Tag-Suche**: Schnelles Filtern nach Typ, Quelle, Kategorie
- **Obsidian Bases**: Dynamische, selbstaktualisierende Views und Tabellen basierend auf Frontmatter-Properties (Details siehe Abschnitt ›Obsidian-native Features‹)
- **Claude-Retrieval**: Maschinenlesbare Metadaten für effiziente Suche

**Inbox-Episode (erstellt von `/get-podcast-url`):**
```yaml
---
type: inbox-episode
podcast: "Praxisflüsterer"
episode: 1
titel: "#1: Der Präsident - Prof. Dr. Roland Frankenberger"
erschienen: "2020-12"
gast: "Prof. Dr. Roland Frankenberger"
dauer: "1 hr 2 min"
audio-url: "https://audio.podigee-cdn.net/..."
screenshot: "praxisfluesterer-ep-001-screenshot.png"
---
```

Dieser Typ ist **temporär** — er existiert nur in `_inbox/` und wird von `/analyze-episode` verarbeitet und gelöscht. Die Metadaten werden direkt in die Analyse übernommen, sodass Max keine Nachfragen beantworten muss.

**Episode-Zusammenfassung:**
```yaml
---
type: episode-zusammenfassung
status: komplett              # komplett | in-arbeit | fehlgeschlagen
quelle: Praxisflüsterer
episode: 42
titel: "Praxisbewertung - Was ist meine Praxis wert?"
erschienen: 2023-06
analysiert: 2026-02-15
personen: ["Dr. Stefan Müller"]
praxen: ["Dental21"]
kategorien: ["finanzen", "praxiskonzepte"]
tags: [finanzen/praxisbewertung, finanzen/ertragswert, goodwill]
zeitlich-sensitiv: ["Marktpreise"]
aliases: ["Ep.42", "Praxisbewertung-Episode"]
---
```

**Strukturiertes Transkript:**
```yaml
---
type: transkript-strukturiert
quelle: Praxisflüsterer
episode: 42
erschienen: 2023-06
analysiert: 2026-02-15
sprecher: ["Host", "Dr. Stefan Müller"]
abschnitte: 14
hat-zeitstempel: true
sprache: de                   # de | en | etc.
---
```

**Max-Notizen:**
```yaml
---
type: max-notizen
quelle: Praxisflüsterer
episode: 42
erstellt: 2026-02-15
bereinigt: false              # true nach /clean-notes
roh-version: null             # Pfad zur Roh-Version nach Bereinigung
---
```

**Web-Recherche:**
```yaml
---
type: web-recherche
quelle: Praxisflüsterer
episode: 42
personen: ["Dr. Stefan Müller"]
praxen: ["Dental21"]
recherche-datum: 2026-02-20
quellen-count: 4
---
```

**Knowledge-Hub-Datei:**
```yaml
---
type: knowledge-hub
kategorie: finanzen
sub-thema: praxisbewertung
letzte-aktualisierung: 2026-02-15
episoden-count: 3
aelteste-quelle: 2022-03
neueste-quelle: 2024-11
---
```

**MOC-Datei:**
```yaml
---
type: knowledge-hub-moc
kategorie: finanzen
sub-themen: ["praxisbewertung", "finanzierung", "roi-analyse"]
letzte-aktualisierung: 2026-02-15
---
```

**Hub-Index:**
```yaml
---
type: hub-index
letzte-aktualisierung: 2026-02-15
kategorien-count: 5
episoden-total: 12
---
```

**Hub-Changelog:**
```yaml
---
type: hub-changelog
letzte-aenderung: 2026-02-15
---
```

**Praxiskonzept-Profil:**
```yaml
---
type: praxiskonzept
praxis: "Dental21"
gruender: "Dr. Stefan Müller"
standorte: ["Berlin", "München", "Hamburg"]
rechtsform: MVZ
spezialisierung: ["Allgemeinzahnheilkunde", "Implantologie"]
gruendungsjahr: 2018
episoden: ["Praxisflüsterer/ep-042"]
info-stand: 2023-06
web-recherche-datum: 2026-02-20
aliases: ["Dental 21", "Dental21 GmbH"]
---
```

**Personen-Profil:**
```yaml
---
type: person
name: "Dr. Stefan Müller"
rolle: "Gründer & Geschäftsführer"
unternehmen: "Dental21"
episoden: ["Praxisflüsterer/ep-042", "Praxisflüsterer/ep-089"]
expertise: ["MVZ-Aufbau", "Skalierung", "Implantologie"]
web-recherche-datum: 2026-02-20
aliases: ["Stefan Müller", "Dr. Müller"]
---
```

### 6. Effizientes Retrieval für Claude

Das System muss so gebaut sein, dass Claude bei Fragen von Max effizient arbeiten kann:

- **Stufe 1 - Hub-Index**: Claude liest `_hub-index.md` (kompakt, wenige KB) → identifiziert relevante Kategorien
- **Stufe 2 - MOC/Kategorie-Datei**: Claude liest die passende Kategorie- oder MOC-Datei → findet das richtige Sub-Thema
- **Stufe 3 - Sub-Thema**: Claude liest die spezifische Sub-Themen-Datei → hat konsolidiertes Wissen + Quellen
- **Stufe 4 - Zusammenfassung**: Bei Bedarf die Episode-Zusammenfassung für mehr Kontext
- **Stufe 5 - Transkript**: Nur wenn wirklich nötig, das volle strukturierte Transkript
- **Kein Kontext-Overload**: Bei 50+ Episoden muss Claude NICHT alle Transkripte laden

### 7. Automatische Notizen-Bereinigung (Skill: `/clean-notes`)

Max spricht seine Notizen oft per Diktat in `max-notizen.md` ein. Diese Roh-Notizen sind dann unstrukturiert, haben Füllwörter, unvollständige Sätze etc.

**Skill `/clean-notes`** wird manuell ausgelöst: `/clean-notes Pfad/zur/max-notizen.md`

Was der Skill tut:
- **Struktur**: Gedanken in logische Abschnitte mit Überschriften unterteilen
- **Bereinigung**: Füllwörter entfernen, Sätze vervollständigen, Diktat-Artefakte korrigieren
- **Kern bewahren**: Max' eigene Meinungen und Gedanken NICHT verändern oder uminterpretieren - nur die Form verbessern, nicht den Inhalt
- **Markierung**: Am Anfang der Datei vermerken: `> Bereinigt am [Datum] - Original-Gedanken von Max, sprachlich überarbeitet`
- **Roh-Version sichern**: Vor der Bereinigung das Original als `max-notizen-roh.md` kopieren, damit nichts verloren geht. Das Roh-Backup wird IMMER erstellt — egal ob Max diktiert oder getippt hat.
- **Frontmatter aktualisieren**: `bereinigt: true` setzen und `roh-version: max-notizen-roh.md` eintragen
- **Knowledge-Hub aktualisieren**: Relevante Erkenntnisse aus Max' Notizen in die Hub-Dateien eintragen mit Quelle `[[Resource Analysis/.../max-notizen|Max' Notizen]]`
- **Gleiche Hub-Regeln wie bei Episoden**: Für Hub-Einträge aus Max' Notizen gelten die gleichen Quellen-, Zeit- und Widerspruchsregeln wie für Episode-basierte Einträge (siehe Abschnitte 2, 3, 4)

### 8. Personen-Verzeichnis

Neben dem Praxiskonzepte-Ordner gibt es ein **Personen-Verzeichnis** für wiederkehrende Experten und Interview-Gäste.

**Warum**: Dieselbe Person kann in mehreren Episoden auftauchen. Dr. Müller wird vielleicht in Ep.42 über Praxisbewertung interviewt und in Ep.89 über Skalierung. Ohne Zusammenführung gehen diese Querverbindungen verloren.

**Wie es funktioniert:**
- Bei jeder Episode prüft Claude: Existiert für diese Person bereits ein Profil?
  - **Vor dem Erstellen** MUSS Claude den Personen-Index UND bestehende `aliases`-Felder im Frontmatter prüfen, um Duplikate zu vermeiden (z.B. "Dr. Stefan Müller" vs. "Stefan Müller" vs. "Herr Müller" könnten dieselbe Person sein)
  - **Ja** → Profil ergänzen:
    - `episoden`-Array im Frontmatter erweitern
    - `info-stand` aktualisieren wenn neuere Infos vorliegen
    - Neue Expertise-Bereiche hinzufügen
    - Bei widersprüchlichen Infos (z.B. Rollenwechsel): Beide Versionen mit zeitlicher Einordnung dokumentieren
    - Neue `aliases` ergänzen wenn die Person in der neuen Episode anders benannt wird
  - **Nein** → Neues Profil erstellen unter `Concepts/Personen/vorname-nachname.md`
- Profil enthält: Steckbrief, Expertise, alle Episoden in denen die Person vorkommt, Web-Recherche-Ergebnisse
- Querverweise: Profil ↔ Episoden ↔ Praxiskonzept (wenn vorhanden)

**Dateistruktur:** Personen-Profile sind einzelne Dateien (keine Unterordner), da ein Profil typischerweise kompakt bleibt. Sollte ein Profil durch viele Episoden sehr umfangreich werden (>200 Zeilen), kann es nach dem gleichen MOC-Prinzip wie beim Knowledge-Hub in einen Ordner umgewandelt werden.

### 9. Praxiskonzepte-Referenz (automatisch bei Episode-Analyse)

Viele Episoden stellen ein konkretes Praxiskonzept vor: Ein Gründer präsentiert seine Praxis, wie er sie aufgebaut hat, skaliert hat, etc.

**Wenn `/analyze-episode` erkennt, dass eine Praxis vorgestellt wird**, passiert automatisch:

1. **Praxis identifizieren**: Name der Praxis, Gründer/Inhaber, Standort(e)
2. **Existenz prüfen**: Gibt es bereits ein Profil für diese Praxis in `Concepts/`?
   - **Ja** → Profil ergänzen mit neuen Infos aus dieser Episode
   - **Nein** → Neues Profil erstellen
3. **Web-Recherche**: Claude sucht automatisch nach:
   - Website der Praxis
   - Weitere Infos zum Gründer (LinkedIn, Interviews, etc.)
   - Größe, Standorte, Spezialisierung
   - Öffentlich verfügbare Informationen zum Geschäftsmodell
4. **Praxiskonzept-Profil erstellen/updaten** unter `Concepts/[Praxisname]/profil.md`:
   - YAML-Frontmatter mit Steckbrief-Daten (siehe Abschnitt ›YAML-Frontmatter‹)
   - Geschäftsmodell: Rechtsform, Spezialisierung, Alleinstellungsmerkmal
   - Skalierungsstrategie: Wie wurde gewachsen? (Filialen, MVZ, Übernahmen)
   - Key Learnings: Was kann Max daraus mitnehmen?
   - Quellen: Obsidian-Links zur Episode + Web-URLs
5. **Querverweise**: Profil ↔ Episode-Zusammenfassung ↔ Personen-Profil
6. **Praxiskonzepte-Index aktualisieren**: `_praxiskonzepte-index.md` ergänzen

### 10. Automatische Personen- & Web-Recherche pro Episode

Bei JEDER Episode (nicht nur bei Praxisvorstellungen) prüft `/analyze-episode`:

- **Wer wird interviewt?** Name, Rolle, Unternehmen der interviewten Person(en)
- **Web-Recherche auslösen**: Claude sucht automatisch nach relevanten Zusatzinfos:
  - Hintergrund der Person (Karriere, Expertise, Veröffentlichungen)
  - Aktuelle Entwicklungen bei deren Praxis/Unternehmen
  - Andere Interviews/Auftritte derselben Person (für Querverweise)
- **Fallback bei fehlgeschlagener Web-Recherche**: Vermerken "Keine Web-Ergebnisse gefunden" und normal weiterarbeiten. Falls WebFetch fehlschlägt → automatisch WebSearch als Fallback nutzen.
- **In Episode-Ordner speichern**: Neue Datei `web-recherche.md` im Episoden-Ordner mit:
  - YAML-Frontmatter (siehe Abschnitt ›YAML-Frontmatter‹)
  - Strukturierte Infos über die Person(en)
  - Alle gefundenen Web-Quellen mit URLs und Datum der Recherche
  - Klare Trennung: "Aus dem Transkript" vs. "Aus Web-Recherche"
- **Quellenangaben**: Web-Recherche-Infos die in den Hub fließen, werden immer markiert als:
  ```markdown
  > Quelle: Web-Recherche zu Dr. Müller (URL, recherchiert am 2026-02-20)
  ```

### 11. Wissensabfrage — Skill `/ask-knowledge`

Max kann jederzeit Fragen an das gesammelte Wissen stellen: `/ask-knowledge Wie funktioniert das Ertragswertverfahren bei Praxisbewertungen?`

**Was der Skill tut:**

1. **Hub-Index lesen**: `_hub-index.md` laden → relevante Kategorien identifizieren
2. **Kategorie-Dateien lesen**: Passende Hub-Datei(en) oder MOC(s) laden → relevante Sub-Themen identifizieren
3. **Sub-Themen lesen**: Spezifische Sub-Themen-Dateien laden → konsolidiertes Wissen + Quellen
4. **Bei Bedarf vertiefen**: Episode-Zusammenfassungen oder Transkripte nur laden, wenn die Hub-Infos nicht ausreichen
5. **Personen/Praxen einbeziehen**: Bei Fragen zu Personen oder Praxen die entsprechenden Indizes und Profile einbeziehen
6. **Antwort formulieren**: Basierend auf dem gesammelten Wissen antworten

**Regeln für die Antwort:**
- **Quellenangaben immer mitliefern**: Jede Aussage mit Quelle belegen (Episode + Datum)
- **Zeitliche Einordnung**: Wenn die relevanten Quellen älter als 2 Jahre sind, proaktiv darauf hinweisen: *"Hinweis: Diese Information stammt aus [Datum]. Der aktuelle Stand könnte abweichen."*
- **Widersprüche transparent machen**: Wenn verschiedene Quellen sich widersprechen, BEIDE Perspektiven nennen mit zeitlicher Einordnung (neuere Quelle zuerst)
- **Wissenslücken benennen**: Wenn der Hub keine Informationen zum Thema hat, ehrlich sagen: *"Dazu habe ich im Knowledge-Hub noch keine Informationen. Das Thema wurde in den bisher analysierten Episoden nicht behandelt."*
- **Kein Kontext-Overload**: Nie alle Transkripte laden — immer die Hub-Hierarchie nutzen (Index → MOC → Sub-Thema → Zusammenfassung → Transkript)

### 12. Fehlerbehandlung & Edge Cases

**Transkript-Probleme:**
- **Sehr langes Transkript (>50.000 Wörter)**: Claude verarbeitet das Transkript in Abschnitten. Erst die Struktur erstellen (Überschriften), dann abschnittsweise zusammenfassen. Falls das Context-Limit erreicht wird: Status auf `in-arbeit` setzen, bisherige Ergebnisse speichern und Max informieren, welche Schritte noch ausstehen.
- **Schlechte Transkript-Qualität** (viele Spracherkennungsfehler): Claude korrigiert offensichtliche Fehler im strukturierten Transkript, markiert aber unsichere Stellen mit `[unklar]`. In der Zusammenfassung nur Informationen verwenden, die eindeutig verständlich sind.
- **Keine Sprecher identifizierbar**: Im strukturierten Transkript als `Sprecher 1`, `Sprecher 2` etc. labeln. In der Zusammenfassung vermerken: *"Sprecher konnten nicht eindeutig identifiziert werden."*
- **Fremdsprachiges Transkript**: Transkript in Originalsprache strukturieren. Zusammenfassung, Hub-Einträge und alle anderen Dateien auf Deutsch verfassen.

**Analyse-Abbruch:**
- Wenn eine Analyse aus beliebigem Grund abbricht (Context-Limit, Fehler, Abbruch durch Max):
  - `status: in-arbeit` im Frontmatter der Zusammenfassung setzen
  - Bereits erstellte Dateien NICHT löschen
  - Im Abschluss-Bericht klar auflisten, was fertig ist und was fehlt
  - Bei erneutem Aufruf: Claude erkennt den Status und bietet an, die Analyse fortzusetzen statt neu zu starten

**Web-Recherche-Fehler:**
- Alle Web-Recherche-Fehler werden in `web-recherche.md` dokumentiert (z.B. "Keine Ergebnisse zu [Person]")
- Web-Recherche blockiert NIE die restliche Analyse
- Falls WebFetch fehlschlägt → automatisch WebSearch als Fallback nutzen

### 13. Dokumentations-Wartung (PFLICHT)

**Problem**: Das System hat drei Dokumentationsebenen: `CLAUDE.md` (Kurzübersicht, wird automatisch geladen), `Resource Analysis/_system-overview.md` (vollständige Systemdoku) und dieser Plan. Wenn das System sich weiterentwickelt aber die Doku nicht mitgezogen wird, arbeitet Claude Code mit veralteten Informationen — das ist schlimmer als keine Doku.

**Regel**: Wenn Claude eine **System-Änderung** vornimmt, MUSS Claude im selben Arbeitsschritt die betroffene Dokumentation aktualisieren.

**Was ist eine System-Änderung (Doku-Update nötig)?**
- Neuer Skill hinzugefügt oder bestehender Skill geändert
- Neue Dateitypen eingeführt oder Frontmatter-Schema geändert
- Workflow-Schritte geändert (Reihenfolge, neue Schritte, Schritte entfernt)
- Neue Regeln aufgestellt oder bestehende geändert
- Ordnerstruktur geändert
- Retrieval-Hierarchie geändert

**Was ist KEINE System-Änderung (kein Doku-Update nötig)?**
- Neue Episode analysiert (Routine)
- Hub-Eintrag geschrieben oder Kategorie angelegt (Routine)
- Hub-Kategorie gesplittet (wird vom Hub-Changelog abgebildet)
- Notizen bereinigt, Profil erstellt (Routine)

**Welche Dateien bei System-Änderungen aktualisieren?**

| Dokument | Wann aktualisieren? |
|:---------|:--------------------|
| `Resource Analysis/_system-overview.md` | Bei JEDER System-Änderung |
| `CLAUDE.md` (Abschnitt Knowledge-System) | Nur wenn Kernstruktur, Skills oder Hauptregeln betroffen |
| `Plans/Knowledge-System-Plan.md` (dieser Plan) | Wenn hier dokumentierte Details betroffen sind |

**Konsistenz-Check bei Unsicherheit:**
- Stimmt die Ordnerstruktur in `_system-overview.md` mit der tatsächlichen überein?
- Sind alle existierenden Skills dokumentiert?
- Sind alle YAML-Frontmatter-Typen aufgeführt?
- Stimmen die Workflow-Schritte mit den SKILL.md-Dateien überein?

### 14. Skalierungsstrategie

**Problem**: Bei 50+ Episoden wächst das System. Claude darf NICHT bei jeder Frage alle Dateien laden.

**Strategie:**

1. **Hub-Index als Einstiegspunkt**: `_hub-index.md` bleibt kompakt (<100 Zeilen). Enthält nur Kategorie-Namen + 1-Satz-Beschreibung + Verweis auf Hub-Datei/MOC. Claude liest IMMER zuerst den Index.

2. **MOC-Splitting konsequent nutzen**: Sobald eine Hub-Datei >200 Zeilen hat → automatisch splitten. So bleibt jede Einzeldatei handhabbar.

3. **Frontmatter als Filter**: Claude nutzt `episoden-count`, `neueste-quelle`, `aelteste-quelle` im Hub-Frontmatter, um schnell einzuschätzen, wie viel Material zu einem Thema existiert und wie aktuell es ist — ohne die Datei komplett zu lesen.

4. **5-Stufen-Retrieval einhalten**: Immer die Hierarchie respektieren (Index → MOC → Sub-Thema → Zusammenfassung → Transkript). Transkripte sind die LETZTE Stufe, nicht die erste.

5. **Personen- und Praxiskonzepte-Indizes**: `_personen-index.md` und `_praxiskonzepte-index.md` als kompakte Verzeichnisse. Claude liest bei Personen-/Praxisfragen zuerst den entsprechenden Index, nicht alle Profile.

### 15. Obsidian-native Features

Das System nutzt Obsidian-spezifische Features für eine reichhaltigere Erfahrung. Diese ergänzen die Markdown-basierten Index-Dateien, ersetzen sie aber NICHT (Claude braucht die Markdown-Indizes für effizientes Retrieval).

#### Obsidian Bases (`.base`-Dateien)

Bases sind dynamische Views, die sich automatisch aus Frontmatter-Properties aktualisieren. Sie ersetzen NICHT die Markdown-Indizes — sie ergänzen sie für Max' interaktive Nutzung in Obsidian.

**Folgende Base-Dateien werden erstellt:**

**`Resource Analysis/_episoden.base`** — Alle Episoden im Überblick:
```yaml
filters:
  and:
    - 'type == "episode-zusammenfassung"'

formulas:
  alter: '(now() - date(erschienen + "-01")).days'
  alter_text: 'if(erschienen, date(erschienen + "-01").relative(), "")'

properties:
  quelle:
    displayName: "Quelle"
  formula.alter_text:
    displayName: "Alter"

views:
  - type: table
    name: "Alle Episoden"
    order:
      - file.name
      - quelle
      - erschienen
      - status
      - kategorien
      - personen
    groupBy:
      property: quelle
      direction: ASC

  - type: table
    name: "Zuletzt analysiert"
    order:
      - file.name
      - quelle
      - erschienen
      - analysiert
      - status
```

**`Concepts/Personen/_personen.base`** — Alle Personen:
```yaml
filters:
  and:
    - 'type == "person"'

formulas:
  episoden_count: 'if(episoden, episoden.length, 0)'

properties:
  formula.episoden_count:
    displayName: "Episoden"

views:
  - type: table
    name: "Alle Personen"
    order:
      - file.name
      - rolle
      - unternehmen
      - formula.episoden_count
      - expertise
```

**`Concepts/_praxiskonzepte.base`** — Alle Praxiskonzepte:
```yaml
filters:
  and:
    - 'type == "praxiskonzept"'

views:
  - type: cards
    name: "Praxiskonzepte"
    order:
      - file.name
      - gruender
      - rechtsform
      - standorte
      - spezialisierung
```

**`Resource Analysis/_knowledge-hub/_hub-dashboard.base`** — Hub-Übersicht:
```yaml
filters:
  and:
    - 'type == "knowledge-hub"'

views:
  - type: table
    name: "Hub-Kategorien"
    order:
      - file.name
      - kategorie
      - episoden-count
      - neueste-quelle
      - aelteste-quelle
      - letzte-aktualisierung
    summaries:
      episoden-count: Sum
```

**Regeln für Bases:**
- Bases werden einmal initial erstellt und müssen danach NICHT manuell gepflegt werden (sie aktualisieren sich automatisch aus dem Frontmatter)
- Neue Bases erstellen wenn ein neuer Dateityp eingeführt wird
- Bases können in andere Markdown-Dateien eingebettet werden: `![[_episoden.base#Alle Episoden]]`

#### Obsidian Callouts

Statt Emoji-basierter Markierungen verwendet das System native Obsidian-Callouts. Die wichtigsten im Knowledge-System:

```markdown
> [!warning] Zeitlicher Hinweis
> Diese Information stammt aus 2022. Der aktuelle Stand könnte abweichen.

> [!question] Unklar
> Diese Stelle im Transkript konnte nicht eindeutig interpretiert werden.

> [!tip] Key Takeaway
> Kernaussage aus der Episode.

> [!example]- Originaltext aus Ep.42
> ![[Resource Analysis/.../transkript-strukturiert#Ertragswertverfahren]]
```

**Callout-Zuordnung im System:**

| Callout-Typ | Verwendung |
|:------------|:-----------|
| `[!warning]` | Zeitliche Hinweise, Widersprüche, veraltete Infos |
| `[!question]` | Unklare Transkript-Stellen, offene Fragen |
| `[!tip]` | Key Takeaways in Zusammenfassungen |
| `[!example]-` | Faltbare Original-Transkript-Einbettungen im Hub |
| `[!note]` | Allgemeine Anmerkungen von Claude |
| `[!abstract]` | Executive Summary in Zusammenfassungen |

**WICHTIG — Einheitliches Quellen-Format**: Das Format `> Quelle: [[...]]` ist der EINZIGE Standard für Quellenangaben. Kein `[!cite]`-Callout verwenden — ein duales Format führt zu Inkonsistenz und erschwert die Suche. Der `[!cite]`-Typ wird in diesem System NICHT genutzt.

#### Nested Tags

Tags im Frontmatter nutzen Obsidians hierarchische Tag-Syntax mit `/`:

```yaml
tags: [finanzen/praxisbewertung, finanzen/ertragswert, personal/gehalt]
```

**Vorteile:**
- Suche nach `#finanzen` in Obsidian findet ALLE Finanz-Themen
- Suche nach `#finanzen/praxisbewertung` findet nur das Sub-Thema
- Tags spiegeln die Hub-Kategorien wider und schaffen eine zusätzliche Navigationsebene

**Regeln:**
- Tag-Hierarchie folgt der Hub-Kategoriestruktur: `#kategorie/sub-thema`
- Maximal 2 Ebenen tief (z.B. `#finanzen/praxisbewertung`, NICHT `#finanzen/praxisbewertung/ertragswert`)
- Tags verwenden Kleinbuchstaben und Bindestriche (wie die Hub-Dateinamen)

#### Embeds im Knowledge-Hub

Obsidian-Embeds (`![[...]]`) können Hub-Einträge reichhaltiger machen, indem relevante Transkript-Abschnitte direkt eingebettet werden:

```markdown
### Ertragswertverfahren

Das Ertragswertverfahren basiert auf dem durchschnittlichen Gewinn der letzten 3 Jahre...

> [!example]- Originaltext aus Ep.42 anzeigen
> ![[Resource Analysis/Praxisflüsterer/ep-042-praxisbewertung/transkript-strukturiert#Ertragswertverfahren]]

> Quelle: [[Resource Analysis/Praxisflüsterer/ep-042-praxisbewertung/transkript-strukturiert#Ertragswertverfahren|Praxisflüsterer Ep.42 (Juni 2023)]]
```

**Regeln für Embeds:**
- Embeds IMMER in faltbare Callouts verpacken (`> [!example]-`), damit der Hub nicht überladen wird
- Embeds sind OPTIONAL — nicht jeder Hub-Eintrag braucht ein Embed
- Sinnvoll bei: komplexen Erklärungen, Zahlen/Statistiken, Zitaten die im Kontext wichtig sind
- NICHT sinnvoll bei: kurzen Fakten, allgemeinen Aussagen

### 16. Technische Umsetzung — Skills

| Skill | Auslösung | Funktion |
|-------|-----------|----------|
| `/get-podcast-url` | Manuell mit Screenshot | Screenshot analysieren, Audio-URL finden, Screenshot als Bild-Asset in `_inbox/` speichern, Inbox-Datei (`type: inbox-episode`) mit Metadaten und eingebettetem Screenshot erstellen. |
| `/analyze-episode` | Manuell nach Transkript-Upload | Vollständige Episode-Analyse: Strukturieren, Zusammenfassen, Hub updaten, Struktur-Check, Praxiskonzept erkennen, Personen-Profil, Web-Recherche. Erkennt `inbox-episode`-Dateien und überspringt Metadaten-Nachfrage. |
| `/clean-notes` | Manuell nach Notizen-Diktat | Max' Roh-Notizen bereinigen, strukturieren, ins Hub eintragen |
| `/ask-knowledge` | Manuell bei Fragen | Systematische Hub-Suche: Index → MOC → Sub-Thema → Details |

**Skill-Konfiguration:**
- Alle Skills als `.claude/skills/[name]/SKILL.md` im Projekt-Verzeichnis
- `/get-podcast-url` braucht `allowed-tools: Read, Write, Bash, Glob, WebSearch, WebFetch` (erstellt Inbox-Dateien, kopiert Screenshot als Bild-Asset)
- `/analyze-episode` und `/clean-notes` brauchen `allowed-tools` im Frontmatter (Read, Write, Edit, Glob, Grep, WebSearch, WebFetch, Bash) damit Claude nicht bei jedem Schritt nach Permission fragt
- `/ask-knowledge` braucht nur `allowed-tools: Read, Glob, Grep` (nur lesen)
- Kein Agent-Team (sequentieller Workflow)

---

## Namenskonventionen

| Element | Format | Beispiel |
|:--------|:-------|:---------|
| **Episoden-Ordner (mit Nr.)** | `ep-NNN-titel-slug` | `ep-042-praxisbewertung` |
| **Episoden-Ordner (ohne Nr.)** | `YYYY-MM-titel-slug` | `2024-03-mvz-aufbau` |
| **YouTube-Videos** | `YYYY-MM-titel-slug` | `2024-05-dental-skalierung` |
| **Personen-Datei** | `vorname-nachname.md` | `stefan-mueller.md` |
| **Praxiskonzept-Ordner** | `Praxisname/` | `Dental21/` |
| **Hub-Kategorie** | Kleinbuchstaben, Bindestriche | `praxis-marketing.md` |

**Regeln:**
- Keine Umlaute in Dateinamen (ä→ae, ö→oe, ü→ue, ß→ss)
- Keine Leerzeichen (Bindestriche statt Leerzeichen)
- Akademische Titel weglassen im Dateinamen (aber im Frontmatter behalten)
- Wenn eine Episode KEINE Nummer hat (z.B. YouTube-Video), wird das Erscheinungsdatum als Präfix verwendet
- Bei Datums-Kollision (zwei Videos vom selben Kanal im selben Monat): Tag hinzufügen → `YYYY-MM-DD-titel-slug` (z.B. `2024-05-12-dental-skalierung`)

---

## Ordnerstruktur (Ziel)

```
Resource Analysis/
├── _inbox/                            # HIER legt Max Transkripte ab (Claude verschiebt sie)
├── _knowledge-hub/                    # Thematisch konsolidiertes Wissen
│   ├── _hub-index.md                 # Top-Level: alle Kategorien + Beschreibung
│   ├── _hub-changelog.md             # Protokoll der Struktur-Änderungen
│   ├── _hub-dashboard.base           # Obsidian Base: dynamische Hub-Übersicht
│   ├── [kategorie].md                # Startet als einzelne Datei
│   ├── [kategorie]/                   # Wird zum Ordner wenn nötig (alte Datei wird GELÖSCHT)
│   │   ├── _[kategorie]-moc.md       # MOC: Übersicht + Links
│   │   ├── [sub-thema-1].md          # Erkenntnisse + Quellen
│   │   └── [sub-thema-2].md
│   └── ...                            # Kategorien entstehen dynamisch
├── _episoden.base                     # Obsidian Base: alle Episoden sortiert/filterbar
├── _system-overview.md                # Systemdokumentation (für Claude-Referenz)
├── Praxisflüsterer/                   # Podcast-Quelle (von Claude erstellt)
│   ├── ep-042-praxisbewertung/        # Episoden-Ordner (von Claude erstellt)
│   │   ├── transkript.md              # Original-Transkript (von Claude aus _inbox/ verschoben)
│   │   ├── transkript-strukturiert.md # Automatisch: thematisch unterteilt
│   │   ├── zusammenfassung.md         # Automatisch: Summary + Takeaways
│   │   ├── web-recherche.md           # Automatisch: Personen/Praxis-Infos aus dem Internet
│   │   └── max-notizen.md             # Automatisch erstellt, Max füllt aus
│   └── ep-043-.../
│       └── ...
├── YouTube-Kanal/                     # Andere Quelle (von Claude erstellt)
│   └── 2024-05-dental-skalierung/     # Ordner mit Datum statt Episodennummer
│       └── ...
└── Weitere-Quelle/
    └── ...

Concepts/
├── _praxiskonzepte-index.md           # Übersicht aller Praxiskonzepte (verlinkt aus Hub-Index)
├── _praxiskonzepte.base               # Obsidian Base: dynamische Praxis-Übersicht
├── Personen/                          # Personen-Verzeichnis
│   ├── _personen-index.md             # Übersicht aller Personen (verlinkt aus Hub-Index)
│   ├── _personen.base                 # Obsidian Base: dynamische Personen-Übersicht
│   └── stefan-mueller.md              # Einzelne Datei pro Person (ohne akad. Titel im Dateinamen)
├── AllDent/                           # (existiert bereits)
│   └── profil.md
├── [Praxisname]/                      # Entsteht automatisch pro erkannter Praxis
│   └── profil.md
└── ...

.claude/skills/
├── analyze-episode/
│   └── SKILL.md
├── clean-notes/
│   └── SKILL.md
└── ask-knowledge/
    └── SKILL.md
```

**Beziehung zwischen den Indizes:**
- `_hub-index.md` ist der zentrale Einstiegspunkt und verlinkt auf ALLE Wissenskategorien
- `_praxiskonzepte-index.md` und `_personen-index.md` werden aus dem Hub-Index verlinkt als Spezial-Verzeichnisse
- Claude liest bei Fragen immer zuerst den Hub-Index → bei Bedarf die Spezial-Indizes

---

## Implementierungs-Checkliste

Diese Checkliste zeigt, was Claude Code bei der Umsetzung erstellen/prüfen muss:

### Struktur erstellen
- [ ] Ordnerstruktur anlegen (siehe Abschnitt ›Ordnerstruktur‹)
- [ ] `Resource Analysis/_knowledge-hub/_hub-index.md` erstellen (leer, mit Frontmatter)
- [ ] `Resource Analysis/_knowledge-hub/_hub-changelog.md` erstellen (leer, mit Frontmatter)
- [ ] `Concepts/_praxiskonzepte-index.md` erstellen (leer, mit Frontmatter)
- [ ] `Concepts/Personen/_personen-index.md` erstellen (leer, mit Frontmatter)
- [ ] `Resource Analysis/_system-overview.md` aktualisieren (falls nötig)

### Skills erstellen
- [ ] `.claude/skills/analyze-episode/SKILL.md` erstellen (Abschnitt 1 als Basis)
- [ ] `.claude/skills/clean-notes/SKILL.md` erstellen (Abschnitt 7 als Basis)
- [ ] `.claude/skills/ask-knowledge/SKILL.md` erstellen (Abschnitt 11 als Basis)

### Obsidian Bases erstellen
- [ ] `Resource Analysis/_episoden.base` (Abschnitt 15)
- [ ] `Resource Analysis/_knowledge-hub/_hub-dashboard.base` (Abschnitt 15)
- [ ] `Concepts/_praxiskonzepte.base` (Abschnitt 15)
- [ ] `Concepts/Personen/_personen.base` (Abschnitt 15)

### Dokumentation synchronisieren
- [ ] `CLAUDE.md` Abschnitt Knowledge-System aktualisieren
- [ ] `Resource Analysis/_system-overview.md` auf Konsistenz mit diesem Plan prüfen

### Abdeckung im Plan (Referenz)

Dieser Plan enthält Spezifikationen für:

| # | Thema | Abschnitt |
|:--|:------|:----------|
| 1 | Ordnerstruktur mit allen Dateien | Ordnerstruktur (Ziel) |
| 2 | Skill-Workflows und allowed-tools | 1, 7, 11, 16 |
| 3 | YAML-Frontmatter für jeden Dateityp | 5 |
| 4 | Quellenreferenz-Format (Wikilinks) | 2 |
| 5 | Dynamische Kategorie-Evolution | 4 |
| 6 | Zeitliche Gewichtung & Widersprüche | 3 |
| 7 | Re-Analyse und Profil-Updates | 1 (Schritt 2), 8, 9 |
| 8 | Fehlerbehandlung & Edge Cases | 12 |
| 9 | Namenskonventionen | Namenskonventionen |
| 10 | Skalierungsstrategie | 14 |
| 11 | Dokumentations-Wartung | 13 |
| 12 | Obsidian Bases & native Features | 15 |
