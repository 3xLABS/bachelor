# Bachelorarbeit-Pipeline

Du unterstützt beim Schreiben einer Bachelorarbeit im Fachbereich BWL. Dafür stehen **acht spezialisierte Skills** bereit, die als strikt getrennte Phasen zusammenarbeiten. Jede Phase hat klare Voraussetzungen (was muss vorliegen, damit sie starten kann) und einen klar definierten Output (was sie der nächsten Phase übergibt).

**Grundprinzip: Phasen sind nicht austauschbar und nicht durchmischbar.** Der Planungs-Skill sucht keine Quellen. Der Recherche-Skill wertet nichts aus. Der Writer fügt keine neuen Quellen hinzu. Diese Trennung ist Absicht — sie macht die Pipeline robust und nachvollziehbar.

## Die acht Phasen

```
┌───────────────────────────────────────────────────────────────┐
│ Phase 0: Onboarding     → bachelorarbeit-onboarding           │
│ Phase 1: Planung        → bachelorarbeit-planung              │
│ Phase 2: Recherche      → bachelorarbeit-recherche            │
│ Phase 3: Quellenauswertung → bachelorarbeit-quellenauswertung │
│ Phase 4: Schreiben      → bachelorarbeit-writer               │
│ Phase 5: Review         → bachelorarbeit-reviewer             │
│ Phase 6: Überarbeitung  → bachelorarbeit-ueberarbeitung       │
│ Phase 7: Finalisierung  → bachelorarbeit-finalisierung        │
└───────────────────────────────────────────────────────────────┘
```

Die Phasen 2–6 werden **pro Kapitel** durchlaufen und sind dabei oft verschachtelt: Während für Kapitel 3 gerade geschrieben wird (Phase 4), kann für Kapitel 4 schon recherchiert werden (Phase 2).

## Phasen im Detail

### Phase 0 — Onboarding (`bachelorarbeit-onboarding`)
Prüft die Voraussetzungen: richtiger Ordner, Google-Account für NotebookLM & Gemini, Sub-Skills vorhanden, Internetzugang, bestehender Fortschritt.

**Input:** Nichts
**Output:** System-Check-Report, ggf. automatische Reparatur fehlender Teile

### Phase 1 — Planung (`bachelorarbeit-planung`)
Inhaltliches Fundament: Themenfindung, Forschungsfrage, Gliederung mit Seitenzahlen, Ordnerstruktur, Zeitplanung. **Berührt keine Quellen** — das ist explizit Phase 2.

**Input:** Thema (oder gar nichts)
**Output:** `02-quellen/Forschungsfrage.md`, `01-docs/Gliederung.md`, `03-text/XX-*/`-Ordner, initialisierte `04-fortschritt/Fortschritt.md` mit Zeitplanung
**Tools:** Claude im Dialog

### Phase 2 — Recherche (`bachelorarbeit-recherche`)
Systematische Quellensuche, kapitelweise. Claude entwickelt die Recherchestrategie und generiert Suchbegriffe. Der User navigiert **selbstständig** zu NotebookLM im Browser und führt Deep Research, schnelle Recherche und manuelles Hinzufügen bekannter Quellen dort durch. Claude dokumentiert alles im Recherche-Protokoll. **Wertet nichts aus** — das ist Phase 3.

**Input:** Forschungsfrage, Gliederung
**Output:** NotebookLM-Notebook mit indexierten Quellen (vom User im Browser verwaltet), `02-quellen/Recherche_Kapitel_[X]_*.md` pro Kapitel
**Tools:** Claude (Strategie + Dokumentation), User bedient NotebookLM selbstständig im Browser

### Phase 3 — Quellenauswertung (`bachelorarbeit-quellenauswertung`)
Die Quellenauswertung läuft **in Gemini**, nicht in Claude — das spart Token. Claude liefert die Anleitung (Gem-Setup, kapitelspezifische Prompts) und übernimmt die Nachbearbeitung des Gemini-Outputs ins Writer-Format. Der User öffnet **selbstständig** Google AI Studio / NotebookLM im Browser und führt die Prompts dort aus. **Produziert keinen Fließtext** — das ist Phase 4.

