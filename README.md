# Bachelorarbeit-Pipeline

Ein KI-gestütztes Skill-System für Bachelorarbeiten im Fachbereich BWL. Acht spezialisierte Claude-Skills arbeiten als Pipeline zusammen — von der Themenfindung bis zur abgabefertigen Word-Datei.

## Überblick

Die Pipeline verteilt die Arbeit auf mehrere Tools, die jeweils das tun, was sie am besten können:

| Tool | Rolle | Wann |
|---|---|---|
| **Perplexity** | Quellenrecherche | Quellen finden (Echtzeit-Websuche mit Quellenangaben) |
| **NotebookLM** | Quellenspeicher | Quellen laden, durchsuchbar machen, mit Gemini verbinden |
| **Gemini** (via NotebookLM) | Quellenauswertung | Quellen analysieren, Argumente extrahieren, Argumentationsketten bauen |
| **Claude** | Strukturarbeit + Schreiben | Planung steuern, Prompts generieren, Kapitel schreiben, reviewen, überarbeiten |
| **Obsidian** | Übersicht | Ordnerstruktur, Fortschritt, alle Dateien an einem Ort |

**Grundregel:** Perplexity sucht, NotebookLM + Gemini werten aus, Claude schreibt, Obsidian hält alles zusammen.

## Die acht Skills

### 0. bachelorarbeit-onboarding
Prüft die Voraussetzungen: richtiger Ordner, NotebookLM CLI installiert und authentifiziert, Sub-Skills vorhanden, Internetzugang, bestehender Fortschritt.

### 1. bachelorarbeit-planung
Der Einstiegspunkt. Bringt dich vom groben Thema zur schreibfertigen Ausgangslage: Forschungsfrage, Gliederung mit Seitenzahlen, Quellenrecherche und -auswertung. Orchestriert den Multi-Tool-Workflow und generiert Copy-Paste-Prompts für Perplexity und Gemini.

### 2. bachelorarbeit-recherche
Systematische Quellensuche mit NotebookLM, kapitelweise. Deep Research, schnelle Recherche, manuelles Hinzufügen bekannter Quellen.

### 3. bachelorarbeit-quellenauswertung
Leitet die Quellenauswertung mit Gemini (via Gem + NotebookLM) an. Claude liefert die Gem-Systemprompt, kapitelspezifische Prompts und übernimmt die Nachbearbeitung ins Writer-Format — die eigentliche Analyse läuft in Gemini, um Token zu sparen.

### 4. bachelorarbeit-writer
Schreibt einzelne Kapitel auf Basis von Forschungsfrage, Gliederung und Quellenauswertung. Produziert wissenschaftlichen Fließtext im Harvard-Zitierstil mit Claim-Reason-Evidence-Argumentation. Berücksichtigt Nachbarkapitel und kapiteltyp-spezifische Anforderungen.

### 5. bachelorarbeit-reviewer
Reviewt ein fertiges Kapitel aus Professorensicht. Bewertet Struktur, Argumentation, Quellenarbeit, Sprache und Formalia. Priorisiert Feedback in Muss/Sollte/Optional.

### 6. bachelorarbeit-ueberarbeitung
Arbeitet Review- oder Betreuer-Feedback systematisch in das Kapitel ein. Bewahrt die Textidentität, stärkt Argumente, ergänzt Quellen, harmonisiert mit der Gesamtarbeit.

### 7. bachelorarbeit-finalisierung
Prüft die gesamte Arbeit als Einheit (roter Faden, Begriffe, Zitierung, Übergänge), erstellt das Literaturverzeichnis und formatiert alles als abgabefertige Word-Datei (.docx).

## Gesamtablauf

```
Phase 0: ONBOARDING  → System-Check, Voraussetzungen prüfen
Phase 1: PLANUNG     → Thema → Forschungsfrage → Gliederung → Zeitplan
Phase 2: RECHERCHE   → Quellen suchen (NotebookLM + Perplexity)
Phase 3: AUSWERTUNG  → Quellen analysieren in Gemini (Claude liefert Prompts + formatiert)
Phase 4-6: SCHREIBEN (pro Kapitel wiederholen)
   Writer → Reviewer → Überarbeitung
                          ↓
              Bei Bedarf: Review → Überarbeitung (Zyklus)
Phase 7: FINALISIERUNG → Gesamtcheck → Literaturverzeichnis → Word-Datei
```

