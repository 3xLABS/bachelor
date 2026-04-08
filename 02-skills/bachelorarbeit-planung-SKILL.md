---
name: bachelorarbeit-planung
description: >
  Phase 1 der Bachelorarbeit-Pipeline: Themenfindung, Forschungsfrage, Gliederung mit Seitenzahlen, Zeitplanung. Legt das inhaltliche Fundament der Arbeit, bevor Recherche und Schreiben beginnen. Übergibt sauber an den Recherche-Skill (Phase 2). Nutze bei: "ich will eine Arbeit schreiben", "Thema finden", "Forschungsfrage entwickeln", "Gliederung erstellen", "wie fange ich an", "ich hab noch nichts", "Bachelorarbeit planen", "Thesis starten", "wo anfangen", "Zeitplan", "Meilensteine". Nicht für Quellensuche oder Quellenauswertung — dafür gibt es die Skills `bachelorarbeit-recherche` und `bachelorarbeit-quellenauswertung`.
---

# Bachelorarbeit-Planung — Phase 1 der Pipeline

Du bist der Einstiegspunkt der Pipeline. Deine Aufgabe: **das inhaltliche Fundament der Arbeit legen**, auf dem später recherchiert, geschrieben und reviewt wird. Konkret:

1. **Thema** — Wenn noch nicht vorhanden, eines finden und eingrenzen
2. **Forschungsfrage** — Scharf, beantwortbar, strukturgebend formulieren
3. **Gliederung** — Mit Seitenzahlen, auf die Forschungsfrage zugeschnitten
4. **Ordnerstruktur** — Obsidian-Vault vorbereiten
5. **Zeitplanung** — Rückwärtsplanung vom Abgabedatum, Meilensteine setzen
6. **Handoff** — Sauber an den Recherche-Skill übergeben

**Wichtig — was NICHT zu diesem Skill gehört:** Die eigentliche Quellenrecherche und die Quellenauswertung sind **eigene Phasen** mit **eigenen Skills**. Der Planungs-Skill berührt keine Quellen jenseits der Frage "wo wird später ungefähr was an Literatur gebraucht". Wenn die Planung steht, übergibst du an `bachelorarbeit-recherche`.

## Die Pipeline im Überblick

```
Phase 0: Onboarding         → bachelorarbeit-onboarding
Phase 1: Planung            → bachelorarbeit-planung              ← DU BIST HIER
Phase 2: Recherche          → bachelorarbeit-recherche
Phase 3: Quellenauswertung  → bachelorarbeit-quellenauswertung
Phase 4: Schreiben          → bachelorarbeit-writer
Phase 5: Review             → bachelorarbeit-reviewer
Phase 6: Überarbeitung      → bachelorarbeit-ueberarbeitung
Phase 7: Finalisierung      → bachelorarbeit-finalisierung
```

## Ausgangslage klären

Frage den User zuerst, wo er steht:

| User hat... | Starte bei... |
|---|---|
| Gar nichts | Schritt 1: Themenfindung |
| Ein grobes Thema | Schritt 2: Forschungsfrage |
| Thema + Forschungsfrage | Schritt 3: Gliederung |
| Thema + Forschungsfrage + Gliederung | Schritt 4: Ordnerstruktur + Schritt 5: Zeitplanung → Handoff an Recherche-Skill |

Frage zusätzlich ab:
- **Studiengang / Fachbereich** — bestimmt Konventionen und Literatur-Ökosystem
- **Hochschule / Lehrstuhl** — für formale Vorgaben
- **Seitenumfang** — typisch Bachelorarbeit 30–50 Seiten
- **Abgabedatum** — für die Zeitplanung in Schritt 5

## Schritt 1: Themenfindung

Falls der User noch kein Thema hat, hilf ihm eines zu finden. Das passiert im Dialog.

**Vorgehen:**
1. Frage nach Interessen, Schwerpunkten im Studium, Praxiserfahrungen, Unternehmenskontakten
2. Schlage 3–5 Themenfelder vor, die wissenschaftlich bearbeitbar und aktuell sind
3. Für das gewählte Themenfeld: Grenze es gemeinsam auf eine bearbeitbare Größe ein

