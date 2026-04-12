---
name: bachelorarbeit-recherche
description: >
  Phase 2 der Bachelorarbeit-Pipeline: Systematische Quellenrecherche mit NotebookLM. Sucht, sammelt und organisiert wissenschaftliche Quellen kapitelweise. Setzt voraus, dass Phase 1 (Planung) abgeschlossen ist — Forschungsfrage und Gliederung müssen vorliegen. Übergibt sauber an Phase 3 (Quellenauswertung). Nutze bei: "Quellen suchen", "Literatur recherchieren", "Papers finden", "Literaturrecherche", "Quellen sammeln", "recherchiere zu [Thema]", "finde Quellen", "Literatursuche", "welche Papers gibt es zu", "Recherche starten", "Deep Research", "Quellensuche", "ich brauche Literatur zu". Nicht für Quellenauswertung — dafür gibt es `bachelorarbeit-quellenauswertung`.
---

# Bachelorarbeit — Phase 2: Recherche

Du führst systematische Literaturrecherchen durch und sammelst wissenschaftliche Quellen für einzelne Kapitel. Dein Hauptwerkzeug ist **NotebookLM**, das du über die CLI (`notebooklm-py`) steuerst.

**Klare Abgrenzung zu anderen Phasen:**
- Phase 1 (Planung) liefert dir Forschungsfrage + Gliederung — du baust darauf auf
- Du **sammelst nur Quellen** und dokumentierst sie. Du interpretierst sie nicht, extrahierst keine Kernaussagen, baust keine Argumentationsketten — das ist Phase 3
- Der Output dieser Phase ist ein gepflegtes NotebookLM-Notebook + Recherche-Protokolle pro Kapitel

## Voraussetzungen (aus Phase 1)

Bevor du startest, prüfe:

1. **NotebookLM ist authentifiziert:** `notebooklm status` — muss eine Email anzeigen
2. **Forschungsfrage existiert:** Lies `02-quellen/Forschungsfrage.md`
3. **Gliederung existiert:** Lies `01-docs/Gliederung.md`
4. **Fortschritt.md existiert:** Lies `04-fortschritt/Fortschritt.md`, um den Überblick zu behalten

Falls eines fehlt, weise auf Phase 1 (`bachelorarbeit-planung`) hin und biete nicht an, die Lücke hier zu schließen — die Phasen sind bewusst getrennt.

## Ablauf

### 1. Recherche-Notebook anlegen

Pro Bachelorarbeit ein zentrales Notebook. Prüfe zuerst, ob eines existiert:

```bash
notebooklm list --json
```

Falls kein BA-Notebook existiert:
```bash
notebooklm create "BA: [Thema aus Forschungsfrage.md]" --json
notebooklm language set de
```

Speichere die Notebook-ID im Recherche-Protokoll für spätere Schritte.

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

Schlage dem User 3–5 Suchbegriffe vor und lass ihn bestätigen oder anpassen.

### 3. Quellen sammeln

Drei Kanäle — nutze alle passenden:

**a) Deep Research (Hauptkanal für neue Quellen)**

Für jedes Kapitel mindestens eine Deep-Recherche:
```bash
notebooklm source add-research "[Suchbegriff]" --mode deep --no-wait
```

Deep Research braucht 2–5 Minuten und findet 20+ Quellen. Starte mehrere parallel mit unterschiedlichen Suchbegriffen.

Status prüfen:
```bash
notebooklm research status
```

Gefundene Quellen importieren:
```bash
notebooklm research wait --import-all --timeout 300
```

**b) Schnelle Recherche (für gezielte Ergänzungen)**

```bash
notebooklm source add-research "[spezifische Suche]" --mode fast
```

Sekundenschnell, 5–10 gezielte Ergebnisse.

**c) Bekannte Quellen hinzufügen**

```bash
notebooklm source add "./pfad/zur/datei.pdf" --json
notebooklm source add "https://doi.org/10.xxxx/..." --json
notebooklm source add "https://youtube.com/watch?v=..." --json
```

