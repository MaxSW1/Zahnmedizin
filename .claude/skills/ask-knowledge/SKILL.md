---
description: "Beantwortet Fragen anhand des Knowledge-Hubs mit systematischem 5-Stufen-Retrieval. Quellenangaben und zeitliche Einordnung immer dabei."
allowed-tools: ["Read", "Glob", "Grep"]
---

# /ask-knowledge

Beantwortet Max' Fragen basierend auf dem gesammelten Wissen im Knowledge-Hub.

## Aufruf

```
/ask-knowledge Wie funktioniert das Ertragswertverfahren bei Praxisbewertungen?
/ask-knowledge Was wissen wir über MVZ-Skalierung?
/ask-knowledge Welche Praxen nutzen das Hub-and-Spoke-Modell?
```

## 5-Stufen-Retrieval (IMMER einhalten)

Nie alle Dateien auf einmal laden. Immer von oben nach unten durch die Hierarchie navigieren:

### Stufe 1 — Hub-Index
`Resource Analysis/_knowledge-hub/_hub-index.md` lesen → relevante Kategorien identifizieren.

### Stufe 2 — Kategorie/MOC
Die passende Kategorie-Datei oder MOC-Datei lesen → relevante Sub-Themen finden.

### Stufe 3 — Sub-Thema
Die spezifische Sub-Themen-Datei lesen → konsolidiertes Wissen mit Quellenangaben.

### Stufe 4 — Zusammenfassung (nur bei Bedarf)
Episode-Zusammenfassungen lesen, wenn mehr Kontext nötig ist.

### Stufe 5 — Transkript (nur wenn wirklich nötig)
Das strukturierte Transkript lesen — nur als letzte Stufe, nie als erste.

**Bei Fragen zu Personen oder Praxen**: Zuerst den entsprechenden Index (`Concepts/Personen/_personen-index.md` oder `Concepts/_praxiskonzepte-index.md`) lesen, dann das passende Profil.

## Regeln für die Antwort

1. **Quellenangaben immer mitliefern**: Jede Aussage mit Quelle belegen (Episode + Datum)
2. **Zeitliche Einordnung**: Bei Quellen älter als 2 Jahre proaktiv darauf hinweisen:
   *"Hinweis: Diese Information stammt aus [Datum]. Der aktuelle Stand könnte abweichen."*
3. **Widersprüche transparent machen**: Wenn verschiedene Quellen sich widersprechen, BEIDE Perspektiven nennen (neuere Quelle zuerst)
4. **Wissenslücken benennen**: Wenn der Hub keine Infos hat, ehrlich sagen:
   *"Dazu habe ich im Knowledge-Hub noch keine Informationen. Das Thema wurde in den bisher analysierten Episoden nicht behandelt."*
5. **Kein Kontext-Overload**: Nie alle Transkripte laden — immer die 5-Stufen-Hierarchie nutzen