**Qualitätskriterien für ein gutes Thema:**
- Eingegrenzt genug, um in der vorgegebenen Seitenanzahl sinnvoll bearbeitbar zu sein
- Aktuell und relevant (für BWL: idealerweise mit Praxisbezug)
- Wissenschaftlich fundierbar (genug peer-reviewed Literatur erwartbar)
- Enthält eine implizite Spannung oder offene Frage — nicht nur deskriptiv

Wenn der User komplett blank ist, biete an, später in Phase 2 (Recherche) eine Trend-Recherche zu machen. Aber zwinge ihn nicht dazu — meist reicht ein Gespräch, um ein Themenfeld zu identifizieren.

## Schritt 2: Forschungsfrage entwickeln

Dies ist der **wichtigste Schritt der gesamten Planung** — die Forschungsfrage bestimmt alles Weitere.

**Vorgehen:**
1. Lies, was der User zum Thema hat (Notizen, Ideen, Betreuer-Hinweise)
2. Prüfe, ob im Arbeitsverzeichnis bereits eine Forschungsfrage oder ein Muster existiert (`04-quellen/Forschungsfrage.md`, `04-quellen/BA_Forschungsfrage.md`)
3. Entwickle mit dem User iterativ eine präzise Forschungsfrage

**Anforderungen an eine gute Forschungsfrage:**
- **Spezifisch** — Nicht "Wie funktioniert Risikomanagement?", sondern "Wie integrieren mittelständische deutsche Unternehmen Cyberrisiken in ihr bestehendes Risikomanagement-Framework?"
- **Beantwortbar** — Im gegebenen Umfang mit dem verfügbaren Zugang zu Daten/Literatur tatsächlich bearbeitbar
- **Nicht trivial** — Die Antwort darf nicht offensichtlich sein
- **Strukturgebend** — Aus der Frage soll sich die Gliederung fast von selbst ergeben

**Struktur:**
- Eine Hauptforschungsfrage (die zentrale Frage der Arbeit)
- 2–3 Unterforschungsfragen (optional, strukturieren die Hauptfrage)

**Speichern als `04-quellen/Forschungsfrage.md`** mit:
- Die Forschungsfrage(n)
- Kurze Herleitung (warum diese Frage relevant ist — wissenschaftlich + praktisch)
- Abgrenzung (was die Arbeit NICHT untersucht)
- Erwartete methodische Herangehensweise (qualitativ/quantitativ/konzeptionell)

## Schritt 3: Gliederung erstellen

Mit der Forschungsfrage steht das Ziel — jetzt der Weg dorthin.

**Vorgehen:**
1. Prüfe, ob Muster-Gliederungen vorliegen (`03-docs/BA-Gliederung-Muster.md`, `03-docs/BA-Struktur-Muster.md`). Falls ja, lies sie und nutze sie als Strukturvorlage.
2. Erstelle eine Gliederung, die auf die konkrete Forschungsfrage zugeschnitten ist
3. Weise jedem Kapitel Seitenzahlen zu (basierend auf dem Gesamtumfang)

**Standardstruktur einer BWL-Abschlussarbeit** (Fallback, falls keine Muster):

| Kapitel | Anteil | Seiten (bei 40 S.) |
|---|---|---|
| 1 Einleitung | 10–15% | 4–6 |
| 2 Theoretischer Rahmen | 25–35% | 10–14 |
| 3 Methodik | 10–20% | 4–8 |
| 4 Ergebnisse / Analyse | 15–25% | 6–10 |
| 5 Diskussion | 10–15% | 4–6 |
| 6 Fazit | 5–10% | 2–4 |

**Qualitätskriterien:**
- Jedes Kapitel hat einen klaren Zweck im Hinblick auf die Forschungsfrage
- Logischer Aufbau: Problem → Theorie → Methode → Ergebnisse → Einordnung
- Max. 3 Gliederungsebenen (1.1.1)
- Kein Kapitel mit nur einem Unterkapitel (wenn 3.1, dann auch 3.2)
- Seitenzahlen addieren sich zum Gesamtumfang

**Speichern als `03-docs/Gliederung.md`.**

## Schritt 4: Ordnerstruktur anlegen

Lege auf Basis der Gliederung die Obsidian-Ordnerstruktur an, damit die nächsten Skills sofort arbeiten können.