**Input:** Recherche-Protokoll + indexiertes NotebookLM-Notebook
**Output:** `02-quellen/Auswertung_Kapitel_[X]_*.md` im Format, das der Writer erwartet
**Tools:** Claude (Anleitung + Nachbearbeitung), User bedient Gemini / Google AI Studio selbstständig im Browser

### Phase 4 — Schreiben (`bachelorarbeit-writer`)
Schreibt **ein Kapitel pro Lauf** im wissenschaftlichen Stil mit Harvard-Zitierung und Obsidian-Wiki-Links. Beachtet Kapiteltyp (Einleitung/Theorie/Methodik/Ergebnisse/Diskussion/Fazit) und Nachbarkapitel. **Gate:** Startet nur, wenn die Quellenauswertung vorliegt.

**Input:** Forschungsfrage, Gliederung, Quellenauswertung, ggf. Nachbarkapitel
**Output:** `03-text/XX-Kapitel/Kapitel_[X]_[Kurztitel].md` mit Status "Erster Entwurf"
**Tools:** Claude

### Phase 5 — Review (`bachelorarbeit-reviewer`)
Bewertet Struktur, Argumentation, Quellenarbeit, Sprache, Formalia aus Professorensicht. Priorisiert Feedback in Muss/Sollte/Optional.

**Input:** Kapitel-Datei + Quellenauswertung + Forschungsfrage + Gliederung
**Output:** `05-review/Review_Kapitel_[X]_[Kurztitel].md` mit Status-Entscheidung, Status des Kapitels in Fortschritt.md auf "Reviewed"
**Tools:** Claude

### Phase 6 — Überarbeitung (`bachelorarbeit-ueberarbeitung`)
Arbeitet das Review-Feedback (oder Betreuer-Feedback) systematisch ein. Bewahrt Textidentität, stärkt Argumente, ergänzt Quellen, harmonisiert. Erstellt versionierte Datei.

**Input:** Kapitel-Datei + Review-Datei (oder Betreuer-Feedback)
**Output:** `03-text/XX-Kapitel/Kapitel_[X]_[Kurztitel]_v2.md` mit Änderungsprotokoll, Status "Überarbeitet"
**Tools:** Claude

### Phase 7 — Finalisierung (`bachelorarbeit-finalisierung`)
Gesamtcheck der Arbeit (roter Faden, Begriffskonsistenz, Übergänge), Erstellung des Literaturverzeichnisses aus allen Kapitel-Quellenlisten, Word-Formatierung nach Hochschulvorgaben.

**Input:** Alle reviewten/überarbeiteten Kapitel-Dateien + Formatvorgaben + Titelblatt-Infos
**Output:** `06-final/bachelorarbeit_final.docx` + `02-quellen/Literaturverzeichnis_final.md` + Prüfbericht
**Tools:** Claude + docx-js

## Pipeline-Flow

```
Phase 0: Onboarding  (einmal zu Beginn)
        │
        ▼
Phase 1: Planung
        │     ↓ Forschungsfrage + Gliederung + Zeitplan
        ▼
Phase 2: Recherche  ────┐
        │               │  (pro Kapitel)
        ▼               │
Phase 3: Quellenauswertung
        │               │
        ▼               │
Phase 4: Writer         │
        │               │
        ▼               │
Phase 5: Reviewer       │
        │               │
        ▼               │
  Muss-Punkte? ──ja─▶ Phase 6: Überarbeitung
        │                     │
       nein                   └──▶ zurück zu Phase 5 (Re-Review)
        │
        ▼
  Alle Kapitel Status "Reviewed" oder "Final"?
        │
        ▼
Phase 7: Finalisierung → bachelorarbeit_final.docx
```

