# Reflexions-Radar · E-Portfolio

**Selbstbeurteilungstool für die Reflexionstiefe im E-Portfolio**  
Studiengang Primarstufe · Pädagogische Hochschule Thurgau (PHTG)

---

## Was ist dieses Tool?

Das Reflexions-Radar ist ein browserbasiertes Self-Assessment-Tool für Studierende im Studiengang Primarstufe. Es unterstützt die systematische Einschätzung der eigenen Reflexionstiefe in den 10 Standardfeldern der Primarschulausbildung – direkt auf Basis der E-Portfolio-Einträge.

Das Tool visualisiert die Selbsteinschätzung als interaktiven Spider-Chart oder als Kuchenstücke-Diagramm und orientiert sich im Export am Layout des offiziellen PHTG-Dokuments (vgl. PHTG, 2024, S. 40), sodass das Ergebnis nahtlos in das E-Portfolio integriert werden kann.

---

## Features

### Neue Einschätzung (5-Schritte-Flow)

1. **Einführung** – Erklärung der 5 Reflexionsstufen mit konkreten Anwendungsbeispielen
2. **Standardfelder wählen** – Auswahl, zu welchen SF der Fragenkatalog ausgefüllt wird (der Chart zeigt immer alle 10 SF)
3. **Fragenkatalog** – Je 5 Aussagen pro gewähltem Standardfeld; Bewertung auf einer Skala von 0–4 (Schritte: 0.5)
4. **Anpassung** – Alle 10 Standardfelder als Schieberegler; berechnete Mittelwerte können manuell überschrieben werden
5. **Visualisierung** – Interaktiver Chart mit zwei Ansichten:
   - **Spider-Chart:** Datenpunkte per Drag-and-Drop anpassen
   - **Kuchenstücke:** 10 Sektoren mit sichtbaren Ring-Abstufungen (Stufe 1–4)
   - Farbauswahl aus der PHTG-Farbpalette (7 Farben + Weiss + Schwarz)
   - Frühere Einschätzung als Vergleichsebene laden (JSON-Import)
   - Einschätzung speichern (JSON-Export)
   - Download als PNG

### Veränderungen darstellen (Vergleichsmodus)

Ein separater, unabhängiger Modus zum Vergleich zweier Einschätzungszeitpunkte:

- **Ausgangslage** – Werte des ersten Messzeitpunkts; manuell eingeben oder aus JSON laden
- **Neue Einschätzung** – Aktuelle Werte (vorausgefüllt mit Ausgangslage); als JSON speicherbar
- **Vergleichs-Chart** – Zweilagen-Spider:
  - Grau = Ausgangslage
  - Farbe = ausschliesslich die Bereiche, die neu dazugekommen sind
  - Die farbige Outline zeigt den vollständigen aktuellen Umriss
- **Zusammenfassung** – Tabellarische Übersicht: Verbesserungen, Rückgänge, unverändert (mit Deltawert)
- Vergleich als JSON oder PNG exportieren

---

## Die 5 Reflexionsstufen

| Stufe | Bezeichnung | Beschreibung |
|-------|-------------|--------------|
| 0 | Keine Ausprägung | Noch keine Dokumentation oder Evidenz im Portfolio vorhanden |
| 1 | Beschreiben | Beschreibung, *was* getan wurde – reine Dokumentation |
| 2 | Beschreibende Reflexion | Beschreibung, *wie* es sich angefühlt hat; erste persönliche Schlüsse |
| 3 | Dialogische Reflexion | Erfahrung wird mit externen Perspektiven (Feedback, Theorie) verbunden |
| 4 | Kritischer Diskurs | Theoriegeleitete Analyse; fundierte Haltungen oder Handlungsabsichten |

---

## Die 10 Standardfelder

