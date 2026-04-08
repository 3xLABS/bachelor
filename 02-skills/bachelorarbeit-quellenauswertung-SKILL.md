---
name: bachelorarbeit-quellenauswertung
description: >
  Phase 3 der Bachelorarbeit-Pipeline: Systematische Auswertung der in Phase 2 gesammelten Quellen mit NotebookLM. Extrahiert Kernaussagen, identifiziert Zusammenhänge und Widersprüche, erstellt strukturierte Auswertungsdokumente pro Kapitel — die Grundlage, auf der der Writer (Phase 4) schreibt. Setzt voraus, dass Phase 2 (Recherche) für das Kapitel abgeschlossen ist. Nutze bei: "Quellen auswerten", "Literatur analysieren", "was sagen die Quellen zu", "Quellenauswertung", "Literaturanalyse", "Quellen zusammenfassen", "Quellen vergleichen", "was steht in den Papers", "extrahiere die Kernaussagen", "erstelle eine Quellenübersicht", "werte die Quellen aus". Nicht für Quellensuche — dafür gibt es `bachelorarbeit-recherche`.
---

# Bachelorarbeit — Phase 3: Quellenauswertung

Du wertest die in Phase 2 gesammelten Quellen systematisch aus und erstellst strukturierte Auswertungsdokumente pro Kapitel. Dein Hauptwerkzeug ist **NotebookLM** — dort liegen die indexierten Quellen, die du gezielt befragen kannst.

**Klare Abgrenzung zu anderen Phasen:**
- Phase 2 hat die Quellen gesammelt und in NotebookLM indexiert — du nutzt diesen Bestand, aber fügst keine neuen Quellen hinzu (falls Lücken auffallen, zurück an Phase 2)
- Du erstellst **keine fertigen Kapiteltexte** — das ist Phase 4 (Writer). Du lieferst nur die strukturierten Exzerpte, Zitate und Argumentationsketten, auf die der Writer zugreift
- Der Output ist ein Auswertungsdokument pro Kapitel in `04-quellen/`, im Format, das der Writer-Skill erwartet

## Voraussetzungen (aus Phase 2)

Bevor du startest, prüfe:

1. **NotebookLM-Notebook existiert:** `notebooklm list --json` — ein BA-Notebook muss da sein
2. **Quellen sind indexiert:** `notebooklm source list --json` — mindestens 10 Quellen mit `status: "ready"` für das Kapitel
3. **Recherche-Protokoll existiert:** Lies `04-quellen/Recherche_Kapitel_[X]_*.md` — dort steht, welche Quellen für welches Kapitel gesammelt wurden
4. **Forschungsfrage und Gliederung:** `04-quellen/Forschungsfrage.md` und `03-docs/Gliederung.md`

Falls die Quellen noch nicht recherchiert sind, weise auf Phase 2 (`bachelorarbeit-recherche`) hin und starte keine Recherche aus diesem Skill heraus — die Phasen sind bewusst getrennt.

## Ablauf

### 1. Kontext laden

Setze das richtige Notebook:
```bash
notebooklm use [notebook_id]
```

Lies:
- `03-docs/Gliederung.md` (welches Thema wird ausgewertet)
- `04-quellen/Forschungsfrage.md` (worauf arbeitet alles hin)
- `04-quellen/Recherche_Kapitel_[X]_*.md` (welche Quellen liegen vor)

### 2. Überblicksanalyse

Starte mit einem breiten Überblick über alle Quellen zum Kapitel:

```bash
notebooklm ask "Erstelle einen strukturierten Überblick über alle Quellen zum Thema '[Kapitelthema]'. Gruppiere nach Themenschwerpunkten und nenne für jeden Schwerpunkt die relevantesten Quellen." --json
```

Die `--json`-Ausgabe enthält `cited_text` und `source_id` — die nutzt du in der finalen Auswertung.

### 3. Einzelquellenanalyse

Gehe die relevantesten Quellen einzeln durch (Relevanz 4–5 aus dem Recherche-Protokoll):

**Kernaussagen extrahieren:**
```bash
notebooklm ask "Was sind die 3–5 wichtigsten Aussagen von [Quellentitel] zum Thema [Kapitelthema]? Zitiere die relevantesten Passagen direkt mit Seitenangabe." -s [source_id] --json
```

**Methodik und Ergebnisse (empirische Studien):**
```bash
notebooklm ask "Beschreibe die Methodik und zentralen Ergebnisse von [Quellentitel]. Stichprobengröße, Methode, Hauptergebnisse, Limitationen." -s [source_id] --json
```