## Status-Flow eines Kapitels

```
Ausstehend → Erster Entwurf → Reviewed → Überarbeitet → Reviewed → Final
(Planung)     (Writer)        (Reviewer) (Überarbeitung) (Reviewer)  (Finalisierung)
```

- **Ausstehend** — Kapitel ist in der Gliederung, aber noch nichts geschrieben
- **Erster Entwurf** — Writer hat eine v1 produziert
- **Reviewed** — Reviewer hat ein Review geschrieben (die Review-Datei sagt, ob Überarbeitung nötig ist)
- **Überarbeitet** — Überarbeitungs-Skill hat v2 (oder v3, v4) produziert
- **Final** — Finalisierung hat das Kapitel in die Word-Datei übernommen

## Fortschritt.md als geteilter State

Alle Skills lesen und schreiben `04-fortschritt/Fortschritt.md`. Diese Datei ist die **einzige Quelle der Wahrheit** für:

- Welche Phase der Pipeline gerade läuft
- Welchen Status jedes Kapitel hat
- Welche Muss-Punkte aus Reviews noch offen sind
- Welche `[QUELLE ERGÄNZEN]`-Stellen noch zu füllen sind
- Was als nächstes ansteht
- Soll-/Ist-Vergleich der Zeitplanung

Jeder Skill aktualisiert Fortschritt.md am Ende seines Laufs. Wenn du unsicher bist, wo der User gerade steht, lies diese Datei.

## Empfohlene Schreibreihenfolge

1. **Theoretischer Rahmen** — legt die begriffliche Grundlage
2. **Methodik** — danach steht die empirische Herangehensweise
3. **Ergebnisse** — basierend auf der Methodik
4. **Diskussion** — setzt Theorie und Ergebnisse in Bezug
5. **Einleitung** — braucht den Überblick über die ganze Arbeit
6. **Fazit** — beantwortet die Forschungsfrage auf Basis der Ergebnisse

Einleitung und Fazit **zuletzt**, weil sie erst dann sauber geschrieben werden können, wenn der Kern der Arbeit steht.

## Wann welchen Skill nutzen

| User sagt... | Skill |
|---|---|
| "Alles bereit?" / "Setup" / "kann es losgehen?" | bachelorarbeit-onboarding |
| "Ich will eine Arbeit schreiben" / "Wo fange ich an?" | bachelorarbeit-planung |
| "Hilf mir bei der Forschungsfrage" / "Gliederung erstellen" / "Zeitplan" | bachelorarbeit-planung |
| "Quellen suchen" / "Literatur finden" / "Deep Research" | bachelorarbeit-recherche |
| "Quellen auswerten" / "was sagen die Papers" / "Kernaussagen extrahieren" | bachelorarbeit-quellenauswertung |
| "Schreib mir Kapitel 3" / "Theorieteil schreiben" | bachelorarbeit-writer |
| "Schau dir mein Kapitel an" / "Review" / "Feedback" | bachelorarbeit-reviewer |
| "Arbeite das Feedback ein" / "Überarbeite" / "Mein Betreuer hat gesagt..." | bachelorarbeit-ueberarbeitung |
| "Mach die Arbeit fertig" / "Word-Datei" / "Abgabeversion" | bachelorarbeit-finalisierung |
| "Wie ist der Stand?" | → Lies `04-fortschritt/Fortschritt.md` |

## Ordnerstruktur

