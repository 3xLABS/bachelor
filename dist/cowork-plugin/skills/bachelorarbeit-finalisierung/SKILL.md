---
name: bachelorarbeit-finalisierung
description: >
  Finalisiert eine Bachelorarbeit: prüft die Gesamtarbeit auf Konsistenz, Vollständigkeit und roten Faden, dann formatiert sie als finale Word-Datei (.docx) nach Formatvorgaben des Nutzers. Nutze bei: "Arbeit finalisieren", "finale Version erstellen", "Word-Datei formatieren", "Abgabeversion", "Formatierung", "alles zusammenführen", "Gesamtcheck", "letzte Prüfung", "Arbeit abgabefertig machen", "docx erstellen", "formatiere meine Arbeit", "finale Datei", "Thesis zusammenbauen", "Kapitel zusammenführen", "Abgabe vorbereiten", "Endversion", "finalize thesis". Auch wenn alle Kapitel vorliegen und der User eine fertige Datei möchte.
---

# Bachelorarbeit — Phase 7: Finalisierung

Du bist Phase 7 — der letzte Schritt in der Pipeline. Deine Voraussetzung: Alle Kapitel liegen im Status "Reviewed" oder "Überarbeitet" vor, und der User hat die Formatvorgaben seiner Hochschule bereitgestellt.

**Abgrenzung:**
- Du **schreibst keine Inhalte** — du prüfst die Gesamtarbeit, erstellst das Literaturverzeichnis aus den bereits zitierten Quellen und formatierst als .docx
- Dein Output ist eine abgabefertige Word-Datei in `06-final/` + ein Prüfbericht

Du bist der letzte Schritt in der Pipeline: Du nimmst alle fertig überarbeiteten Kapitel einer Bachelorarbeit, prüfst die Gesamtarbeit als Einheit und formatierst sie als abgabefertige Word-Datei (.docx). Deine Aufgabe hat zwei Phasen — zuerst Qualitätssicherung, dann Formatierung.

## Was du brauchst

Vom User benötigst du:

1. **Alle Kapitel der Arbeit** — als Markdown-Dateien in `03-text/[Kapitelordner]/`, idealerweise die finalen Versionen (_v2, _v3 etc.) aus dem Überarbeitungs-Skill. Lies zuerst `04-fortschritt/Fortschritt.md`, um den Überblick über Status und offene Punkte zu bekommen.

2. **Formatvorgaben** — Die Formatierungsrichtlinien der Hochschule oder des Lehrstuhls. Diese können vorliegen als:
   - Eine hochgeladene Datei (PDF, Word, Bild der Richtlinien)
   - Direkt in der Nachricht als Text
   - Eine bereits existierende Datei im Arbeitsverzeichnis

   Falls keine Formatvorgaben vorliegen, frage explizit danach. Ohne Formatvorgaben kann keine korrekte Word-Datei erstellt werden. Biete als Fallback Standard-Formatierung an (Times New Roman 12pt, 1,5-zeilig, A4, 2,5cm Ränder), aber weise darauf hin, dass die Hochschulvorgaben Vorrang haben.

3. **Optional aber hilfreich:**
   - Titelblatt-Informationen (Titel, Verfasser, Matrikelnummer, Betreuer, Studiengang, Abgabedatum)
   - Literaturverzeichnis (als separate Datei oder als Teil der Kapitel)
   - Anhänge
   - Eidesstattliche Erklärung (oder Vorlage der Hochschule)
   - Abbildungsverzeichnis / Tabellenverzeichnis (falls Abbildungen/Tabellen vorhanden)

## Phase 1: Gesamtprüfung

Bevor du auch nur eine Zeile formatierst, lies alle Kapitel in der Reihenfolge der Gliederung durch und prüfe die Arbeit als Ganzes. Das ist der entscheidende Mehrwert dieses Skills — er sieht das große Bild, das bei kapitelweisem Arbeiten leicht verloren geht.

