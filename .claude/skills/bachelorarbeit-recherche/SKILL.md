# bachelorarbeit-recherche

**Trigger:** „Quellen suchen" / „Literatur finden" / „Deep Research"

## Beschreibung
Systematische Quellensuche pro Kapitel. Claude entwickelt Recherchestrategie und Suchbegriffe. **User führt selbstständig Deep Research in NotebookLM durch.** Claude dokumentiert im Recherche-Protokoll. Wertet **nichts aus** (Phase 3).

**Input:** Forschungsfrage, Gliederung  
**Output:** NotebookLM-Notebook (User-verwaltet), `02-quellen/Recherche_Kapitel_[X]_*.md` pro Kapitel

---

## Ablauf

1. Recherchestrategie entwickeln
   - Pro Kapitel: 3–5 Suchbegriffe
   - Kombinationen: AND, OR, NOT
   - Priorität: Aktualität, Relevanz, Zugang

2. User zu NotebookLM führen
   - „Öffne NotebookLM im Browser"
   - Claude teilt Suchbegriffe mit

3. User führt Recherche durch
   - Deep Research (Claude analysiert Top-10-Ergebnisse)
   - Schnelle Suche (Keywords direkt)
   - Manuelle Quelle hinzufügen (bekannte Paper)
   - Quellen-Indexierung im Notebook

4. Claude dokumentiert
   - Suchbegriffe pro Kapitel
   - Anzahl gefundener Quellen
   - Lücken/offene Fragen
   - Datei: `02-quellen/Recherche_Kapitel_[X]_*.md`

5. Fortschritt.md aktualisieren
   - Status: Recherche abgeschlossen für Kapitel X
