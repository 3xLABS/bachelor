---
name: bachelorarbeit-planung
description: >
  Plant eine Bachelorarbeit von Grund auf: Themenfindung, Forschungsfrage, Gliederung mit Seitenzahlen und Quellenrecherche/-auswertung. Orchestriert einen Multi-Tool-Workflow: Perplexity für Quellenrecherche, NotebookLM + Gemini für Quellenauswertung, Claude für Strukturarbeit, Obsidian für Übersicht. Nutze bei: "ich will eine Arbeit schreiben", "Thema finden", "Forschungsfrage entwickeln", "Gliederung erstellen", "Quellen suchen", "wie fange ich an", "ich hab noch nichts", "Bachelorarbeit planen", "Thesis starten", "wo anfangen", "Quellenrecherche", "Quellen auswerten". Auch wenn der User ein Thema hat, aber weder Forschungsfrage noch Gliederung noch Quellen.
---

# Bachelorarbeit-Planung

Du bist der Einstiegspunkt der Pipeline. Bevor der Writer auch nur einen Satz schreiben kann, braucht er drei Dinge: eine Forschungsfrage, eine Gliederung mit Seitenzahlen, und ausgewertete Quellen. Dieser Skill hilft dem User, genau das zu erarbeiten — Schritt für Schritt, mit einem Multi-Tool-Workflow.

## Tool-Rollen im Workflow

Die Planung nutzt bewusst verschiedene Tools für verschiedene Stärken:

| Tool | Rolle | Warum |
|---|---|---|
| **Perplexity** | Quellenrecherche | Echtzeit-Websuche mit Quellenangaben, findet aktuelle Studien, Reports, Bücher |
| **NotebookLM** | Quellenspeicher | Lädt PDFs/URLs, macht sie durchsuchbar, verbindet mit Gemini |
| **Gemini** (via NotebookLM) | Quellenauswertung | Analysiert geladene Quellen, extrahiert Argumente, baut Argumentationsketten |
| **Claude** | Strukturarbeit | Forschungsfrage schärfen, Gliederung bauen, Qualität prüfen, Ergebnisse zusammenführen |
| **Obsidian** | Übersicht | Ordnerstruktur, Fortschritt, alle Dateien an einem Ort |

**Claudes Rolle in diesem Skill:** Du steuerst den Prozess, generierst Copy-Paste-Prompts für die externen Tools, prüfst die Ergebnisse, und bereitest alles so auf, dass der Writer-Skill nahtlos übernehmen kann.

## Ausgangslage klären

Frage den User zuerst, wo er steht. Es gibt typischerweise vier Einstiegspunkte:

| User hat... | Starte bei... |
|---|---|
| Gar nichts (nur "ich will eine Arbeit schreiben") | Phase 1: Themenfindung |
| Ein grobes Thema ("irgendwas mit Digitalisierung") | Phase 2: Forschungsfrage |
| Thema + Forschungsfrage | Phase 3: Gliederung |
| Thema + Forschungsfrage + Gliederung, aber keine Quellen | Phase 4: Quellenrecherche |
| Alles, aber Quellen nicht ausgewertet | Phase 5: Quellenauswertung |

Frage auch nach:
- **Studiengang** — bestimmt fachlichen Kontext
- **Hochschule/Lehrstuhl** — für eventuelle Vorgaben
- **Seitenumfang** — typisch: Bachelorarbeit 30-50 Seiten
- **Abgabefrist** — für die Zeitplanung

## Phase 1: Themenfindung

Falls der User noch kein Thema hat, hilf ihm eines zu finden. Das passiert primär im Gespräch mit Claude.

**Vorgehen:**
1. Frage nach Interessen, Schwerpunkten im Studium, Praxiserfahrungen
2. Schlage 3-5 Themenfelder vor, die wissenschaftlich bearbeitbar und aktuell sind
3. Für das gewählte Themenfeld: Grenze es ein auf eine bearbeitbare Größe

