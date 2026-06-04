# bachelorarbeit-onboarding

**Trigger:** „Alles bereit?" / „Setup" / „kann es losgehen?"

## Beschreibung
Prüft Voraussetzungen: Ordnerstruktur, Google-Account (NotebookLM/Gemini), Sub-Skills, Internet. Erstellt System-Check-Report und repariert fehlende Teile automatisch.

**Input:** Nichts  
**Output:** System-Check-Report, initialisierte `04-fortschritt/Fortschritt.md`

---

## Ablauf

1. Ordnerstruktur prüfen
   - `/01-docs`, `/02-quellen`, `/03-text`, `/04-fortschritt`, `/05-review`, `/06-final` müssen existieren
   - Ggf. anlegen

2. Google-Account prüfen
   - NotebookLM und Google AI Studio erreichbar?
   - Gemini API-Zugang?

3. Sub-Skills vorhanden?
   - Alle 7 anderen Skill-Ordner existieren?

4. System-Report erstellen
   - ✅ Bestandene Checks
   - ❌ Fehlende Items (mit Lösungsvorschlag)

5. `04-fortschritt/Fortschritt.md` initialisieren (falls nicht vorhanden)
   - Struktur: Leere Kapitel-Tabelle, Zeitplan-Template, Phase-Marker

6. Benutzer informieren
   - „Setup abgeschlossen" oder „Folgende Items manuell beheben…"
