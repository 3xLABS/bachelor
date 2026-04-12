---
name: bachelorarbeit-quellenauswertung
description: >
  Phase 3 der Bachelorarbeit-Pipeline: Leitet den User durch die Quellenauswertung mit Gemini (via NotebookLM oder Gem). Claude liefert Anleitung, kapitelspezifische Prompts und die Gem-Systemprompt, der User führt die Auswertung in Gemini durch, Claude hilft beim Nachbearbeiten ins Writer-Format. Spart Token, weil die eigentliche Analyse bei Gemini läuft. Nutze bei: "Quellen auswerten", "Literatur analysieren", "was sagen die Quellen zu", "Quellenauswertung", "Literaturanalyse", "Quellen zusammenfassen", "Quellen vergleichen", "was steht in den Papers", "extrahiere die Kernaussagen", "erstelle eine Quellenübersicht", "werte die Quellen aus", "Gem erstellen", "Gemini Auswertung". Nicht für Quellensuche — dafür gibt es `bachelorarbeit-recherche`.
---

# Bachelorarbeit — Phase 3: Quellenauswertung (via Gemini)

Die Quellenauswertung läuft **nicht in Claude**, sondern in **Gemini** — entweder über einen dedizierten Gem oder direkt im NotebookLM-Chat. Das spart Token und nutzt Geminis Stärke: es hat direkten Zugriff auf die indexierten Quellen in NotebookLM.

**Claudes Rolle in Phase 3:**
1. **Vorbereitung:** Gem-Setup-Anleitung, kapitelspezifische Prompts generieren
2. **Nachbearbeitung:** Gemini-Output ins exakte Format bringen, das der Writer-Skill (Phase 4) erwartet

**Claudes Rolle ist NICHT:** Die Quellen selbst zu lesen oder auszuwerten. Das macht Gemini.

## Übersicht: Workflow

```
Claude                          User                           Gemini
──────                          ────                           ──────
1. Gem-Setup-Anleitung    →     User erstellt Gem              
2. Kapitel-Prompts        →     User gibt Prompts in Gem  →   Gemini analysiert Quellen
                                User kopiert Output       →   
3. Nachbearbeitung        ←     User gibt Output an Claude
4. Fertige Auswertung     →     Datei in 02-quellen/
```

## Ablauf

### Schritt 1: Voraussetzungen prüfen

Bevor du startest, lies:
- `01-docs/Gliederung.md` — Welches Kapitel wird ausgewertet?
- `02-quellen/Forschungsfrage.md` — Worauf arbeitet alles hin?
- `02-quellen/Recherche_Kapitel_[X]_*.md` — Welche Quellen liegen vor? (aus Phase 2)

Falls die Recherche für das Kapitel noch nicht abgeschlossen ist → zurück zu Phase 2 (`bachelorarbeit-recherche`).

### Schritt 2: Gem erstellen (einmalig)

Der User muss einmalig einen Gem in Google AI Studio erstellen. Leite ihn Schritt für Schritt an:

**Anleitung für den User:**