| Nr. | Bezeichnung |
|-----|-------------|
| SF 1 | Fachwissen und -können |
| SF 2 | Lernen und Entwickeln |
| SF 3 | Umgang mit Heterogenität |
| SF 4 | Eigenständiges Lernen, kritisches Denken, Problemlösen |
| SF 5 | Soziales Umfeld |
| SF 6 | Kommunikation |
| SF 7 | Planung, Durchführung und Auswertung von Unterricht |
| SF 8 | Beurteilung |
| SF 9 | Sicherung der Qualität und professionelle Weiterentwicklung |
| SF 10 | Schule im Spannungsfeld von Kultur, Gesellschaft, Demokratie, Ökonomie und Ökologie |

---

## Technisches

Das Tool ist eine **einzelne HTML-Datei** (`index.html`) ohne Build-Prozess, ohne Backend und ohne Abhängigkeiten ausser einer externen CDN-Referenz.

### Abhängigkeiten

| Bibliothek | Version | Einbindung |
|-----------|---------|------------|
| [Chart.js](https://www.chartjs.org/) | 4.4.0 | CDN (jsDelivr) |

### Architektur

- **Vanilla JavaScript** (kein Framework)
- **Custom Chart.js Plugins:**
  - `sfLabelPlugin` – Zeichnet die Achsenbeschriftungen direkt auf den Canvas mit gemischter Schriftstärke (fett: «Standardfeld X», regular: Bezeichnung) – im PHTG-Layoutstil
  - `deltaFillPlugin` – Berechnet per Offscreen-Canvas und `destination-out`-Compositing die Differenzfläche zwischen Ausgangslage und neuer Einschätzung; nur der echte Zuwachs wird eingefärbt
- **Kuchenstücke-Ansicht:** Eigene Canvas-Implementierung mit 10 Sektoren und sichtbaren Ring-Abstufungen pro Stufe
- **Import/Export:** JSON-basiert für alle Einschätzungen und Vergleiche
- **Schieberegler:** Schrittgrösse 0.5 (Werte: 0, 0.5, 1, 1.5, 2, 2.5, 3, 3.5, 4)
- **Drag-Interaktion** auf dem Spider-Chart (Achsenwinkel-basiert, snapped auf 0.5)
- **PNG-Export** via `canvas.toDataURL()`

### Lokale Nutzung

```bash
open index.html
```

---

## Deployment mit Vercel oder GitHub Pages

### GitHub Pages (empfohlen)

1. `index.html` in ein GitHub-Repository pushen
2. Repository → Settings → Pages
3. Source: «Deploy from a branch» → `main` → `/ (root)`
4. Die Seite ist unter `https://<username>.github.io/<repo>/` erreichbar

### Vercel

1. Repository auf GitHub erstellen und `index.html` pushen
2. Auf [vercel.com](https://vercel.com) einloggen → «Add New Project» → Repo auswählen
3. Framework Preset: **Other** → Deploy

---

## Repository-Struktur

```
reflexions-radar/
├── index.html        # Das vollständige Tool (eine Datei)
├── README.md         # Diese Datei
└── .gitignore
```

---

## Entstehung und Kontext

Dieses Tool wurde im Rahmen der Arbeit in der **Fachstelle Schule und Digitalität** an der Pädagogischen Hochschule Thurgau entwickelt.

**Erstellt im:** Frühlingssemester 2026; letzter Stand Oktober 2026  
**Entwickelt mit:** Claude (Anthropic)  
**Autorin:** Sabrina Meier, PHTG  
**Fachlicher Hintergrund:** Die Standardfelder und Reflexionsstufen orientieren sich an der PHTG-Publikation zur Selbsteinschätzung im E-Portfolio (Pädagogische Hochschule Thurgau, 2024).

---

## Lizenz

Dieses Projekt steht unter der [MIT License](LICENSE).  
Das Tool darf frei verwendet, angepasst und weitergegeben werden.

---

*Fachstelle Schule und Digitalität · Pädagogische Hochschule Thurgau · [phtg.ch](https://www.phtg.ch)*
