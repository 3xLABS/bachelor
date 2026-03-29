# Bachelorarbeit-Pipeline

Du unterstützt beim Schreiben einer Bachelorarbeit im Fachbereich BWL. Dafür stehen fünf spezialisierte Skills bereit, die als Pipeline zusammenarbeiten. Der Prozess verteilt sich über mehrere Tools — jedes Tool übernimmt, was es am besten kann.

## Tool-Rollen

| Tool | Rolle | Wann |
|---|---|---|
| **Perplexity** | Quellenrecherche | Phase 4: Quellen finden (Echtzeit-Websuche mit Quellenangaben) |
| **NotebookLM** | Quellenspeicher | Phase 4-5: Quellen laden, durchsuchbar machen, mit Gemini verbinden |
| **Gemini** (via NotebookLM) | Quellenauswertung | Phase 5: Quellen analysieren, Argumente extrahieren, Argumentationsketten bauen |
| **Claude** | Strukturarbeit + Schreiben | Alle Phasen: Planung steuern, Prompts generieren, Kapitel schreiben, reviewen, überarbeiten, finalisieren |
| **Obsidian** | Übersicht | Durchgehend: Ordnerstruktur, Fortschritt, alle Dateien an einem Ort |

**Grundregel:** Perplexity sucht, NotebookLM + Gemini werten aus, Claude schreibt, Obsidian hält alles zusammen.

## Die fünf Skills

### 0. bachelorarbeit-planung
Der Einstiegspunkt. Bringt den User vom groben Thema zur schreibfertigen Ausgangslage: Forschungsfrage, Gliederung mit Seitenzahlen, Quellenrecherche und -auswertung. Orchestriert den Multi-Tool-Workflow und generiert Copy-Paste-Prompts für Perplexity und Gemini.

**Input:** Thema (oder gar nichts)
**Output:** Forschungsfrage, Gliederung, Quellenverzeichnis, kapitelweise Quellenauswertungen, initialisierte Fortschritt.md
**Tools:** Perplexity → NotebookLM → Gemini → Claude

### 1. bachelorarbeit-writer
Schreibt einzelne Kapitel auf Basis von Forschungsfrage, Gliederung mit Seitenzahlen und Quellenauswertung. Produziert wissenschaftlichen Fließtext im Harvard-Zitierstil mit Claim-Reason-Evidence-Argumentation.

**Input:** Forschungsfrage, Gliederung, Quellenauswertung
**Output:** `kapitel_X_Y_name.md` + aktualisierte `Fortschritt.md` (Status: "Erster Entwurf")
**Tools:** Claude

### 2. bachelorarbeit-reviewer
Reviewt ein fertig geschriebenes Kapitel aus Professorensicht. Bewertet Struktur, Argumentation, Quellenarbeit, Sprache und Formalia. Priorisiert Feedback in Muss/Sollte/Optional.

**Input:** Kapitel-Datei (.md), optional Forschungsfrage + Gliederung
**Output:** `review_kapitel_X_Y.md` + aktualisierte `Fortschritt.md` (Status: "Reviewed")
**Tools:** Claude

### 3. bachelorarbeit-ueberarbeitung
Arbeitet das Review-Feedback systematisch in das Kapitel ein. Bewahrt die Textidentität, stärkt Argumente, ergänzt Quellen, harmonisiert mit der Gesamtarbeit.

**Input:** Kapitel-Datei + Review-Datei, optional neue Quellen
**Output:** `kapitel_X_Y_name_v2.md` (mit Änderungsprotokoll) + aktualisierte `Fortschritt.md` (Status: "Überarbeitet")
**Tools:** Claude

### 4. bachelorarbeit-finalisierung
Prüft die gesamte Arbeit als Einheit (roter Faden, Begriffe, Zitierung, Übergänge) und formatiert sie als abgabefertige Word-Datei (.docx) nach den Formatvorgaben der Hochschule.

**Input:** Alle finalen Kapitel-Dateien + Formatvorgaben
**Output:** `bachelorarbeit_final.docx` + Prüfbericht + aktualisierte `Fortschritt.md` (Status: "Final")
**Tools:** Claude

## Gesamtablauf

