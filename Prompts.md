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

## Gemini (via NotebookLM)

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

### G-2: Kapitelspezifische Quellenauswertung

```
Durchsuche die geladenen Quellen und erstelle eine detaillierte Quellenauswertung für Kapitel [X]: "[Kapiteltitel]" meiner Bachelorarbeit.

Die Forschungsfrage lautet: "[Forschungsfrage]"

Für jede relevante Quelle liefere:

### [Autor, Jahr] — [Kurztitel]
**Kernaussagen für dieses Kapitel:**
- [Aussage 1] (S. [XX])
- [Aussage 2] (S. [XX])

**Verwendbare direkte Zitate:**
- "[Zitat 1]" (S. [XX])
- "[Zitat 2]" (S. [XX])

**Daten/Statistiken/Fakten:**
- [Fakt mit Seitenangabe]

**Relevanz:** [1-2 Sätze: Warum ist diese Quelle für dieses Kapitel wichtig?]

---

Erstelle am Ende eine Zusammenfassung:
- Welche Quellen sind die wichtigsten für dieses Kapitel?
- Wo gibt es Übereinstimmungen zwischen Autoren?
- Wo gibt es Widersprüche?
- Welche Aspekte sind durch Quellen gut abgedeckt, welche dünn?
```

### G-3: Argumentationsketten bauen

```
Basierend auf den Quellen in diesem Notebook: Baue eine wissenschaftliche Argumentationskette für Kapitel [X]: "[Kapiteltitel]".

Die zentrale These dieses Kapitels soll sein: "[These, z.B. Cyberrisiken erfordern ein integriertes Risikomanagement, das über klassische IT-Sicherheit hinausgeht]"

Strukturiere die Argumentation so:

### Argument 1: [Titel]
**Behauptung (Claim):** [Was wird behauptet?]
**Begründung (Reason):** [Warum ist das plausibel?]
**Beleg (Evidence):** [Welche Quellen stützen das? Mit Autor, Jahr, Seitenangabe]

### Argument 2: [Titel]
...

### Gegenargumente
**Position:** [Was spricht dagegen?]
**Quelle:** [Wer vertritt diese Position?]
**Entkräftung/Einordnung:** [Wie geht man damit um?]

### Synthese
[Wie fügen sich die Argumente zu einer schlüssigen Gesamtargumentation zusammen?]

Wichtig:
- Jedes Argument muss durch mindestens eine konkrete Quelle mit Seitenangabe belegt sein
- Zeige auch Gegenargumente — das stärkt die wissenschaftliche Qualität
- Die Argumentationskette soll den roten Faden des Kapitels bilden
```

### G-4: Definitionen und Begriffsklärung

```
Durchsuche alle Quellen nach Definitionen für folgende Begriffe, die in meiner Arbeit zentral sind:

1. [Begriff 1, z.B. Risikomanagement]
2. [Begriff 2, z.B. Digitale Transformation]
3. [Begriff 3, z.B. Cyberrisiko]
4. [Begriff 4, z.B. KI-Governance]

Für jeden Begriff:
- Alle Definitionen aus den Quellen (mit Autor, Jahr, Seite)
- Gemeinsamkeiten und Unterschiede zwischen den Definitionen
- Empfehlung: Welche Definition eignet sich als Arbeitsdefinition für meine Arbeit und warum?
```

### G-5: Quellen für Methodenkapitel auswerten

```
Durchsuche die methodenbezogenen Quellen und erstelle eine Auswertung für mein Methodenkapitel.

Meine geplante Methode: [z.B. Qualitative Inhaltsanalyse nach Mayring]

Ich brauche:
1. Methodenbeschreibung: Wie definieren die Quellen diese Methode? (mit Seitenangaben)
2. Begründung: Welche Argumente liefern die Quellen dafür, diese Methode bei meiner Forschungsfrage einzusetzen?
3. Ablauf: Welche Schritte beschreiben die Quellen? (z.B. Kategorienbildung, Kodierung, Auswertung)
4. Gütekriterien: Welche Qualitätskriterien nennen die Quellen? (z.B. Interkoderreliabilität, Nachvollziehbarkeit)
5. Limitationen: Welche Grenzen/Einschränkungen der Methode werden diskutiert?
6. Alternative Methoden: Was wäre alternativ möglich und warum ist meine Wahl besser?
```

### G-6: Diskussionskapitel vorbereiten

```
Ich bereite mein Diskussionskapitel vor. Durchsuche alle Quellen und hilf mir bei folgenden Punkten:

1. **Theorie-Empirie-Abgleich:** Welche theoretischen Vorhersagen aus meinem Theoriekapitel werden durch welche Quellen bestätigt oder widerlegt?

2. **Einordnung in den Forschungsstand:** Wie ordnen sich meine Ergebnisse in die bestehende Literatur ein? Wo bestätigen sie, wo widersprechen sie?

3. **Praktische Implikationen:** Welche konkreten Handlungsempfehlungen lassen sich aus den Quellen und meinen Ergebnissen ableiten?

4. **Limitationen:** Welche methodischen und inhaltlichen Grenzen diskutieren ähnliche Studien in den Quellen?

5. **Forschungsbedarf:** Welche offenen Fragen identifizieren die Quellen? Was sollte zukünftige Forschung untersuchen?

Gib für jeden Punkt konkrete Quellenbelege (Autor, Jahr, Seite).
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
