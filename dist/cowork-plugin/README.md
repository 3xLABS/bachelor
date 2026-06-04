# Bachelorarbeit-Pipeline (Cowork-Plugin)

Acht spezialisierte Skills, die zusammen eine komplette Bachelorarbeit im Fachbereich BWL begleiten — von der Themenfindung bis zur abgabefertigen Word-Datei.

## Phasen

| Phase | Skill | Output |
|---|---|---|
| 0 | `bachelorarbeit-onboarding` | System-Check, ggf. Reparatur fehlender Teile |
| 1 | `bachelorarbeit-planung` | Forschungsfrage, Gliederung, Ordnerstruktur, Zeitplan |
| 2 | `bachelorarbeit-recherche` | Recherche-Protokoll pro Kapitel, NotebookLM-Notebook |
| 3 | `bachelorarbeit-quellenauswertung` | Auswertung pro Kapitel im Writer-Format |
| 4 | `bachelorarbeit-writer` | Fließtext pro Kapitel (Harvard, Wiki-Links) |
| 5 | `bachelorarbeit-reviewer` | Review pro Kapitel aus Professorensicht |
| 6 | `bachelorarbeit-ueberarbeitung` | Versionierte Überarbeitung (_v2, _v3) |
| 7 | `bachelorarbeit-finalisierung` | `bachelorarbeit_final.docx` + Literaturverzeichnis |

Zusätzlich enthalten:

- `bachelorarbeit-pipeline` — Orchestrator-Skill, der die Phasen erklärt, Konventionen festhält und Status-Fragen beantwortet
- `humanizer` — Hilfsskill zum Entfernen KI-typischer Schreibmuster

## Installation

In Cowork: Klick auf die `bachelorarbeit-pipeline.plugin`-Datei → "Save plugin" → Plugin wird in deine Cowork-Plugins eingespielt.

## Externe Tools

Die Pipeline ist Multi-Tool:

- **NotebookLM** (notebooklm.google.com) — Quellenspeicher
- **Gemini / Google AI Studio** — Quellenauswertung (Phase 3 läuft dort, um Token zu sparen)
- **Perplexity** — Quellenrecherche (Phase 2)
- **Obsidian** (optional) — Vault-Ansicht des Ordners

Claude liefert für jeden externen Schritt fertige Copy-Paste-Prompts.

## Start

Sage Claude einfach:

> "Ich will eine Bachelorarbeit schreiben."

oder

> "/start"

Claude startet das Onboarding und führt dich von dort.

## Quelle & Lizenz

[github.com/e3xler/bachelor](https://github.com/e3xler/bachelor) — MIT-Lizenz, frei nutzbar.
