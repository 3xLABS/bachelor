# Prompts für die Bachelorarbeit-Pipeline

Diese Datei enthält Copy-Paste-Prompts für alle externen Tools im Workflow. Ersetze die `[Platzhalter]` durch deine konkreten Angaben.

---

## Perplexity

### P-1: Themenfindung

```
Recherchiere aktuelle Trendthemen für eine Bachelorarbeit im Fachbereich [BWL/Wirtschaftsinformatik/...].

Anforderungen an die Themen:
- Wissenschaftlich fundiert (genug Fachliteratur vorhanden)
- Praxisbezug für Unternehmen
- Aktuell und relevant (2024-2026)
- Enthält eine offene Forschungsfrage (nicht rein deskriptiv)

Gib mir 10 Themenvorschläge mit jeweils:
1. Thema (präzise formuliert)
2. Warum aktuell relevant (1-2 Sätze)
3. Mögliche Forschungsfrage
4. Einschätzung der Quellenlage (gut/mittel/dünn)
```

### P-2: Quellenrecherche (Hauptrecherche)

```
Recherchiere [80] Quellen für meine [Bachelorarbeit] mit dem Thema "[Thema]".

Aufteilung:
- 40 Online-Quellen (Studien, Fachartikel, Reports, Whitepaper, Standards)
- 40 Bücher (bevorzugt mit ISBN und online lesbar)

Thematische Schwerpunkte (orientiert an meiner Gliederung):
- [Kapitel 2: z.B. Theoretische Grundlagen des Risikomanagements]
- [Kapitel 3: z.B. Cyberrisiken und Datenschutz]
- [Kapitel 4: z.B. Methodik — qualitative Inhaltsanalyse]
- [Kapitel 5: z.B. KI-Risiken und Regulierung]

Qualitätskriterien:
- Bevorzuge peer-reviewed Quellen und anerkannte Institutionen
- Aktualität: Hauptsächlich 2020-2026, Standardwerke dürfen älter sein
- Mischung aus deutsch- und englischsprachigen Quellen
- Keine Blogposts, Wikipedia oder populärwissenschaftliche Artikel

Output-Format pro Quelle:

**[O-1]** (fortlaufende Nummerierung)
**Autor(en):** [Autor]
**Titel:** [Titel]
**Erscheinungsjahr:** [Jahr]
**Quelle/Institution:** [Verlag/Journal/Institution]
**URL:** [Link falls verfügbar]
**Kurzbeschreibung:** [2-3 Sätze: Worum geht es? Warum relevant für die Arbeit?]

---
```

### P-3: Kapitelspezifische Nachrecherche

```
Recherchiere 10-15 weitere wissenschaftliche Quellen speziell zum Thema "[Kapitelthema]" im Kontext meiner Bachelorarbeit über "[Gesamtthema]".

Die Forschungsfrage lautet: "[Forschungsfrage]"

Ich brauche Quellen, die:
- [Aspekt 1, z.B. empirische Daten zu Cyberangriffen im Mittelstand liefern]
- [Aspekt 2, z.B. das NIST Cybersecurity Framework kritisch einordnen]
- [Aspekt 3, z.B. Wechselwirkungen zwischen Datenschutz und KI-Risiken belegen]

Bevorzuge:
- Peer-reviewed Fachartikel (2020-2026)
- Branchenreports mit konkreten Zahlen
- Standardwerke, die noch nicht in meiner Quellensammlung sind

Gleiches Output-Format wie oben (Autor, Titel, Jahr, Quelle, URL, Kurzbeschreibung).
```

### P-4: URL-Liste extrahieren

```
Hier ist mein Quellenverzeichnis:

[Quellenverzeichnis einfügen]

Extrahiere alle URLs und gib sie als nummerierte Liste aus, die ich direkt in NotebookLM kopieren kann. Format:

1. [URL 1]
2. [URL 2]
...

Falls eine Quelle keine URL hat, schreibe: [X] — Kein Link (Buch: [Titel], ISBN: [ISBN])
```

### P-5: Lückenanalyse

```
Hier ist meine Gliederung:

[Gliederung einfügen]

Und hier ist mein bisheriges Quellenverzeichnis:

[Quellenverzeichnis einfügen]

Analysiere:
1. Welche Kapitel/Abschnitte haben genug Quellen (mind. 5-8 pro Hauptkapitel)?
2. Welche Kapitel haben zu wenige Quellen?
3. Welche Art von Quellen fehlt? (z.B. empirische Studien, Standardwerke, aktuelle Reports)
4. Gibt es thematische Lücken, die mit den vorhandenen Quellen nicht abgedeckt sind?

Recherchiere anschließend 5-10 ergänzende Quellen gezielt für die identifizierten Lücken.
```

