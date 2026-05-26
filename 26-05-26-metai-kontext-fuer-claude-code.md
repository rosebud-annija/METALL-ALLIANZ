# METAi Chatbot – Projektkontext für Claude Code

**Datum:** 26.05.2026  
**Dateien:** `26-05-26-metai-chatbot.html` · `index.html`  
**Status:** Redesign abgeschlossen · Deployed auf GitHub Pages ✅

---

## Was ist METAi?

METAi ist ein interaktiver Chatbot – die „Stimme der Metall Allianz" (Initiative Zukunft Metall, Österreich). Er beantwortet Fragen rund um Metall, Klimaschutz, Kreislaufwirtschaft und die Metallbranche auf Deutsch.

- **Name:** METAi
- **Slogan / Markensprache:** „Das hält." → kurze, aktive Sätze, direkt, faktenbasiert aber emotional
- **Sprache:** Deutsch (österreichischer Kontext)
- **Technologie:** Reines HTML/CSS/JS (kein externes API, kein Framework)
- **Wissensquelle:** Rule-based Keyword-Matching gegen eine eingebettete Wissensbasis

---

## GitHub Repository

- **Repo:** [https://github.com/rosebud-annija/METALL-ALLIANZ](https://github.com/rosebud-annija/METALL-ALLIANZ) (privat)
- **Live-URL:** [https://rosebud-annija.github.io/METALL-ALLIANZ/](https://rosebud-annija.github.io/METALL-ALLIANZ/)
- **Branch:** `main`
- **Git remote:** `origin` → HTTPS (`https://github.com/rosebud-annija/METALL-ALLIANZ.git`)
- **Git user:** `rosebud-annija` · `ac@rosebud.cc` (lokal konfiguriert)
- **Credential helper:** macOS `osxkeychain` (kein SSH)

### Update deployen

```bash
# Im Repo-Verzeichnis:
git add 26-05-26-metai-chatbot.html index.html
git commit -m "Update: ..."
git push
# GitHub Pages baut automatisch (~60 Sekunden)
```

> **Wichtig:** `index.html` ist eine Kopie von `26-05-26-metai-chatbot.html` — beide müssen bei Änderungen synchron gehalten werden. GitHub Pages braucht `index.html` im Root.

---

## Markenstimme & Tonalität

Abgeleitet aus dem Slogan **„Das hält."** und dem Rosebud-Agenturkonzept „ELEMETALL":

- Kurze Sätze. Keine langen Erklärungen.
- Aktiv, nicht passiv.
- Fakten emotional aufgeladen – aber kein Pathos.
- Satzanfänge wie: „Hält Österreich in Bewegung.", „Hält Wort in Sachen Klima.", „Hält Schritt mit der Zukunft."
- Jede Bot-Antwort endet mit dem Markenabschluss: **Das hält.**
- Adjektive aus dem Brand-Universum: *handfest, formbar, verlässlich, präzise*

---

## Design-System (aktuell: Light Theme)

Redesign im Mai 2026: Wechsel vom dunklen Industrielook zu einem cleanen, modernen Weißdesign passend zur Website der Metall Allianz.

### CSS Custom Properties

```css
:root {
  --bg:          #ffffff;
  --surface:     #ffffff;
  --surface2:    #f4f5f4;
  --surface3:    #eaeaea;
  --border:      #e0e0e0;
  --accent:      #79FFE1;        /* Mint – primäre Markenfarbe */
  --accent-ink:  #007d65;        /* Dunkle Mint für Text auf hellem BG */
  --text:        #111111;
  --text-dim:    #777777;
  --user-bubble: #111111;
  --bot-bubble:  #f4f5f4;
  --radius:      12px;
  --font:        'Futura', 'Outfit', 'Century Gothic', 'Trebuchet MS', system-ui, sans-serif;
}
```

### Typografie
- **Primär:** Futura (lokal, falls vorhanden)
- **Fallback:** Outfit (Google Fonts, geladen via `<link>`) → Century Gothic → System
- Gewichte: 400, 600, 700, 900
- Header: `font-weight: 900`, `text-transform: uppercase`, `letter-spacing: 0.06em`

### Key-Elemente
- **Header:** weißer BG, `border-bottom: 2px solid var(--text)`, Logo-Mark mit Mint-Hintergrund
- **Bot-Avatar:** Mint-BG, schwarzer Text, schwarzer Border
- **User-Avatar:** schwarzer BG, Mint-Text, schwarzer Border
- **Bot-Bubble:** hellgrau (`#f4f5f4`), subtiler Border
- **User-Bubble:** schwarz, weißer Text
- **`.hält`-Pill:** Mint-BG, schwarzer Text, Uppercase, `border-radius: 20px`
- **Chips:** transparent, grauer Border → Hover: Mint-Fill + schwarzer Text
- **Send-Button:** Mint-BG, schwarzer Border → Hover: invertiert

### Sicherheit
- Keine Claude API-Keys oder Credentials in den Dateien
- Keine externen API-Calls
- 100 % client-side Keyword-Matching

---

## Wissensbase (Themen & Key-Facts)

### Kernbotschaften
- Metall ist das Rückgrat der österreichischen Wirtschaft
- „Metall ist kein Klimaproblem – es ist Teil der Lösung"
- Metall ist zu 100 % recycelbar, ohne Qualitätsverlust
- Aluminium spart beim Recycling bis zu 95 % Energie
- Über 130.000 Beschäftigte in der österreichischen Metallbranche
- Heute arbeitet Metall präzise, vernetzt und im Kreislauf

### Technologie & Innovation
- **Green Steel:** Stahl ohne fossile Energie, z. B. via Elektrolichtbogenöfen & Eisenoxid-Elektrolyse
- **Wasserstoff-Stahl:** CO₂-neutrale Produktion via grünem Wasserstoff
- Digitalisierung & Automatisierung verändern die Produktion
- Smarte Legierungen, Medizintechnik, Raumfahrt

### Kreislaufwirtschaft
- Metall als Idealmaterial für Circular Economy
- Stahl: weltweit meistrecyclierter Werkstoff
- Kein anderer Werkstoff erreicht gleiche Recyclingrate + Qualität

### Energiewende & Klima
- Windräder brauchen bis zu 300 t Stahl pro Anlage
- Solarmodule: Aluminium + Kupfer
- E-Autos und Batterien: Lithium, Kobalt, Nickel, Mangan
- Stromnetze: Kupfer und Aluminium über tausende Kilometer

### Österreich & Jobs
- Weltklasse-Unternehmen: voestalpine, Anton Paar, AVL List, FACC, Engel
- Export-Stärke der Metallbranche
- Metall hält Können im Land

### Metall Allianz / Initiative Zukunft Metall
5 Missionen:
1. Emotion wecken
2. Transformation gestalten
3. Wissen schaffen
4. Wissen teilen
5. Zukunft denken

Keine klassische Lobby – „Nicht als Branche. Nicht als Lobby. Sondern als gemeinsame Haltung."

---

## Features (aktuell)

### Splash-Karte beim Laden
- Zeigt beim Start eine rotierende „Wusstest du?"-Karte
- 8 Fakten/Fragen, wechseln automatisch alle 7 Sekunden
- Manuell navigierbar via Dot-Navigation
- Button „Erzähl mir mehr →" löst die Chat-Anfrage aus
- Zufälliger Startpunkt bei jedem Reload

### Chat
- Bot-Begrüßung beim Laden (mit Tipp-Animation)
- Keyword-Matching: 15 Themenbereiche
- Fallback-Antwort wenn kein Keyword passt
- Tipp-Indikator (animierte Dots) während „Antwort lädt"
- Zeitstempel bei jeder Nachricht

### Suggestion Chips (Quick-Reply)
- 8 vorgeschlagene Fragen als anklickbare Chips:
  - Warum ist Metall wichtig?
  - Was ist nur mit Metall möglich?
  - Metall und Klimaschutz?
  - Was ist Green Steel?
  - Metall & Kreislaufwirtschaft
  - Wie viele Jobs gibt es in der Metallbranche?
  - Was ist die Metall Allianz?
  - Warum ist Metall zukunftsfähig?

---

## Dateistruktur

```
/
├── 26-05-26-metai-chatbot.html    ← Hauptdatei (alles in einer Datei)
├── index.html                     ← Identische Kopie für GitHub Pages
└── 26-05-26-metai-kontext-fuer-claude-code.md  ← Diese Datei
```

Alles – HTML, CSS, JavaScript – ist in einer einzigen `.html`-Datei.  
`index.html` ist eine 1:1-Kopie und muss bei Updates synchron gehalten werden.

---

## Mögliche nächste Schritte / Erweiterungen

### Inhalt
- [ ] Mehr KB-Einträge (z. B. Medizintechnik, Raumfahrt, Baustoffe, Berufsbilder)
- [ ] Dritte PDF auslesen: `Konzeption_Initiative „Zukunft Metall" – Leitbild, Ziele, Maßnahmen.pdf` (Sonderzeichen im Dateinamen → umbenennen und einlesen)
- [ ] Mehrsprachigkeit (EN/DE Toggle)

### UX / Design
- [ ] Animierter Mint-Gradient im Header
- [ ] „Zurück zur Startseite"-Button / Reset-Chat
- [ ] Feedback-Buttons (👍 👎) pro Antwort

### Technik
- [ ] Fuzzy Matching (z. B. mit Fuse.js) statt exaktem Substring-Match
- [ ] Antworten-Variationen (mehrere Versionen pro Thema, zufällig ausgewählt)
- [ ] Exportierbar als Webkomponente / iFrame-embed
- [ ] Anbindung an echtes LLM-Backend (z. B. Claude API) für offene Fragen
- [ ] localStorage: Chatverlauf speichern

---

## Quell-PDFs (Wissensbasis)

| Datei | Status | Inhalt |
|-------|--------|--------|
| `Executive Summary – Initiative Zukunft Metall.pdf` | ✅ Gelesen | 2 Seiten, 5 Missionen, Kernaussagen |
| `ZUKUNFT METALL_FINAL.pdf` | ✅ Gelesen | 86 Seiten, Brand-Konzept, ELEMETALL, Slogan-System |
| `Konzeption_Initiative „Zukunft Metall" – Leitbild, Ziele, Maßnahmen.pdf` | ❌ Fehler (Sonderzeichen im Dateinamen) | Nicht gelesen – umbenennen und erneut einlesen |

---

## Prompt für Claude Code (Weiterarbeit)

```
Ich arbeite an einem interaktiven Chatbot namens "METAi" – die Stimme der Metall Allianz.
Die Datei heißt 26-05-26-metai-chatbot.html (und index.html als identische Kopie für GitHub Pages).
Alles in einer HTML-Datei (kein Framework, kein Build-Tool).
Der Chatbot nutzt Rule-based Keyword-Matching in JavaScript.
Markensprache: kurze, aktive Sätze, Tonalität von "Das hält." abgeleitet.
Alle Antworten auf Deutsch.
Jede Bot-Antwort endet mit <span class="hält">Das hält.</span>

Design: Light Theme, Mint-Akzent #79FFE1, Futura/Outfit Font, Schwarz-Weiß-Kontrast.
GitHub: https://github.com/rosebud-annija/METALL-ALLIANZ
Live: https://rosebud-annija.github.io/METALL-ALLIANZ/

[Aufgabe hier einfügen]
```

---

*Erstellt in Cowork · 26.05.2026 · Redesign & Deployment: 26.05.2026*
