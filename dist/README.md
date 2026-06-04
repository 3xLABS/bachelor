# Distribution-Artefakte

Vorgefertigte Cowork-Pakete für die Bachelorarbeit-Pipeline. Beide enthalten dieselbe Pipeline-Logik — du wählst nach Geschmack.

## Was hier liegt

| Datei / Ordner | Was es ist | Wann nutzen |
|---|---|---|
| `bachelorarbeit-pipeline.plugin` | Cowork-Plugin (ZIP) mit allen 9 Skills + `/start`-Command | Empfohlen für Cowork. Installation per Klick auf die Datei → "Save plugin". |
| `bachelorarbeit.skill` | Einzelner Master-Skill (ZIP) mit allen Phasen als `references/` | Wenn du nur eine einzige `.skill` installieren willst statt eines Plugins. |
| `cowork-plugin/` | Quellordner des Plugins (nicht-gezippt) | Inspektion, eigene Anpassungen, alternative Packaging-Workflows. |
| `master-skill/` | Quellordner des Master-Skills (nicht-gezippt) | Inspektion und Anpassung der Master-Variante. |

## Installation

### Variante A: Marketplace (empfohlen, ein Befehl)

Das Repo ist ein Claude-Plugin-Marketplace — kein Datei-Download nötig, nichts kann beim Download kaputtgehen. In Claude Code oder im Cowork-Chat:

```
/plugin marketplace add e3xler/bachelor
/plugin install bachelorarbeit-pipeline@bachelor
```

Updates später: `/plugin marketplace update bachelor`.

### Variante B: Plugin-Datei (Drag-&-Drop-Fallback)

1. Lade `bachelorarbeit-pipeline.plugin` herunter (Endung muss `.plugin` bleiben — nicht entpacken lassen; ggf. zurück in `.plugin` umbenennen).
2. Doppelklick auf die Datei oder ziehe sie in den Cowork-Chat.
3. Im Plugin-Preview "Save plugin" klicken.
4. Cowork lädt alle Skills (`bachelorarbeit-pipeline`, `-onboarding`, `-planung`, `-recherche`, `-quellenauswertung`, `-writer`, `-reviewer`, `-ueberarbeitung`, `-finalisierung`, `humanizer`) und den `/start`-Command.

### Variante C: Einzelner Skill

1. Lade `bachelorarbeit.skill` herunter.
2. Doppelklick oder Drag-&-Drop in Cowork.
3. "Save skill" klicken.
4. Cowork lädt einen einzigen Skill `bachelorarbeit`, der per `references/` zwischen den Phasen routet.

## Unterschied zwischen Plugin und Master-Skill

- **Plugin (9 Skills + Command):** Jede Phase hat einen eigenen, fokussierten Skill mit eigenen Trigger-Phrasen. Cowork wählt automatisch den passenden Skill je nach Anfrage. Genauere Triggerung, modularer.
- **Master-Skill (1 Skill mit references):** Ein einziger Skill, der alle Phasen als Referenzdateien enthält und sie selbst routet. Schlankere Plugin-Liste, ein bisschen mehr Kontextverbrauch beim Routing.

Beide Varianten produzieren am Ende dasselbe Ergebnis: eine abgabefertige `bachelorarbeit_final.docx`.

## Pakete selbst neu bauen

Beide Pakete sind reproduzierbar:

```bash
# Plugin
cd dist/cowork-plugin
zip -r ../bachelorarbeit-pipeline.plugin . -x "*.DS_Store" "*/.DS_Store"

# Master-Skill
cd dist/master-skill/bachelorarbeit
zip -r ../../bachelorarbeit.skill . -x "*.DS_Store" "*/.DS_Store"
```
