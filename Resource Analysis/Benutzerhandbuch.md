# Benutzerhandbuch: Knowledge-System

Dieses Handbuch erklärt, wie Max das Wissensmanagement-System in diesem Repo nutzt.

---

## Was das System macht

Das System verwandelt Podcast-Transkripte und Video-Mitschriften in durchsuchbares, strukturiertes Wissen. Statt sich alles merken zu müssen, baut Max Stück für Stück eine persönliche Wissensdatenbank auf — sortiert nach Themen, mit Quellenangaben, und jederzeit per Frage abrufbar.

**Das System hat fünf Fähigkeiten (Skills):**

| Skill | Was er tut | Wann benutzen |
|:------|:-----------|:--------------|
| `/get-podcast-url` | Podcast-Screenshot → Inbox-Datei mit Metadaten + Audio-URL | Vor dem Transkribieren einer Podcast-Episode |
| `/get-youtube-url` | YouTube-Screenshot → Inbox-Datei mit Metadaten + YouTube-URL | Vor dem Transkribieren eines YouTube-Videos |
| `/analyze-episode` | Transkript komplett verarbeiten | Nach dem Einfügen des Transkripts in die Inbox-Datei |
| `/clean-notes` | Diktierte Notizen aufräumen | Nachdem Max eigene Gedanken eingesprochen hat |
| `/ask-knowledge` | Fragen ans gesammelte Wissen stellen | Jederzeit, wenn Max etwas nachschlagen will |

---

## Neue Episode verarbeiten

### Podcast-Episoden (Spotify, Apple Podcasts etc.)

#### 1. Screenshot machen

In Spotify, Apple Podcasts oder einer anderen Podcast-App die gewünschte Episode öffnen und einen Screenshot machen. Der Screenshot sollte möglichst zeigen:
- Podcast-Name
- Episode-Titel und Nummer
- Erscheinungsdatum
- Dauer
- Beschreibung (so viel wie sichtbar)

#### 2. Inbox-Datei erstellen lassen

In Claude Code den Screenshot beifügen und eingeben:

```
/get-podcast-url
```

Claude erstellt automatisch:
- Eine Markdown-Datei in `Resource Analysis/_inbox/` mit allen Metadaten
- Den **Screenshot** als Bild eingebettet (direkt in der Datei sichtbar in Obsidian)
- Die direkte **Audio-URL** wird gesucht und in die Datei eingefügt

Am Ende zeigt Claude die Audio-URL an — diese kopieren.

#### 3. In MacWhisper transkribieren

MacWhisper öffnen → Audio-URL in das URL-Feld einfügen → Transkribieren lassen.

#### 4. Transkript einfügen

Das fertige Transkript aus MacWhisper kopieren und in die Inbox-Datei einfügen — unter der Überschrift `## Transkript` (dort steht ein Platzhalter).

Die Inbox-Datei liegt z.B. unter:
```
Resource Analysis/_inbox/praxisfluesterer-ep-001.md
```

#### 5. Analyse starten

```
/analyze-episode Resource Analysis/_inbox/praxisfluesterer-ep-001.md
```

Da alle Metadaten bereits in der Datei stehen, **fragt Claude nichts nach** und startet sofort mit der Analyse.

---

### YouTube-Videos

#### 1. Screenshot machen

Auf YouTube die Videoseite öffnen und einen Screenshot machen. Der Screenshot sollte möglichst zeigen:
- Kanal-Name
- Video-Titel
- Erscheinungsdatum
- Aufrufe
- Beschreibung (so viel wie sichtbar)
- Kapitelmarken (falls vorhanden)

#### 2. Inbox-Datei erstellen lassen

In Claude Code den Screenshot beifügen und eingeben:

```
/get-youtube-url
```

Claude erstellt automatisch:
- Eine Markdown-Datei in `Resource Analysis/_inbox/` mit allen Metadaten
- Den **Screenshot** als Bild eingebettet (direkt in der Datei sichtbar in Obsidian)
- Die **YouTube-URL** wird gesucht und in die Datei eingefügt

Am Ende zeigt Claude die YouTube-URL an — diese kopieren.

#### 3. In MacWhisper transkribieren