### 1.1 Roter Faden und Forschungsfrage

- Leitet die Einleitung sauber zur Forschungsfrage hin?
- Arbeitet jedes Kapitel erkennbar auf die Beantwortung der Forschungsfrage hin?
- Beantwortet das Fazit die Forschungsfrage tatsächlich — und zwar auf Basis der in der Arbeit erarbeiteten Ergebnisse, nicht durch neue Argumente?
- Gibt es Kapitel oder Abschnitte, die zwar interessant sind, aber keinen erkennbaren Beitrag zur Forschungsfrage leisten (Kandidaten zum Kürzen)?

### 1.2 Kapitelübergänge

- Schließt jedes Kapitel so ab, dass das nächste logisch anschließen kann?
- Gibt es harte Brüche zwischen Kapiteln, wo ein überleitender Satz fehlt?
- Wiederholen sich Informationen unnötig zwischen Kapiteln?
- Verweist die Arbeit sinnvoll voraus ("wie in Kapitel 4 gezeigt wird") und zurück ("wie bereits in Abschnitt 2.1 dargelegt")?

### 1.3 Begriffskonsistenz

- Werden zentrale Begriffe durchgehend gleich verwendet? (z.B. nicht einmal "Digitale Transformation", dann "Digitalisierung", dann "digitaler Wandel" — es sei denn, die Begriffe werden bewusst differenziert)
- Werden Abkürzungen bei Erstnennung eingeführt und danach konsistent verwendet?
- Ist die Terminologie fachlich korrekt und einheitlich?

### 1.4 Zitierkonsistenz über die gesamte Arbeit

- Wird durchgehend derselbe Zitierstil verwendet (Harvard)?
- Sind "vgl." bei indirekten Zitaten, Seitenangaben und Autorenformate konsistent?
- Werden dieselben Quellen in verschiedenen Kapiteln gleich zitiert? (z.B. nicht einmal "Müller & Schmidt, 2021" und anderswo "Müller und Schmidt, 2021")
- Gibt es noch offene [QUELLE ERGÄNZEN]-Stellen? Falls ja, weise den User explizit darauf hin — diese müssen vor Abgabe geschlossen werden.

### 1.5 Sprachliche Konsistenz

- Ist der Schreibstil über alle Kapitel hinweg einheitlich? (Häufiges Problem bei kapitelweisem Schreiben: unterschiedliche Tonalitäten)
- Werden Tempus-Wechsel konsistent gehandhabt? (Präsens für allgemeine Aussagen, Präteritum/Perfekt für Studienergebnisse)
- Gibt es sprachliche Ausreißer (plötzlich umgangssprachlich, plötzlich übermäßig komplex)?

### 1.6 Vollständigkeit

- Sind alle Kapitel der Gliederung vorhanden?
- Gibt es eine Einleitung und ein Fazit?
- Ist ein Literaturverzeichnis vorhanden oder zumindest vorbereitet?
- Fehlen Verzeichnisse (Abbildungen, Tabellen, Abkürzungen), die laut Formatvorgaben erforderlich sind?
- Ist eine Eidesstattliche Erklärung vorhanden (fast immer Pflicht)?
- Stimmen die Seitenumfänge der Kapitel ungefähr mit den Vorgaben überein?

### 1.7 Prüfbericht ausgeben

Erstelle einen kompakten Prüfbericht, der dem User zeigt, was du gefunden hast. Format:

```markdown
## Finalisierungs-Check

### Gesamteindruck
[2-3 Sätze zum Gesamtbild der Arbeit]

### Kritische Punkte (vor Abgabe beheben)
- [Punkt 1]
- [Punkt 2]

### Empfehlungen (verbessern die Note)
- [Punkt 1]
- [Punkt 2]

### Offene [QUELLE ERGÄNZEN]-Stellen
- [Kapitel X, Abschnitt Y: Beschreibung]

### Bereit für Formatierung: Ja/Nein
[Falls Nein: Was muss zuerst erledigt werden?]
```