---

## NotebookLM

### N-1: Notebook einrichten

**Anleitung (kein Prompt, sondern Schritte):**
1. Gehe zu [notebooklm.google.com](https://notebooklm.google.com)
2. Klicke "Neues Notebook"
3. Benenne es: `[Thema der Arbeit]`
4. Klicke "Quellen hinzufügen"
5. Füge die URLs aus Prompt P-4 ein (eine nach der anderen oder als Batch)
6. Lade PDFs hoch, die du lokal gespeichert hast (Bücher, Reports)
7. Warte, bis alle Quellen verarbeitet sind (grüner Haken)

### N-2: Quellenübersicht generieren

```
Erstelle eine Übersicht aller geladenen Quellen in diesem Notebook.

Für jede Quelle:
- Autor und Titel
- Hauptthema in einem Satz
- Die 3 wichtigsten Aussagen/Erkenntnisse

Sortiere die Quellen thematisch nach diesen Kategorien:
- [Kategorie 1, z.B. Risikomanagement-Grundlagen]
- [Kategorie 2, z.B. Cyberrisiken]
- [Kategorie 3, z.B. Datenschutz]
- [Kategorie 4, z.B. KI-Risiken]
- [Kategorie 5, z.B. Methodik]
```

### N-3: Widersprüche und Debatten finden

```
Durchsuche alle Quellen in diesem Notebook und identifiziere:

1. Wo widersprechen sich Autoren? (z.B. unterschiedliche Definitionen, gegensätzliche Befunde)
2. Wo gibt es offene Debatten in der Literatur?
3. Wo sind sich die meisten Autoren einig (Konsens)?

Das ist wichtig für mein Diskussionskapitel. Gib für jeden Widerspruch/jede Debatte an:
- Wer vertritt welche Position?
- Wie lässt sich der Widerspruch erklären?
- Welche Position ist besser belegt?
```

---

## Gemini (via Gem + NotebookLM)

> **Empfohlen:** Erstelle einmalig den Gem „BA Quellenauswertung" in Google AI Studio (Anleitung und Systemprompt liefert Claude automatisch über den Quellenauswertungs-Skill). Der Gem kennt das Ausgabeformat und liefert konsistentere Ergebnisse als die Einzel-Prompts unten.
>
> Die Prompts unten funktionieren auch ohne Gem — direkt im NotebookLM-Chat.

### G-1: Forschungsfrage ableiten

```
Analysiere alle Quellen in diesem Notebook zum Thema "[Thema]" und leite daraus eine Forschungsfrage ab.

Gehe dabei so vor:
1. Identifiziere die zentrale Forschungslücke — was wird in der Literatur noch nicht ausreichend behandelt?
2. Formuliere eine Hauptforschungsfrage, die:
   - Spezifisch genug ist, um in [30-50 / 60-100] Seiten beantwortbar zu sein
   - Nicht trivial ist (die Antwort ist nicht offensichtlich)
   - Wissenschaftlich und praktisch relevant ist
3. Formuliere 2-3 Unterforschungsfragen, die die Hauptfrage strukturieren

Output:
- Identifizierte Forschungslücke (mit Bezug auf konkrete Quellen)
- Hauptforschungsfrage
- Unterforschungsfragen
- Begründung der Relevanz (wissenschaftlich + praktisch)
- Methodischer Vorschlag (welche Methode passt zur Frage?)
```

### G-2: Kapitelspezifische Quellenauswertung (Hauptprompt)

```
Erstelle eine vollständige Quellenauswertung für Kapitel [X]: "[Kapiteltitel]" meiner Bachelorarbeit.

Die Forschungsfrage lautet: "[Forschungsfrage]"

Dieses Kapitel soll folgende Unterkapitel abdecken:
- [Unterkapitel 1]
- [Unterkapitel 2]
- [...]

Nutze dieses Ausgabeformat:

# Quellenauswertung Kapitel [X]: [Kapiteltitel]

Für jede relevante Quelle:
### [Autor, Jahr] — [Kurztitel]
**Typ:** [Studie/Fachbuch/Review/Report/Standard]
**Kernaussagen:** (mit Seitenangaben)
**Methodik** (falls empirisch): [Methode, Stichprobe, Design]
**Verwendbare Zitate:** (direkt zitieren, mit Seite)
**Relevanz für die Arbeit:**
**Limitationen:**

Dann:
## Vergleichende Analyse (Gemeinsamkeiten, Widersprüche, Definitionen im Vergleich)
## Argumentationsketten (Claim → Reason → Evidence, mit Gegenargumenten)
## Forschungslücken und offene Fragen
## Empfehlung für den Kapitelaufbau
## Quellenverzeichnis (Harvard, alphabetisch)
```

### G-3: Argumentationsketten bauen

```
Baue eine wissenschaftliche Argumentationskette für Kapitel [X]: "[Kapiteltitel]".

Die zentrale These dieses Kapitels: "[These]"

Für jedes Argument:
**Behauptung (Claim):** [Was wird behauptet?]
**Begründung (Reason):** [Warum ist das plausibel?]
**Beleg (Evidence):** [Welche Quellen stützen das? Mit Autor, Jahr, Seitenangabe]

Zeige auch Gegenargumente und eine Synthese.
Jedes Argument muss durch mindestens eine konkrete Quelle mit Seitenangabe belegt sein.
```

### G-4: Definitionen und Begriffsklärung

```
Durchsuche alle Quellen nach Definitionen für folgende Begriffe:

1. [Begriff 1]
2. [Begriff 2]
3. [Begriff 3]

Für jeden Begriff:
- Alle Definitionen aus den Quellen (mit Autor, Jahr, Seite)
- Gemeinsamkeiten und Unterschiede
- Empfehlung: Welche eignet sich als Arbeitsdefinition und warum?
```

### G-5: Quellen für Methodenkapitel auswerten

```
Werte die methodenbezogenen Quellen für mein Methodenkapitel aus.

Geplante Methode: [z.B. Qualitative Inhaltsanalyse nach Mayring]

Liefere:
1. Methodenbeschreibung (mit Seitenangaben)
2. Begründung für den Einsatz bei meiner Forschungsfrage
3. Ablauf/Schritte laut Quellen
4. Gütekriterien
5. Limitationen
6. Alternative Methoden und warum meine Wahl besser ist
```

### G-6: Diskussionskapitel vorbereiten

```
Bereite mein Diskussionskapitel vor:

1. Theorie-Empirie-Abgleich: Welche theoretischen Vorhersagen werden bestätigt/widerlegt?
2. Einordnung in den Forschungsstand
3. Praktische Implikationen und Handlungsempfehlungen
4. Limitationen ähnlicher Studien
5. Offene Fragen und Forschungsbedarf

Immer mit konkreten Quellenbelegen (Autor, Jahr, Seite).
```

### G-7: Widersprüche und Forschungslücken

```
Analysiere die Quellen zu Kapitel [X] auf:

1. Wo widersprechen sich Autoren? Wer vertritt welche Position? Welche ist besser belegt?
2. Welche Aspekte von [Kapitelthema] werden NICHT oder nur unzureichend abgedeckt?
3. Gibt es einen erkennbaren Forschungstrend oder Paradigmenwechsel?
```

---

## Claude (Bachelorarbeit-Pipeline)

### C-1: Planung starten

```
Ich möchte eine Bachelorarbeit im Fach [BWL] schreiben.

Thema: [Thema oder "ich habe noch kein Thema"]
Umfang: ca. [X] Seiten
Hochschule: [Name]
Abgabe: [Datum]

Was ich schon habe:
- Forschungsfrage: [ja/nein — wenn ja, welche?]
- Gliederung: [ja/nein]
- Quellen: [ja/nein — wenn ja, wie viele?]
- Quellenauswertung: [ja/nein]

Hilf mir, die fehlenden Schritte zu erarbeiten.
```

### C-2: Kapitel schreiben

```
Schreib mir Kapitel [X.Y]: "[Kapiteltitel]"

Forschungsfrage: [Forschungsfrage]
Seitenumfang: ca. [X] Seiten
Gliederung des Kapitels:
[Unterkapitel auflisten]

Quellenauswertung: [Datei angeben oder direkt einfügen]
```

### C-3: Review anfordern

```
Reviewe dieses Kapitel: [Dateiname oder Text einfügen]

Forschungsfrage: [Forschungsfrage]
Gliederung der Gesamtarbeit: [Datei angeben]
```

### C-4: Überarbeitung anfordern

```
Arbeite das Feedback ein:

Kapitel: [Dateiname]
Review: [Dateiname]
Neue Quellen (falls vorhanden): [Quellenauswertung einfügen]
```

### C-5: Finalisierung

```
Finalisiere meine Arbeit und erstelle die Word-Datei.

Alle Kapitel liegen in: [Ordner/Dateien]
Formatvorgaben: [Datei oder direkt beschreiben]
Titelblatt-Infos:
- Titel: [Titel]
- Verfasser: [Name]
- Matrikelnummer: [Nummer]
- Studiengang: [Studiengang]
- Betreuer: [Name]
- Abgabedatum: [Datum]
```