## Voraussetzungen

- **Claude** (Desktop-App mit Cowork-Mode oder Claude Code)
- **Perplexity** (für Quellenrecherche — kostenlose Version reicht)
- **Google NotebookLM** (kostenlos unter notebooklm.google.com)
- **Obsidian** (kostenlos unter obsidian.md — optional, aber empfohlen)

## Installation

### Schritt 1: Repository klonen

```bash
git clone https://github.com/3xLABS/bachelor.git
```

### Schritt 2: In Claude laden

1. Öffne **Claude Desktop** (Cowork-Mode) oder **Claude Code**
2. Wähle den `bachelor/`-Ordner als Arbeitsverzeichnis
3. Fertig — Claude erkennt `.claude/CLAUDE.md` und alle Skills automatisch

Alle Skills liegen in `.claude/skills/` und werden von Claude beim Ordner-Öffnen sofort geladen. Kein manuelles Kopieren nötig.

### Schritt 3: In Obsidian öffnen (optional)

Öffne den `bachelor/`-Ordner als Obsidian-Vault: Obsidian → Vault öffnen → Ordner auswählen.

### Schritt 4: Loslegen

Sage Claude einfach:
> „Ich will eine Bachelorarbeit schreiben."

oder:
> „Hilf mir bei der Forschungsfrage zu [dein Thema]."

Claude startet automatisch den Planungs-Skill.

## Ordnerstruktur

```
bachelor/                        ← Obsidian Vault Root + Git-Repo
├── .claude/
│   ├── CLAUDE.md                ← Pipeline-Orchestrierung (liest Claude automatisch)
│   └── skills/                  ← Alle 8 Skills (werden automatisch erkannt)
│       ├── bachelorarbeit-onboarding/
│       ├── bachelorarbeit-planung/
│       ├── bachelorarbeit-recherche/
│       ├── bachelorarbeit-quellenauswertung/
│       ├── bachelorarbeit-writer/
│       ├── bachelorarbeit-reviewer/
│       ├── bachelorarbeit-ueberarbeitung/
│       ├── bachelorarbeit-finalisierung/
│       └── notebooklm/
├── 01-docs/
│   ├── Gliederung.md            ← Deine Gliederung (wird in Phase 1 erstellt)
│   ├── BA-Gliederung-Muster.md  ← Vorlage mit Beispielgliederung
│   └── BA-Struktur-Muster.md    ← Standard-BWL-Struktur mit Seitenverteilung
├── 02-quellen/
│   ├── Forschungsfrage.md       ← Deine Forschungsfrage (wird in Phase 1 erstellt)
│   ├── Quellenverzeichnis.md    ← Alle gesammelten Quellen
│   └── Auswertung_KapX_*.md    ← Quellenauswertungen pro Kapitel
├── 03-text/
│   ├── 01-Einleitung/
│   ├── 02-Theoretischer Rahmen/
│   ├── 03-Methodik/
│   ├── 04-Ergebnisse/
│   ├── 05-Diskussion/
│   └── 06-Fazit/
├── 04-fortschritt/
│   └── Fortschritt.md           ← Zentrales Protokoll (geteilter State aller Skills)
├── 05-review/
│   └── Review_Kapitel_*.md      ← Reviews
├── 06-final/
│   └── bachelorarbeit_final.docx  ← Abgabe-Datei
└── Prompts.md                   ← 17 Copy-Paste-Prompts für alle Tools
```

## Schritt-für-Schritt-Anleitung

### Phase 0: Planung (1–2 Tage)

1. **Starte den Planungs-Skill** — Sage Claude: „Ich will eine Arbeit über [Thema] schreiben"
2. **Forschungsfrage entwickeln** — Claude führt dich durch die Themenfindung und hilft bei der Eingrenzung
3. **Gliederung erstellen** — Claude erstellt eine Gliederung mit Seitenvorgaben pro Kapitel
4. **Quellen recherchieren** — Claude generiert Perplexity-Prompts (siehe `Prompts.md`, Codes P-1 bis P-5). Kopiere die Prompts in Perplexity und sammle 40–80 Quellen
5. **Quellen in NotebookLM laden** — Erstelle ein Notebook pro Kapitelgruppe und lade die gefundenen PDFs/URLs hoch
6. **Quellen auswerten** — Sage Claude „Quellen auswerten für Kapitel X". Claude leitet dich durch das Gem-Setup und generiert fertige Prompts für Gemini. Du wertest in Gemini aus, Claude formatiert das Ergebnis danach ins Writer-Format.

