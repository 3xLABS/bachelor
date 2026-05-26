---
name: bachelorarbeit
description: >
  Komplette Pipeline für eine wissenschaftliche Bachelorarbeit (BWL) — von der
  Themenfindung über Recherche, Quellenauswertung und Schreiben bis zur
  abgabefertigen Word-Datei. Acht klar getrennte Phasen, Harvard-Zitierstil,
  Obsidian-Wiki-Links, Multi-Tool-Workflow mit NotebookLM, Gemini und
  Perplexity. Nutze diesen Skill bei JEDER Anfrage, die mit einer
  Bachelorarbeit oder wissenschaftlichen Abschlussarbeit zu tun hat:
  "ich will eine Bachelorarbeit schreiben", "Forschungsfrage entwickeln",
  "Gliederung erstellen", "Zeitplan", "Quellen suchen", "Literaturrecherche",
  "Deep Research", "Quellen auswerten", "Kernaussagen extrahieren",
  "Kapitel schreiben", "Theorieteil", "Methodik formulieren", "Fazit
  schreiben", "Einleitung", "Diskussion", "Kapitel reviewen", "Feedback zu
  meinem Text", "Betreuer-Feedback einarbeiten", "Überarbeitung", "Revision",
  "Arbeit finalisieren", "Word-Datei erstellen", "Abgabeversion",
  "Literaturverzeichnis", "wie ist der Stand", "wo bin ich gerade". Auch wenn
  der User nur ein Kapitel teilt und fragt "schau mal drüber" oder eine
  Gliederung pastet und sagt "schreib mir Kapitel 2" — diesen Skill nutzen.
---

# Bachelorarbeit-Pipeline (Master-Skill)

Du unterstützt beim Schreiben einer Bachelorarbeit im Fachbereich BWL. Dieser Skill bündelt **acht spezialisierte Phasen** in einem einzigen Skill — die Detail-Anleitung pro Phase liegt in `references/`. Lade die Phase, in der du gerade arbeitest, und folge ihrer Anleitung.

**Grundprinzip: Phasen sind nicht austauschbar und nicht durchmischbar.** Die Planungs-Phase sucht keine Quellen. Die Recherche-Phase wertet nichts aus. Der Writer fügt keine neuen Quellen hinzu. Diese Trennung ist Absicht — sie macht die Pipeline robust und nachvollziehbar.

## Wie du diesen Skill benutzt

1. Lies zuerst diese SKILL.md komplett.
2. Bestimme aus der User-Anfrage, welche **Phase** dran ist (siehe Routing-Tabelle unten).
3. Lies die zugehörige Datei in `references/` — sie ist die vollständige Anleitung für diese Phase.
4. Folge der Phasen-Anleitung. Aktualisiere am Ende `04-fortschritt/Fortschritt.md`.
5. Übergib sauber an die nächste Phase, wenn die aktuelle abgeschlossen ist.

## Die acht Phasen

```
Phase 0: Onboarding         → references/phase-0-onboarding.md
Phase 1: Planung            → references/phase-1-planung.md
Phase 2: Recherche          → references/phase-2-recherche.md
Phase 3: Quellenauswertung  → references/phase-3-quellenauswertung.md
Phase 4: Schreiben          → references/phase-4-writer.md
Phase 5: Review             → references/phase-5-reviewer.md
Phase 6: Überarbeitung      → references/phase-6-ueberarbeitung.md
Phase 7: Finalisierung      → references/phase-7-finalisierung.md
```

Die Phasen 2–6 werden **pro Kapitel** durchlaufen.

## Routing — welche Phase bei welcher Anfrage

| User sagt... | Phase | Reference |
|---|---|---|
| "Alles bereit?", "Setup", "kann es losgehen?" | 0 | `phase-0-onboarding.md` |
| "Ich will eine Arbeit schreiben", "wo fange ich an?" | 1 | `phase-1-planung.md` |
| "Hilf mir bei der Forschungsfrage", "Gliederung erstellen" | 1 | `phase-1-planung.md` |
| "Quellen suchen", "Literatur finden", "Deep Research" | 2 | `phase-2-recherche.md` |
| "Quellen auswerten", "Kernaussagen extrahieren" | 3 | `phase-3-quellenauswertung.md` |
| "Schreib mir Kapitel 3", "Theorieteil schreiben" | 4 | `phase-4-writer.md` |
| "Schau dir mein Kapitel an", "Review", "Feedback" | 5 | `phase-5-reviewer.md` |
| "Arbeite das Feedback ein", "Mein Betreuer hat gesagt..." | 6 | `phase-6-ueberarbeitung.md` |
| "Mach die Arbeit fertig", "Word-Datei", "Abgabeversion" | 7 | `phase-7-finalisierung.md` |
| "Wie ist der Stand?" | — | Lies `04-fortschritt/Fortschritt.md` |

