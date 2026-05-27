# METAI – Projektkontext für Claude Code

**Stand:** 27.05.2026 (Session 5) · **Status:** Live auf GitHub Pages ✅

---

## Was ist METAI?

Interaktiver Chatbot der Metall Allianz (Initiative Zukunft Metall, Österreich). Beantwortet Fragen zu Metall, Klimaschutz, Kreislaufwirtschaft und der Metallbranche auf Deutsch.

- **Technologie:** Reines HTML/CSS/JS, eine einzige Datei, kein Framework, kein Build-Tool
- **Wissensquelle (Offline-Modus):** Rule-based Keyword-Matching gegen eingebettete Wissensbasis (15 Themen)
- **Wissensquelle (Online-Modus):** Claude API (`claude-opus-4-7`) mit eingebettetem Wissen aus metalltechnischeindustrie.at und netzwerk-metall.at, plus Gesprächs-History für Nicht-Wiederholung

---

## Repository & Deployment

- **Repo:** https://github.com/rosebud-annija/METALL-ALLIANZ (privat)
- **Live:** https://rosebud-annija.github.io/METALL-ALLIANZ/
- **Branch:** `main` · **Remote:** HTTPS · **Credentials:** macOS osxkeychain
- **Lokales Repo:** `/tmp/METALL-ALLIANZ` (bei Bedarf neu klonen)

```bash
# Klonen falls nicht vorhanden:
git -C /tmp clone https://github.com/rosebud-annija/METALL-ALLIANZ.git

# Nach Änderungen an der Arbeitsdatei:
cp "26-05-26-metai-chatbot.html" /tmp/METALL-ALLIANZ/index.html
cp "26-05-26-metai-chatbot.html" /tmp/METALL-ALLIANZ/26-05-26-metai-chatbot.html
cd /tmp/METALL-ALLIANZ
git add index.html 26-05-26-metai-chatbot.html
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

Arbeitsdatei während Cowork-Session:
`~/Library/Application Support/Claude/local-agent-mode-sessions/.../outputs/26-05-26-metai-chatbot.html`

---

## Markenstimme

Abgeleitet aus dem Slogan **„Das hält."** und dem Rosebud-Agenturkonzept „ELEMETALL":

- Kurze Sätze. Aktiv. Direkt. Faktenbasiert aber emotional.
- Adjektive: *handfest, formbar, verlässlich, präzise*
- Kein Pathos. Kein „Das hält." am Satzende.

---

## Design-System (Light Theme)

```css
--bg:          #ffffff
--surface2:    #f4f5f4   /* Bot-Bubble */
--accent:      #79FFE1   /* Mint */
--accent-ink:  #007d65   /* Mint dunkel, für Text/Links */
--text:        #111111
--text-dim:    #777777
--user-bubble: #111111
--radius:      12px
--font:        'Futura', 'Outfit', 'Century Gothic', system-ui, sans-serif
```

- **Header:** weißer BG, `border-bottom: 2px solid #111` über volle Bildschirmbreite
- **Input-Bereich:** `border-top: 2px solid #111` über volle Bildschirmbreite
- **Titel:** METAI komplett in Schwarz, Uppercase, font-weight 900, **font-size: 50px**
- **Subline:** „Stimme der Metall Allianz", Uppercase, font-weight 600, color: `--text-dim`, **font-size: 23px**
- **Bot-Bubble:** hellgrau, subtiler Border · **User-Bubble:** schwarz, weißer Text
- **Keine Avatare**
- **Send-Button:** Mint-BG, schwarzer Border → Hover: invertiert · Pfeil zeigt nach oben (`M12 4L4 12h5v8h6v-8h5z`)

### Layout

`.app` ist volle Breite. `.messages` ist ebenfalls volle Breite — Zentrierung über `padding: max(24px, calc((100% - 780px) / 2))`, damit der Scrollbalken am rechten Bildschirmrand liegt. Header/Input haben `.header-inner` / `.input-inner` Wrapper mit max-width 780px für den Inhalt, aber der Border läuft außerhalb über 100% Breite.