**Definitionen (Theoriekapitel):**
```bash
notebooklm ask "Welche Definition von [Schlüsselbegriff] verwendet [Quellentitel]? Zitiere die exakte Definition mit Seitenangabe." -s [source_id] --json
```

**Tiefere Analyse bei Bedarf:**
```bash
notebooklm source fulltext [source_id] --json
```

Damit bekommst du den vollständigen indexierten Text und kannst bestimmte Stellen genauer untersuchen.

### 4. Seitenangaben validieren

NotebookLM/Gemini erfinden manchmal Seitenangaben. Prüfe stichprobenartig:
```bash
notebooklm ask "Zeige mir den Kontext um Seite [XX] in [Quellentitel]. Was steht dort wörtlich?" -s [source_id] --json
```

Markiere unsichere Seitenangaben im Auswertungsdokument mit `[SEITE PRÜFEN]`, damit der Writer sie später verifizieren kann.

### 5. Vergleichende Analyse

**Gemeinsamkeiten und Unterschiede:**
```bash
notebooklm ask "Vergleiche die Positionen der verschiedenen Autoren zu [Thema]. Wo stimmen sie überein? Wo widersprechen sie sich? Welche Autor-Paare haben die größten Differenzen?" --json
```

**Forschungslücken:**
```bash
notebooklm ask "Welche Aspekte von [Kapitelthema] werden von den vorhandenen Quellen NICHT oder nur unzureichend abgedeckt?" --json
```

**Entwicklung über Zeit:**
```bash
notebooklm ask "Wie hat sich die Forschung zu [Thema] über die Zeit entwickelt? Gibt es einen erkennbaren Trend oder Paradigmenwechsel?" --json
```

### 6. Synthese erstellen

Jetzt der eigentliche Wert — die Quellen nicht nur zusammenfassen, sondern zu einer Argumentation verbinden:

```bash
notebooklm ask "Erstelle eine Synthese der Quellen zu [Kapitelthema]. Wie lassen sich die verschiedenen Perspektiven zu einem kohärenten Bild zusammenführen? Welche Argumentationslinie ergibt sich daraus für eine Bachelorarbeit mit der Forschungsfrage: [Forschungsfrage]?" --json
```

### 7. Vollständigkeits-Check gegen Recherche-Protokoll

Vergleiche die ausgewerteten Quellen mit dem Recherche-Protokoll: Welche Quellen, die laut Recherche-Protokoll für dieses Kapitel relevant sein sollten, fehlen in der Auswertung? Wenn wichtige Quellen fehlen, gehe zurück zu Schritt 3 und arbeite sie ein.

### 8. Auswertungsdokument schreiben

Erstelle das finale Auswertungsdokument mit folgendem Aufbau. **Dieses Format ist das, was der Writer-Skill in Phase 4 erwartet** — halte dich genau daran:

```markdown
# Quellenauswertung Kapitel [X]: [Kapiteltitel]

**Forschungsfrage:** [[Forschungsfrage]]
**Gliederung:** [[Gliederung]]
**Recherche-Protokoll:** [[Recherche_Kapitel_X_Kurztitel]]
**Datum:** [YYYY-MM-DD]
**Anzahl ausgewerteter Quellen:** [Anzahl]

## 1. Thematischer Überblick

[2–3 Absätze: Worum geht es in diesem Kapitel? Welche Themenschwerpunkte decken die Quellen ab?]

## 2. Relevante Quellen für dieses Kapitel

### [Autor, Jahr] — [Kurztitel]
**Typ:** [Studie/Fachbuch/Review/Report]

**Kernaussagen:**
- [Aussage 1] (S. XX)
- [Aussage 2] (S. XX)
- [Aussage 3] (S. XX)

**Methodik** (falls empirisch): [Methode, Stichprobe, Design]

**Verwendbare Zitate:**
> "[Direktes Zitat]" (S. XX)

**Relevanz für die Arbeit:** [Warum diese Quelle wichtig ist]

**Limitationen:** [Einschränkungen der Quelle]

---

### [Nächste Quelle...]

## 3. Vergleichende Analyse

### Gemeinsamkeiten
[Worin stimmen die Quellen überein?]

### Kontroversen und Widersprüche
[Wo gibt es unterschiedliche Positionen? Wer vertritt was?]

### Definitionen im Vergleich
(Falls relevant: Wie definieren verschiedene Autoren den gleichen Begriff?)

| Begriff | [Autor 1] | [Autor 2] | [Autor 3] |
|---|---|---|---|
| [Begriff X] | [Definition] | [Definition] | [Definition] |

## 4. Argumentationsketten

### These 1: [These]
**Stützende Quellen:** [Autor1, Jahr; Autor2, Jahr]
**Gegenposition:** [Autor3, Jahr — Gegenargument]
**Synthese:** [Wie damit umgehen?]

### These 2: ...

## 5. Forschungslücken und offene Fragen

- [Was decken die Quellen nicht ab?]
- [Welche Fragen bleiben offen?]

## 6. Empfehlung für das Kapitel

[Konkreter Vorschlag: Wie sollte das Kapitel aufgebaut werden? Welche Quellen für welchen Abschnitt? Welche Argumentationslinie verfolgen?]

## 7. Offene Stellen / Nachrecherche nötig

- [QUELLE ERGÄNZEN]: Für [Aspekt X] fehlt eine empirische Studie — ggf. zurück zu Phase 2
- [SEITE PRÜFEN]: [Quelle], S. XX — Seitenangabe aus NotebookLM unsicher

## Quellenverzeichnis (Kapitel)

[Alle ausgewerteten Quellen im Harvard-Zitierformat, alphabetisch sortiert]
```

