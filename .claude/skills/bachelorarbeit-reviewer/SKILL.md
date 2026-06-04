# bachelorarbeit-reviewer

**Trigger:** „Schau dir mein Kapitel an" / „Review" / „Feedback"

## Beschreibung
Bewertet Struktur, Argumentation, Quellenarbeit, Sprache, Formalia aus Professorensicht. Priorisiert Feedback in Muss/Sollte/Optional.

**Input:** Kapitel-Datei + Quellenauswertung + Forschungsfrage + Gliederung  
**Output:** `05-review/Review_Kapitel_[X]_[Kurztitel].md`, Status in Fortschritt.md = "Reviewed"

---

## Ablauf

1. Muss-Checks durchlaufen
   - Struktur: Logisch, nachvollziehbar?
   - Argumente: Alle gestützt (Claim → Evidence)?
   - Quellen: Vollständig, konsistent?
   - Sprache: Wissenschaftlich, dritte Person?
   - Harvard: Korrekt angewendet?

2. Sollte-Punkte identifizieren
   - Übergänge zwischen Absätzen
   - Begriffskonsistenz
   - Wortwahl (zu casual, zu umschreibend?)
   - Satzbau-Varianz

3. Optionale Verbesserungen
   - Stylistische Feinheiten
   - Zusätz-Kontext
   - Alternative Argumentationen

4. Review-Datei schreiben
   - Format: Sections pro Muss/Sollte/Optional
   - Konkrete Vorschläge (nicht nur Kritik)
   - Datei: `05-review/Review_Kapitel_[X]_[Kurztitel].md`

5. Status-Entscheidung treffen
   - **Muss-Punkte vorhanden?** → Status "Überarbeitung erforderlich"
   - **Keine Muss-Punkte?** → Status "Approved (Sollte optional)"
   - Fortschritt.md aktualisieren
