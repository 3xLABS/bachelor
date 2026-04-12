# Pipeline-Analyse: Lücken, Limitierungen, Verbesserungsvorschläge

Stand: 29. März 2026
Analysiert: 5 Skills, CLAUDE.md, Prompts.md, Obsidian-Struktur

---

## 1. Dateipfad-Inkonsistenzen (Kritisch)

Die Skills wissen nicht, wo sie ihre Dateien ablegen sollen. Das ist das größte strukturelle Problem.

### Problem

| Skill | Sagt wo Dateien hin sollen | Obsidian-Struktur sagt |
|---|---|---|
| **Writer** | "im selben Verzeichnis" (unspezifisch) | `03-text/XX-Kapitelname/` |
| **Reviewer** | "Speichere als `review_kapitel_X_Y.md`" (kein Ordner) | `05-review/` |
| **Überarbeitung** | "Speichere mit Suffix `_v2`" (kein Ordner) | `03-text/XX-Kapitelname/` |
| **Finalisierung** | "`bachelorarbeit_final.docx`" (kein Ordner) | `06-final/` |
| **Writer** (Fortschritt) | "im selben Verzeichnis wie Kapitel" | `04-fortschritt/Fortschritt.md` |

**Risiko:** Jeder Skill legt Dateien woanders ab. Der nächste Skill in der Pipeline findet sie nicht.

### Fix

Jeden Skill explizit auf die Obsidian-Ordnerstruktur referenzieren:
- Writer: Speichere in `03-text/[Kapitelordner]/`
- Reviewer: Speichere in `05-review/`
- Überarbeitung: Speichere in `03-text/[Kapitelordner]/`
- Finalisierung: Speichere in `06-final/`
- Fortschritt.md: Immer `04-fortschritt/Fortschritt.md`

---

## 2. Fortschritt.md — Inkonsistenter Status-Flow

### Problem

Jeder Skill verwendet andere Statusbezeichnungen:

| Skill | Setzt Status auf |
|---|---|
| Writer | "Erster Entwurf" |
| Reviewer | "Reviewed — Überarbeitung nötig" ODER "Reviewed — Freigabe" |
| Überarbeitung | "Überarbeitet" |
| Finalisierung | "Final" |
| CLAUDE.md | "Erster Entwurf → Reviewed → Überarbeitet → Final" |
| Planung | "Planung" (in der Planungstabelle, nicht in der Kapiteltabelle) |

Der Reviewer schreibt "Reviewed — Überarbeitung nötig" oder "Reviewed — Freigabe", aber die CLAUDE.md dokumentiert nur "Reviewed". Die Überarbeitung prüft nicht, ob der Status "Freigabe" ist (dann bräuchte man keine Überarbeitung).

### Fix

Standardisierte Status-Enum definieren und in allen Skills referenzieren:
```
Erster Entwurf → Reviewed → Überarbeitet → Final
```
Reviewer setzt immer "Reviewed" und dokumentiert in den Offenen Punkten, ob Überarbeitung nötig ist. Die Unterscheidung "Freigabe vs. Überarbeitung nötig" gehört in den Review-Text, nicht in den Status.

---

## 3. Literaturverzeichnis — Niemand erstellt es

### Problem

Das Literaturverzeichnis ist eine Pflichtkomponente jeder Abschlussarbeit, aber kein Skill ist dafür verantwortlich:

- **Writer** erstellt pro Kapitel eine Liste "Verwendete Quellen in diesem Kapitel" — das sind Fragmente, kein vollständiges Verzeichnis
- **Planung** erstellt ein Quellenverzeichnis (`02-quellen/Quellenverzeichnis.md`), aber im Perplexity-Format (Autor, Titel, Jahr, URL, Kurzbeschreibung) — nicht im Harvard-Bibliographieformat
- **Finalisierung** sagt "Falls ein Literaturverzeichnis vorliegt, formatiere es" — aber wer erstellt es?

**Ergebnis:** Der User kommt zur Finalisierung und hat kein korrekt formatiertes Literaturverzeichnis. Die Finalisierung wartet darauf, dass es "vorliegt", aber niemand hat es erzeugt.

### Fix

Zwei Optionen:

**Option A:** Neuer Schritt im Überarbeitungs-Skill oder eigener Mini-Skill "Literaturverzeichnis": Sammelt alle `## Verwendete Quellen in diesem Kapitel`-Abschnitte aus allen Kapiteln, dedupliziert sie, formatiert sie im Harvard-Bibliographieformat, speichert als `02-quellen/Literaturverzeichnis.md`.