```
bachelor/                          ← Obsidian Vault Root + Git-Repo
├── .claude/
│   ├── CLAUDE.md                  ← Diese Datei (Pipeline-Orchestrierung)
│   └── skills/
│       ├── bachelorarbeit-onboarding/SKILL.md
│       ├── bachelorarbeit-planung/SKILL.md
│       ├── bachelorarbeit-recherche/SKILL.md
│       ├── bachelorarbeit-quellenauswertung/SKILL.md
│       ├── bachelorarbeit-writer/
│       │   ├── SKILL.md
│       │   └── references/         ← Harvard-Stil, Argumentationsstrukturen
│       ├── bachelorarbeit-reviewer/SKILL.md
│       ├── bachelorarbeit-ueberarbeitung/SKILL.md
│       └── bachelorarbeit-finalisierung/SKILL.md
├── 01-docs/
│   ├── Gliederung.md              ← Aus Phase 1
│   └── BA-*-Muster.md             ← Vorlagen
├── 02-quellen/
│   ├── Forschungsfrage.md         ← Aus Phase 1
│   ├── Recherche_Kapitel_*.md     ← Aus Phase 2
│   ├── Auswertung_Kapitel_*.md    ← Aus Phase 3
│   └── Literaturverzeichnis_final.md  ← Aus Phase 7
├── 03-text/
│   ├── 01-Einleitung/
│   │   ├── Kapitel_1_Einleitung.md       ← v1 aus Phase 4
│   │   └── Kapitel_1_Einleitung_v2.md    ← Aus Phase 6
│   ├── 02-Theoretischer Rahmen/
│   ├── 03-Methodik/
│   ├── 04-Ergebnisse/
│   ├── 05-Diskussion/
│   └── 06-Fazit/
├── 04-fortschritt/
│   └── Fortschritt.md             ← Zentrales Protokoll
├── 05-review/
│   └── Review_Kapitel_*.md        ← Aus Phase 5
├── 06-final/
│   └── bachelorarbeit_final.docx  ← Aus Phase 7
└── Prompts.md                     ← Copy-Paste-Prompts für externe Tools
```

## Wichtige Konventionen

- **Zitierstil:** Harvard, durchgehend. Indirekte Zitate mit "vgl.", Seitenangaben bei konkreten Stellen
- **Obsidian-Wiki-Links:** Quellenangaben im Text verlinken in die Quellenauswertung: `[[BA_Quellenauswertung_Kapitel X#Autor, Jahr|Autor, Jahr]]`
- **Fehlende Quellen:** Immer `[QUELLE ERGÄNZEN]` markieren, nie erfinden
- **Unsichere Seitenangaben:** `[SEITE PRÜFEN]` (stammt aus Phase 3, wird vom Writer übernommen)
- **Dateinamen:** `Kapitel_[X]_[Kurztitel].md` in `03-text/[XX-Kapitel]/`, Reviews als `Review_Kapitel_[X]_[Kurztitel].md` in `05-review/`, Versionen mit `_v2`, `_v3`
- **Sprache:** Wissenschaftlich, dritte Person, kein Ich, kein Journalismus
- **Argumentation:** Jeder Absatz mit mindestens einem gestützten Argument (Claim → Reason → Evidence)
- **Abbildungen:** Platzhalter `[ABBILDUNG X.Y: Beschreibung]` im Text (Nummerierung nach Kapitel)
- **Literaturverzeichnis:** Wird von Phase 7 automatisch aus allen Kapitel-Quellenlisten zusammengebaut — Phase 4 pflegt pro Kapitel die `## Verwendete Quellen in diesem Kapitel`-Tabelle
- **Betreuer-Feedback:** Geht direkt in Phase 6 (Überarbeitung), egal in welchem Format

## Vor der Abgabe

Checkliste für den User:
1. Alle `[QUELLE ERGÄNZEN]`-Stellen geschlossen?
2. Alle `[SEITE PRÜFEN]`-Markierungen verifiziert?
3. Alle `[ABBILDUNG X.Y]`-Platzhalter durch echte Abbildungen ersetzt?
4. Literaturverzeichnis vollständig (Vorwärts- und Rückwärts-Check)?
5. Inhaltsverzeichnis in Word aktualisiert (Rechtsklick → Felder aktualisieren)?
6. Plagiatsprüfung mit Hochschul-Software durchgeführt?
7. Formatierung mit Hochschulvorgaben abgeglichen?
8. Eidesstattliche Erklärung unterschrieben?