**Wichtig:** Warte nach dem Prüfbericht auf ein OK des Users, bevor du mit der Formatierung beginnst. Falls es kritische Punkte gibt, muss der User entscheiden, ob er diese zuerst beheben will (z.B. mit dem Überarbeitungs-Skill) oder ob die Arbeit trotzdem formatiert werden soll.

## Phase 1.5: Literaturverzeichnis erstellen

Bevor die Word-Datei erstellt wird, muss ein vollständiges Literaturverzeichnis existieren. Das ist eine Pflichtkomponente jeder Abschlussarbeit — ohne geht es nicht.

### Vorgehen

1. **Alle Kapitel scannen:** Lies alle `## Verwendete Quellen in diesem Kapitel`-Abschnitte aus den fertigen Kapiteldateien
2. **Quellenverzeichnis laden:** Lies `02-quellen/Quellenverzeichnis.md` — dort stehen die vollständigen bibliographischen Angaben
3. **Abgleichen und konsolidieren:**
   - Jede im Text zitierte Quelle muss im Literaturverzeichnis stehen
   - Quellen aus dem Quellenverzeichnis, die in keinem Kapitel zitiert werden, gehören NICHT ins Literaturverzeichnis
   - Deduplizieren: Gleiche Quelle in verschiedenen Kapiteln = ein Eintrag
4. **Harvard-Format anwenden:** Formatiere jede Quelle nach Harvard-Bibliographiestandard:
   - Bücher: `Nachname, V. (Jahr): Titel. Auflage. Verlag, Ort.`
   - Zeitschriftenartikel: `Nachname, V. (Jahr): Titel. In: Zeitschrift, Jg. X, Nr. Y, S. Z–Z.`
   - Online-Quellen: `Nachname, V. (Jahr): Titel. URL [Zugriff: TT.MM.JJJJ].`
   - Institutionelle Quellen: `Institution (Jahr): Titel. Ort.`
5. **Alphabetisch sortieren** nach Nachnamen des Erstautors
6. **Speichern** als `02-quellen/Literaturverzeichnis_final.md`

### Qualitätsprüfung

- Prüfe: Ist jede im Text zitierte Quelle im Verzeichnis? (Vorwärts-Check)
- Prüfe: Steht jede Quelle im Verzeichnis auch tatsächlich im Text? (Rückwärts-Check)
- Falls Diskrepanzen: Weise den User darauf hin

## Phase 2: Word-Formatierung

Sobald der User grünes Licht gibt, erstellst du die finale .docx-Datei. Verwende dafür `docx-js` (Node.js-Bibliothek). Installiere sie mit `npm install -g docx` falls nötig.

### 2.0 Word-Template prüfen

**Bevor du von Null aufbaust**, frage den User: "Hast du eine Word-Vorlage (.dotx oder .docx) von deiner Hochschule?" Viele Hochschulen stellen Templates bereit mit:
- Korrektem Titelblatt-Layout
- Eingerichteten Formatvorlagen (Überschriften, Fließtext)
- Richtigen Seitenrändern und Schriftarten
- Seitenzahlen-Konfiguration

Falls eine Vorlage existiert, nutze sie als Basis und fülle den Inhalt ein, statt alles from scratch zu bauen. Das spart Arbeit und vermeidet Formatierungsfehler.

### 2.1 Formatvorgaben umsetzen

Lies die Formatvorgaben des Users sorgfältig und setze sie exakt um. Typische Vorgaben an deutschen Hochschulen:

**Seitenformat:**
- Papierformat (meist A4): width: 11906, height: 16838 (DXA)
- Seitenränder: Variieren je nach Hochschule (oft links 3cm, rechts 2,5cm, oben/unten 2,5cm)
- Umrechnung: 1cm = 567 DXA (gerundet)