```
Phase 0: PLANUNG (bachelorarbeit-planung)
   Thema → Forschungsfrage → Gliederung → Quellen suchen (Perplexity)
   → Quellen laden (NotebookLM) → Quellen auswerten (Gemini)

Phase 1-3: SCHREIBEN (pro Kapitel wiederholen)
   Quellenauswertung → Writer → Reviewer → Überarbeitung
                                    ↓
                        Bei Bedarf: Review → Überarbeitung (Zyklus)

Phase 4: FINALISIERUNG
   Alle Kapitel → Gesamtcheck → Word-Datei
```

## Standardablauf pro Kapitel

```
Writer → Reviewer → Überarbeitung
         ↓              ↓
    review_*.md    kapitel_*_v2.md
```

1. **Schreiben**: Forschungsfrage + Gliederung + Quellenauswertung → Writer erstellt das Kapitel
2. **Review**: Das fertige Kapitel wird dem Reviewer übergeben → Review mit Bewertung und Handlungsbedarf
3. **Überarbeitung**: Kapitel + Review gehen an den Überarbeitungs-Skill → verbesserte Version _v2

Falls das Review nach der Überarbeitung noch offene Punkte zeigt, kann der Zyklus Review → Überarbeitung wiederholt werden (_v3, _v4 etc.).

## Empfohlene Schreibreihenfolge

1. **Theoretischer Rahmen** — legt die begriffliche und theoretische Grundlage
2. **Methodik** — damit die empirische Herangehensweise steht
3. **Ergebnisse** — basierend auf der Methodik
4. **Diskussion** — setzt Theorie und Ergebnisse in Bezug
5. **Einleitung** — braucht den Überblick über die ganze Arbeit
6. **Fazit** — beantwortet die Forschungsfrage auf Basis der Ergebnisse

## Wenn alle Kapitel fertig sind

```
Alle kapitel_*_v2.md → Finalisierung → bachelorarbeit_final.docx
```

Der Finalisierungs-Skill wird erst aufgerufen, wenn alle Kapitel mindestens den Status "Überarbeitet" haben.

## Fortschritt.md als geteilter State

Alle fünf Skills lesen und schreiben `Fortschritt.md` in `06-fortschritt/`. Diese Datei ist das zentrale Protokoll:

- **Forschungsfrage** steht einmal oben und gilt für die gesamte Arbeit
- **Planungstabelle** zeigt den Status der Vorbereitungsphasen
- **Kapiteltabelle** zeigt Dateinamen, Wörter, Seiten, Datum und Status jedes Kapitels
- **Offene Punkte** listet alle [QUELLE ERGÄNZEN]-Stellen mit Kontext
- **Nächste Schritte** zeigt, was als nächstes ansteht

Status-Flow eines Kapitels durch die Pipeline:
```
Planung → Erster Entwurf → Reviewed → Überarbeitet → Final
(Planung)    (Writer)      (Reviewer)  (Überarbeitung)  (Finalisierung)
```

## Wann welchen Skill nutzen

| User sagt... | Skill |
|---|---|
| "Ich will eine Arbeit schreiben" / "Wo fange ich an?" | bachelorarbeit-planung |
| "Hilf mir bei der Forschungsfrage" / "Gliederung erstellen" | bachelorarbeit-planung |
| "Quellen suchen" / "Quellen auswerten" | bachelorarbeit-planung |
| "Schreib mir Kapitel 3" | bachelorarbeit-writer |
| "Schau dir mein Kapitel an" / "Review" | bachelorarbeit-reviewer |
| "Arbeite das Feedback ein" / "Überarbeite" | bachelorarbeit-ueberarbeitung |
| "Mein Betreuer hat gesagt..." / "Betreuer-Feedback" | bachelorarbeit-ueberarbeitung |
| "Mach die Arbeit fertig" / "Word-Datei" / "Abgabeversion" | bachelorarbeit-finalisierung |
| "Wie ist der Stand?" | → Lies `06-fortschritt/Fortschritt.md` |

## Obsidian-Ordnerstruktur

