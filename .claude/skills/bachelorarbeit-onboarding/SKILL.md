---
name: bachelorarbeit-onboarding
description: |
  Prüft ob alle Voraussetzungen für die Bachelorarbeit-Pipeline erfüllt sind: richtiger Ordner ausgewählt, Ordnerstruktur vorhanden, Internetzugang, Humanizer verfügbar, Sub-Skills vorhanden. Nutze diesen Skill beim allerersten Start, bei "Setup", "Onboarding", "Einrichten", "alles bereit?", "kann es losgehen?", "Voraussetzungen prüfen", "Check", "Environment prüfen" oder wenn der User zum ersten Mal die Bachelorarbeit-Pipeline nutzt. Auch bei Fehlern in anderen Skills diesen Skill zur Diagnose verwenden.
---

# Bachelorarbeit — Onboarding & System-Check

Bevor die Bachelorarbeit-Pipeline starten kann, müssen mehrere Voraussetzungen erfüllt sein. Dieser Skill prüft sie alle systematisch und hilft dem User, fehlende Teile einzurichten.

## Ablauf

Führe alle Checks der Reihe nach durch. Zeige dem User nach jedem Check das Ergebnis an (bestanden / nicht bestanden / Warnung). Am Ende eine Zusammenfassung mit allen Ergebnissen.

Nutze dieses Format für die Ausgabe:

```
BACHELORARBEIT — System-Check
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[✅ / ❌ / ⚠️] Check-Name — Ergebnis
```

---

## Check 1: Richtiger Ordner ausgewählt

**Was prüfen:**
Der User muss den `bachelor`-Ordner (oder einen Ordner, der die BA-Projektstruktur enthält) als Workspace ausgewählt haben.

**Wie prüfen:**
1. Prüfe ob der aktuelle Workspace-Mount existiert und beschreibbar ist
2. Suche nach diesen Indikatoren für den richtigen Ordner:
   - Datei `README.md` oder `Forschungsfrage.md` im Root
   - Ordner `.claude/skills/` mit Bachelor-Skills
   - Ordner `02-quellen/` oder `03-text/`
   - Datei `Gliederung.md` oder `Prompts.md`

**Ergebnis:**
- ✅ wenn mindestens 2 der Indikatoren gefunden werden
- ⚠️ wenn der Ordner existiert aber leer ist oder keine BA-Struktur hat → biete an, die Struktur zu erstellen
- ❌ wenn kein Ordner gemountet ist → weise den User an, den bachelor-Ordner auszuwählen

**Falls die Ordnerstruktur fehlt, erstelle sie:**
```
bachelor/
├── .claude/
│   └── skills/
├── 01-docs/
├── 02-quellen/
├── 03-text/
├── 04-fortschritt/
├── 05-review/
├── 06-final/
└── Fortschritt.md
```

---

## Check 2: Internetzugang

**Was prüfen:**
Claude braucht Internetzugang für Web-Recherche und Quellensuche.

**Wie prüfen:**
```bash
curl -s --max-time 10 -o /dev/null -w "%{http_code}" https://www.google.com
```

**Ergebnis:**
- ✅ wenn HTTP 200 oder 301/302 zurückkommt
- ❌ wenn Timeout oder Fehler → weise den User darauf hin, dass Netzwerkzugang in den Claude-Einstellungen aktiviert sein muss

---

## Check 3: Google-Account für NotebookLM & Gemini

**Was prüfen:**
Der User braucht einen Google-Account, um NotebookLM und Google AI Studio (Gemini) nutzen zu können. Diese Tools werden in Phase 2 (Recherche) und Phase 3 (Quellenauswertung) vom User **manuell im Browser** bedient — Claude gibt Anleitungen und Prompts, aber die Navigation und Bedienung liegt beim User.

**Wie prüfen:**
Frage den User: "Hast du einen Google-Account, mit dem du auf NotebookLM (notebooklm.google.com) und Google AI Studio (aistudio.google.com) zugreifen kannst?"

**Ergebnis:**
- ✅ wenn der User bestätigt
- ⚠️ wenn der User unsicher ist → weise ihn an, sich unter notebooklm.google.com einzuloggen und zu prüfen, ob er Zugang hat
- ❌ wenn der User keinen Google-Account hat → er muss einen erstellen

---

## Check 4: Humanizer verfügbar

**Was prüfen:**
Der Humanizer-Skill muss als Referenz im Plugin vorhanden sein.

