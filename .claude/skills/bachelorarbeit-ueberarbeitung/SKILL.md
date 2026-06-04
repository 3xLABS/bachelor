# bachelorarbeit-ueberarbeitung

**Trigger:** „Arbeite das Feedback ein" / „Überarbeite" / „Mein Betreuer hat gesagt…"

## Beschreibung
Arbeitet Review-Feedback (oder Betreuer-Feedback) systematisch ein. Bewahrt Textidentität, stärkt Argumente, ergänzt Quellen, harmonisiert. Erstellt versionierte Datei mit Änderungsprotokoll.

**Input:** Kapitel-Datei + Review-Datei (oder Betreuer-Feedback)  
**Output:** `03-text/XX-Kapitel/Kapitel_[X]_[Kurztitel]_v2.md`, Status = "Überarbeitet"

---

## Ablauf

1. Feedback laden
   - Review-Datei oder Betreuer-Feedback (Mail, PDF, etc.)
   - Muss-Punkte extrahieren

2. Pro Muss-Punkt: Änderung umsetzen
   - Argument stärken: Zusatz-Evidenz + Wiki-Link
   - Quelle ergänzen: `[[Auswertung_...|...]]` hinzufügen
   - Satz/Absatz umschreiben (Verständlichkeit)
   - Logik reparieren (Übergänge, Struktur)

3. Text harmonisieren
   - Begriffe konsistent?
   - Tonalität durchgehend wissenschaftlich?
   - Satzbau-Variation ausreichend?

4. Sollte-Punkte optional einarbeiten
   - Styling-Verbesserungen
   - Wortwahl-Refinement

5. Änderungsprotokoll anlegen
   - Kopfzeile: „## Änderungen in v2"
   - Stichpunkte: Was, Warum, Zeile
   - Optional: Diff (alt → neu)

6. Datei speichern + Status
   - Pfad: `03-text/XX-Kapitel/Kapitel_[X]_[Kurztitel]_v2.md`
   - Fortschritt.md: Status = "Überarbeitet", Re-Review einplanen
