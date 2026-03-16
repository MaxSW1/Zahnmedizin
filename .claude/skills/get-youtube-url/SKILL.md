---
description: "Erkennt YouTube-Video aus Screenshot, findet Video-URL, erstellt Inbox-Datei mit Metadaten fuer /analyze-episode."
allowed-tools: ["Read", "Write", "Bash", "Glob", "WebSearch", "WebFetch"]
---

# /get-youtube-url

Erkennt ein YouTube-Video aus einem Screenshot, findet die Video-URL und erstellt eine vorbereitete Inbox-Datei mit allen Metadaten. Max kann dann das Transkript (z.B. aus MacWhisper oder YouTube-Untertiteln) in die Inbox-Datei einsetzen und `/analyze-episode` aufrufen — ohne nochmal Metadaten eingeben zu muessen.

Der Screenshot wird als Bild-Asset in `_inbox/` gespeichert und per Obsidian-Embed (`![[...]]`) in die Inbox-Datei eingebettet.

## Aufruf

Max fuegt einen Screenshot eines YouTube-Videos bei und ruft den Skill auf:

```
/get-youtube-url
```

Der Screenshot kann von der YouTube-Videoseite stammen (Desktop oder Mobil).

## Workflow

### Schritt 1 — Screenshot analysieren

Claude liest den beigefuegten Screenshot und extrahiert alle sichtbaren Informationen:

- **Kanal-Name** (z.B. "Denta1 Clinic - Dr. Stefan Helka")
- **Video-Titel** (z.B. "Diese 3 Trends werden Zahnaerzte massiv beeinflussen")
- **Gast/Sprecher** (falls aus Titel/Beschreibung erkennbar)
- **Erscheinungsdatum** (falls sichtbar)
- **Aufrufe** (falls sichtbar)
- **Dauer** (falls sichtbar)
- **Beschreibung** (falls sichtbar — so viel wie lesbar)
- **Kapitelmarken** (falls sichtbar — alle Zeitstempel und Titel)

Falls kein Screenshot beigefuegt ist, fragt Claude Max danach.

### Schritt 2 — YouTube-URL finden

Claude sucht die YouTube-Video-URL. Strategie:

1. **Direkte Suche**: WebSearch nach `site:youtube.com "[Kanal-Name]" "[Video-Titel]"` → YouTube-URL extrahieren
2. **Erweiterte Suche**: WebSearch nach `youtube.com [Kanal-Name] [Video-Titel]` (ohne site:-Filter)
3. **Kanal-Suche**: WebSearch nach `[Kanal-Name] youtube channel` → Kanal finden → Video in Upload-Liste suchen

Claude probiert die Strategien der Reihe nach, bis die YouTube-URL gefunden ist. Die URL hat typischerweise das Format `https://www.youtube.com/watch?v=XXXXXXXXXXX`.

### Schritt 3 — Screenshot speichern

Claude speichert den beigefuegten Screenshot als Bild-Datei in `Resource Analysis/_inbox/`:

**Dateiname-Format**: `[kanal-slug]-YYYY-MM-titel-slug-screenshot.png`
- Beispiel: `denta1-clinic-2022-01-3-trends-zahnaerzte-screenshot.png`
- Namensregeln: Keine Umlaute (ae, oe, ue, ss), keine Leerzeichen, Kleinbuchstaben

Claude nutzt `Bash` (cp), um den Screenshot vom temporaeren Pfad nach `Resource Analysis/_inbox/` zu kopieren.

### Schritt 4 — Inbox-Datei erstellen

Claude erstellt eine Markdown-Datei in `Resource Analysis/_inbox/` mit folgendem Aufbau:

**Dateiname-Format**: `[kanal-slug]-YYYY-MM-titel-slug.md`
- Beispiel: `denta1-clinic-2022-01-3-trends-zahnaerzte.md`
- Namensregeln: Keine Umlaute, keine Leerzeichen, Kleinbuchstaben

**Inhalt:**

```markdown
---
type: inbox-episode
podcast: "[Kanal-Name]"
episode: null
titel: "[Vollstaendiger Video-Titel]"
erschienen: "[YYYY-MM]"
gast: "[Name des Gasts/Interviewpartners]"
dauer: "[Dauer falls bekannt]"
youtube-url: "[YouTube-URL]"
screenshot: "[Screenshot-Dateiname.png]"
---

# [Video-Titel]

![[Screenshot-Dateiname.png]]

## Metadaten
- **Kanal**: [Name]
- **Erschienen**: [Datum, lesbar formatiert]
- **Aufrufe**: [Anzahl falls bekannt]
- **Dauer**: [Dauer falls bekannt]
- **Gast**: [Name oder "k.A."]

## YouTube-URL

YOUTUBE_URL_PLACEHOLDER

## Beschreibung

[Beschreibungstext aus dem Screenshot, so viel wie lesbar]

## Kapitel

[Kapitelmarken aus dem Screenshot, falls vorhanden — Format: `MM:SS Titel`]

## Transkript

[Hier das Transkript einfuegen]
```

**WICHTIG fuer die YouTube-URL-Sektion**: Die URL wird als reiner Text auf einer eigenen Zeile ausgegeben (KEIN Code-Block, KEINE Backticks), damit Max sie einfach markieren und kopieren kann. Im Template oben steht `YOUTUBE_URL_PLACEHOLDER` als Platzhalter — Claude ersetzt das mit der tatsaechlichen URL.

### Schritt 5 — Ausgabe an Max

Claude gibt eine kompakte Zusammenfassung aus:

```
Inbox-Datei erstellt: Resource Analysis/_inbox/denta1-clinic-2022-01-3-trends-zahnaerzte.md

YouTube-URL:
https://www.youtube.com/watch?v=XXXXXXXXXXX

Naechste Schritte:
1. URL oben in MacWhisper einfuegen → Transkript erstellen
2. Transkript in die Inbox-Datei einfuegen (unter ## Transkript)
3. /analyze-episode Resource Analysis/_inbox/denta1-clinic-2022-01-3-trends-zahnaerzte.md
```

## Fallback-Strategien

**YouTube-URL nicht gefunden:**
- Claude erstellt die Inbox-Datei trotzdem (mit `youtube-url: null` im Frontmatter)
- Claude gibt Max einen Hinweis: "YouTube-URL konnte nicht automatisch gefunden werden. Bitte die URL manuell eintragen."

**Screenshot nicht beigefuegt:**
- Claude fragt Max nach einem Screenshot ODER nach Kanal-Name + Video-Titel
- Falls Max Text-Infos statt Screenshot gibt: Inbox-Datei normal erstellen

**Beschreibung nicht lesbar:**
- Nur das eintragen, was klar erkennbar ist
- Claude kann die Beschreibung auch von der YouTube-Seite holen (als Teil der URL-Suche)

## Kompatibilitaet mit /analyze-episode

Die Inbox-Datei nutzt `type: inbox-episode` im Frontmatter — genau wie bei `/get-podcast-url`. Dadurch erkennt `/analyze-episode` die Datei automatisch und ueberspringt die Metadaten-Nachfrage. Das `podcast`-Feld wird mit dem YouTube-Kanal-Namen befuellt, da `/analyze-episode` dieses Feld fuer den Quellen-Ordner nutzt.

## Hinweis

Dieser Skill erstellt eine Markdown-Datei und speichert den Screenshot als Bild-Asset in `Resource Analysis/_inbox/`. Das Screenshot-Bild ist per Obsidian-Embed in der Markdown-Datei eingebettet. Die eigentliche Analyse und Verschiebung in den Episoden-Ordner passiert erst durch `/analyze-episode`.