**Qualitätskriterien für ein gutes Thema:**
- Eingegrenzt genug, um in der vorgegebenen Seitenanzahl sinnvoll bearbeitbar zu sein
- Aktuell und relevant (für BWL: Praxisbezug)
- Wissenschaftlich fundierbar (es gibt genug Literatur)
- Enthält eine implizite Spannung oder offene Frage (nicht nur deskriptiv)

**Wenn der User gar keine Idee hat**, biete an, mit Perplexity aktuelle Trendthemen im Fachbereich zu recherchieren. Gib dem User diesen Prompt zum Kopieren:

```
Recherchiere aktuelle Trendthemen für eine Bachelorarbeit im Fachbereich [BWL/Wirtschaftsinformatik/...]. Fokussiere dich auf Themen, die:
- Wissenschaftlich fundiert sind (genug Literatur vorhanden)
- Einen Praxisbezug haben
- Aktuell und relevant sind (2024-2026)
Gib mir 10 Themenvorschläge mit jeweils einer kurzen Begründung der Relevanz.
```

## Phase 2: Forschungsfrage entwickeln

Sobald ein Thema steht, wird daraus eine präzise Forschungsfrage. Das ist der wichtigste Schritt der gesamten Planung — die Forschungsfrage bestimmt alles Weitere.

**Vorgehen:**
1. Lies, was der User zum Thema hat (Notizen, Ideen, Vorgaben vom Betreuer)
2. Prüfe, ob im Arbeitsverzeichnis bereits eine Forschungsfrage existiert (z.B. `04-quellen/BA_Forschungsfrage.md`)
3. Falls nicht: Entwickle mit dem User eine Forschungsfrage

**Anforderungen an eine gute Forschungsfrage:**
- **Spezifisch:** Nicht "Wie funktioniert Risikomanagement?", sondern "Wie integrieren mittelständische Unternehmen Cyberrisiken in ihr bestehendes Risikomanagement?"
- **Beantwortbar:** Die Frage muss mit dem gewählten methodischen Ansatz und im gegebenen Umfang beantwortbar sein
- **Nicht trivial:** Die Antwort darf nicht offensichtlich sein ("Ja, Risikomanagement ist wichtig")
- **Strukturgebend:** Aus der Frage soll sich die Gliederung quasi von selbst ergeben

**Struktur der Forschungsfrage:**
- Eine Hauptforschungsfrage (die zentrale Frage der Arbeit)
- 2-3 Unterforschungsfragen (optional, strukturieren die Hauptfrage)

Speichere die fertige Forschungsfrage als `04-quellen/Forschungsfrage.md` mit:
- Die Forschungsfrage(n)
- Kurze Herleitung (warum diese Frage relevant ist)
- Abgrenzung (was die Arbeit NICHT untersucht)

**Wenn ein Muster vorliegt:** Prüfe, ob `04-quellen/BA_Forschungsfrage.md` existiert und nutze es als Vorlage für Struktur und Tiefe.

## Phase 3: Gliederung erstellen

Mit der Forschungsfrage steht das Ziel — jetzt braucht es den Weg dorthin. Die Gliederung ist die Architektur der Arbeit.

**Vorgehen:**
1. Prüfe, ob Muster-Gliederungen im Verzeichnis liegen (z.B. `03-docs/BA-Gliederung-Muster.md`, `03-docs/BA-Struktur-Muster.md`). Falls ja, lies sie und nutze sie als Strukturvorlage.
2. Erstelle eine Gliederung, die auf die konkrete Forschungsfrage zugeschnitten ist
3. Weise jedem Kapitel Seitenzahlen zu (basierend auf dem Gesamtumfang)

**Standardstruktur einer BWL-Abschlussarbeit** (falls keine Muster vorliegen):

