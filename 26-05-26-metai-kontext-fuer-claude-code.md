# METAi – Projektkontext für Claude Code

**Stand:** 26.05.2026 · **Status:** Live auf GitHub Pages ✅

---

## Was ist METAi?

Interaktiver Chatbot der Metall Allianz (Initiative Zukunft Metall, Österreich). Beantwortet Fragen zu Metall, Klimaschutz, Kreislaufwirtschaft und der Metallbranche auf Deutsch.

- **Technologie:** Reines HTML/CSS/JS, eine einzige Datei, kein Framework, kein Build-Tool
- **Wissensquelle:** Rule-based Keyword-Matching gegen eingebettete Wissensbasis (15 Themen)

---

## Repository & Deployment

- **Repo:** https://github.com/rosebud-annija/METALL-ALLIANZ (privat)
- **Live:** https://rosebud-annija.github.io/METALL-ALLIANZ/
- **Branch:** `main` · **Remote:** HTTPS · **Credentials:** macOS osxkeychain

```bash
git add 26-05-26-metai-chatbot.html index.html
git commit -m "Update: ..."
git push
# GitHub Pages baut automatisch (~60 Sekunden)
```

> `index.html` ist eine 1:1-Kopie von `26-05-26-metai-chatbot.html` — beide immer synchron halten.

---

## Dateistruktur

```
/
├── 26-05-26-metai-chatbot.html    ← Hauptdatei (alles in einer Datei: HTML + CSS + JS)
├── index.html                     ← Identische Kopie für GitHub Pages
└── 26-05-26-metai-kontext-fuer-claude-code.md
```

---

## Markenstimme

Abgeleitet aus dem Slogan **„Das hält."** und dem Rosebud-Agenturkonzept „ELEMETALL":

- Kurze Sätze. Aktiv. Direkt. Faktenbasiert aber emotional.
- Adjektive: *handfest, formbar, verlässlich, präzise*
- Kein Pathos. Kein „Das hält." am Satzende (wurde entfernt).

---

## Design-System (Light Theme)

```css
--bg:          #ffffff
--surface2:    #f4f5f4   /* Bot-Bubble */
--accent:      #79FFE1   /* Mint */
--accent-ink:  #007d65   /* Mint dunkel, für Text */
--text:        #111111
--text-dim:    #777777
--user-bubble: #111111
--radius:      12px
--font:        'Futura', 'Outfit', 'Century Gothic', system-ui, sans-serif
```

- **Header:** weißer BG, `border-bottom: 2px solid #111` — läuft über volle Bildschirmbreite
- **Input-Bereich:** `border-top: 2px solid #111` — läuft über volle Bildschirmbreite
- **Titel:** METAi komplett in Schwarz (kein farbiges i), Uppercase, font-weight 900
- **Bot-Bubble:** hellgrau, subtiler Border · **User-Bubble:** schwarz, weißer Text
- **Keine Avatare** (Mi/Du wurden entfernt)
- **Send-Button:** Mint-BG, schwarzer Border → Hover: invertiert

### Layout

`.app` ist volle Breite. `.messages` hat `max-width: 780px; margin: 0 auto`. Header/Input haben jeweils einen `.header-inner` / `.input-inner` Wrapper mit max-width 780px für den Inhalt, aber der Border läuft außerhalb davon über 100% Breite.

---

## Features (aktuell)

### Splash-Karte
- Rotierende „Wusstest du?"-Karte beim Start (8 Fakten, alle 7 Sek.)
- Dot-Navigation, Button „Erzähl mir mehr →" löst Chat-Anfrage aus
- Zufälliger Startpunkt bei jedem Reload

### Chat
- Bot-Begrüßung beim Laden (mit Tipp-Animation)
- Keyword-Matching: 15 Themenbereiche
- Fallback-Antwort wenn kein Keyword passt
- Tipp-Indikator (animierte Dots)
- Zeitstempel bei jeder Nachricht
- **Keine Suggestion-Chips** (wurden entfernt)
- **Keine Avatare** (wurden entfernt)

### KB-Themen
Metall allgemein · Klimaschutz · Green Steel · Kreislaufwirtschaft · Jobs · Metall Allianz · Zukunft/Innovation · Energie/Energiewende · Einzelne Metalle · Österreich · Architektur · Mobilität · Begrüßung · Dankeschön/Lob · Fallback

---

## Mögliche nächste Schritte

- Mehr KB-Einträge (Medizintechnik, Raumfahrt, Berufsbilder)
- Dritte PDF einlesen: `Konzeption_Initiative Zukunft Metall.pdf` (Sonderzeichen im Dateinamen → umbenennen)
- Fuzzy Matching (z. B. Fuse.js) statt reinem Substring-Match
- Antworten-Variationen (mehrere Versionen pro Thema, zufällig)
- Feedback-Buttons (👍 👎) pro Antwort
- Anbindung an Claude API für offene Fragen
