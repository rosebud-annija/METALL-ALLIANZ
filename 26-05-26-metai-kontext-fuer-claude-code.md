# METAi Chatbot – Projektkontext für Claude Code

**Datum:** 26.05.2026  
**Datei:** `26-05-26-metai-chatbot.html`  
**Status:** Erste funktionsfähige Version fertig

---

## Was ist METAi?

METAi ist ein interaktiver Chatbot – die „Stimme der Metall Allianz" (Initiative Zukunft Metall, Österreich). Er beantwortet Fragen rund um Metall, Klimaschutz, Kreislaufwirtschaft und die Metallbranche auf Deutsch.

- **Name:** METAi
- **Slogan / Markensprache:** „Das hält." → kurze, aktive Sätze, direkt, faktenbasiert aber emotional
- **Sprache:** Deutsch (österreichischer Kontext)
- **Technologie:** Reines HTML/CSS/JS (kein externes API, kein Framework)
- **Wissensquelle:** Rule-based Keyword-Matching gegen eine eingebettete Wissensbasis

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

## Wissensbase (Themen & Key-Facts)

Aus zwei PDFs extrahiert:

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

## Aktuelle Features (v1)

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

### Design
- Dunkel-industriell (Hintergrund: #0e0f11)
- Goldener Markenakzent (#c8a96e) für Highlights & CTA
- Teal-Akzent (#7ec8c8) für Sekundärhighlights in Antworten
- CSS Custom Properties für einfaches Theming
- Responsive (flex-basiertes Layout)
- Google Fonts: Inter

---

## Dateistruktur

```
26-05-26-metai-chatbot.html    ← Hauptdatei (alles in einer Datei)
```

Alles – HTML, CSS, JavaScript – ist in einer einzigen `.html`-Datei.

---

## Mögliche nächste Schritte / Erweiterungen

### Inhalt
- [ ] Mehr KB-Einträge (z. B. Medizintechnik, Raumfahrt, Baustoffe, Berufsbilder)
- [ ] Dritte PDF auslesen: `Konzeption_Initiative „Zukunft Metall" – Leitbild, Ziele, Maßnahmen.pdf` (konnte wegen Sonderzeichen im Dateinamen nicht gelesen werden → umbenennen und nochmal versuchen)
- [ ] Mehrsprachigkeit (EN/DE Toggle)

### UX / Design
- [ ] Light Mode Toggle
- [ ] Animierter Metall-Gradient im Header
- [ ] Antworten mit Icons (z. B. 🔩 ♻️) – falls gewünscht
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

Wenn du Claude Code verwendest, kannst du diesen Kontext direkt mitgeben:

```
Ich arbeite an einem interaktiven Chatbot namens "METAi" – die Stimme der Metall Allianz.
Die Datei heißt 26-05-26-metai-chatbot.html und enthält alles in einer HTML-Datei (kein Framework, kein Build-Tool).
Der Chatbot nutzt Rule-based Keyword-Matching in JavaScript.
Markensprache: kurze, aktive Sätze, Tonalität von "Das hält." abgeleitet.
Alle Antworten auf Deutsch.
Jede Bot-Antwort endet mit <span class="hält">Das hält.</span>

[Aufgabe hier einfügen – z. B.: "Füge 5 neue KB-Einträge hinzu für das Thema Medizintechnik."]
```

---

*Erstellt in Cowork · 26.05.2026*
