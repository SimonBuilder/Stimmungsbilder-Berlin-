# Stimmungsbilder Berlin

## Was das ist

Website für ein Kulturprojekt in Berlin. Aktuell nur eine Coming-Soon-Seite mit dem
Claim „Wir hören zu." Später kommen Galerie, Video und Konzepttext dazu.

Es ist ein Uni-Seminarprojekt an der UdK Berlin (kein kommerzielles Vorhaben).
Relevant für rechtliche Einordnung (z. B. Impressumspflicht), s. Offene Punkte.

## Konzept (für die Website-Dokumentation)

**Stimmungsbilder** — interaktive Plakatkampagne mit der Möglichkeit, analoge
Stimmen/Perspektiven/Wünsche zu sammeln. Künstlerisches Installationsprojekt,
keine empirische Datenerhebung.

- Ort: Bauzaun als temporäre Installation, plus Stand mit uns als Moderation.
- Zielgruppe: nicht primär Nichtwähler, sondern alle, die politische Wünsche
  äußern wollen.
- Motivation: Wünsche innerhalb der Installation sichtbar machen.
- Unsere Rolle danach: Dokumentation des Projekts auf dieser Website.

## Technische Grundregeln

- **Statisches HTML. Kein Framework, kein Build-Schritt, keine Abhängigkeiten.**
  Das ist eine bewusste Entscheidung, keine Übergangslösung. Die Seite soll ohne
  Wartung jahrelang laufen. Schlag kein React, Next.js oder Tailwind vor.
- Eine `index.html` mit CSS und JS inline. Erst bei mehreren Seiten aufteilen.
- Bilder als WebP, längste Kante max. 2000 px, `loading="lazy"`.
- Video nur selbst gehostet, stumm, als Loop. Kein YouTube-/Vimeo-Embed, das
  würde einen Consent-Banner erzwingen.

## Deployment

- GitHub-Repo → **Netlify** (nicht Cloudflare Pages, siehe unten), Deploy über
  „Import from GitHub", kein Build-Befehl, Publish directory `/` (Root).
- Repo: [github.com/SimonBuilder/Stimmungsbilder-Berlin-](https://github.com/SimonBuilder/Stimmungsbilder-Berlin-)
- Domain bei netcup registriert. Für Netlify müssen die Nameserver nicht
  zwingend umgestellt werden — reicht auch ein DNS-Eintrag bei netcup, der auf
  Netlify zeigt. Noch offen, welche Variante genutzt wird.
- Ursprünglich war Cloudflare Pages vorgesehen (daher die alte 25-MiB-Regel
  und der ToS-Hinweis zu Video/großen Dateien) — am 2026-09-08 spontan auf
  Netlify gewechselt, weil das Cloudflare-Dashboard kurzzeitig nicht
  erreichbar war und der Nutzer stattdessen direkt über Netlify deployt hat.
  Netlifys eigene Limits (Bandbreite/Dateigröße auf dem Free-Tier) sind noch
  nicht geprüft — vor dem Hochladen von Video/großen Medien in der aktuellen
  Netlify-Doku nachsehen, nicht die alten Cloudflare-Zahlen annehmen.

## Gestaltung

| Token | Wert |
|---|---|
| Hintergrund | `#FFFFFF` |
| Kleiner Text | `#4A4A4A` |

### Akzentfarben (Schriftzug + Linie)

Drei Projektfarben, bei jedem Seitenaufruf wird per JS eine zufällig gewählt
(`--accent`-CSS-Variable, gesetzt in `index.html` vor dem ersten Rendern,
damit es nicht flackert). Bleibt für die Dauer eines Seitenaufrufs fix, ändert
sich erst beim nächsten Laden.

| Farbe | Hex | Kontrast auf Weiß |
|---|---|---|
| Teal | `#20B3AF` | ~2,6:1 |
| Beige | `#C69E77` | ~2,5:1 |
| Pink | `#DC5498` | ~3,7:1 |

Nur Pink erreicht die WCAG-Mindestgrenze für großen Text (3:1) knapp; Teal und
Beige liegen darunter. Bewusst akzeptiert für den großen, dekorativen
Schriftzug — für Fließtext (falls später ergänzt) trotzdem immer Dunkelgrau
verwenden, nie eine der Akzentfarben.

### Position des Schriftzugs (aus dem Original-Banner gemessen)

- Linke Kante 14,54 %, Breite 70,91 % der Fläche
- Optische Mitte vertikal bei 47,86 %, nicht bei 50 %
- Unter 700 px Breite: 7 % links, 86 % breit, Mitte bei 46 %

### Animation

Ein einziger Auftritt beim Laden: Schriftzug blendet auf, danach zieht die Linie
von links nach rechts. Nichts weiter animieren. `prefers-reduced-motion` respektieren.

## Schriften — wichtig

Die Hausschrift kommt von Adobe Fonts. **Die Schriftdateien dürfen nicht selbst
gehostet werden**, das verbieten Adobes Nutzungsbedingungen.

Deshalb: Der Schriftzug „Wir hören zu." ist ein SVG mit in Pfade umgewandeltem
Text. Es wird keine Schrift geladen. Nicht versuchen, das durch einen Webfont zu
ersetzen.

Für spätere Fließtexte gibt es zwei Wege, beide noch offen:
1. Adobe-Embed-Code (`use.typekit.net`) plus Einwilligung im Consent-Banner
2. Webfont-Lizenz direkt bei der Foundry kaufen, dann selbst hosten erlaubt

## Offene Punkte

- [ ] `impressum.html` und `datenschutz.html` fehlen noch. Bewusste
      Entscheidung: Seite geht trotzdem vorerst live (nur Coming-Soon-Claim,
      keine weiteren Inhalte), während bei der UdK wegen einer nutzbaren
      Adresse fürs Impressum nachgefragt wird. Rechtliches Risiko dadurch
      akzeptiert, nicht behoben — Impressum/Datenschutz nachreichen, sobald
      die Adresse geklärt ist.
- [ ] Ungeklärt: welche Adresse ins Impressum? Braucht eine ladungsfähige
      Anschrift (Postfach reicht nicht). Als Uni-Seminarprojekt evtl. c/o-Adresse
      der UdK nutzbar, statt Privatadresse — muss mit Seminarleitung/Fachbereich
      geklärt werden, ob die UdK dafür Post annimmt/das erlaubt. Auch ungeklärt,
      ob das Projekt (öffentliche Kampagne, eigene Domain) überhaupt unter die
      Ausnahme für rein private Seiten fällt oder als „geschäftsmäßig" im Sinne
      der Impressumspflicht gilt — im Zweifel eher Ja.
- [ ] Im SVG ist die Linie genau so breit wie der Schriftzug. Im Original-Banner
      ragte sie links 1,5 % und rechts 2 % darüber hinaus, und saß weiter vom
      Text entfernt. Ungeklärt, welche Version gilt.
- [ ] Timing der Animation ist ungeprüft.
