---
description: "Erkennt Podcast-Episode aus Screenshot, findet Audio-URL, erstellt Inbox-Datei mit Metadaten fuer MacWhisper und /analyze-episode."
allowed-tools: ["Read", "Write", "Bash", "Glob", "WebSearch", "WebFetch"]
---

# /get-podcast-url

Erkennt eine Podcast-Episode aus einem Screenshot (Spotify, Apple Podcasts, etc.), findet die direkte Audio-URL und erstellt eine vorbereitete Inbox-Datei mit allen Metadaten. Max kann dann die URL in MacWhisper einfuegen, das Transkript in die Inbox-Datei einsetzen und `/analyze-episode` aufrufen — ohne nochmal Metadaten eingeben zu muessen.

Der Screenshot wird als Bild-Asset in `_inbox/` gespeichert und per Obsidian-Embed (`![[...]]`) in die Inbox-Datei eingebettet — so ist er direkt in Obsidian sichtbar.

## Aufruf

Max fuegt einen Screenshot einer Podcast-Episode bei und ruft den Skill auf:

```
/get-podcast-url
```

Der Screenshot kann von Spotify, Apple Podcasts, Pocket Casts, der Podcast-Website oder jeder anderen Plattform stammen.

## Workflow

### Schritt 1 — Screenshot analysieren

Claude liest den beigefuegten Screenshot und extrahiert alle sichtbaren Informationen:

- **Podcast-Name** (z.B. "Praxisfluesterer Podcast")
- **Episode-Titel** (z.B. "#1: Der Praesident - Prof. Dr. Roland Frankenberger")
- **Episodennummer** (falls sichtbar)
- **Gast/Sprecher** (falls aus Titel/Beschreibung erkennbar)
- **Erscheinungsdatum** (falls sichtbar)
- **Dauer** (falls sichtbar)
- **Beschreibung** (falls sichtbar — so viel wie lesbar)

Falls kein Screenshot beigefuegt ist, fragt Claude Max danach.

### Schritt 2 — Audio-URL finden

Claude sucht die direkte Audio-Download-URL. Strategie:

1. **Podigee-Check** (haeufigste Plattform fuer deutsche Podcasts): WebSearch nach `[Podcast-Name] site:podigee.io` → Episode-Seite aufrufen → Audio-URL extrahieren
2. **RSS-Feed suchen**: WebSearch nach `[Podcast-Name] RSS feed` → Feed abrufen → `<enclosure url="...">` fuer die Episode finden
3. **Apple Podcasts Lookup**: WebFetch `https://itunes.apple.com/search?term=[Podcast-Name]&media=podcast&entity=podcast` → Feed-URL extrahieren
4. **Direkte Episode-Suche**: WebSearch nach `[Podcast-Name] [Episode-Titel]` → Episode-Seite finden → Audio-URL aus dem HTML-Player extrahieren

Claude probiert die Strategien der Reihe nach, bis die Audio-URL gefunden ist.

### Schritt 3 — Screenshot speichern

Claude speichert den beigefuegten Screenshot als Bild-Datei in `Resource Analysis/_inbox/`:

**Dateiname-Format**: `[podcast-slug]-ep-[NNN]-screenshot.png`
- Beispiel: `praxisfluesterer-ep-001-screenshot.png`
- Ohne Episodennummer: `[podcast-slug]-YYYY-MM-titel-slug-screenshot.png`
- Namensregeln: Keine Umlaute, keine Leerzeichen, Kleinbuchstaben

Claude nutzt `Bash` (cp), um den Screenshot vom temporaeren Pfad nach `Resource Analysis/_inbox/` zu kopieren.

### Schritt 4 — Inbox-Datei erstellen

Claude erstellt eine Markdown-Datei in `Resource Analysis/_inbox/` mit folgendem Aufbau:

**Dateiname-Format**: `[podcast-slug]-ep-[NNN].md`
- Beispiel: `praxisfluesterer-ep-001.md`
- Ohne Episodennummer: `[podcast-slug]-YYYY-MM-titel-slug.md`
- Namensregeln: Keine Umlaute, keine Leerzeichen, Kleinbuchstaben

**Inhalt:**

```markdown
---
type: inbox-episode
podcast: "[Podcast-Name]"
episode: [Nummer oder null]
titel: "[Vollstaendiger Episode-Titel]"
erschienen: "[YYYY-MM]"
gast: "[Name des Gasts/Interviewpartners]"
dauer: "[Dauer wie im Screenshot]"
audio-url: "[Direkte Audio-URL]"
screenshot: "[Screenshot-Dateiname.png]"
---

# [Episode-Titel]

![[Screenshot-Dateiname.png]]

## Metadaten
- **Podcast**: [Name]
- **Episode**: [Nummer oder "k.A."]
- **Erschienen**: [Datum, lesbar formatiert]
- **Dauer**: [Dauer]
- **Gast**: [Name]

## Audio-URL fuer MacWhisper

AUDIO_URL_PLACEHOLDER

## Beschreibung

[Beschreibungstext aus dem Screenshot, so viel wie lesbar]

## Transkript

[Hier das Transkript aus MacWhisper einfuegen]
```

**WICHTIG fuer die Audio-URL-Sektion**: Die URL wird als reiner Text auf einer eigenen Zeile ausgegeben (KEIN Code-Block, KEINE Backticks), damit Max sie einfach markieren und kopieren kann. Im Template oben steht `AUDIO_URL_PLACEHOLDER` als Platzhalter — Claude ersetzt das mit der tatsaechlichen URL.

### Schritt 5 — Ausgabe an Max

Claude gibt eine kompakte Zusammenfassung aus:

```
Inbox-Datei erstellt: Resource Analysis/_inbox/praxisfluesterer-ep-001.md

Audio-URL fuer MacWhisper:
https://audio.podigee-cdn.net/xxxxx.mp3?source=web_download&dl=1

Naechste Schritte:
1. URL oben in MacWhisper einfuegen → Transkript erstellen
2. Transkript in die Inbox-Datei einfuegen (unter ## Transkript)
3. /analyze-episode Resource Analysis/_inbox/praxisfluesterer-ep-001.md
```

## Fallback-Strategien

**Audio-URL nicht gefunden:**
- Claude erstellt die Inbox-Datei trotzdem (mit `audio-url: null` im Frontmatter)
- Statt der URL gibt Claude den Link zur Episode-Seite an mit Hinweis: "Audio-URL konnte nicht automatisch extrahiert werden. Auf dieser Seite gibt es einen Download-Button."

**Screenshot nicht beigefuegt:**
- Claude fragt Max nach einem Screenshot ODER nach Podcast-Name + Episode-Titel
- Falls Max Text-Infos statt Screenshot gibt: Inbox-Datei normal erstellen

**Beschreibung nicht lesbar:**
- Nur das eintragen, was klar erkennbar ist
- Claude kann die Beschreibung auch von der Episode-Seite holen (als Teil der URL-Suche)

## Hinweis

Dieser Skill erstellt eine Markdown-Datei und speichert den Screenshot als Bild-Asset in `Resource Analysis/_inbox/`. Das Screenshot-Bild ist per Obsidian-Embed in der Markdown-Datei eingebettet — zusammen bilden sie ein Dokument. Die eigentliche Analyse und Verschiebung in den Episoden-Ordner passiert erst durch `/analyze-episode`.