| Kapitel | Anteil | Seiten (bei 40 S.) |
|---|---|---|
| 1 Einleitung | 10-15% | 4-6 |
| 2 Theoretischer Rahmen | 25-35% | 10-14 |
| 3 Methodik | 10-20% | 4-8 |
| 4 Ergebnisse | 15-25% | 6-10 |
| 5 Diskussion | 10-15% | 4-6 |
| 6 Fazit | 5-10% | 2-4 |

**Qualitätskriterien:**
- Jedes Kapitel hat einen klaren Zweck im Hinblick auf die Forschungsfrage
- Logischer Aufbau: Problem → Theorie → Methode → Ergebnisse → Einordnung
- Nicht mehr als 3 Gliederungsebenen (1.1.1 ist das Maximum)
- Kein Kapitel mit nur einem Unterkapitel (wenn 3.1, dann auch 3.2)
- Seitenzahlen addieren sich zum Gesamtumfang

Speichere die Gliederung als `03-docs/Gliederung.md`.

**Obsidian-Ordnerstruktur anlegen:** Erstelle für jedes Hauptkapitel einen Unterordner in `05-text/`:

```
05-text/
├── 01-Einleitung/
├── 02-Theoretischer Rahmen/
├── 03-Methodik/
├── 04-Ergebnisse/
├── 05-Diskussion/
└── 06-Fazit/
```

## Phase 4: Quellenrecherche

Jetzt wird systematisch nach Quellen gesucht. Das passiert primär mit **Perplexity** — Claude steuert den Prozess und prüft die Ergebnisse.

### 4.1 Recherche-Strategie

Erstelle zuerst eine Recherche-Strategie basierend auf der Gliederung:

- Welche Kapitel brauchen welche Art von Quellen?
- Theoriekapitel: Grundlagenwerke, Standardliteratur, Lehrbücher
- Empirische Kapitel: Aktuelle Studien, Reports, Branchenberichte
- Methodenkapitel: Methodenliteratur (Mayring, Yin, Creswell etc.)

### 4.2 Perplexity-Prompts generieren

Nutze die Prompt-Vorlagen aus `Prompts.md` (im Vault-Root) als Basis. Passe die Platzhalter an das konkrete Thema, die Forschungsfrage und die Gliederung des Users an:

- **P-2** (Hauptrecherche): Setze Thema, Kapitelthemen und gewünschte Quellenanzahl ein
- **P-3** (Nachrecherche): Für Kapitel mit zu wenig Quellen
- **P-5** (Lückenanalyse): Nachdem das erste Quellenverzeichnis steht

Gib dem User den fertigen, ausgefüllten Prompt zum direkten Kopieren — keine Platzhalter mehr, alles eingesetzt.

### 4.3 Quellenverzeichnis prüfen

Wenn der User das Ergebnis aus Perplexity zurückbringt:

1. **Prüfe die Qualität:** Sind die Quellen wissenschaftlich? Aktuell? Relevant für die Forschungsfrage?
2. **Prüfe auf Duplikate:** Gleiche Quelle unter verschiedenen Titeln?
3. **Prüfe die Abdeckung:** Hat jedes Kapitel der Gliederung genug Quellen?
4. **Identifiziere Lücken:** Welche Kapitel brauchen noch mehr Quellen?

Speichere das geprüfte Quellenverzeichnis als `04-quellen/Quellenverzeichnis.md`.

### 4.4 URL-Liste für NotebookLM

Extrahiere alle URLs aus dem Quellenverzeichnis und gib sie dem User als kopierbare Liste:

```
Hier sind die URLs zum Laden in NotebookLM:

1. https://www.iso.org/standard/65694.html
2. https://example.com/studie.pdf
3. ...
```

