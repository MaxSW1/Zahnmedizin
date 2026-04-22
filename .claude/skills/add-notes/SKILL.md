---
description: "Max diktiert Notizen zu einer Episode — Claude bereinigt sie, hängt sie an die max-notizen.md an und aktualisiert den Hub."
allowed-tools: ["Read", "Write", "Edit", "Glob", "Grep"]
---

# /add-notes

Max hört sich eine Episode an und diktiert seine Gedanken in Conductor. Dieser Skill bereinigt die Notizen und fügt sie an die richtige `max-notizen.md` an — damit sie im Embed am Ende der Episoden-Zusammenfassung sichtbar werden.

## Aufruf

Max diktiert frei in Conductor, z.B.:

```
/add-notes Praxisflüsterer Episode 1: Ich finde spannend dass Frankenberger mit 32 habilitiert hat das ist extrem jung und zeigt wie wichtig Mentoren sind...
```

Oder kürzer:

```
/add-notes Ep 1: Frankenberger habilitiert mit 32, Mentoren sind key...
```

Falls Max die Episode nicht benennt sondern nur ein Thema beschreibt, die richtige Episode anhand des Inhalts identifizieren. Falls unklar: kurz nachfragen.

## Workflow

### Schritt 1 — Episode identifizieren

Die richtige `max-notizen.md` finden:

1. Episodennummer, Titel, Personenname oder Thema aus Max' Nachricht extrahieren
2. Episoden-Zusammenfassungen durchsuchen: `Resource Analysis/**/type: episode-zusammenfassung`
3. Die passende `max-notizen.md` im selben Ordner identifizieren
4. Falls keine eindeutige Zuordnung möglich: Max fragen

### Schritt 2 — Notizen bereinigen

Max' Diktat aufbereiten:

- **Füllwörter entfernen**: "ähm", "also", "halt", "sozusagen", Wiederholungen
- **Sätze vervollständigen**: Grammatik, Interpunktion korrigieren
- **Kern bewahren**: Max' Meinungen und Gedanken NICHT verändern oder uminterpretieren — nur die Form verbessern
- **Kurze Überschrift** generieren, die den Inhalt der Notiz zusammenfasst (z.B. `## Habilitation mit 32 — Mentoren als Erfolgsfaktor`)

### Schritt 3 — An max-notizen.md anhängen

Die bereinigte Notiz ans Ende der `max-notizen.md` anhängen:

```markdown
## [Überschrift]

[Bereinigte Notiz]
```

**Regeln:**
- ANHÄNGEN, nicht überschreiben — bestehende Notizen bleiben erhalten
- Jede neue Notiz bekommt eine eigene `##`-Überschrift
- Datum nicht einfügen (das Frontmatter hat `erstellt`, das reicht)

### Schritt 4 — Knowledge-Hub aktualisieren (nur wenn relevant)

Falls die Notiz Hub-relevante Erkenntnisse enthält (eigene Schlussfolgerungen, Verknüpfungen, strategische Überlegungen):

1. `Resource Analysis/_knowledge-hub/_hub-index.md` lesen → relevante Kategorien identifizieren
2. Erkenntnisse ANHÄNGEN (nicht überschreiben)
3. Quellenangabe mitliefern:
   ```markdown
   > Quelle: [[Resource Analysis/.../max-notizen|Max' Notizen zu [Episodentitel]]]
   ```
4. Gleiche Hub-Regeln wie bei Episoden-Analyse

**Nicht alles gehört in den Hub** — persönliche Reaktionen ("fand ich spannend") oder Fragen sind Notizen, keine Hub-Einträge. Nur konkrete Erkenntnisse oder strategische Schlussfolgerungen eintragen.

### Schritt 5 — Ergebnis melden

Kurze Bestätigung an Max (1-2 Zeilen):
- Welche Episode
- Überschrift der Notiz
- Ob Hub aktualisiert wurde (und wenn ja, welche Kategorien)