> **Gem erstellen — Schritt für Schritt:**
>
> 1. Öffne [Google AI Studio](https://aistudio.google.com/) → Melde dich mit deinem Google-Konto an
> 2. Klicke links auf **„Gems"** (oder gehe direkt zu aistudio.google.com/gems)
> 3. Klicke **„New Gem"** / **„Neuer Gem"**
> 4. **Name:** `BA Quellenauswertung`
> 5. **Systemprompt:** Kopiere den Inhalt, den Claude dir gleich gibt, komplett in das Systemprompt-Feld
> 6. Klicke **„Save"** / **„Speichern"**
> 7. Fertig — der Gem ist jetzt in deiner Gem-Liste und kann mit NotebookLM-Notebooks verbunden werden

Gib dem User dann den Inhalt der Datei `references/gem-systemprompt.md` als Copy-Paste-Block. Lies dazu:

```
.claude/skills/bachelorarbeit-quellenauswertung/references/gem-systemprompt.md
```

**Wichtig:** Der Gem muss nur einmal erstellt werden. Bei weiteren Kapiteln nutzt der User denselben Gem.

### Schritt 3: Kapitelspezifische Prompts generieren

Für jedes Kapitel generierst du **konkrete, fertige Prompts** — keine Platzhalter, sondern mit den tatsächlichen Werten aus Forschungsfrage und Gliederung vorausgefüllt.

Generiere diese Prompts und gib sie dem User als nummerierte Copy-Paste-Blöcke:

#### Prompt A — Kapitelauswertung (Hauptprompt)

Fülle die Platzhalter mit den konkreten Werten des Users:

```
Erstelle eine vollständige Quellenauswertung für Kapitel [X]: "[Kapiteltitel]" meiner Bachelorarbeit.

Die Forschungsfrage lautet: "[Forschungsfrage]"

Dieses Kapitel soll folgende Unterkapitel abdecken:
[Unterkapitel aus Gliederung auflisten]

Nutze EXAKT das Ausgabeformat aus deiner Systemprompt. Gehe alle relevanten Quellen im Notebook durch und werte sie kapitelspezifisch aus. Achte besonders auf:
- Kernaussagen mit Seitenangaben
- Verwendbare direkte Zitate
- Argumentationsketten
- Vergleichende Analyse (Gemeinsamkeiten, Widersprüche)
- Konkrete Empfehlung für den Kapitelaufbau
```

#### Prompt B — Definitionen (für Theoriekapitel)

```
Durchsuche alle Quellen nach Definitionen für folgende Begriffe, die in Kapitel [X] zentral sind:

1. [Begriff 1]
2. [Begriff 2]
3. [Begriff 3]

Für jeden Begriff: Alle Definitionen mit Autor, Jahr, Seite. Gemeinsamkeiten, Unterschiede, und eine Empfehlung für die Arbeitsdefinition.
```

#### Prompt C — Argumentationsketten

```
Baue eine wissenschaftliche Argumentationskette für Kapitel [X]: "[Kapiteltitel]".

Die zentrale These dieses Kapitels: "[These — aus Gliederung/Forschungsfrage ableiten]"

Für jedes Argument: Claim → Reason → Evidence (mit konkreten Quellen und Seitenangaben). Zeige auch Gegenargumente und eine Synthese.
```

#### Prompt D — Methodik-Auswertung (nur für Methodenkapitel)

```
Werte die methodenbezogenen Quellen für mein Methodenkapitel aus.

Geplante Methode: [Methode aus Gliederung]

Liefere:
1. Methodenbeschreibung (mit Seitenangaben)
2. Begründung für den Einsatz bei meiner Forschungsfrage
3. Ablauf/Schritte laut Quellen
4. Gütekriterien
5. Limitationen
6. Alternative Methoden und warum meine Wahl besser ist
```

#### Prompt E — Widersprüche und Forschungslücken

```
Analysiere die Quellen zu Kapitel [X] auf:

1. Wo widersprechen sich Autoren? Wer vertritt welche Position? Welche ist besser belegt?
2. Welche Aspekte von [Kapitelthema] werden NICHT oder nur unzureichend abgedeckt?
3. Gibt es einen erkennbaren Forschungstrend oder Paradigmenwechsel?
```

#### Prompt F — Diskussionsvorbereitung (nur für Diskussionskapitel)

```
Bereite mein Diskussionskapitel vor:

1. Theorie-Empirie-Abgleich: Welche theoretischen Vorhersagen werden bestätigt/widerlegt?
2. Einordnung in den Forschungsstand
3. Praktische Implikationen und Handlungsempfehlungen
4. Limitationen ähnlicher Studien
5. Offene Fragen und Forschungsbedarf

Immer mit konkreten Quellenbelegen (Autor, Jahr, Seite).
```

**Welche Prompts du generierst, hängt vom Kapiteltyp ab:**

| Kapiteltyp | Prompts |
|---|---|
| Theoretischer Rahmen | A + B + C + E |
| Methodik | A + D |
| Ergebnisse | A + C + E |
| Diskussion | A + C + E + F |
| Einleitung | A (nur Überblick) |
| Fazit | A (nur Überblick) |

### Schritt 4: User führt Auswertung in Gemini durch

Erkläre dem User:

> **So nutzt du die Prompts:**
>
> 1. Öffne deinen **BA Quellenauswertung**-Gem in Google AI Studio
> 2. Verbinde ihn mit deinem NotebookLM-Notebook (oder öffne NotebookLM und nutze den Gem dort)
> 3. Gib **Prompt A** ein und warte auf die vollständige Antwort
> 4. Gib dann die weiteren Prompts (B, C, D, E, F — je nach Kapitel) einzeln ein
> 5. **Kopiere alle Antworten** und gib sie mir (Claude) — ich bringe sie ins richtige Format

**Tipp für den User:** In NotebookLM kann der User vor dem Chat bestimmte Quellen auswählen (Häkchen setzen), um die Antwort auf die kapitelrelevanten Quellen einzuschränken.

### Schritt 5: Nachbearbeitung (Claude)

Wenn der User den Gemini-Output zurückbringt, machst du Folgendes:

1. **Prüfe die Struktur:** Entspricht der Output dem Format, das der Writer-Skill erwartet? (Siehe Template unten)
2. **Ergänze fehlende Abschnitte:** Falls Gemini einen Abschnitt ausgelassen hat (z.B. Argumentationsketten, Forschungslücken), weise darauf hin
3. **Markierungen setzen:**
   - `[SEITE PRÜFEN]` bei Seitenangaben, die verdächtig rund oder unplausibel wirken
   - `[QUELLE ERGÄNZEN]` bei Aspekten, die keine Quellenabdeckung haben
4. **Formatierung normalisieren:** Harvard-Zitierformat konsistent machen, Obsidian-Wiki-Links ergänzen wo nötig
5. **Quellenverzeichnis prüfen:** Sind alle zitierten Quellen im Verzeichnis am Ende aufgeführt?
6. **Datei erstellen:** Speichere als `02-quellen/Auswertung_Kapitel_[X]_[Kurztitel].md`

**Was Claude in der Nachbearbeitung NICHT tut:**
- Keine neuen Quellen erfinden oder ergänzen
- Keine inhaltlichen Aussagen ohne Quellengrundlage hinzufügen
- Keine Quellen selbst auswerten (das hat Gemini gemacht)

### Schritt 6: Vollständigkeits-Check

Prüfe gegen das Recherche-Protokoll (`02-quellen/Recherche_Kapitel_[X]_*.md`):

- Sind alle als "Relevanz 4–5" markierten Quellen in der Auswertung verarbeitet?
- Gibt es Lücken, die eine Nachrecherche (Phase 2) erfordern?

Falls ja, sage dem User:
> Für [Aspekt X] fehlen Quellen. Du solltest mit dem Recherche-Skill (`bachelorarbeit-recherche`) nachlegen, bevor wir zum Schreiben übergehen.

### Schritt 7: Fortschritt.md aktualisieren

Trage in `04-fortschritt/Fortschritt.md` ein:
- Phase 3 für Kapitel [X]: "Abgeschlossen"
- Offene Punkte (z.B. `[QUELLE ERGÄNZEN]`-Stellen)
- Nächster Schritt: Phase 4 (Writer) für dieses Kapitel

## Erwartetes Dateiformat (Template)

Das ist das Format, das der Writer-Skill (Phase 4) erwartet. Die Nachbearbeitung muss sicherstellen, dass das Auswertungsdokument diesem Format entspricht:

```markdown
# Quellenauswertung Kapitel [X]: [Kapiteltitel]

**Forschungsfrage:** [[Forschungsfrage]]
**Gliederung:** [[Gliederung]]
**Recherche-Protokoll:** [[Recherche_Kapitel_X_Kurztitel]]
**Datum:** [YYYY-MM-DD]
**Anzahl ausgewerteter Quellen:** [Anzahl]

## 1. Thematischer Überblick
## 2. Relevante Quellen für dieses Kapitel
## 3. Vergleichende Analyse
## 4. Argumentationsketten
## 5. Forschungslücken und offene Fragen
## 6. Empfehlung für den Kapitelaufbau
## 7. Offene Stellen
## Quellenverzeichnis (Kapitel)
```

## Handoff an Phase 4

Wenn die Auswertung für ein Kapitel abgeschlossen ist:

> Phase 3 (Quellenauswertung) für Kapitel [X] ist abgeschlossen. Die Auswertung liegt unter `02-quellen/Auswertung_Kapitel_[X]_[Kurztitel].md`.
>
> **Nächster Schritt — Phase 4: Schreiben.**
> Sag einfach: „Schreib mir Kapitel [X]" — der Writer-Skill greift auf Forschungsfrage, Gliederung und die Quellenauswertung zurück.

## Zusammenspiel mit anderen Skills

- **Vor Phase 3** → `bachelorarbeit-recherche` sammelt die Quellen
- **Nach Phase 3** → `bachelorarbeit-writer` nutzt die Auswertung als Schreibgrundlage
- **Zurück zu Phase 2** → Bei unzureichender Quellenlage Nachrecherche starten
- **Beim Review (Phase 5)** → Der Reviewer prüft, ob die Quellen korrekt eingearbeitet wurden