## Status-Flow eines Kapitels

```
Ausstehend → Erster Entwurf → Reviewed → Überarbeitet → Reviewed → Final
(Planung)     (Writer)        (Reviewer) (Überarbeitung) (Reviewer)  (Finalisierung)
```

## Fortschritt.md als geteilter State

Alle Phasen lesen und schreiben `04-fortschritt/Fortschritt.md`. Diese Datei ist die **einzige Quelle der Wahrheit** für:

- Welche Phase gerade läuft
- Welchen Status jedes Kapitel hat
- Welche Muss-Punkte aus Reviews noch offen sind
- Welche `[QUELLE ERGÄNZEN]`-Stellen noch zu füllen sind
- Was als nächstes ansteht

Wenn du unsicher bist, wo der User gerade steht: lies diese Datei.

## Empfohlene Schreibreihenfolge

1. **Theoretischer Rahmen** — legt die begriffliche Grundlage
2. **Methodik**
3. **Ergebnisse**
4. **Diskussion**
5. **Einleitung** (zuletzt — braucht den Überblick)
6. **Fazit** (zuletzt — beantwortet die Forschungsfrage)

## Ordnerstruktur

```
bachelor/                          ← Vault-Root
├── 01-docs/Gliederung.md
├── 02-quellen/
│   ├── Forschungsfrage.md
│   ├── Recherche_Kapitel_*.md
│   ├── Auswertung_Kapitel_*.md
│   └── Literaturverzeichnis_final.md
├── 03-text/[01-Einleitung, 02-Theoretischer Rahmen, ...]
├── 04-fortschritt/Fortschritt.md
├── 05-review/Review_Kapitel_*.md
└── 06-final/bachelorarbeit_final.docx
```

## Wichtige Konventionen (gelten phasenübergreifend)

- **Zitierstil:** Harvard, durchgehend. Indirekte Zitate mit "vgl.", Seitenangaben bei konkreten Stellen. Detail-Regeln in `references/harvard-zitierstil.md`.
- **Argumentationsstruktur:** Jeder Absatz mit mindestens einem gestützten Argument (Claim → Reason → Evidence). Mehr in `references/argumentationsstrukturen.md`.
- **Obsidian-Wiki-Links:** `[[BA_Quellenauswertung_Kapitel X#Autor, Jahr|Autor, Jahr]]`
- **Fehlende Quellen:** Immer `[QUELLE ERGÄNZEN]` markieren, nie erfinden
- **Unsichere Seitenangaben:** `[SEITE PRÜFEN]`
- **Dateinamen:** `Kapitel_[X]_[Kurztitel].md` in `03-text/[XX-Kapitel]/`, Reviews als `Review_Kapitel_[X]_[Kurztitel].md` in `05-review/`, Versionen mit `_v2`, `_v3`
- **Sprache:** Wissenschaftlich, dritte Person, kein Ich, kein Journalismus
- **Abbildungen:** Platzhalter `[ABBILDUNG X.Y: Beschreibung]`
- **Literaturverzeichnis:** Wird in Phase 7 automatisch aus den Kapitel-Quellenlisten zusammengebaut

## Externe Tools

Die Pipeline ist Multi-Tool. Claude liefert für jeden externen Schritt fertige Copy-Paste-Prompts.

| Tool | Wofür | Wann |
|---|---|---|
| **Perplexity** | Quellenrecherche | Phase 2 |
| **NotebookLM** | Quellenspeicher | Phase 2 + 3 |
| **Gemini** (via NotebookLM) | Quellenauswertung | Phase 3 |
| **Obsidian** | Vault-Ansicht | jederzeit |

## Vor der Abgabe

Wenn die Finalisierung (Phase 7) durchgelaufen ist, prüfe mit dem User:

1. Alle `[QUELLE ERGÄNZEN]`-Stellen geschlossen?
2. Alle `[SEITE PRÜFEN]`-Markierungen verifiziert?
3. Alle `[ABBILDUNG X.Y]`-Platzhalter durch echte Abbildungen ersetzt?
4. Literaturverzeichnis vollständig (Vorwärts- und Rückwärts-Check)?
5. Inhaltsverzeichnis in Word aktualisiert?
6. Plagiatsprüfung mit Hochschul-Software durchgeführt?
7. Formatierung mit Hochschulvorgaben abgeglichen?
8. Eidesstattliche Erklärung unterschrieben?

---

**Wichtig:** Diese SKILL.md ist die **Routing-Schicht**. Die operative Anleitung pro Phase steht in der jeweiligen `references/phase-N-*.md`. Wenn du eine Phase startest, **lies die Reference komplett** — sie enthält Schritt-für-Schritt-Anweisungen, Prompts und Output-Spezifikationen.
