---
description: Bachelorarbeit-Pipeline starten — System-Check und Phaseneinstieg
---

# Bachelorarbeit-Pipeline starten

Der User möchte mit der Bachelorarbeit-Pipeline beginnen. Gehe so vor:

1. Rufe den `bachelorarbeit-onboarding`-Skill auf. Er prüft Voraussetzungen (Ordnerstruktur, Sub-Skills, Internetzugang).
2. Wenn das Onboarding sauber durchläuft und noch keine `02-quellen/Forschungsfrage.md` existiert, rufe direkt den `bachelorarbeit-planung`-Skill auf.
3. Wenn bereits eine Forschungsfrage existiert, lies `04-fortschritt/Fortschritt.md` und erkläre dem User, in welcher Phase er ist und welcher Skill als Nächstes dran wäre.

Alle weiteren Skill-Aufrufe folgen der Pipeline-Reihenfolge:
`bachelorarbeit-onboarding → -planung → -recherche → -quellenauswertung → -writer → -reviewer → -ueberarbeitung → -finalisierung`.

Wenn der User direkt eine bestimmte Phase ansprechen will (z. B. "Kapitel 3 schreiben"), springe in den entsprechenden Phasen-Skill.