MacWhisper öffnen → YouTube-URL in das URL-Feld einfügen → Transkribieren lassen.

#### 4. Transkript einfügen

Das fertige Transkript aus MacWhisper kopieren und in die Inbox-Datei einfügen — unter der Überschrift `## Transkript` (dort steht ein Platzhalter).

Die Inbox-Datei liegt z.B. unter:
```
Resource Analysis/_inbox/denta1-clinic-2022-01-3-trends-zahnaerzte.md
```

#### 5. Analyse starten

```
/analyze-episode Resource Analysis/_inbox/denta1-clinic-2022-01-3-trends-zahnaerzte.md
```

Da alle Metadaten bereits in der Datei stehen, **fragt Claude nichts nach** und startet sofort mit der Analyse.

#### 6. Claude erledigt den Rest

Claude macht automatisch:

1. **Ordner erstellen** — Richtiger Ordnername, richtige Stelle
2. **Transkript extrahieren** — Aus der Inbox-Datei in den Episoden-Ordner
3. **Transkript strukturieren** — Thematische Abschnitte mit Überschriften
4. **Zusammenfassung erstellen** — Executive Summary und Key Takeaways
5. **Personen erkennen** — Interview-Gäste identifizieren, Profile anlegen
6. **Praxen erkennen** — Vorgestellte Praxen dokumentieren
7. **Web-Recherche** — Zusatzinfos aus dem Internet
8. **Wissen konsolidieren** — Erkenntnisse in den Knowledge-Hub eintragen
9. **Notiz-Datei vorbereiten** — Leere Datei für Max' Gedanken

Am Ende gibt Claude einen Abschluss-Bericht mit allem, was erstellt wurde.

---

### Alternativer Weg: Transkript direkt ablegen (ohne Screenshot)

Falls das Transkript schon vorhanden ist (z.B. von YouTube-Untertiteln):

1. Markdown-Datei in `Resource Analysis/_inbox/` legen
2. `/analyze-episode Resource Analysis/_inbox/dateiname.md`
3. Claude fragt nach fehlenden Metadaten (Podcast-Name, Episodennummer, Datum, Titel)

---

### Eigene Gedanken ergänzen (optional, aber empfohlen)

Im Episoden-Ordner liegt jetzt eine `max-notizen.md`. Dort eigene Gedanken, Ideen und Einschätzungen festhalten — per Diktat oder Tippen.

Danach die Notizen bereinigen lassen:

```
/clean-notes Resource Analysis/Praxisfluesterer/ep-042-praxisbewertung/max-notizen.md
```

Claude räumt die Notizen auf (Füllwörter raus, Struktur rein) und trägt relevante Erkenntnisse in den Hub ein. Die Roh-Version wird als Backup gespeichert.

---

## Wissen abrufen: `/ask-knowledge`

Jederzeit Fragen an das gesammelte Wissen stellen:

```
/ask-knowledge Wie funktioniert das Ertragswertverfahren?
/ask-knowledge Was wissen wir über MVZ-Skalierung?
/ask-knowledge Welche Experten haben über Personalführung gesprochen?
/ask-knowledge Was hat Dr. Müller über Praxisbewertung gesagt?
```

**Was Claude dann tut:**
- Durchsucht systematisch den Knowledge-Hub (nicht alle Transkripte)
- Liefert eine Antwort mit Quellenangaben (welche Episode, welches Datum)
- Weist darauf hin, wenn Informationen älter als 2 Jahre sind
- Zeigt Widersprüche zwischen verschiedenen Quellen transparent auf
- Sagt ehrlich, wenn es zu einem Thema noch kein Wissen gibt

---

## Wo Max sein Wissen findet (in Obsidian)

Das Repo ist gleichzeitig ein Obsidian-Vault. Max kann den Ordner `farmerville/` direkt in Obsidian öffnen.

### Wichtigste Anlaufstellen

| Was | Wo | Beschreibung |
|:----|:---|:-------------|
| **Gesammeltes Wissen** | `Resource Analysis/_knowledge-hub/` | Nach Themen sortierte Erkenntnisse |
| **Themen-Übersicht** | `_knowledge-hub/_hub-index.md` | Einstiegspunkt: alle Wissenskategorien |
| **Alle Episoden** | `_episoden.base` | Dynamische Tabelle aller verarbeiteten Episoden |
| **Praxiskonzepte** | `Praxis-Konzepte/` | Profile aller dokumentierten Praxen |
| **Personen** | `Praxis-Konzepte/Personen/` | Profile aller Experten und Interview-Gäste |