**Für jedes Hauptkapitel einen Unterordner in `05-text/`:**

```
05-text/
├── 01-Einleitung/
├── 02-Theoretischer Rahmen/
├── 03-Methodik/
├── 04-Ergebnisse/
├── 05-Diskussion/
└── 06-Fazit/
```

**Komplette Vault-Struktur** (falls noch nicht vorhanden, anlegen):

```
bachelor/                        ← Obsidian Vault Root
├── 01-claude/
│   └── CLAUDE.md                ← Pipeline-Orchestrierung
├── 02-skills/                   ← Alle .skill-Dateien
├── 03-docs/
│   └── Gliederung.md            ← Aus Schritt 3
├── 04-quellen/
│   ├── Forschungsfrage.md       ← Aus Schritt 2
│   ├── Quellenverzeichnis.md    ← Kommt in Phase 2 (Recherche)
│   └── Auswertung_KapX_*.md     ← Kommt in Phase 3 (Quellenauswertung)
├── 05-text/                     ← Aus Schritt 4
│   └── XX-Kapitelname/
├── 06-fortschritt/
│   └── Fortschritt.md           ← Aus Schritt 5
├── 07-review/                   ← Wird vom Reviewer befüllt
└── 08-final/                    ← Wird vom Finalisierer befüllt
```

## Schritt 5: Zeitplanung und Fortschritt.md

Erstelle eine Rückwärtsplanung basierend auf dem Abgabedatum und initialisiere die `06-fortschritt/Fortschritt.md`.

**Faustregel für die Zeitverteilung:**

| Phase | Anteil der Gesamtzeit |
|---|---|
| Planung (Phase 1) + Recherche (Phase 2) + Quellenauswertung (Phase 3) | 25–30% |
| Schreiben (Phase 4, alle Kapitel) | 40–45% |
| Review + Überarbeitung (Phasen 5–6) | 15–20% |
| Finalisierung (Phase 7) + Korrekturlesen + Plagiatcheck | 10–15% |
| Puffer (unvorhergesehenes) | 5–10% |

**Vorgehen Rückwärtsplanung:**
1. Vom Abgabedatum 1 Woche Puffer abziehen → Deadline für Finalisierung
2. Davon nochmal 1–2 Wochen → Deadline für letzte Review/Überarbeitungsrunde
3. Restliche Zeit auf die Kapitel verteilen (gewichtet nach Seitenumfang)
4. Empfohlene Schreibreihenfolge: Theorie → Methodik → Ergebnisse → Diskussion → Einleitung → Fazit

**`06-fortschritt/Fortschritt.md` initialisieren:**

```markdown
# Fortschritt Bachelorarbeit

**Thema:** [Thema]
**Forschungsfrage:** [[BA_Forschungsfrage]]
**Gliederung:** [[Gliederung]]
**Gesamtumfang:** ca. [X] Seiten
**Abgabe:** [Datum]
**Letzte Aktualisierung:** [Heute]

## Pipeline-Status

| Phase | Skill | Status | Datum |
|---|---|---|---|
| 0 Onboarding | bachelorarbeit-onboarding | ✅ Abgeschlossen | [Datum] |
| 1 Planung | bachelorarbeit-planung | ✅ Abgeschlossen | [Heute] |
| 2 Recherche | bachelorarbeit-recherche | ⬜ Ausstehend | — |
| 3 Quellenauswertung | bachelorarbeit-quellenauswertung | ⬜ Ausstehend | — |
| 4 Schreiben | bachelorarbeit-writer | ⬜ Ausstehend | — |
| 5 Review | bachelorarbeit-reviewer | ⬜ Ausstehend | — |
| 6 Überarbeitung | bachelorarbeit-ueberarbeitung | ⬜ Ausstehend | — |
| 7 Finalisierung | bachelorarbeit-finalisierung | ⬜ Ausstehend | — |

## Kapitelübersicht

| Kapitel | Datei | Review | Bewertung | Muss-Punkte | Quellen offen | Status |
|---|---|---|---|---|---|---|
| 1 Einleitung | — | — | — | — | — | Ausstehend |
| 2 [Titel] | — | — | — | — | — | Ausstehend |
| ... | — | — | — | — | — | Ausstehend |

## Status-Flow

Ausstehend → Erster Entwurf → Reviewed → Überarbeitet → Final

## Zeitplanung

| Meilenstein | Soll-Datum | Ist-Datum | Status |
|---|---|---|---|
| Planung abgeschlossen | [Datum] | [Heute] | ✅ |
| Quellenrecherche abgeschlossen | [Datum] | — | ⬜ |
| Quellenauswertung abgeschlossen | [Datum] | — | ⬜ |
| Kap. 2 Theorie geschrieben | [Datum] | — | ⬜ |
| Kap. 3 Methodik geschrieben | [Datum] | — | ⬜ |
| Kap. 4 Ergebnisse geschrieben | [Datum] | — | ⬜ |
| Kap. 5 Diskussion geschrieben | [Datum] | — | ⬜ |
| Kap. 1 Einleitung + Kap. 6 Fazit geschrieben | [Datum] | — | ⬜ |
| Alle Kapitel reviewed + überarbeitet | [Datum] | — | ⬜ |
| Finalisierung + Word-Datei | [Datum] | — | ⬜ |
| Korrekturlesen + Plagiatcheck | [Datum] | — | ⬜ |
| **Abgabe** | **[Datum]** | — | ⬜ |

## Offene Punkte
- Quellenrecherche steht als nächstes an (Phase 2)

## Nächste Schritte
- Phase 2 starten: `bachelorarbeit-recherche` — systematische Quellenrecherche, beginnend mit dem Theoriekapitel
```

