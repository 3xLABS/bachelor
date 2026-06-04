# bachelorarbeit-quellenauswertung

**Trigger:** „Quellen auswerten" / „Was sagen die Papers?" / „Kernaussagen extrahieren"

## Beschreibung
Auswertung läuft in **Gemini** (nicht Claude, spart Token). Claude liefert Anleitung (Google AI Studio-Setup, Prompts) und Nachbearbeitung. **User führt Prompts selbstständig im Browser aus.** Produziert **keinen Fließtext** (Phase 4).

**Input:** Recherche-Protokoll + NotebookLM-Notebook  
**Output:** `02-quellen/Auswertung_Kapitel_[X]_*.md` (Writer-Format)

---

## Ablauf

1. Gemini-Setup erklären
   - Google AI Studio öffnen: `aistudio.google.com`
   - Neues Chat-Fenster pro Kapitel
   - Context: NotebookLM-Notebook laden (Copy-Paste)

2. Kapitelspezifische Prompts generieren
   - Pro Kapitel: 1–2 Prompts
   - Struktur: „Extrahiere Kernaussagen zu [Thema]"
   - Format: Mindmap, Bullet-Points, Tabelle

3. User führt Prompts aus
   - Copy-Paste-Prompt in Gemini
   - Gemini antwortet
   - Claude wartet auf Output

4. Claude verarbeitet Output
   - Standardisierung ins Writer-Format
   - Struktur: Autor, Thema, Kernaussagen, Zitat-Auszüge
   - Wiki-Link-Platzhalter einfügen
   - Datei: `02-quellen/Auswertung_Kapitel_[X]_*.md`

5. Fortschritt.md aktualisieren
   - Status: Auswertung abgeschlossen für Kapitel X
