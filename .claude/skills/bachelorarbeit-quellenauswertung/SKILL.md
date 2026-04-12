---
name: bachelorarbeit-quellenauswertung
description: >
  Phase 3 der Bachelorarbeit-Pipeline: Leitet den User durch die Quellenauswertung mit Gemini und NotebookLM. Der User hat seine Quellen bereits in einem NotebookLM-Notebook gesammelt (Phase 2). Jetzt öffnet er Gemini im Browser, verknüpft das Notebook, und wertet die Quellen dort mit vorbereiteten Prompts von Claude aus. Claude liefert die Prompts und den Gem-Systemprompt, der User führt alles im Browser durch, und Claude übernimmt die Nachbearbeitung des Gemini-Outputs ins Writer-Format. Spart Token, weil die eigentliche Analyse bei Gemini läuft. Nutze bei: "Quellen auswerten", "Literatur analysieren", "was sagen die Quellen zu", "Quellenauswertung", "Literaturanalyse", "Quellen zusammenfassen", "Quellen vergleichen", "was steht in den Papers", "extrahiere die Kernaussagen", "erstelle eine Quellenübersicht", "werte die Quellen aus", "Gem erstellen", "Gemini Auswertung". Nicht für Quellensuche — dafür gibt es `bachelorarbeit-recherche`.
---

# Bachelorarbeit — Phase 3: Quellenauswertung (via Gemini)

Die Quellenauswertung läuft **nicht in Claude**, sondern in **Gemini** — der User bedient Gemini und NotebookLM selbstständig im Browser. Das spart Token und nutzt Geminis Stärke: über die NotebookLM-Verknüpfung hat Gemini direkten Zugriff auf alle indexierten Quellen.

**Claudes Rolle in Phase 3:**
1. **Vorbereitung:** Gem-Systemprompt bereitstellen, kapitelspezifische Prompts generieren
2. **Nachbearbeitung:** Gemini-Output ins exakte Format bringen, das der Writer-Skill (Phase 4) erwartet

**Claudes Rolle ist NICHT:** Die Quellen selbst zu lesen oder auszuwerten. Das macht Gemini.

## Übersicht: Workflow

```
Claude                          User (im Browser)                Gemini
──────                          ─────────────────                ──────
1. Gem-Systemprompt +           User erstellt Gem in Gemini
   Schritt-für-Schritt      →  User verknüpft NotebookLM     
   Anleitung                    Notebook mit Gemini

2. Kapitel-Prompts           →  User gibt Prompts ein         → Gemini analysiert Quellen
                                                                 anhand des Notebooks
                                User kopiert Markdown-Output  →   
3. Nachbearbeitung           ←  User gibt Output an Claude
4. Fertige Auswertung        →  Datei in 02-quellen/
```

## Ablauf

### Schritt 1: Voraussetzungen prüfen

Bevor du startest, lies:
- `01-docs/Gliederung.md` — Welches Kapitel wird ausgewertet?
- `02-quellen/Forschungsfrage.md` oder `02-quellen/BA_Forschungsfrage.md` — Worauf arbeitet alles hin?
- `02-quellen/Recherche_Kapitel_[X]_*.md` — Welche Quellen liegen vor? (aus Phase 2)

Falls die Recherche für das Kapitel noch nicht abgeschlossen ist → zurück zu Phase 2 (`bachelorarbeit-recherche`).

### Schritt 2: NotebookLM + Gemini verknüpfen (einmalig)

Das ist der zentrale Schritt — hier verbindet der User seine gesammelten Quellen mit Gemini. Es gibt zwei Wege, und Claude erklärt dem User beide:

#### Weg A: Gem in Gemini erstellen und Notebook verknüpfen (empfohlen)

Gib dem User diese Anleitung:

> **NotebookLM-Quellen mit Gemini verbinden — Schritt für Schritt:**
>
> **Teil 1: Gem erstellen**
> 1. Öffne [gemini.google.com](https://gemini.google.com) in deinem Browser
> 2. Melde dich mit dem **gleichen Google-Konto** an, das du für NotebookLM benutzt
> 3. Klicke links in der Seitenleiste auf **„Gem Manager"** oder **„Gems"**
> 4. Klicke **„Neuen Gem erstellen"** / **„New Gem"**
> 5. **Name:** `BA Quellenauswertung`
> 6. **Anweisungen / Instructions:** Kopiere den Systemprompt, den ich dir gleich gebe, komplett in dieses Feld
> 7. Klicke **„Speichern"** / **„Save"**
>
> **Teil 2: NotebookLM-Notebook verknüpfen**
> 1. Öffne deinen neuen Gem (klicke auf „BA Quellenauswertung" in der Gem-Liste)
> 2. Unten links im Chat-Eingabefeld siehst du einen **+**-Button
> 3. Klicke darauf und wähle **„NotebookLM"** als Quelle
> 4. Wähle dein BA-Notebook aus der Liste
> 5. Jetzt hat Gemini Zugriff auf alle Quellen in deinem Notebook
>
> **Fertig!** Du kannst jetzt im Gem-Chat Fragen zu deinen Quellen stellen, und Gemini antwortet basierend auf den Dokumenten im Notebook.
>
> Bestätige mir, wenn der Gem erstellt und das Notebook verknüpft ist.

Gib dem User dann den Inhalt der Datei `references/gem-systemprompt.md` als Copy-Paste-Block für das Anweisungen-Feld. Lies dazu:

```
.claude/skills/bachelorarbeit-quellenauswertung/references/gem-systemprompt.md
```

#### Weg B: Direkt in NotebookLM chatten (einfacher, aber weniger steuerbar)

Falls der User den Gem-Weg zu kompliziert findet:

> **Alternative: Direkt in NotebookLM auswerten**
>
> 1. Öffne [notebooklm.google.com](https://notebooklm.google.com)
> 2. Öffne dein BA-Notebook
> 3. Wähle links die Quellen aus, die zu diesem Kapitel gehören (Häkchen setzen)
> 4. Nutze den **Chat** unten, um die Prompts einzugeben, die ich dir gleich gebe
>
> Nachteil: Ohne den Gem-Systemprompt gibt Gemini die Antworten nicht im exakten Auswertungsformat aus. Du musst dann ggf. nachfragen oder Claude macht mehr Nachbearbeitung.

**Empfehlung:** Weg A (Gem), weil der Systemprompt dafür sorgt, dass Gemini die Quellen gleich im richtigen Format auswertet — mit Seitenangaben, Harvard-Zitierung und strukturierten Argumentationsketten.

**Wichtig:** Der Gem und die Notebook-Verknüpfung müssen nur **einmal** eingerichtet werden. Bei weiteren Kapiteln öffnet der User einfach denselben Gem.

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

Gehe alle relevanten Quellen im Notebook durch und werte sie kapitelspezifisch aus. Gib die Antwort als vollständiges Markdown-Dokument aus. Achte besonders auf:
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

Für jeden Begriff: Alle Definitionen mit Autor, Jahr, Seite. Gemeinsamkeiten, Unterschiede, und eine Empfehlung für die Arbeitsdefinition. Formatiere die Antwort als Markdown.
```

#### Prompt C — Argumentationsketten

```
Baue eine wissenschaftliche Argumentationskette für Kapitel [X]: "[Kapiteltitel]".

Die zentrale These dieses Kapitels: "[These — aus Gliederung/Forschungsfrage ableiten]"

Für jedes Argument: Claim → Reason → Evidence (mit konkreten Quellen und Seitenangaben). Zeige auch Gegenargumente und eine Synthese. Formatiere als Markdown.
```

#### Prompt D — Methodik-Auswertung (nur für Methodenkapitel)

```
Werte die methodenbezogenen Quellen für mein Methodenkapitel aus.

Geplante Methode: [Methode aus Gliederung]

Liefere als Markdown-Dokument:
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

Formatiere als Markdown mit klaren Überschriften.
```

#### Prompt F — Diskussionsvorbereitung (nur für Diskussionskapitel)

```
Bereite mein Diskussionskapitel vor:

1. Theorie-Empirie-Abgleich: Welche theoretischen Vorhersagen werden bestätigt/widerlegt?
2. Einordnung in den Forschungsstand
3. Praktische Implikationen und Handlungsempfehlungen
4. Limitationen ähnlicher Studien
5. Offene Fragen und Forschungsbedarf

Immer mit konkreten Quellenbelegen (Autor, Jahr, Seite). Formatiere als Markdown.
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

Gib dem User diese Anleitung:

> **So wertest du die Quellen aus:**
>
> 1. Öffne deinen **BA Quellenauswertung**-Gem in Gemini (gemini.google.com → Gems → BA Quellenauswertung)
> 2. Stelle sicher, dass dein NotebookLM-Notebook verknüpft ist (du siehst es als Kontext-Quelle im Chat)
> 3. Kopiere **Prompt A** und füge ihn in den Chat ein → warte auf die vollständige Antwort
> 4. Gib dann die weiteren Prompts (B, C, D, E, F — je nach Kapitel) **einzeln** ein
> 5. **Wichtig — Markdown-Output sichern:**
>    - Markiere die gesamte Antwort von Gemini und kopiere sie
>    - Oder klicke auf das **Kopieren-Symbol** neben der Antwort
>    - Gib die kopierten Antworten hier bei mir (Claude) ein — ich bringe sie ins richtige Format
>
> **Tipp:** Falls eine Antwort zu lang wird und Gemini abbricht, sage "Fahre fort" oder "Bitte den Rest ausgeben".
>
> **Tipp für NotebookLM-Weg:** Wenn du direkt in NotebookLM arbeitest statt im Gem, kannst du vor dem Chat bestimmte Quellen auswählen (Häkchen setzen), um die Antwort auf die kapitelrelevanten Quellen einzuschränken.

### Schritt 5: Nachbearbeitung (Claude)

Wenn der User den Gemini-Output zurückbringt, machst du Folgendes:

1. **Prüfe die Struktur:** Entspricht der Output dem Format, das der Writer-Skill erwartet? (Siehe Template unten)
2. **Ergänze fehlende Abschnitte:** Falls Gemini einen Abschnitt ausgelassen hat (z.B. Argumentationsketten, Forschungslücken), weise darauf hin und schlage einen Nachfrage-Prompt für Gemini vor
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

- **Vor Phase 3** → `bachelorarbeit-recherche` sammelt die Quellen im NotebookLM-Notebook (User im Browser)
- **Nach Phase 3** → `bachelorarbeit-writer` nutzt die Auswertung als Schreibgrundlage
- **Zurück zu Phase 2** → Bei unzureichender Quellenlage Nachrecherche starten (User recherchiert selbst in NotebookLM im Browser)
- **Beim Review (Phase 5)** → Der Reviewer prüft, ob die Quellen korrekt eingearbeitet wurden