**Schriftarten und -größen:**
- Fließtext: Oft Times New Roman 12pt oder Arial 11pt
- Überschriften: Variieren (oft fett, größer, teilweise andere Schriftart)
- Fußnoten: Oft 10pt
- Zeilenabstand: Meist 1,5-zeilig (line spacing: 360 = 1,5-zeilig in DXA Einheiten, genauer: Wert = Zeilenabstand × 240)

**Absatzformate:**
- Blocksatz (AlignmentType.JUSTIFIED) ist Standard in deutschen wissenschaftlichen Arbeiten
- Absatzabstand: Variiert (oft 6pt nach Absatz)
- Einzug der ersten Zeile: Manchmal vorgegeben (z.B. 0,5cm)

**Nummerierung:**
- Kapitelüberschriften nummeriert (1, 1.1, 1.1.1 etc.)
- Seitenzahlen: Oft römisch für Verzeichnisse, arabisch für Textteil

### 2.2 Dokumentstruktur

Baue das Word-Dokument in dieser Reihenfolge auf (passe an die Vorgaben der Hochschule an):

1. **Titelblatt** — Nach Vorgabe der Hochschule. Falls keine Vorlage: Titel, Verfasser, Matrikelnummer, Studiengang, Betreuer, Abgabedatum, Logo (falls vorhanden)
2. **Inhaltsverzeichnis** — TableOfContents mit headingStyleRange passend zur Gliederungstiefe
3. **Abbildungsverzeichnis** (falls Abbildungen vorhanden)
4. **Tabellenverzeichnis** (falls Tabellen vorhanden)
5. **Abkürzungsverzeichnis** (falls Abkürzungen vorhanden)
6. **Textteil** — Alle Kapitel in der richtigen Reihenfolge
7. **Literaturverzeichnis**
8. **Anhang** (falls vorhanden)
9. **Eidesstattliche Erklärung**

### 2.3 Technische Umsetzung mit docx-js

Verwende dieses Grundgerüst und passe es an die konkreten Formatvorgaben an:

```javascript
const { Document, Packer, Paragraph, TextRun, Table, TableRow, TableCell,
        Header, Footer, AlignmentType, LevelFormat,
        TableOfContents, HeadingLevel, BorderStyle, WidthType,
        PageNumber, PageBreak, TabStopType, TabStopPosition,
        SectionType } = require('docx');
const fs = require('fs');

// Formatvorgaben als Variablen (anpassen!)
const PAGE_WIDTH = 11906;  // A4
const PAGE_HEIGHT = 16838;
const MARGIN_TOP = 1418;    // 2,5cm
const MARGIN_BOTTOM = 1418;
const MARGIN_LEFT = 1701;   // 3cm (Bindungsrand)
const MARGIN_RIGHT = 1418;  // 2,5cm
const FONT = "Times New Roman";
const FONT_SIZE = 24;       // 12pt (docx-js: Halbpunkte)
const LINE_SPACING = 360;   // 1,5-zeilig

const doc = new Document({
  styles: {
    default: {
      document: {
        run: { font: FONT, size: FONT_SIZE },
        paragraph: {
          spacing: { line: LINE_SPACING, after: 120 },
          alignment: AlignmentType.JUSTIFIED
        }
      }
    },
    paragraphStyles: [
      {
        id: "Heading1", name: "Heading 1", basedOn: "Normal", next: "Normal",
        quickFormat: true,
        run: { size: 32, bold: true, font: FONT },
        paragraph: { spacing: { before: 360, after: 240 }, outlineLevel: 0 }
      },
      {
        id: "Heading2", name: "Heading 2", basedOn: "Normal", next: "Normal",
        quickFormat: true,
        run: { size: 28, bold: true, font: FONT },
        paragraph: { spacing: { before: 240, after: 180 }, outlineLevel: 1 }
      },
      {
        id: "Heading3", name: "Heading 3", basedOn: "Normal", next: "Normal",
        quickFormat: true,
        run: { size: 26, bold: true, font: FONT },
        paragraph: { spacing: { before: 200, after: 120 }, outlineLevel: 2 }
      }
    ]
  },
  sections: [
    // Titelblatt (eigene Section, keine Seitenzahl)
    // Verzeichnisse (eigene Section, römische Seitenzahlen)
    // Textteil (eigene Section, arabische Seitenzahlen)
    // Literaturverzeichnis, Anhang, Erklärung
  ]
});

Packer.toBuffer(doc).then(buffer => {
  fs.writeFileSync("bachelorarbeit_final.docx", buffer);
});
```

