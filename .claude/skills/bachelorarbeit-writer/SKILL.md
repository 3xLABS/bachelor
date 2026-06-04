# bachelorarbeit-writer

**Trigger:** „Schreib mir Kapitel 3" / „Theorieteil schreiben" / „Schreib Kapitel X"

## Beschreibung
Schreibt ein Kapitel im wissenschaftlichen Stil mit Harvard-Zitierung und Obsidian-Wiki-Links. Beachtet Kapiteltyp und Nachbarkapitel. **Gate:** Quellenauswertung muss vorliegen.

**Input:** Forschungsfrage, Gliederung, Quellenauswertung, ggf. Nachbarkapitel  
**Output:** `03-text/XX-Kapitel/Kapitel_[X]_[Kurztitel].md` (Status: Erster Entwurf)

---

## Ablauf

1. Kapiteltyp prüfen
   - Einleitung: Problem, Forschungsfrage, Struktur
   - Theorie: Linear, deduktiv, Konzepte aufbauen
   - Ergebnisse: Faktenorientiert, strukturiert
   - Diskussion: Theorie ↔ Ergebnisse, kritisch
   - Fazit: Forschungsfrage beantworten

2. Quellenauswertung laden
   - Aus `02-quellen/Auswertung_Kapitel_[X]_*.md`
   - Strukturen + Zitate extrahieren

3. Text schreiben
   - Absatzweise Argumentation (Claim → Reason → Evidence)
   - Harvard-Stil: `(Autor, Jahr)` oder `(Autor, Jahr: S. XY)`
   - Wiki-Links: `[[Auswertung_Kapitel X#Autor, Jahr|Autor, Jahr]]`
   - Fehler markieren: `[QUELLE ERGÄNZEN]`, `[SEITE PRÜFEN]`

4. Abbildungen
   - Platzhalter: `[ABBILDUNG X.Y: Beschreibung]`
   - Nummerierung nach Kapitel

5. Quellenliste ergänzen
   - `## Verwendete Quellen in diesem Kapitel`-Tabelle am Ende
   - Format: Autor, Jahr, Zitierweise

6. Datei speichern + Status
   - Pfad: `03-text/XX-Kapitel/Kapitel_[X]_[Kurztitel].md`
   - Fortschritt.md: Status = "Erster Entwurf"