**Scrollbalken:** In `.messages` ausgeblendet (`scrollbar-width: none` + `.messages::-webkit-scrollbar { display: none }`). `html, body` haben `overflow: hidden` um Body-Scrollbar zu verhindern. Scroll-Funktionalität bleibt in `.messages` erhalten (`overflow-y: auto`).

### Bubble-Sizing

```css
.bubble {
  width: fit-content;
  max-width: 90%;
  padding: 13px 17px;
}

.message.user .bubble {
  padding: 13px 24px;  /* mehr Luft rechts */
}

/* Per JS gesetzt wenn Text kein Leerzeichen enthält (Chip-Fragen): */
.message.user .bubble.nowrap { white-space: nowrap; }
```

In `addMessage()`: `if (role === 'user' && !html.includes(' ')) bubbleEl.classList.add('nowrap');`

---

## Features

### Claude API Integration

- **Zahnrad-Icon im Header** (rechts) + **API-Badge** unter dem Titel öffnen das Einstellungs-Modal
- **Settings-Modal:**
  - Eingabefeld für Anthropic API Key (`sk-ant-...`)
  - Key wird nur lokal per `localStorage('metai_api_key')` gespeichert — verlässt das Gerät nie
  - Validierung: Key muss mit `sk-ant-` beginnen
  - „Key entfernen"-Button erscheint wenn Key gesetzt
- **Status-Badge im Header:**
  - `Offline-Modus` (grauer Punkt) — kein Key gesetzt, KB-Fallback aktiv
  - `Claude aktiv` (grüner Punkt, grüner Text) — Key gesetzt, Claude antwortet
- **Claude-Modus:**
  - Modell: `claude-opus-4-7`
  - Streaming via SSE (`stream: true`, `anthropic-dangerous-direct-browser-access: true`)
  - Gesprächs-History in `conversationHistory[]` — Claude wiederholt sich nicht
  - Antworten werden als HTML rendered (Claude gibt `<strong>`, `<ul>`, `<li>` aus)
  - Follow-up Chips nach jeder Antwort (zufällig aus `FOLLOW_UP_CHIPS`-Pool, 3 Stück)
- **Offline-Fallback** (kein Key): Rule-based KB wie bisher
- **Footer-Note** aktualisiert sich dynamisch: „Claude (Anthropic) verbunden" vs. „Zukunft Metall Initiative"

#### System-Prompt Gesprächsregeln (aktuell)

1. Antworte immer auf Deutsch
2. **Gesprächig, nicht akademisch** — wie jemand, der einem Freund etwas erklärt
3. **Knappe Antworten** — 2–4 Sätze reichen meist, kein Aufzählungs-Overkill
4. **Fakten einweben**, nicht auflisten — Zahlen als Teil des Gesprächs
5. Keine Wiederholungen — auf vorherige Infos aufbauen
6. Format: sparsam HTML-Tags, nur bei echten Listen `<ul>/<li>`, kein Markdown
7. Ehrlichkeit — spekuliere nicht
8. **Ton: zugänglich, warm, neugierig machend** — darf auch mal eine Gegenfrage stellen
9. Kontext: im Namen der Metall Allianz sprechen
10. Bei FMTI/Netzwerk Metall auf jeweilige Website verweisen

#### Relevante JS-Globals

| Name | Zweck |
|---|---|
| `CLAUDE_MODEL` | `'claude-opus-4-7'` |
| `SYSTEM_PROMPT` | Eingebettetes Wissen + Gesprächsregeln |
| `conversationHistory` | Array mit `{role, content}` für Multi-Turn |
| `FOLLOW_UP_CHIPS` | Pool von 14 Follow-up-Fragen für Claude-Modus |
| `getApiKey()` | Liest Key aus localStorage |
| `saveApiKey(key)` | Speichert/löscht Key, aktualisiert Badge |
| `updateApiIndicator()` | Synct Badge + Footer-Note mit Key-Status |
| `openSettings()` | Öffnet Modal, füllt Feld vor |
| `closeSettings()` | Schließt Modal |
| `saveSettings()` | Validiert + speichert Key |
| `clearApiKey()` | Entfernt Key + leert conversationHistory |
| `callClaudeAPI(userText)` | Streaming-Fetch zur Anthropic API, gibt fullText zurück |
| `getFollowUpChips()` | Gibt 3 zufällige Chips aus FOLLOW_UP_CHIPS zurück |

