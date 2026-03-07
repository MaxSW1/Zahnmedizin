---
description: "Bereinigt Max' diktierte oder getippte Notizen: strukturieren, Füllwörter entfernen, Roh-Backup erstellen, Erkenntnisse in den Hub eintragen."
allowed-tools: ["Read", "Write", "Edit", "Glob", "Grep"]
---

# /clean-notes

Bereinigt Max' Roh-Notizen und trägt relevante Erkenntnisse in den Knowledge-Hub ein.

## Aufruf

```
/clean-notes Pfad/zur/max-notizen.md
```

## Workflow

### Schritt 1 — Roh-Version sichern (IMMER)

Vor jeder Änderung das Original als `max-notizen-roh.md` im selben Ordner kopieren. Das Backup wird IMMER erstellt, egal ob diktiert oder getippt.

### Schritt 2 — Notizen bereinigen

- **Struktur**: Gedanken in logische Abschnitte mit `## Überschriften` unterteilen
- **Bereinigung**: Füllwörter entfernen, Sätze vervollständigen, Diktat-Artefakte korrigieren (z.B. "ähm", "also", falsche Interpunktion)
- **Kern bewahren**: Max' eigene Meinungen und Gedanken NICHT verändern oder uminterpretieren — nur die Form verbessern, nie den Inhalt
- **Markierung**: Am Anfang der Datei einfügen:
  ```markdown
  > Bereinigt am [YYYY-MM-DD] — Original-Gedanken von Max, sprachlich überarbeitet
  ```

### Schritt 3 — Frontmatter aktualisieren

```yaml
bereinigt: true
roh-version: max-notizen-roh.md
```

### Schritt 4 — Knowledge-Hub aktualisieren

Relevante Erkenntnisse aus Max' Notizen in die Hub-Dateien eintragen:

1. `Resource Analysis/_knowledge-hub/_hub-index.md` lesen → relevante Kategorien identifizieren
2. Erkenntnisse ANHÄNGEN (nicht überschreiben)
3. Quellenangabe immer mitliefern:
   ```markdown
   > Quelle: [[Resource Analysis/.../max-notizen|Max' Notizen zu Ep.42]]
   ```
4. Gleiche Hub-Regeln wie bei Episoden-Analyse: Quellenangaben, zeitliche Einordnung, Widerspruchs-Behandlung

### Schritt 5 — Ergebnis melden

Kurze Zusammenfassung an Max:
- Wie viele Abschnitte strukturiert
- Welche Hub-Kategorien aktualisiert
- Roh-Backup-Pfad nennen