### Navigation in Obsidian

- **Klick auf Quellenangabe** → Springt direkt zur Stelle im strukturierten Transkript
- **Graph View** → Zeigt Verbindungen zwischen Episoden, Themen und Personen
- **Tag-Suche** → `#finanzen` findet alle Finanz-Themen, `#finanzen/praxisbewertung` nur das Sub-Thema
- **Base-Views** → Dynamische Tabellen die sich automatisch aktualisieren (Episoden, Personen, Praxen, Hub-Dashboard)

---

## Tipps

### Beim Screenshot für `/get-podcast-url` oder `/get-youtube-url`

- **Möglichst viel sichtbar** — Je mehr Infos im Screenshot (Titel, Datum, Beschreibung), desto weniger muss Claude recherchieren.
- **Spotify-Episodenseite ideal für Podcasts** — Dort sind Titel, Datum, Dauer und Beschreibung direkt sichtbar.
- **YouTube-Videoseite ideal für Videos** — Titel, Kanal, Datum, Beschreibung und Kapitelmarken direkt sichtbar.
- **Funktioniert auch mit Apple Podcasts, Pocket Casts, Podcast-Websites** — Alles was die Episode-Infos zeigt.

### Beim Transkript

- **MacWhisper mit Large v3 Turbo** — Bestes Ergebnis für deutsche Podcasts.
- **Audio-URL direkt aus der Inbox-Datei kopieren** — Steht unter "Audio-URL für MacWhisper".
- **Transkript unter `## Transkript` einfügen** — Den Platzhalter-Text ersetzen.

### Bei eigenen Notizen

- **Einfach drauflos diktieren** — `/clean-notes` räumt auf. Keine Angst vor Füllwörtern.
- **Eigene Meinung festhalten** — "Ich glaube, das passt nicht zu unserem Konzept, weil..." ist genau die Art von Gedanken, die wertvoll sind.
- **Notizen zeitnah machen** — Direkt nach dem Hören, solange die Gedanken frisch sind.

### Bei der Wissensabfrage

- **Spezifische Fragen stellen** — "Wie funktioniert das Ertragswertverfahren?" ist besser als "Was wissen wir über Finanzen?"
- **Nach Personen fragen** — "Was hat [Name] über [Thema] gesagt?" nutzt die Personen-Profile.

---

## Wie das System wächst

Das System startet leer und wächst mit jeder analysierten Episode:

```
Erste Episoden  →  Initiale Themen-Kategorien entstehen
Mehr Episoden   →  Kategorien füllen sich, neue kommen dazu
Viele Episoden  →  Große Kategorien werden automatisch in Sub-Themen aufgeteilt
```

Max muss sich um die Struktur nicht kümmern — Claude verwaltet den Hub automatisch.

---

## Zusammenfassung: Der komplette Workflow

**Podcast-Episode:**
```
1. Screenshot der Episode machen (Spotify etc.)
2. /get-podcast-url  (mit Screenshot)
3. Audio-URL aus der Inbox-Datei in MacWhisper kopieren
4. Transkript in die Inbox-Datei einfügen (unter ## Transkript)
5. /analyze-episode Resource Analysis/_inbox/dateiname.md
6. Optional: Eigene Gedanken in max-notizen.md → /clean-notes
7. Jederzeit: /ask-knowledge Deine Frage?
```

**YouTube-Video:**
```
1. Screenshot des Videos machen (YouTube-Videoseite)
2. /get-youtube-url  (mit Screenshot)
3. YouTube-URL aus der Inbox-Datei in MacWhisper kopieren
4. Transkript in die Inbox-Datei einfügen (unter ## Transkript)
5. /analyze-episode Resource Analysis/_inbox/dateiname.md
6. Optional: Eigene Gedanken in max-notizen.md → /clean-notes
7. Jederzeit: /ask-knowledge Deine Frage?
```