---

### Splash-Karte

- Rotierende „Wusstest du?"-Karte beim Start (8 Fakten, alle **22 Sek.**)
- Dot-Navigation, Button „Erzähl mir mehr →" löst Chat-Anfrage aus
- Zufälliger Startpunkt bei jedem Reload
- **Reihenfolge:** Bot-Begrüßung erscheint zuerst, Splash-Karte wird darunter angehängt

### Chat

- Bot-Begrüßung beim Laden (mit Tipp-Animation) — Text: „Servus! Ich bin METAI."
- Keyword-Matching (Offline): 15 Themenbereiche
- **Keine Antwortwiederholungen (Offline):** `usedKBIndices` (Set) trackt bereits verwendete KB-Einträge
- **Keine Wiederholungen (Claude):** Gesprächs-History wird mitgeführt, System-Prompt weist darauf hin
- Fallback-Antwort wenn kein Keyword passt (Offline) / Fehler-Meldung (Claude)
- Tipp-Indikator (animierte Dots)
- Zeitstempel bei jeder Nachricht
- **Suggestion-Chips** nach jeder Bot-Antwort — 3 klickbare Pills
- Bestehende Chips werden beim nächsten Senden entfernt

### Schreibweise: METAI

Der Name wird **immer in Versalien** geschrieben: `METAI` — nie `METAi` oder `Metai`.

---

## Suggestion-Chips — Implementierung

```css
.chips-row { display: flex; flex-wrap: wrap; gap: 8px; padding: 4px 0 8px; animation: fadeSlide .35s; }
.chip { font-size: 12px; font-weight: 700; letter-spacing: 0.05em; text-transform: uppercase;
        padding: 7px 14px; border-radius: 20px; border: 1.5px solid var(--text);
        background: transparent; color: var(--text); cursor: pointer; }
.chip:hover { background: var(--accent); }
```

```js
// Offline: jeder KB-Eintrag hat chips: ["Label 1?", "Label 2?", "Label 3?"]
// FALLBACK_CHIPS: ["Klimaschutz & Metall?", "Was ist Green Steel?", "Jobs in der Branche?", "Kreislaufwirtschaft?"]
// getAnswerWithChips(query) → { answer, chips }

// Claude: FOLLOW_UP_CHIPS Pool (14 Einträge), getFollowUpChips() gibt 3 zufällige zurück

// addChips(chipsArr) fügt .chips-row nach letzter Nachricht ein
// sendMessage() entfernt zuerst alle .chips-row, ruft dann addChips() nach der Antwort
```

---

## KB-Themen + Chips (Offline-Modus)

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

## Session-Verlauf (Patches)

| Session | Änderungen |
|---|---|
| Session 1–2 | Grundstruktur, Splash-Karte, KB mit 15 Themen, Suggestion-Chips |
| Session 3 | Schriftgrößen angepasst (Titel 50px, Subline 23px), Scrollbalken ausgeblendet, GitHub Push |
| Session 4 | Claude API Integration: Settings-Modal, API-Badge, callClaudeAPI() mit Streaming, SYSTEM_PROMPT mit FMTI + Netzwerk Metall Wissen, conversationHistory, Follow-up Chips |
| Session 5 | Bubble-Fix: fit-content + max-width 90%, nowrap per JS für Einwort-Texte, overflow:hidden auf body, System-Prompt Ton auf gesprächig/kurz umgestellt |

---

## Mögliche nächste Schritte

- Mehr KB-Einträge für Offline-Modus (Medizintechnik, Raumfahrt, Berufsbilder)
- Fuzzy Matching (z. B. Fuse.js) statt reinem Substring-Match im Offline-Modus
- Streaming live anzeigen (Bubble-Text während des Streams aktualisieren)
- Website-Inhalte via GitHub Actions aktuell halten (wöchentlicher Scrape → System-Prompt updaten)
- Feedback-Buttons (👍 👎) pro Antwort
- PHP-Hintergrundwissen einbauen (layerpic.php — als Textdatei ablegen)

---

## Preview-Server (Cowork)

In `.claude/launch.json` als **„METAi Chatbot"** eingetragen — starten mit:
```
preview_start("METAi Chatbot")
```