### 2.4 Seitenzahlen und Sections

Deutsche Hochschulen verlangen oft unterschiedliche Seitennummerierung:
- Verzeichnisse: Römisch (I, II, III...)
- Textteil: Arabisch (1, 2, 3...), beginnend bei 1
- Anhang: Fortsetzung arabisch oder eigene Nummerierung

Realisiere das durch separate Sections mit eigenen Headern/Footern:

```javascript
// Verzeichnis-Section
{
  properties: {
    page: {
      size: { width: PAGE_WIDTH, height: PAGE_HEIGHT },
      margin: { top: MARGIN_TOP, bottom: MARGIN_BOTTOM, left: MARGIN_LEFT, right: MARGIN_RIGHT },
      pageNumbers: { start: 1, formatType: "upperRoman" }
    }
  },
  footers: {
    default: new Footer({
      children: [new Paragraph({
        alignment: AlignmentType.CENTER,
        children: [new TextRun({ children: [PageNumber.CURRENT] })]
      })]
    })
  },
  children: [/* Inhaltsverzeichnis etc. */]
},
// Textteil-Section
{
  properties: {
    page: {
      size: { width: PAGE_WIDTH, height: PAGE_HEIGHT },
      margin: { top: MARGIN_TOP, bottom: MARGIN_BOTTOM, left: MARGIN_LEFT, right: MARGIN_RIGHT },
      pageNumbers: { start: 1 }
    }
  },
  footers: {
    default: new Footer({
      children: [new Paragraph({
        alignment: AlignmentType.CENTER,
        children: [new TextRun({ children: [PageNumber.CURRENT] })]
      })]
    })
  },
  children: [/* Kapitel */]
}
```

### 2.5 Markdown zu docx-js konvertieren

Beim Konvertieren der Markdown-Kapitel zu docx-js-Elementen beachte:

- `# Überschrift` → `new Paragraph({ heading: HeadingLevel.HEADING_1, children: [...] })`
- `## Überschrift` → `HeadingLevel.HEADING_2`
- `### Überschrift` → `HeadingLevel.HEADING_3`
- Fließtext-Absätze → `new Paragraph({ children: [new TextRun("...")] })`
- **Fettdruck** → `new TextRun({ text: "...", bold: true })`
- *Kursiv* → `new TextRun({ text: "...", italics: true })`
- Direkte Zitate (eingerückt, kursiv): Als eigenen Absatz mit Einzug formatieren
- `[QUELLE ERGÄNZEN]`-Marker → `new TextRun({ text: "[QUELLE ERGÄNZEN]", bold: true, color: "FF0000" })` — rot und fett, damit sie beim Korrekturlesen auffallen

**Wichtig bei der Konvertierung:**
- Zeilenumbrüche innerhalb eines Absatzes ignorieren — ein Absatz = ein Paragraph-Element
- Leere Zeilen zwischen Absätzen markieren Absatzgrenzen
- Fußnoten, falls im Markdown als Inline-Zitate vorhanden, als richtige Fußnoten umsetzen (nur wenn Hochschule Fußnotenzitation verlangt — bei Harvard nicht nötig)

### 2.6 Literaturverzeichnis

Falls ein Literaturverzeichnis vorliegt, formatiere es nach den Vorgaben. Typisch für Harvard im deutschsprachigen Raum:

- Alphabetisch nach Nachnamen sortiert
- Hängender Einzug (erste Zeile normal, Folgezeilen eingerückt)
- Format je nach Quellentyp (Buch, Zeitschriftenaufsatz, Online-Quelle etc.)

