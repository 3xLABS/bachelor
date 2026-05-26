---
name: bachelorarbeit-recherche
description: >
  Phase 2 der Bachelorarbeit-Pipeline: Systematische Quellenrecherche für die Bachelorarbeit. Claude entwickelt die Recherchestrategie, generiert Suchbegriffe und gibt dem User Schritt-für-Schritt-Anleitungen für die Recherche in NotebookLM (im Browser). Der User navigiert selbstständig zu NotebookLM und führt die Suche dort durch. Claude dokumentiert alles im Recherche-Protokoll. Setzt voraus, dass Phase 1 (Planung) abgeschlossen ist — Forschungsfrage und Gliederung müssen vorliegen. Übergibt sauber an Phase 3 (Quellenauswertung). Nutze bei: "Quellen suchen", "Literatur recherchieren", "Papers finden", "Literaturrecherche", "Quellen sammeln", "recherchiere zu [Thema]", "finde Quellen", "Literatursuche", "welche Papers gibt es zu", "Recherche starten", "Deep Research", "Quellensuche", "ich brauche Literatur zu". Nicht für Quellenauswertung — dafür gibt es `bachelorarbeit-quellenauswertung`.
---

# Bachelorarbeit — Phase 2: Recherche

Du unterstützt den User bei der systematischen Literaturrecherche. Der User arbeitet **selbstständig in NotebookLM im Browser** — du lieferst die Strategie, Suchbegriffe, Anleitungen und dokumentierst die Ergebnisse.

**Klare Abgrenzung zu anderen Phasen:**
- Phase 1 (Planung) liefert dir Forschungsfrage + Gliederung — du baust darauf auf
- Du **planst und dokumentierst die Recherche**. Du interpretierst die Quellen nicht, extrahierst keine Kernaussagen, baust keine Argumentationsketten — das ist Phase 3
- Der Output dieser Phase ist ein Recherche-Protokoll pro Kapitel + ein gepflegtes NotebookLM-Notebook (das der User im Browser verwaltet)

## Voraussetzungen (aus Phase 1)

Bevor du startest, prüfe:

1. **Forschungsfrage existiert:** Lies `02-quellen/Forschungsfrage.md` oder `02-quellen/BA_Forschungsfrage.md`
2. **Gliederung existiert:** Lies `01-docs/Gliederung.md` oder `01-docs/BA-Gliederung-Muster.md`
3. **Fortschritt.md existiert:** Lies `04-fortschritt/Fortschritt.md`, um den Überblick zu behalten

Falls eines fehlt, weise auf Phase 1 (`bachelorarbeit-planung`) hin und biete nicht an, die Lücke hier zu schließen — die Phasen sind bewusst getrennt.

## Ablauf

### 1. NotebookLM-Notebook anlegen (User-Anleitung)

Der User muss ein zentrales Notebook in NotebookLM anlegen. Gib ihm diese Anleitung:

> **NotebookLM-Notebook erstellen:**
>
> 1. Öffne [notebooklm.google.com](https://notebooklm.google.com) in deinem Browser
> 2. Klicke auf **"Neues Notebook"** / **"New Notebook"**
> 3. Benenne es: `BA: [Dein Thema]`
> 4. Das Notebook ist jetzt bereit — hier sammelst du alle Quellen für die Bachelorarbeit
>
> Bestätige mir, wenn das Notebook angelegt ist.

### 2. Recherche-Strategie festlegen

Frage den User, welches Kapitel recherchiert werden soll. Empfehlung: **Beginne mit dem Theoriekapitel**, weil es die begriffliche Grundlage legt, die alle anderen Kapitel brauchen.

Lies die Gliederung und formuliere Suchbegriffe. Gute Suchbegriffe sind:

- **Spezifisch zum Kapitelthema**, nicht zum Gesamtthema
- **Englisch UND Deutsch** — wissenschaftliche Literatur ist oft englisch
- **Mit Fachbegriffen und Synonymen** — ein Thema hat oft mehrere Bezeichnungen

Beispiel für Kapitel "Theoretische Grundlagen des Risikomanagements":
- `"risk management theoretical framework ISO 31000 COSO"`
- `"Risikomanagement theoretische Grundlagen Risikoidentifikation"`
- `"enterprise risk management ERM framework comparison"`

Schlage dem User 3–5 Suchbegriffe pro Kapitel vor und lass ihn bestätigen oder anpassen.

### 3. Quellen sammeln (User-Anleitung)

Leite den User durch drei Kanäle:

**a) Deep Research in NotebookLM (Hauptkanal für neue Quellen)**