**Option B (einfacher):** In die Finalisierung einbauen — vor der Word-Erstellung alle Kapitel scannen, alle Zitate extrahieren, Literaturverzeichnis automatisch zusammenbauen. Dafür das Quellenverzeichnis aus der Planung als Datenbasis nutzen.

---

## 4. Cross-Tool-Handoff: Gemini → Claude (Fragil)

### Problem

Der aufwendigste und fehleranfälligste Schritt ist der Übergang von Gemini/NotebookLM zu Claude:

1. **Copy-Paste-Verlust:** User muss Gemini-Output manuell kopieren und in Claude einfügen. Dabei gehen Formatierungen verloren, Seitenangaben werden abgeschnitten, Markdown-Syntax bricht
2. **Keine Validierung:** Claude hat keine Möglichkeit zu prüfen, ob Geminis Seitenangaben stimmen. Wenn Gemini "S. 45" sagt, muss Claude das glauben
3. **NotebookLM-Ladeprobleme:** Nicht alle URLs laden in NotebookLM (Paywalls, Login-Walls, PDF-Captchas). Der User merkt es vielleicht nicht, und die Quellenauswertung hat dann Lücken
4. **Kein Rückkanal:** Wenn Claude bei der Qualitätsprüfung der Quellenauswertung Lücken findet, muss der User zurück zu Gemini, neuen Prompt formulieren, Ergebnis wieder kopieren — viele manuelle Schritte

### Fix

- **Checkliste für NotebookLM-Upload** in den Planungs-Skill einbauen: "Prüfe nach dem Upload, ob alle Quellen einen grünen Haken haben. Liste die fehlgeschlagenen Quellen und lade sie manuell als PDF hoch."
- **Validierungsschritt in der Quellenauswertung:** Claude prüft jede Auswertung gegen das Quellenverzeichnis — sind alle Quellen, die laut Verzeichnis relevant sein sollten, auch tatsächlich ausgewertet?
- **Standard-Kopierformat** definieren: Markdown-Codeblock, damit Formatierung beim Paste erhalten bleibt

---

## 5. Kein Abbildungen/Tabellen-Workflow

### Problem

Wissenschaftliche Arbeiten enthalten fast immer Abbildungen und Tabellen:
- Modelle und Frameworks (z.B. COSO ERM als Grafik)
- Ergebnistabellen
- Vergleichsmatrizen
- Prozessdiagramme

Kein Skill adressiert das:
- **Writer** erwähnt keine Abbildungen
- **Finalisierung** erwähnt Abbildungsverzeichnis, aber nur "falls vorhanden"
- **Keine Anleitung**, wie Abbildungen erstellt, nummeriert und referenziert werden

### Fix

Im Writer-Skill ergänzen:
- Wenn ein Kapitel eine Abbildung oder Tabelle braucht, beschreibe sie als Platzhalter: `[ABBILDUNG X: Beschreibung]`
- Nummerierungskonvention: Abb. 2.1 = erste Abbildung in Kapitel 2
- Quellenangabe unter Abbildungen: "Quelle: Eigene Darstellung in Anlehnung an Porter (2008, S. 214)"

In der Finalisierung ergänzen:
- Abbildungsverzeichnis und Tabellenverzeichnis automatisch aus den Platzhaltern generieren
- Canva-MCP für Abbildungserstellung nutzen (ist verfügbar!)

---

## 6. Fehlende Betreuer-Feedback-Schleife

### Problem

In der Realität läuft eine Abschlussarbeit nicht Writer → Reviewer → Überarbeitung → fertig. Der reale Zyklus ist:

```
Schreiben → Eigenes Review → Überarbeitung → Betreuer zeigen
→ Betreuer-Feedback → Überarbeitung → Betreuer zeigen → ...
```

Das Betreuer-Feedback hat eine fundamental andere Qualität als das Claude-Review:
- Der Betreuer kennt die Prüfungsordnung
- Der Betreuer hat inhaltliche Präferenzen
- Der Betreuer gibt oft vage Hinweise ("das müssen Sie noch vertiefen")

### Fix

Im Überarbeitungs-Skill eine zweite Eingabevariante einbauen:
- Input kann nicht nur ein Review vom Reviewer-Skill sein, sondern auch **Freitext-Feedback vom Betreuer** (Stichpunkte, E-Mail, Kommentare in Word)
- Claude übersetzt das Betreuer-Feedback in das Muss/Sollte/Optional-Format und arbeitet es ein
- Das ist teilweise schon da ("Feedback in anderer Form: Stichpunkte, Kommentare, Freitext"), aber es wird nicht als eigener Anwendungsfall hervorgehoben

