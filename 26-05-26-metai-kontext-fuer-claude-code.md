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
- **Lokales Repo:** nicht dauerhaft geklont — bei Bedarf nach `/tmp/METALL-ALLIANZ` klonen

```bash
git -C /tmp clone https://github.com/rosebud-annija/METALL-ALLIANZ.git
# Datei bearbeiten (Quelle: Cowork-Session-Output), dann:
cp 26-05-26-metai-chatbot.html index.html
git -C /tmp/METALL-ALLIANZ add 26-05-26-metai-chatbot.html index.html
git -C /tmp/METALL-ALLIANZ commit -m "Update: ..."
git -C /tmp/METALL-ALLIANZ push
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

Die Arbeitsdatei liegt während einer Cowork-Session typischerweise unter:
`~/Library/Application Support/Claude/local-agent-mode-sessions/.../outputs/26-05-26-metai-chatbot.html`

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
- **Titel:** METAi komplett in Schwarz, Uppercase, font-weight 900, **font-size 50px**
- **Subline:** „Stimme der Metall Allianz", Uppercase, font-weight 600, **font-size 23px**, color: `--text-dim`
- **Bot-Bubble:** hellgrau, subtiler Border · **User-Bubble:** schwarz, weißer Text
- **Keine Avatare** (Mi/Du wurden entfernt)
- **Send-Button:** Mint-BG, schwarzer Border → Hover: invertiert · **Pfeil zeigt nach oben** (filled upward arrow `M12 4L4 12h5v8h6v-8h5z`)

### Layout

`.app` ist volle Breite. `.messages` hat `max-width: 780px; margin: 0 auto`. Header/Input haben jeweils einen `.header-inner` / `.input-inner` Wrapper mit max-width 780px für den Inhalt, aber der Border läuft außerhalb davon über 100% Breite.

---

## Features (aktuell)

### Splash-Karte
- Rotierende „Wusstest du?"-Karte beim Start (8 Fakten, alle **12 Sek.**)
- Dot-Navigation, Button „Erzähl mir mehr →" löst Chat-Anfrage aus
- Zufälliger Startpunkt bei jedem Reload

### Chat
- Bot-Begrüßung beim Laden (mit Tipp-Animation)
- Keyword-Matching: 15 Themenbereiche
- Fallback-Antwort wenn kein Keyword passt
- Tipp-Indikator (animierte Dots)
- Zeitstempel bei jeder Nachricht
- **Suggestion-Chips nach jeder Bot-Antwort** — 3 themenspezifische, klickbare Pills erscheinen unter der Antwort; Klick sendet die Frage automatisch, bestehende Chips werden beim nächsten Senden entfernt
- **Keine Avatare** (wurden entfernt)

### Suggestion-Chips — Implementierung

```css
.chips-row { display: flex; flex-wrap: wrap; gap: 8px; padding: 4px 0 8px; animation: fadeSlide .35s; }
.chip { font-size: 12px; font-weight: 700; letter-spacing: 0.05em; text-transform: uppercase;
        padding: 7px 14px; border-radius: 20px; border: 1.5px solid var(--text);
        background: transparent; color: var(--text); cursor: pointer; }
.chip:hover { background: var(--accent); }
```

```js
// Jeder KB-Eintrag hat: chips: ["Label 1?", "Label 2?", "Label 3?"]
// FALLBACK_CHIPS: ["Klimaschutz & Metall?", "Was ist Green Steel?", "Jobs in der Branche?", "Kreislaufwirtschaft?"]
// getAnswerWithChips(query) → { answer, chips }
// addChips(chipsArr) fügt .chips-row nach letzter Nachricht ein
// sendMessage() entfernt zuerst alle .chips-row, ruft dann addChips() nach addMessage(answer, 'bot')
```

### KB-Themen + Chips (Übersicht)

| Thema | Chips |
|---|---|
| Metall allgemein | Kreislaufwirtschaft?, Klimaschutz & Metall?, Jobs in der Branche? |
| Was nur Metall kann | Metall in der Architektur?, Metall & Mobilität?, Metall & Energiewende? |
| Klimaschutz | Was ist Green Steel?, Kreislaufwirtschaft?, Metall & Energiewende? |
| Green Steel | Kreislaufwirtschaft?, Metall & Energiewende?, Jobs in der Branche? |
| Kreislaufwirtschaft | Was ist Green Steel?, Einzelne Metalle?, Klimaschutz & Metall? |
| Jobs | Metall in Österreich?, Zukunft & Innovation?, Was ist die Metall Allianz? |
| Metall Allianz | Jobs in der Branche?, Metall in Österreich?, Zukunft & Innovation? |
| Zukunft | Was ist Green Steel?, Metall & Energiewende?, Kreislaufwirtschaft? |
| Energie | Was ist Green Steel?, Kreislaufwirtschaft?, Metall & Mobilität? |
| Einzelne Metalle | Kreislaufwirtschaft?, Metall & Energiewende?, Metall & Mobilität? |
| Österreich | Jobs in der Branche?, Metall in der Architektur?, Metall & Mobilität? |
| Begrüßung | Klimaschutz & Metall?, Jobs in der Branche?, Metall & Energiewende? |
| Danke | Was ist Green Steel?, Kreislaufwirtschaft?, Jobs in der Branche? |
| Architektur | Einzelne Metalle?, Metall in Österreich?, Kreislaufwirtschaft? |
| Mobilität | Metall & Energiewende?, Einzelne Metalle?, Was ist Green Steel? |
| Fallback | Klimaschutz & Metall?, Was ist Green Steel?, Jobs in der Branche?, Kreislaufwirtschaft? |

---

## Mögliche nächste Schritte

- PHP-Hintergrundwissen einbauen (layerpic.php — Datei lag als Mail-Anhang vor, war aus Sandbox nicht lesbar; bitte als Textdatei ablegen)
- Mehr KB-Einträge (Medizintechnik, Raumfahrt, Berufsbilder)
- Dritte PDF einlesen: `Konzeption_Initiative Zukunft Metall.pdf` (Sonderzeichen im Dateinamen → umbenennen)
- Fuzzy Matching (z. B. Fuse.js) statt reinem Substring-Match
- Antworten-Variationen (mehrere Versionen pro Thema, zufällig)
- Feedback-Buttons (👍 👎) pro Antwort
- Anbindung an Claude API für offene Fragen

---

## Preview-Server (Cowork)

In `.claude/launch.json` als **„METAi Chatbot"** eingetragen — starten mit:
```
preview_start("METAi Chatbot")  // serverId für weitere preview_* Calls verwenden
```