> **Deep Research starten:**
>
> 1. Öffne dein BA-Notebook in NotebookLM
> 2. Nutze die **Research**-Funktion (Symbol oben rechts oder im Chat)
> 3. Gib den folgenden Suchbegriff ein: `[Suchbegriff]`
> 4. Wähle **Deep Research** — das dauert 2–5 Minuten und findet 20+ Quellen
> 5. Importiere die relevanten Ergebnisse ins Notebook
> 6. Wiederhole mit den weiteren Suchbegriffen
>
> Sag mir Bescheid, wenn du fertig bist — nenne mir die Anzahl der gefundenen Quellen.

**b) Bekannte Quellen manuell hinzufügen**

> **Quellen manuell hinzufügen:**
>
> In NotebookLM kannst du verschiedene Quellentypen hinzufügen:
> - **PDFs** — über "Upload" oder Drag & Drop
> - **Webseiten/URLs** — über "Link hinzufügen" (DOI-Links, Artikel-URLs)
> - **YouTube-Videos** — URL einfügen
> - **Google Docs** — direkt aus deinem Drive verknüpfen
>
> Warte jeweils, bis die Quelle als "indexiert" / "ready" angezeigt wird.

**c) Ergänzende Web-Recherche (Claude)**

Claude kann ergänzend im Web suchen (Google Scholar, Fachportale), um Quellen-Tipps zu liefern. Diese gibt Claude als Links, die der User dann manuell in NotebookLM importiert.

### 4. Upload-Validierung

Erkläre dem User, worauf er achten muss:

> **Prüfe nach dem Upload:**
>
> Nicht alle URLs laden in NotebookLM — Paywalls, Login-Walls und Captchas können den Import blockieren.
>
> - Prüfe in der Quellenliste, ob jede Quelle den Status **"Ready"** hat
> - Bei fehlgeschlagenen Uploads: Suche eine alternative URL (z.B. Open-Access-Version) oder lade die PDF manuell hoch
> - Notiere fehlgeschlagene Quellen — ich dokumentiere sie im Recherche-Protokoll

Frage den User nach fehlgeschlagenen Uploads und dokumentiere sie.

### 5. Quellen sichten und filtern

Leite den User an, die Quellen grob zu sichten:

> **Relevanz-Check in NotebookLM:**
>
> 1. Gib im NotebookLM-Chat ein: "Welche der importierten Quellen sind für das Thema '[Kapitelthema]' am relevantesten? Bewerte jede Quelle auf einer Skala von 1–5 und begründe in EINEM Satz."
> 2. Kopiere die Antwort und gib sie mir — ich verarbeite sie fürs Recherche-Protokoll
> 3. Quellen mit Relevanz 1–2 kannst du aus dem Notebook entfernen (Häkchen entfernen oder löschen)

### 6. Recherche-Protokoll erstellen

Erstelle auf Basis der User-Rückmeldungen ein Recherche-Protokoll in `02-quellen/`:

```markdown
# Recherche-Protokoll Kapitel [X]: [Titel]

**Datum:** [Datum]
**NotebookLM-Notebook:** [Titel des Notebooks, vom User genannt]
**Forschungsfrage:** [[Forschungsfrage]]

## Suchbegriffe
- [Suchbegriff 1] (deep research, [Anzahl] Quellen)
- [Suchbegriff 2] (deep research, [Anzahl] Quellen)
- [manuell hinzugefügt: X Quellen]

## Gesammelte Quellen

| # | Titel | Autor | Jahr | Typ | Relevanz |
|---|---|---|---|---|---|
| 1 | [Titel] | [Autor] | 2023 | Paper/Buch/Web | ★★★★☆ |
| 2 | ... | ... | ... | ... | ... |

## Fehlgeschlagene Uploads
- [URL] — Grund: [Paywall / Login / Captcha / ...]

## Offene Punkte
- Quellen die noch fehlen
- Themen die noch nicht abgedeckt sind

## Nächster Schritt
Phase 3: `bachelorarbeit-quellenauswertung` für dieses Kapitel ausführen.
```

**Dateiname:** `02-quellen/Recherche_Kapitel_[X]_[Kurztitel].md`

### 7. Ergänzungsrecherche

Prüfe nach der ersten Runde:
- Sind alle Aspekte des Kapitels durch Quellen abgedeckt?
- Gibt es Forschungslücken, die weitere Recherche erfordern?
- Hat der User eigene Quellen, die noch fehlen?

Falls Lücken bestehen, wiederhole Schritt 3 mit spezifischeren Suchbegriffen. Erst wenn mindestens **10–15 relevante Quellen** (Relevanz 4–5) pro Kapitel vorliegen, ist die Recherche für dieses Kapitel abgeschlossen.

### 8. Fortschritt.md aktualisieren

Trage den Recherche-Fortschritt in `04-fortschritt/Fortschritt.md` ein:
- Pipeline-Status für Phase 2: "In Bearbeitung" oder "Abgeschlossen für Kapitel [X]"
- Offene Punkte aktualisieren
- Nächste Schritte: Phase 3 für das gleiche Kapitel

## Qualitätskriterien für Quellen

Weise den User auf diese Kriterien hin, wenn Quellen grenzwertig sind:

- **Aktualität** — Bevorzugt aus den letzten 5–10 Jahren, Grundlagenwerke ausgenommen
- **Wissenschaftlichkeit** — Peer-reviewed Papers, Fachbücher, Reports etablierter Institutionen bevorzugen
- **Relevanz** — Direkte Verbindung zum Kapitelthema, nicht nur am Rande verwandt
- **Vielfalt** — Verschiedene Perspektiven, nicht nur Autoren der gleichen Schule

## Handoff an Phase 3

Wenn die Recherche für ein Kapitel abgeschlossen ist:

**Checkliste:**
- [ ] NotebookLM-Notebook enthält mindestens 10–15 relevante Quellen für das Kapitel
- [ ] Alle Quellen sind in NotebookLM indexiert (Status "ready")
- [ ] Recherche-Protokoll `02-quellen/Recherche_Kapitel_[X]_*.md` ist geschrieben
- [ ] Fehlgeschlagene Uploads sind dokumentiert
- [ ] Fortschritt.md ist aktualisiert

**Handoff-Nachricht:**

> Phase 2 (Recherche) für Kapitel [X] ist abgeschlossen. Im NotebookLM-Notebook liegen [Anzahl] indexierte Quellen. Das Recherche-Protokoll findest du unter [[Recherche_Kapitel_X_Kurztitel]].
>
> **Nächster Schritt — Phase 3: Quellenauswertung.**
> Starte den `bachelorarbeit-quellenauswertung`-Skill. Er führt dich durch die Auswertung der Quellen mit Gemini und bereitet die Ergebnisse für den Writer-Skill auf.

## Zusammenspiel mit anderen Skills

- **Vor Phase 2** → `bachelorarbeit-planung` liefert Forschungsfrage und Gliederung
- **Nach Phase 2** → `bachelorarbeit-quellenauswertung` analysiert die gesammelten Quellen (via Gemini im Browser)
- **Quer** → Bei Lücken, die erst beim Review auffallen, kann Phase 2 für einzelne Kapitel erneut gestartet werden (Nachrecherche)
