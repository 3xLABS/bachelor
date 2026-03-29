# Bachelorarbeit-Pipeline

Ein KI-gestütztes Skill-System für Bachelorarbeiten im Fachbereich BWL. Fünf spezialisierte Claude-Skills arbeiten als Pipeline zusammen — von der Themenfindung bis zur abgabefertigen Word-Datei.

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

## Die fünf Skills

### 0. bachelorarbeit-planung
Der Einstiegspunkt. Bringt dich vom groben Thema zur schreibfertigen Ausgangslage: Forschungsfrage, Gliederung mit Seitenzahlen, Quellenrecherche und -auswertung. Orchestriert den Multi-Tool-Workflow und generiert Copy-Paste-Prompts für Perplexity und Gemini.

### 1. bachelorarbeit-writer
Schreibt einzelne Kapitel auf Basis von Forschungsfrage, Gliederung und Quellenauswertung. Produziert wissenschaftlichen Fließtext im Harvard-Zitierstil mit Claim-Reason-Evidence-Argumentation. Berücksichtigt Nachbarkapitel und kapiteltyp-spezifische Anforderungen.

### 2. bachelorarbeit-reviewer
Reviewt ein fertiges Kapitel aus Professorensicht. Bewertet Struktur, Argumentation, Quellenarbeit, Sprache und Formalia. Priorisiert Feedback in Muss/Sollte/Optional.

### 3. bachelorarbeit-ueberarbeitung
Arbeitet Review- oder Betreuer-Feedback systematisch in das Kapitel ein. Bewahrt die Textidentität, stärkt Argumente, ergänzt Quellen, harmonisiert mit der Gesamtarbeit.

### 4. bachelorarbeit-finalisierung
Prüft die gesamte Arbeit als Einheit (roter Faden, Begriffe, Zitierung, Übergänge), erstellt das Literaturverzeichnis und formatiert alles als abgabefertige Word-Datei (.docx).

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
   Alle Kapitel → Gesamtcheck → Literaturverzeichnis → Word-Datei
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

### Schritt 2: In Obsidian öffnen (optional)

Öffne den `bachelor/`-Ordner als Obsidian-Vault: Obsidian → Vault öffnen → Ordner auswählen.

### Schritt 3: Skills in Claude laden

Die Skills befinden sich als `.skill`-Dateien in `02-skills/`. Um sie in Claude zu nutzen:

1. Öffne Claude Desktop (Cowork-Mode) oder Claude Code
2. Wähle den `bachelor/`-Ordner als Arbeitsverzeichnis
3. Claude erkennt die CLAUDE.md in `01-claude/` automatisch und weiß, welchen Skill er wann nutzen soll

**Alternativ** kannst du die `.skill`-Dateien manuell in deinen Claude-Skills-Ordner kopieren:
```bash
cp 02-skills/*.skill ~/.claude/skills/
```

### Schritt 4: Loslegen

Sage Claude einfach:
> „Ich will eine Bachelorarbeit schreiben."

oder:
> „Hilf mir bei der Forschungsfrage zu [dein Thema]."

Claude startet automatisch den Planungs-Skill.

## Ordnerstruktur

```
bachelor/                        ← Obsidian Vault Root
├── 01-claude/
│   └── CLAUDE.md                ← Pipeline-Orchestrierung (liest Claude automatisch)
├── 02-skills/
│   └── *.skill + *-SKILL.md    ← Alle 5 Skill-Dateien
├── 03-docs/
│   ├── Gliederung.md            ← Deine Gliederung (wird in Phase 0 erstellt)
│   ├── BA-Gliederung-Muster.md  ← Vorlage mit Beispielgliederung
│   └── BA-Struktur-Muster.md    ← Standard-BWL-Struktur mit Seitenverteilung
├── 04-quellen/
│   ├── Forschungsfrage.md       ← Deine Forschungsfrage (wird in Phase 0 erstellt)
│   ├── Quellenverzeichnis.md    ← Alle gesammelten Quellen
│   └── Auswertung_KapX_*.md    ← Quellenauswertungen pro Kapitel
├── 05-text/
│   ├── 01-Einleitung/
│   ├── 02-Theoretischer Rahmen/
│   ├── 03-Methodik/
│   ├── 04-Ergebnisse/
│   ├── 05-Diskussion/
│   └── 06-Fazit/
├── 06-fortschritt/
│   └── Fortschritt.md           ← Zentrales Protokoll (geteilter State aller Skills)
├── 07-review/
│   └── review_kapitel_*.md      ← Reviews
├── 08-final/
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
6. **Quellen auswerten** — Nutze die Gemini-Prompts (G-1 bis G-6 in `Prompts.md`) direkt in NotebookLM, um kapitelweise Auswertungen zu erstellen. Speichere die Ergebnisse als `Auswertung_KapX_*.md` in `04-quellen/`

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

Die `Fortschritt.md` in `06-fortschritt/` wird von allen Skills automatisch aktualisiert. Sie zeigt:

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