---

## 7. Plagiatsprüfung / KI-Erkennung — Komplett fehlend

### Problem

Zwei reale Risiken, die die Pipeline nicht adressiert:

1. **Plagiat:** Wenn Claude Formulierungen aus den Quellen übernimmt, die zu nah am Original sind, schlägt Turnitin/PlagScan an
2. **KI-Erkennung:** Viele Hochschulen nutzen mittlerweile KI-Detektoren. Claude-generierter Text hat erkennbare Muster

### Fix

**Im Writer-Skill ergänzen:**
- Explizite Anweisung: Nie Formulierungen aus den Quellenauswertungen 1:1 übernehmen, immer in eigenen Worten formulieren
- Stilvariation: Satzlänge variieren, nicht immer die gleichen Konnektoren verwenden
- Direkte Zitate nur wenn wörtlich aus der Quelle und als solches markiert

**Neuer Prüfschritt vor Finalisierung:**
- Checkliste: "Hat der User die Arbeit durch einen Plagiatscheck laufen lassen?"
- Hinweis: "Empfehlung: Lasse die Arbeit vor Abgabe durch [Turnitin/PlagScan/eigene Hochschul-Software] laufen"

---

## 8. Prompts.md ist vom Skill entkoppelt

### Problem

Der Planungs-Skill generiert intern Prompts für Perplexity/Gemini. Gleichzeitig existiert `Prompts.md` als separate Datei mit (teilweise anderen) Prompts. Der User weiß nicht, welche er nutzen soll — die aus dem Skill oder die aus der Datei.

### Fix

Zwei Optionen:

**Option A:** Planungs-Skill referenziert explizit die Prompts.md: "Öffne `Prompts.md` und nutze Prompt P-2 für die Quellenrecherche." Der Skill generiert keine eigenen Prompts mehr, sondern verweist auf die zentrale Datei.

**Option B:** Prompts.md wird zur reinen Referenz/Nachschlagewerk, der Skill generiert kontextspezifische Prompts (mit konkretem Thema, konkreter Forschungsfrage eingesetzt). Aber: Prompts.md sollte dann als "Vorlagen-Bibliothek" markiert werden, nicht als Arbeitsanleitung.

**Empfehlung:** Option B — der Skill generiert maßgeschneiderte Prompts (besser für den User), Prompts.md dient als Referenz für manuelle Nutzung.

---

## 9. Keine Zeitplanung / Meilensteine

### Problem

Die Pipeline sagt, WAS zu tun ist, aber nicht WANN. Eine Abschlussarbeit hat eine Deadline, und die Kapitel müssen zeitlich geplant werden. Fortschritt.md trackt den Ist-Stand, aber nicht den Soll-Stand.

### Fix

Im Planungs-Skill ergänzen — Phase 6.5 "Zeitplanung":
- Abgabedatum wird schon abgefragt, aber nicht weiterverwendet
- Rückwärtsplanung: Vom Abgabedatum 2 Wochen für Korrekturlesen, 1 Woche für Finalisierung abziehen
- Wochenweise Meilensteine: "KW 14: Theoriekapitel fertig, KW 16: Methodik fertig"
- In Fortschritt.md als Soll/Ist-Vergleich tracken

---

## 10. Writer kennt keine Nachbarkapitel

### Problem

Der Writer schreibt Kapitel isoliert. Er kennt nur die Gliederung und die Quellenauswertung für das aktuelle Kapitel. Er weiß nicht:
- Was im vorherigen Kapitel steht (→ kann nicht anknüpfen)
- Was im nächsten Kapitel kommen wird (→ kann nicht vorbereiten)
- Welche Begriffe schon definiert wurden (→ definiert doppelt)

Der Überarbeitungs-Skill versucht, das nachträglich zu reparieren ("Harmonisierung"), aber das ist Symptombehandlung.

### Fix

Im Writer-Skill ergänzen:
- "Falls bereits andere Kapitel geschrieben wurden, lies zumindest den letzten Absatz des vorherigen und den ersten Absatz des nächsten Kapitels (falls vorhanden)"
- "Lies die Fortschritt.md, um zu sehen, welche Begriffe bereits eingeführt wurden"
- Optional: "Wenn das vorherige Kapitel als Datei vorliegt, lies die letzten 2-3 Absätze, um einen sauberen Übergang zu schaffen"