### Phase 1: Kapitel schreiben

Empfohlene Reihenfolge:
1. Theoretischer Rahmen
2. Methodik
3. Ergebnisse
4. Diskussion
5. Einleitung (braucht den Überblick über die ganze Arbeit)
6. Fazit

Sage Claude pro Kapitel: „Schreib mir Kapitel 2: Theoretischer Rahmen" — der Writer-Skill übernimmt.

### Phase 2: Review

Sage Claude: „Review mein Kapitel 2" — der Reviewer-Skill prüft aus Professorensicht.

### Phase 3: Überarbeitung

Sage Claude: „Arbeite das Feedback ein" — der Überarbeitungs-Skill setzt die Review-Ergebnisse um.

Falls dein Betreuer eigenes Feedback gibt, sage: „Mein Betreuer hat gesagt: [Feedback]" — der Skill übersetzt das in konkrete Verbesserungen.

**Wiederhole Phase 1–3 für jedes Kapitel.**

### Phase 4: Finalisierung

Wenn alle Kapitel mindestens den Status „Überarbeitet" haben:

Sage Claude: „Mach die Arbeit fertig" — der Finalisierungs-Skill prüft den roten Faden, erstellt das Literaturverzeichnis und generiert die Word-Datei.

## Die Prompts.md

Die `Prompts.md` im Wurzelverzeichnis enthält 17 vorbereitete Prompts mit Platzhaltern:

| Code | Tool | Zweck |
|---|---|---|
| P-1 bis P-5 | Perplexity | Themenfindung, Hauptrecherche (80 Quellen), Nachrecherche, URL-Extraktion, Lückenanalyse |
| N-1 bis N-3 | NotebookLM | Setup-Anleitung, Quellenübersicht, Widersprüche finden |
| G-1 bis G-6 | Gemini | Forschungsfrage, Kapitel-Auswertung, Argumentationsketten, Definitionen, Methodik, Diskussion |
| C-1 bis C-5 | Claude | Planung, Kapitel schreiben, Review, Überarbeitung, Finalisierung |

Der Planungs-Skill füllt die `{{PLATZHALTER}}` automatisch mit deinen konkreten Werten aus.

## Fortschritt verfolgen

Die `Fortschritt.md` in `04-fortschritt/` wird von allen Skills automatisch aktualisiert. Sie zeigt:

- Forschungsfrage
- Status der Planungsphasen
- Kapiteltabelle mit Wörtern, Seiten, Datum und Status
- Offene `[QUELLE ERGÄNZEN]`-Stellen
- Nächste Schritte

Status-Flow eines Kapitels:
```
Planung → Erster Entwurf → Reviewed → Überarbeitet → Final
```

Frage jederzeit: „Wie ist der Stand?" — Claude liest die Fortschritt.md und gibt dir eine Übersicht.

## Konventionen

- **Zitierstil:** Harvard, durchgehend (vgl. Müller, 2023, S. 45)
- **Fehlende Quellen:** Werden als `[QUELLE ERGÄNZEN]` markiert, nie erfunden
- **Argumentation:** Jeder Absatz folgt dem Claim-Reason-Evidence-Muster
- **Sprache:** Wissenschaftlich, dritte Person, Präsens/Präteritum
- **Abbildungen:** Platzhalter `[ABBILDUNG X.Y: Beschreibung]` im Text

## Checkliste vor der Abgabe

1. Alle `[QUELLE ERGÄNZEN]`-Stellen geschlossen?
2. Alle `[ABBILDUNG X.Y]`-Platzhalter durch echte Abbildungen ersetzt?
3. Literaturverzeichnis vollständig (Vorwärts- und Rückwärts-Check)?
4. Inhaltsverzeichnis in Word aktualisiert?
5. Plagiatsprüfung mit Hochschul-Software durchgeführt?
6. Formatierung mit Hochschul-Vorgaben abgeglichen?
7. Eidesstattliche Erklärung unterschrieben?

## Lizenz

Frei nutzbar für persönliche und akademische Zwecke.

---

Erstellt mit der [Bachelorarbeit-Pipeline](https://github.com/3xLABS/bachelor) von [3xLABS](https://3xlabs.xyz).