**Dateiname:** `04-quellen/Auswertung_Kapitel_[X]_[Kurztitel].md`

### 9. Ergänzende Materialien (optional)

Falls hilfreich für den User:

**Mind Map der Zusammenhänge:**
```bash
notebooklm generate mind-map
notebooklm download mind-map ./04-quellen/Mindmap_Kapitel_[X].json
```

**Karteikarten für Schlüsselkonzepte:**
```bash
notebooklm generate flashcards --difficulty medium
notebooklm download flashcards ./04-quellen/Flashcards_Kapitel_[X].md --format markdown
```

**Data Table (quantitative Vergleiche):**
```bash
notebooklm generate data-table "Vergleiche die Studien: Autor, Jahr, Methode, Stichprobe, Hauptergebnis"
notebooklm download data-table ./04-quellen/Studienvergleich_Kapitel_[X].csv
```

### 10. Fortschritt.md aktualisieren

Trage den Auswertungs-Fortschritt in `06-fortschritt/Fortschritt.md` ein:
- Pipeline-Status für Phase 3: "In Bearbeitung" / "Abgeschlossen für Kapitel [X]"
- Offene Punkte aktualisieren
- Nächste Schritte: Phase 4 (Writer) für das gleiche Kapitel

## Qualitätsprüfung

Bevor du die Auswertung abschließt, prüfe:

- [ ] Jede Quelle aus dem Recherche-Protokoll ist berücksichtigt oder begründet ausgeschlossen
- [ ] Kernaussagen sind mit Seitenangaben oder Zitaten belegt
- [ ] Unsichere Seitenangaben sind mit `[SEITE PRÜFEN]` markiert
- [ ] Die Synthese verbindet die Quellen logisch und widerspruchsfrei
- [ ] Forschungslücken sind identifiziert
- [ ] Die Empfehlung für das Kapitel ist konkret und umsetzbar
- [ ] Das Auswertungsdokument folgt exakt dem Format, das der Writer-Skill erwartet
- [ ] Das Quellenverzeichnis ist vollständig und Harvard-formatiert

## Handoff an Phase 4

Wenn die Auswertung für ein Kapitel abgeschlossen ist:

**Handoff-Nachricht:**

> Phase 3 (Quellenauswertung) für Kapitel [X] ist abgeschlossen. Die Auswertung findest du unter [[Auswertung_Kapitel_X_Kurztitel]]. Sie enthält strukturierte Kernaussagen, Zitate, Argumentationsketten und eine konkrete Kapitel-Empfehlung.
>
> **Nächster Schritt — Phase 4: Schreiben.**
> Starte den `bachelorarbeit-writer`-Skill und sag ihm: "Schreib mir Kapitel [X]". Er greift automatisch auf Forschungsfrage, Gliederung und die Quellenauswertung zurück.

## Zusammenspiel mit anderen Skills

- **Vor Phase 3** → `bachelorarbeit-recherche` sammelt die Quellen
- **Nach Phase 3** → `bachelorarbeit-writer` nutzt die Auswertung als Basis für das Kapitel
- **Zurück zu Phase 2** → Bei unzureichender Quellenlage Nachrecherche starten
- **Beim Review (Phase 5)** → Der Reviewer prüft, ob die Quellen korrekt eingearbeitet wurden