---

## 11. Finalisierung: Keine Word-Template-Unterstützung

### Problem

Viele Hochschulen stellen .dotx-Templates bereit (mit korrekt eingerichtetem Titelblatt, Formatvorlagen, Seitenzahlen). Die Finalisierung baut alles von Null auf mit docx-js — aufwendig und fehleranfällig.

### Fix

Im Finalisierungs-Skill ergänzen:
- "Falls der User eine .dotx- oder .docx-Vorlage der Hochschule hat, lade sie als Basis und fülle den Inhalt ein, statt alles from scratch zu bauen"
- Technisch: docx-js unterstützt das Laden bestehender Dokumente über `Packer.toBuffer()` nicht direkt, aber man kann die Template-Styles extrahieren und übernehmen
- Alternativ: python-docx als Fallback, das bestehende Templates beschreiben kann

---

## 12. Quellenauswertungs-Format nicht rückwärts-validiert

### Problem

Der Planungs-Skill definiert ein Format für kapitelweise Quellenauswertungen. Der Writer-Skill erwartet "Zusammenfassungen, Exzerpte, oder Notizen zu den Quellen". Diese zwei Beschreibungen sind kompatibel, aber nicht explizit verknüpft. Wenn das Gemini-Output vom definierten Format abweicht, merkt es keiner.

### Fix

Im Writer-Skill explizit referenzieren:
- "Die Quellenauswertung liegt idealerweise im Format des Planungs-Skills vor (siehe `02-quellen/Auswertung_KapX_*.md`). Falls sie in einem anderen Format vorliegt, arbeite damit — aber weise den User darauf hin, dass das Standardformat die Qualität verbessert."

---

## 13. Fehlende Kapitel-Typen im Writer

### Problem

Der Writer kennt Argumentationsstrukturen (linear, dialektisch, deduktiv, induktiv), aber er hat keine spezifische Anleitung für bestimmte Kapiteltypen:

- **Einleitung:** Hat eigene Regeln (Problemstellung → Forschungsfrage → Aufbau der Arbeit). Ist keine normale Argumentation.
- **Methodik:** Beschreibt Vorgehen, ist weder argumentativ noch theoretisch.
- **Fazit:** Fasst zusammen, bringt keine neuen Argumente. Beantwortet die Forschungsfrage.

Alle drei werden aktuell wie Theorie- oder Diskussionskapitel behandelt.

### Fix

Im Writer-Skill kapitelspezifische Hinweise ergänzen:
- Einleitung: Trichterstruktur (breit → eng → Forschungsfrage → Aufbau)
- Methodik: Beschreibend, nicht argumentativ. Klare Begründung der Methodenwahl.
- Fazit: Keine neuen Quellen, keine neuen Argumente. Kompakte Beantwortung der Forschungsfrage.

---

## Zusammenfassung nach Priorität

### Kritisch (brechen den Workflow)
1. **Dateipfad-Inkonsistenzen** — Skills wissen nicht, wo sie speichern sollen
2. **Literaturverzeichnis fehlt** — Pflichtkomponente, niemand erstellt es
3. **Fortschritt.md Location** — Writer legt sie woanders an als CLAUDE.md vorgibt

### Hoch (verschlechtern die Qualität deutlich)
4. **Cross-Tool-Handoff Gemini→Claude** — Copy-Paste-Fehler, keine Validierung
5. **Writer kennt keine Nachbarkapitel** — Kapitel stehen isoliert
6. **Kapiteltyp-spezifische Anleitung fehlt** — Einleitung/Methodik/Fazit
7. **Quellenformat nicht rückwärts-validiert** — Gemini-Output passt vielleicht nicht

### Mittel (verbessern den Prozess)
8. **Prompts.md entkoppelt** — Doppelte Prompt-Quellen verwirren
9. **Status-Flow inkonsistent** — Reviewer-Status weicht ab
10. **Keine Zeitplanung** — Pipeline sagt Was, nicht Wann
11. **Betreuer-Feedback-Schleife** — Realer Workflow fehlt

### Niedrig (Nice-to-have)
12. **Abbildungen/Tabellen-Workflow** — Platzhalter-System + Canva
13. **Word-Template-Unterstützung** — Hochschul-Vorlagen nutzen
14. **Plagiat/KI-Erkennung** — Hinweis + Stilvariation