```
bachelor/                        ← Obsidian Vault Root
├── 01-claude/
│   └── CLAUDE.md                ← Diese Datei (Pipeline-Orchestrierung)
├── 02-skills/
│   └── *.skill                  ← Alle Skill-Dateien
├── 03-docs/
│   ├── Gliederung.md            ← Deine Gliederung
│   ├── BA-Gliederung-Muster.md  ← Vorlage
│   └── BA-Struktur-Muster.md   ← Vorlage
├── 04-quellen/
│   ├── Forschungsfrage.md       ← Deine Forschungsfrage
│   ├── Quellenverzeichnis.md    ← Alle Quellen
│   └── Auswertung_KapX_*.md    ← Quellenauswertungen pro Kapitel
├── 05-text/
│   ├── 01-Einleitung/
│   ├── 02-Theoretischer Rahmen/
│   ├── 03-Methodik/
│   ├── 04-Ergebnisse/
│   ├── 05-Diskussion/
│   └── 06-Fazit/
├── 06-fortschritt/
│   └── Fortschritt.md           ← Zentrales Protokoll (geteilter State)
├── 07-review/
│   └── review_kapitel_*.md      ← Reviews
└── 08-final/
    └── bachelorarbeit_final.docx  ← Abgabe-Datei
```

## Wichtige Konventionen

- **Zitierstil:** Harvard, durchgehend. Indirekte Zitate mit "vgl.", Seitenangaben bei konkreten Stellen
- **Fehlende Quellen:** Immer `[QUELLE ERGÄNZEN]` markieren, nie erfinden
- **Dateinamen:** `kapitel_X_Y_beschreibung.md` in `05-text/`, Reviews als `review_kapitel_X_Y.md` in `07-review/`, Versionen mit `_v2`, `_v3` etc.
- **Sprache:** Wissenschaftlich, dritte Person, Präsens/Präteritum, kein Ich, kein Journalismus
- **Argumentation:** Jeder Absatz braucht mindestens ein gestütztes Argument (Claim → Reason → Evidence)
- **Vorlagen:** Prüfe immer zuerst `03-docs/` und `04-quellen/` auf existierende Muster und Beispiele
- **Abbildungen:** Platzhalter `[ABBILDUNG X.Y: Beschreibung]` im Text, Nummerierung nach Kapitel (Abb. 2.1 = erste Abb. in Kap. 2)
- **Prompts.md:** Enthält Copy-Paste-Vorlagen für Perplexity, NotebookLM und Gemini. Der Planungs-Skill füllt die Platzhalter mit konkreten Werten aus.
- **Literaturverzeichnis:** Wird von der Finalisierung automatisch aus allen Kapitel-Quellenübersichten + dem Quellenverzeichnis zusammengebaut
- **Betreuer-Feedback:** Kann direkt in den Überarbeitungs-Skill gegeben werden (Stichpunkte, E-Mail, Word-Kommentare) — wird intern in Muss/Sollte/Optional übersetzt

## Vor der Abgabe

Checkliste, die der User vor dem Einreichen durchgehen sollte:
1. Alle [QUELLE ERGÄNZEN]-Stellen geschlossen?
2. Alle [ABBILDUNG X.Y]-Platzhalter durch echte Abbildungen ersetzt?
3. Literaturverzeichnis vollständig (Vorwärts- und Rückwärts-Check)?
4. Inhaltsverzeichnis in Word aktualisiert (Rechtsklick → Felder aktualisieren)?
5. Plagiatsprüfung mit Hochschul-Software durchgeführt?
6. Formatierung mit Hochschul-Vorgaben abgeglichen?
7. Eidesstattliche Erklärung unterschrieben?

## Reihenfolge bei neuem Projekt

Wenn ein User komplett neu beginnt:

1. **Planung starten** → bachelorarbeit-planung: Thema, Forschungsfrage, Gliederung, Quellen
2. **Quellen recherchieren** → User arbeitet mit Perplexity (Prompts vom Planungs-Skill)
3. **Quellen laden** → User lädt URLs/PDFs in NotebookLM
4. **Quellen auswerten** → User nutzt Gemini/NotebookLM (Prompts vom Planungs-Skill)
5. **Kapitel schreiben** → bachelorarbeit-writer (kapitelweise, Theorie zuerst)
6. **Kapitel reviewen** → bachelorarbeit-reviewer
7. **Feedback einarbeiten** → bachelorarbeit-ueberarbeitung
8. **Schritte 5-7 für jedes Kapitel wiederholen**
9. **Finalisieren** → bachelorarbeit-finalisierung: Gesamtcheck + Word-Datei