Weise den User an (siehe auch `Prompts.md`, Abschnitt N-1):
1. Gehe zu **NotebookLM** (notebooklm.google.com)
2. Erstelle ein neues Notebook mit dem Titel der Arbeit
3. Lade alle URLs/PDFs als Quellen hoch
4. Verbinde **Gemini** mit dem Notebook (falls nicht automatisch)
5. **Wichtig: Prüfe nach dem Upload, ob alle Quellen einen grünen Haken haben.** Manche URLs laden nicht (Paywalls, Login-Walls, PDF-Captchas). Liste die fehlgeschlagenen Quellen und lade sie manuell als PDF hoch oder suche alternative URLs.

## Phase 5: Quellenauswertung

Die Quellenauswertung ist der aufwendigste Schritt. Hier werden aus Roh-Quellen die Exzerpte und Argumentationsketten, die der Writer-Skill braucht. Das passiert primär mit **Gemini via NotebookLM** — Claude liefert die Prompts und prüft die Ergebnisse.

### 5.1 Gemini-Prompts für Quellenauswertung

Nutze die Prompt-Vorlagen aus `Prompts.md` als Basis. Die Auswertung erfolgt **kapitelweise**, nicht für alle Quellen auf einmal.

- **G-2** (Kapitelspezifische Quellenauswertung): Der Hauptprompt — setze Kapitel, Forschungsfrage und spezifische Aspekte ein
- **G-3** (Argumentationsketten): Für Theorie- und Diskussionskapitel besonders wichtig
- **G-4** (Definitionen): Für das Theoriekapitel — zentrale Begriffe aus verschiedenen Quellen sammeln
- **G-5** (Methodenkapitel): Speziell für die Methodenbegründung
- **G-6** (Diskussion vorbereiten): Wenn Ergebnisse und Theorie zusammengeführt werden

Passe die Platzhalter an das konkrete Kapitel an und gib dem User den fertigen Prompt zum Kopieren.

**Wichtig: Kopierformat.** Weise den User an, den Gemini-Output als Markdown-Codeblock zu kopieren (damit die Formatierung erhalten bleibt):
1. In Gemini: Auf "Kopieren" klicken (nicht manuell markieren)
2. In Claude: Als Codeblock einfügen oder als Datei hochladen

### 5.2 Ergebnis prüfen und aufbereiten

Wenn der User die Auswertung aus Gemini/NotebookLM zurückbringt:

1. **Prüfe die Quellenangaben:** Stimmen Autoren, Jahre, Seitenangaben? Gleiche sie gegen `04-quellen/Quellenverzeichnis.md` ab. Gemini erfindet manchmal Seitenangaben — markiere unsichere Stellen mit [SEITENANGABE PRÜFEN]
2. **Vollständigkeits-Check:** Vergleiche die ausgewerteten Quellen mit dem Quellenverzeichnis. Welche Quellen, die laut Verzeichnis für dieses Kapitel relevant sein sollten, fehlen in der Auswertung? → Weise den User darauf hin, diese in NotebookLM gezielt nachzufragen
3. **Prüfe die Relevanz:** Arbeiten die Exzerpte auf die Forschungsfrage hin?
4. **Ergänze Struktur:** Ordne die Exzerpte den Unterkapiteln der Gliederung zu
5. **Identifiziere Lücken:** Wo fehlen Quellen für bestimmte Argumente? → Markiere mit [QUELLE ERGÄNZEN]

Speichere die aufbereitete Quellenauswertung kapitelweise:
```
04-quellen/
├── Quellenverzeichnis.md
├── Forschungsfrage.md
├── Auswertung_Kap2_Theoretischer_Rahmen.md
├── Auswertung_Kap3_Methodik.md
├── Auswertung_Kap4_Ergebnisse.md
└── ...
```

### 5.3 Format der Quellenauswertung

Jede kapitelspezifische Auswertung folgt diesem Format (damit der Writer-Skill sie direkt verwenden kann):

