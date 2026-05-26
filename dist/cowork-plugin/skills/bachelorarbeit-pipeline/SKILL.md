---
name: bachelorarbeit-pipeline
description: >
  Orchestrator-Skill für die Bachelorarbeit-Pipeline. Erklärt die acht Phasen
  (Onboarding, Planung, Recherche, Quellenauswertung, Schreiben, Review,
  Überarbeitung, Finalisierung), den Status-Flow eines Kapitels und welche
  Konventionen für Zitierung, Obsidian-Links und Argumentation gelten. Nutze
  diesen Skill bei Anfragen wie "wie funktioniert die Bachelorarbeit-Pipeline",
  "welche Phasen gibt es", "wie ist der Stand", "Stand der Arbeit", "was kommt
  als Nächstes", "wo bin ich gerade", "Überblick", "wie geht das hier",
  "Pipeline erklären", "wie hängen die Skills zusammen", "Konventionen",
  "Zitierstil", "Status meines Kapitels". Wenn der User klar in einer
  bestimmten Phase ist (z. B. "Forschungsfrage entwickeln", "Kapitel 3
  schreiben", "Review machen"), nutze stattdessen den jeweiligen Phasen-Skill.
---

# Bachelorarbeit-Pipeline — Orchestrator

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

## Ordnerstruktur

Die Pipeline erwartet diese Struktur im ausgewählten Vault-Ordner:

```
bachelor/                          ← Vault-Root
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

Wenn diese Struktur nicht existiert, leitet die Planungs-Phase (`bachelorarbeit-planung`) ihren Aufbau.

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