**Wie prüfen:**
Suche nach `references/humanizer.md` im Orchestrator-Skill-Ordner oder nach einer separaten Humanizer-Installation:
```bash
# Im Plugin
find . -name "humanizer.md" -path "*/references/*" 2>/dev/null

# Global installiert
ls ~/.claude/skills/humanizer/SKILL.md 2>/dev/null
```

**Ergebnis:**
- ✅ wenn die Humanizer-Referenz gefunden wird
- ⚠️ wenn nicht gefunden → biete an, den Humanizer von GitHub zu installieren:
  ```bash
  git clone https://github.com/blader/humanizer.git /tmp/humanizer
  ```

---

## Check 5: Sub-Skills vorhanden

**Was prüfen:**
Alle Kern-Skills der Pipeline müssen verfügbar sein.

**Wie prüfen:**
Suche nach diesen Dateien im `.claude/skills/`-Ordner:

| Skill | Datei |
|-------|-------|
| Planung | `bachelorarbeit-planung/SKILL.md` |
| Recherche | `bachelorarbeit-recherche/SKILL.md` |
| Quellenauswertung | `bachelorarbeit-quellenauswertung/SKILL.md` |
| Writer | `bachelorarbeit-writer/SKILL.md` |
| Reviewer | `bachelorarbeit-reviewer/SKILL.md` |
| Überarbeitung | `bachelorarbeit-ueberarbeitung/SKILL.md` |
| Finalisierung | `bachelorarbeit-finalisierung/SKILL.md` |

**Ergebnis:**
- ✅ wenn alle sieben gefunden werden
- ⚠️ wenn einige fehlen → liste die fehlenden auf und prüfe ob sie als .skill-Dateien vorhanden sind (können entpackt werden)
- ❌ wenn keiner gefunden wird → der User muss die Skills zuerst installieren

---

## Check 6: Python-Umgebung

**Was prüfen:**
Python 3 muss verfügbar sein (wird für diverse Skripte in der Finalisierungsphase benötigt).

**Wie prüfen:**
```bash
python3 --version 2>/dev/null || python --version 2>/dev/null
```

**Ergebnis:**
- ✅ wenn Python 3.8+ verfügbar ist
- ❌ wenn nicht vorhanden oder zu alte Version

---

## Check 7: Bestehender Fortschritt

**Was prüfen:**
Ob der User bereits Fortschritt gemacht hat (um die richtige Phase zu empfehlen).

**Wie prüfen:**
1. Existiert `Forschungsfrage.md` oder `BA_Forschungsfrage.md`? → Phase 1 (Planung) begonnen
2. Existiert `Gliederung.md`? → Phase 1 (Planung) weiter fortgeschritten
3. Existieren `Recherche_Kapitel_*.md` in `02-quellen/`? → Phase 2 (Recherche) begonnen
4. Existieren `Auswertung_Kapitel_*.md` in `02-quellen/`? → Phase 3 (Auswertung) begonnen
5. Dateien in `03-text/`? → Phase 4 (Schreiben) begonnen
6. Dateien in `05-review/`? → Phase 5 (Review) begonnen
7. Dateien in `06-final/`? → Phase 7 (Finalisierung) begonnen

**Ergebnis:**
- Zeige eine Übersicht des aktuellen Stands
- Empfehle die nächste Phase basierend auf dem Fortschritt
- Falls kein Fortschritt: "Bereit für Phase 1 — Planung"

---

## Zusammenfassung anzeigen

Am Ende zeige eine kompakte Übersicht:

```
BACHELORARBEIT — System-Check Ergebnis
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✅ Ordner          bachelor/ korrekt ausgewählt
✅ Internet         Verbindung aktiv
✅ Google-Account   User hat Zugang zu NotebookLM & AI Studio
✅ Humanizer        Referenz vorhanden
✅ Sub-Skills       7/7 gefunden
✅ Python           3.11.2
⚠️ Fortschritt      Kein bisheriger Fortschritt

Ergebnis: 6/7 Checks bestanden, 1 Hinweis
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
→ Alles bereit! Starte mit Phase 1: Planung
```

Falls kritische Checks (❌) fehlschlagen:
```
→ Bitte behebe die markierten Probleme, bevor du startest.
   Danach kannst du den Check erneut ausführen.
```

## Automatische Reparatur

Biete dem User an, behebbare Probleme automatisch zu lösen:
- Ordnerstruktur erstellen → Ordner anlegen
- Humanizer installieren → von GitHub klonen
- `Fortschritt.md` erstellen → Initiale Datei anlegen

Frage vor jeder automatischen Aktion um Erlaubnis.