```markdown
# Quellenauswertung: Kapitel [X] — [Kapiteltitel]

## Relevante Quellen für dieses Kapitel

### [Autor, Jahr] — [Kurztitel]
**Kernaussagen:**
- [Aussage 1] (S. XX)
- [Aussage 2] (S. XX)

**Verwendbare Zitate:**
- "[Direktes Zitat]" (S. XX)

**Relevanz:** [Warum diese Quelle für dieses Kapitel wichtig ist]

---

### [Nächste Quelle...]

## Argumentationsketten

### These 1: [These]
**Stützende Quellen:** [Autor1, Jahr; Autor2, Jahr]
**Gegenposition:** [Autor3, Jahr — Gegenargument]
**Synthese:** [Wie damit umgehen?]

## Offene Stellen
- [QUELLE ERGÄNZEN]: Für [Aspekt X] fehlt eine empirische Studie
- [QUELLE ERGÄNZEN]: Definition von [Begriff Y] braucht eine zusätzliche Grundlagenquelle
```

## Phase 6: Handoff an den Writer

Wenn alle Phasen abgeschlossen sind, prüfe die Bereitschaft für den Writer-Skill:

**Checkliste vor Handoff:**
- [ ] Forschungsfrage liegt vor (`04-quellen/Forschungsfrage.md`)
- [ ] Gliederung mit Seitenzahlen liegt vor (`03-docs/Gliederung.md`)
- [ ] Quellenverzeichnis ist vollständig (`04-quellen/Quellenverzeichnis.md`)
- [ ] Quellenauswertungen existieren für mindestens das erste zu schreibende Kapitel
- [ ] Obsidian-Ordnerstruktur ist angelegt
- [ ] Fortschritt.md ist initialisiert

**Fortschritt.md initialisieren:**

```markdown
# Fortschritt Bachelorarbeit


**Thema:** [Thema]
**Forschungsfrage:** [Hauptforschungsfrage]
**Gesamtumfang:** ca. [X] Seiten
**Abgabe:** [Datum]
**Letzte Aktualisierung:** [Heute]

## Planung

| Phase | Status | Datum |
|---|---|---|
| Themenfindung | Abgeschlossen | [Datum] |
| Forschungsfrage | Abgeschlossen | [Datum] |
| Gliederung | Abgeschlossen | [Datum] |
| Quellenrecherche | Abgeschlossen | [Datum] |
| Quellenauswertung | [Status] | [Datum] |

## Fertiggestellte Kapitel

| Kapitel | Dateiname | Wörter | Seiten (ca.) | Datum | Status |
|---|---|---|---|---|---|
| — | — | — | — | — | — |

## Offene Punkte

- Quellenauswertung für Kapitel [X] steht noch aus
- [QUELLE ERGÄNZEN]-Stellen: noch keine (Planung abgeschlossen)

## Nächste Schritte

- Erstes Kapitel schreiben: [Empfehlung, welches Kapitel zuerst]
- Auswertung für [Kapitel] in NotebookLM/Gemini durchführen
```

Speichere die Fortschritt.md in `06-fortschritt/Fortschritt.md`.

## Phase 7: Zeitplanung

Erstelle eine Rückwärtsplanung basierend auf dem Abgabedatum. Das hilft dem User, den Überblick zu behalten und realistisch zu planen.

**Faustregel für Zeitverteilung:**

| Phase | Anteil der Gesamtzeit |
|---|---|
| Planung & Quellenarbeit (Phasen 1-5) | 20-25% |
| Schreiben (alle Kapitel) | 40-50% |
| Review & Überarbeitung | 15-20% |
| Finalisierung & Korrekturlesen | 10-15% |
| Puffer (unvorhergesehenes) | 5-10% |

**Vorgehen:**
1. Vom Abgabedatum 1 Woche abziehen → Deadline für Finalisierung
2. Davon nochmal 1 Woche → Deadline für letztes Review/Überarbeitung
3. Restliche Zeit auf Kapitel verteilen (gewichtet nach Seitenumfang)
4. Ergebnis als Meilenstein-Tabelle in die Fortschritt.md eintragen:

```markdown
## Zeitplanung

| Meilenstein | Soll-Datum | Ist-Datum | Status |
|---|---|---|---|
| Planung abgeschlossen | [Datum] | [Datum] | ✅ |
| Kap. 2 Theorie geschrieben | [Datum] | — | ⬜ |
| Kap. 2 reviewed + überarbeitet | [Datum] | — | ⬜ |
| Kap. 3 Methodik geschrieben | [Datum] | — | ⬜ |
| ... | ... | ... | ... |
| Alle Kapitel überarbeitet | [Datum] | — | ⬜ |
| Finalisierung + Word-Datei | [Datum] | — | ⬜ |
| Korrekturlesen + Plagiatcheck | [Datum] | — | ⬜ |
| **Abgabe** | **[Datum]** | — | ⬜ |
```

**Empfehlung für die Schreibreihenfolge:**
- Beginne mit dem **Theoriekapitel** — es legt die begriffliche Grundlage
- Dann **Methodik** — damit die empirische Herangehensweise steht
- Dann **Ergebnisse** — basierend auf der Methodik
- Dann **Diskussion** — setzt Theorie und Ergebnisse in Bezug
- **Einleitung** und **Fazit** zuletzt — sie brauchen den Überblick über die ganze Arbeit

Teile dem User mit, dass er jetzt den **bachelorarbeit-writer** Skill nutzen kann. Gib ihm eine kurze Anleitung:

> Alles ist bereit für den Writer. Sag einfach: "Schreib mir Kapitel [X]" und stelle die Forschungsfrage, die Gliederung und die Quellenauswertung für das Kapitel bereit. Der Writer übernimmt von hier.

## Obsidian-Ordnerstruktur

Dieser Skill arbeitet innerhalb der Obsidian-Vault-Struktur. Alle Dateien werden an ihren vorgesehenen Orten gespeichert:

```
bachelor/                        ← Obsidian Vault Root
├── 01-claude/
│   └── CLAUDE.md                ← Pipeline-Orchestrierung
├── 02-skills/
│   └── *.skill                  ← Alle Skill-Dateien
├── 03-docs/
│   ├── Gliederung.md            ← Deine Gliederung
│   ├── BA-Gliederung-Muster.md  ← Muster (Vorlage)
│   └── BA-Struktur-Muster.md   ← Muster (Vorlage)
├── 04-quellen/
│   ├── Forschungsfrage.md       ← Deine Forschungsfrage
│   ├── Quellenverzeichnis.md    ← Alle Quellen
│   └── Auswertung_KapX_*.md    ← Quellenauswertungen pro Kapitel
├── 05-text/
│   ├── 01-Einleitung/
│   ├── 02-Theoretischer Rahmen/
│   └── ...                      ← Kapitel-Ordner
├── 06-fortschritt/
│   └── Fortschritt.md           ← Zentrales Protokoll
├── 07-review/
│   └── review_kapitel_*.md      ← Reviews vom Reviewer-Skill
└── 08-final/
    └── bachelorarbeit_final.docx  ← Finale Abgabe-Datei
```

## Wenn Vorlagen existieren

Prüfe immer zuerst, ob im Arbeitsverzeichnis bereits Vorlagen oder Muster liegen:

- `03-docs/BA-Gliederung-Muster.md` → Nutze als Strukturvorlage für die Gliederung
- `03-docs/BA-Struktur-Muster.md` → Nutze für Kapitelaufteilung und Seitenanteile
- `04-quellen/BA_Forschungsfrage.md` → Nutze als Qualitätsbeispiel für Forschungsfragen
- `04-quellen/BA_Quellenverzeichnis_Gesamt.md` → Nutze das Format als Vorlage für das Quellenverzeichnis

Falls diese Dateien existieren, lies sie und orientiere dich an ihrem Format und ihrer Tiefe. Sie sind Referenzbeispiele dafür, wie die Outputs dieses Skills aussehen sollen.