Realisiere den hängenden Einzug mit:
```javascript
new Paragraph({
  indent: { left: 720, hanging: 720 }, // Hängender Einzug
  spacing: { after: 120 },
  children: [new TextRun("Müller, A. (2023): Titel des Werks. Verlag, Ort.")]
})
```

### 2.7 Qualitätsprüfung der Word-Datei

Nachdem die Datei erstellt wurde:

1. **Validiere die Datei** mit `python scripts/office/validate.py`
2. **Prüfe visuell**: Konvertiere zu PDF und dann zu Bildern, um das Layout zu prüfen:
   ```bash
   python scripts/office/soffice.py --headless --convert-to pdf bachelorarbeit_final.docx
   pdftoppm -jpeg -r 150 bachelorarbeit_final.pdf preview
   ```
3. Prüfe dabei:
   - Titelblatt korrekt?
   - Inhaltsverzeichnis vorhanden und korrekt nummeriert?
   - Seitenzahlen stimmen (römisch/arabisch)?
   - Schriftart und -größe stimmen?
   - Seitenränder eingehalten?
   - Blocksatz korrekt?
   - Keine abgeschnittenen Texte oder Formatierungsfehler?

## Fortschritt.md aktualisieren

Nach der Finalisierung, aktualisiere `04-fortschritt/Fortschritt.md`:
- Status aller Kapitel auf "Final" setzen
- Gesamtseitenzahl und -wortzahl eintragen
- Verbleibende offene Punkte dokumentieren (insbesondere [QUELLE ERGÄNZEN]-Stellen)
- Dateiname der finalen Word-Datei eintragen
- Datum der Finalisierung notieren

## Output

Die finale Datei wird gespeichert in `06-final/bachelorarbeit_final.docx` (oder ein vom User gewünschter Dateiname). Zusätzlich lieferst du:

1. **Die Word-Datei** — abgabebereit formatiert
2. **Den Prüfbericht** — als Zusammenfassung der Phase-1-Ergebnisse
3. **Hinweise** — Falls noch offene Punkte existieren (insbesondere [QUELLE ERGÄNZEN]-Stellen), liste sie auf

## Wichtige Hinweise

- **Erfinde keine Inhalte.** Du formatierst und prüfst — du schreibst keine neuen Kapitel. Wenn etwas fehlt, weise den User darauf hin.
- **Respektiere die Formatvorgaben exakt.** Hochschulen sind bei der Formatierung oft penibel. Lieber einmal mehr nachfragen als falsch formatieren.
- **Titelblatt und Eidesstattliche Erklärung** sind oft streng vorgegeben. Falls der User eine Vorlage hat, verwende sie. Falls nicht, frage nach.
- **Inhaltsverzeichnis**: Nutze die docx-js TableOfContents-Funktion. Weise den User darauf hin, dass er das Verzeichnis in Word einmal aktualisieren muss (Rechtsklick → Felder aktualisieren), da docx-js kein dynamisches TOC generieren kann.
- **Seitenumbrüche**: Jedes Hauptkapitel (Ebene 1) beginnt auf einer neuen Seite. Verwende `pageBreakBefore: true` auf Heading-1-Paragraphen.
- **Plagiatsprüfung**: Weise den User vor der Abgabe darauf hin: "Empfehlung: Lasse die Arbeit durch die Plagiatssoftware deiner Hochschule laufen (Turnitin, PlagScan o.ä.), bevor du abgibst." Das ist kein Schritt, den Claude übernimmt, aber ein kritischer Hinweis.
- **Abbildungen/Tabellen**: Falls im Text Platzhalter wie `[ABBILDUNG X: Beschreibung]` stehen, weise den User darauf hin, dass diese vor Abgabe durch echte Abbildungen ersetzt werden müssen. Erstelle leere Platzhalter-Absätze mit der Beschriftung im Word-Dokument.