Warte auf Indexierung:
```bash
notebooklm source list --json
```

Alle Quellen müssen `status: "ready"` haben, bevor sie in Phase 3 ausgewertet werden können.

### 4. Upload-Validierung (kritisch)

**Prüfe nach jedem Upload-Durchlauf**, ob alle Quellen erfolgreich indexiert wurden. Nicht alle URLs laden in NotebookLM (Paywalls, Login-Walls, PDF-Captchas).

```bash
notebooklm source list --json
```

Liste fehlgeschlagene Quellen und versuche:
1. Alternative URL finden (z.B. Open-Access-Version statt Paywall)
2. PDF manuell beschaffen und lokal hochladen
3. Quelle notfalls als nicht verfügbar markieren und im Recherche-Protokoll dokumentieren

### 5. Quellen sichten und filtern

**Alle Quellen auflisten:**
```bash
notebooklm source list --json
```

**Relevanz prüfen (grobe Sichtung, keine Auswertung!):**
```bash
notebooklm ask "Welche der importierten Quellen sind für das Thema '[Kapitelthema]' am relevantesten? Bewerte jede Quelle auf einer Skala von 1–5 und begründe in EINEM Satz." --json
```

**Irrelevante Quellen entfernen** nach Rücksprache mit dem User:
```bash
notebooklm source delete [source_id]
```

Das hält das Notebook sauber und verbessert die Qualität in Phase 3.

### 6. Recherche-Protokoll erstellen

Speichere ein Recherche-Protokoll pro Kapitel in `02-quellen/`:

```markdown
# Recherche-Protokoll Kapitel [X]: [Titel]

**Datum:** [Datum]
**NotebookLM-Notebook:** [Notebook-ID + Titel]
**Forschungsfrage:** [[Forschungsfrage]]

## Suchbegriffe
- [Suchbegriff 1] (deep research, [Anzahl] Quellen)
- [Suchbegriff 2] (fast research, [Anzahl] Quellen)
- [manuell hinzugefügt: X Quellen]

## Gesammelte Quellen

| # | Titel | Autor | Jahr | Typ | Relevanz | Source-ID |
|---|---|---|---|---|---|---|
| 1 | [Titel] | [Autor] | 2023 | Paper/Buch/Web | ★★★★☆ | [ID] |
| 2 | ... | ... | ... | ... | ... | ... |

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

Falls Lücken bestehen, wiederhole Schritt 3 mit spezifischeren Suchbegriffen. Erst wenn du mindestens **10–15 relevante Quellen** (Relevanz 4–5) pro Kapitel hast, ist die Recherche für dieses Kapitel abgeschlossen.

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
- [ ] Alle Quellen haben `status: "ready"`
- [ ] Recherche-Protokoll `02-quellen/Recherche_Kapitel_[X]_*.md` ist geschrieben
- [ ] Fehlgeschlagene Uploads sind dokumentiert
- [ ] Fortschritt.md ist aktualisiert

**Handoff-Nachricht:**

> Phase 2 (Recherche) für Kapitel [X] ist abgeschlossen. Im NotebookLM-Notebook liegen [Anzahl] indexierte Quellen. Das Recherche-Protokoll findest du unter [[Recherche_Kapitel_X_Kurztitel]].
>
> **Nächster Schritt — Phase 3: Quellenauswertung.**
> Starte den `bachelorarbeit-quellenauswertung`-Skill. Er extrahiert systematisch Kernaussagen, Zitate und Argumentationsketten aus den gesammelten Quellen und bereitet sie für den Writer-Skill auf.

## Zusammenspiel mit anderen Skills

- **Vor Phase 2** → `bachelorarbeit-planung` liefert Forschungsfrage und Gliederung
- **Nach Phase 2** → `bachelorarbeit-quellenauswertung` analysiert die gesammelten Quellen
- **Quer** → Bei Lücken, die erst beim Review auffallen, kann Phase 2 für einzelne Kapitel erneut gestartet werden (Nachrecherche)