## Schritt 6: Handoff an Phase 2 (Recherche)

Wenn alle Schritte abgeschlossen sind, prüfe die Bereitschaft und übergib sauber an den Recherche-Skill.

**Checkliste vor Handoff:**
- [ ] `04-quellen/Forschungsfrage.md` existiert und ist scharf formuliert
- [ ] `03-docs/Gliederung.md` existiert mit Seitenzahlen pro Kapitel
- [ ] `05-text/XX-Kapitelname/` Unterordner sind für alle Kapitel angelegt
- [ ] `06-fortschritt/Fortschritt.md` ist initialisiert mit Pipeline-Status und Zeitplanung
- [ ] Forschungsfrage und Gliederung sind inhaltlich konsistent

**Handoff-Nachricht an den User:**

> Die Planung (Phase 1) ist abgeschlossen. Du hast jetzt:
> - Eine scharfe Forschungsfrage ([[Forschungsfrage]])
> - Eine Gliederung mit Seitenzahlen ([[Gliederung]])
> - Eine initialisierte Fortschritts-Übersicht ([[Fortschritt]])
> - Eine angelegte Ordnerstruktur für alle Kapitel
> - Einen Zeitplan bis zur Abgabe
>
> **Nächster Schritt — Phase 2: Quellenrecherche.**
> Starte den `bachelorarbeit-recherche`-Skill. Er sammelt systematisch wissenschaftliche Quellen — kapitelweise, mit NotebookLM. Empfehlung: Beginne mit dem Theoriekapitel, da es die begriffliche Grundlage der Arbeit legt.

**Wichtig:** Versuche nicht, in diesem Skill selbst schon Quellen zu suchen oder auszuwerten. Das ist explizit Aufgabe der Phasen 2 und 3. Saubere Phasentrennung ist der ganze Sinn dieses Refactorings.

## Wenn Vorlagen existieren

Prüfe immer zuerst, ob im Arbeitsverzeichnis bereits Vorlagen liegen:

- `03-docs/BA-Gliederung-Muster.md` → Strukturvorlage für die Gliederung
- `03-docs/BA-Struktur-Muster.md` → Kapitelaufteilung und Seitenanteile
- `04-quellen/BA_Forschungsfrage.md` → Qualitätsbeispiel für Forschungsfragen

Nutze sie als Referenz für Format und Tiefe.

## Zusammenspiel mit anderen Skills

- **Vor Phase 1** → `bachelorarbeit-onboarding` prüft Voraussetzungen
- **Nach Phase 1** → `bachelorarbeit-recherche` übernimmt und sammelt Quellen
- **Quer zu Phase 1** → Zeitplanung wird in allen folgenden Phasen referenziert (Fortschritt.md ist die gemeinsame Quelle der Wahrheit)
