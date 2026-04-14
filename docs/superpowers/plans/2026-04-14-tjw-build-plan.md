# TJW Build Plan — tulumjunglewedding.com
Erstellt: 2026-04-14
Schritt 9 des Design-Workflows

---

## ÜBERBLICK

- **Projekt:** tulumjunglewedding.com — separater Wedding-Funnel für Casa Arkaana
- **Stack:** Astro 4 + Tailwind v4, statischer Export (output: 'static')
- **Deploy:** Neuer Docker-Container auf Hetzner 178.104.15.187
- **Mockup-Referenz:** `public/tulumjunglewedding-homepage-mockup.html` — ist visuelle Wahrheit
- **Seitenstruktur:** Onepager — eine `src/pages/index.astro` mit allen Sektionen

---

## 1. 21ST.DEV CHECK

Scouting via bu-scout Recherche (2026-04-14): 21st.dev + awesome-claude-code + GitHub + Reddit.

| Komponente | 21st.dev Befund | Entscheidung | Begründung |
|------------|-----------------|-------------|------------|
| Testimonial | **Clean Testimonial** (lucasheriques) — einzeiliger Slide, Serif-Quote, Attribution | **ADOPT** | Passt direkt auf TJW-Ästhetik — Serif, keine Karten, kein Karussell. CSS-Variablen anpassen. |
| Hero Interaction | **Scroll Media Expansion** (aceternity) — Bild expandiert beim Scroll, nicht statisch | **ADOPT** | Premium-Interaction die kein generischer Wedding-Site-Baukasten hat. Anti-AI-Slop. |
| FAQ Accordion | **Accordion** (originui) — animiert, keyboard-accessible, ARIA | **ADAPT** | Basis-Logik direkt nutzbar. Restyling auf TJW light-theme. |
| Gallery | **Masonry Grid** (mehrere Varianten vorhanden) | **ADAPT** | Masonry-Logik für WeddingGallery adaptieren (Mockup-Rows als Basis behalten). |
| Navigation | **Minimal Nav** (mehrere) | **ADAPT** | Scroll-behavior-Logik übernehmen, TJW Text-Logo + 5 Links integrieren. |
| Pricing Cards | Pricing Sections vorhanden, zu generisch | **BUILD** | 3-Tier mit Featured-Badge + Gold-Divider exakt wie Mockup — kein 21st.dev-Match. |
| Contact Form | Web3Forms-spezifisch, nicht auf 21st.dev | **BUILD** | 2-col Layout + Web3Forms-Integration nach Mockup-Spec. |

**Fazit:** 2× ADOPT (Testimonial + Hero-Interaction) · 3× ADAPT (FAQ + Gallery + Nav) · 2× BUILD (Pricing + Form). Kein "alles selbst bauen" mehr.

### ADOPT-Implementierungsnotizen

**Clean Testimonial** (lucasheriques/21st.dev):
- Wechsel von CA TestimonialHero.astro auf diesen Basis-Code
- Serif-Quote (Cormorant Garamond 300), `--color-neutral` Attribution
- B&A 2024 Zitat + Google Reviews Badge darunter

**Scroll Media Expansion Hero** (aceternity-style):
- Hero-Bild startet komprimiert (80vh), expandiert auf 100vh beim ersten Scroll
- CSS transform + IntersectionObserver — kein extra JS-Framework
- Scarcity-Signal bleibt, scrollt mit in finale Hero-Position

---

## 2. CA-KOMPONENTEN ANALYSE

Alle Komponenten in `~/code/CasaArkaana/website/src/components/`.

### DIREKT ADAPTIERBAR (CSS-Variablen tauschen, Props anpassen)

| CA-Komponente | TJW-Verwendung | Anpassungen |
|---------------|----------------|-------------|
| `TestimonialHero.astro` | S03 Safety Moment | CSS-Variablen: `--gold` → `#B5904E`, `--font-display` → Cormorant Garamond. Mockup-Stil: großes `::before` Anführungszeichen links, Attribution mit `-- `Prefix. Props: quote + name reichen. |
| `FaqAccordion.astro` | S09 FAQ | Aktuell dark-theme hard-coded (border `rgba(255,255,255,0.06)`). Anpassen: Border auf `var(--color-cream)`, Font auf `var(--font-serif)`, Farbe auf `var(--color-text)`. SchemaMarkup-Prop bleibt. |
| `GoogleReviewsBadge.astro` | S03 nach Testimonial | Nur Google-Maps-URL anpassen (bleibt gleiche CA-URL). Badge-Styling für hellen Hintergrund — border auf `var(--color-cream)`. |
| `EyebrowLabel.astro` | Alle Sektionen | Props passen. CSS-Variable `--gold` anpassen. |
| `SectionWrapper.astro` | Wrapper für Sektionen | `theme='light'` für helle Sektionen. CSS-Variable `--section-py` und `--max-width` anpassen. |

### NEU BAUEN (CA-Logik zu stark CA-spezifisch)

| Neues TJW-Komponente | Warum neu | Komplexität |
|---------------------|-----------|-------------|
| `NavBar.astro` | CA Header hat Logo-Bild + Dropdown für CA-Seiten — TJW braucht Text-Logo + 5 flache Links + scroll-behavior | Mittel |
| `HeroSection.astro` | PageHero.astro ist für CA mit CA-spezifischem CSS. TJW-Hero hat Gradient, Scarcity-Signal, Scroll-Indicator — komplett neu | Mittel |
| `WeddingGallery.astro` | CA GalleryGrid ist 3-spaltig mit `badge`-Prop — TJW braucht 4-reihiges Custom-Grid (Ratio 1.6:1 / 3er-gleich / 1:1.8 / 2er-gleich) | Mittel |
| `StylesGrid.astro` | Asymmetrisch: 1 featured (3fr) + 2 small (2fr) — nicht in CA vorhanden | Einfach |
| `IncludedGrid.astro` | 4-spaltige Photo-Cards mit Nummer-Overlay und Body-Texten — CA FactCard.astro zu anders | Einfach |
| `PricingSection.astro` | 3-Tier Karten mit Featured-Badge — komplett neu | Mittel |
| `FullWidthPool.astro` | Full-Width Image mit Overlay-Text — einfach, aber kein CA-Äquivalent | Einfach |
| `ContactForm.astro` | Web3Forms, 2-spaltig (Info links / Form rechts) — CA hat kein Kontaktformular-Komponente | Mittel |
| `FooterSimple.astro` | CA Footer ist 4-spaltig mit Nav-Links zu CA-Seiten. TJW braucht minimalen Footer (Logo + 3 Links + CA-Link) | Einfach |

### NICHT VERWENDEN (zu CA-spezifisch)

- `Header.astro` — CA-Logo-Bild, CA-Dropdown-Navigation, CA-Klassen
- `Footer.astro` — CA-Branding, CA-Seiten-Links
- `PageHero.astro` — CA-Bildpfade, CA-CSS-Klassen
- `GalleryGrid.astro` — 3-spaltig mit badge-Prop, CA-CSS
- `ParallaxDivider.astro` — CA-spezifisch
- `PathCard.astro` — CA-spezifisch
- `DroneVideo.astro` — Video vorhanden (`public/wedding-video-1080.mp4`), aber CA-Komponente hat CA-spezifisches Styling

---

## 3. SHARED COMPONENTS LISTE

Alle wiederverwendbaren TJW-Komponenten unter `src/components/`:

```
src/components/
├── NavBar.astro          — Sticky Nav, Text-Logo, scroll-behavior, mobile-toggle
├── HeroSection.astro     — Vollbild-Hero, Overlay-Gradient, Scarcity-Signal, Scroll-Indicator
├── EyebrowLabel.astro    — Adapt von CA (gold | neutral Variante)
├── GoldLine.astro        — 40px horizontale Linie, wiederverwendbar (oder als Utility-CSS)
├── WeddingGallery.astro  — 4-reihiges Custom-Grid, alle 8 Fotos
├── SplitSection.astro    — Adapt von CA: theme=light, 55/45, imagePosition=left|right
├── TestimonialHero.astro — Adapt von CA: light-theme, großes Anführungszeichen, Attribution
├── ReviewsBadge.astro    — Adapt von CA GoogleReviewsBadge: hell + TJW-Border
├── StylesGrid.astro      — Asymmetrisch: 1 featured + 2 small
├── IncludedGrid.astro    — 4-spaltige Photo-Cards
├── FullWidthPool.astro   — Full-Width Image + Overlay-Text
├── PricingSection.astro  — 3-Tier Karten, Featured-Badge, Gold-Divider
├── SustainabilitySection.astro — Zentriert, Serif-Stat, Body-Text
├── FaqAccordion.astro    — Adapt von CA: light-theme, serif questions
├── ContactForm.astro     — Web3Forms, 2-col Layout
└── FooterSimple.astro    — Logo + Links + CA-Backlink
```

---

## 4. SEITENSTRUKTUR

```
src/
├── pages/
│   └── index.astro        — Onepager, alle 10 Sektionen (+ Gallery + Pool als eigene Sektionen)
├── layouts/
│   └── BaseLayout.astro   — <html>, <head>, Global CSS, Google Fonts, NavBar, Footer
├── components/
│   └── [alle oben gelisteten]
├── styles/
│   └── global.css         — Design-Tokens als CSS Custom Properties, Reset, Shared-Classes
└── assets/
    └── images/            — Optimierte Bilder (Astro Image Service)
```

### index.astro Sektions-Reihenfolge

```astro
<BaseLayout>
  <HeroSection />                      <!-- S01 -->
  <WeddingGallery />                   <!-- Gallery — "This is what it looks like" -->
  <SplitSection id="venue" />          <!-- S02 The Venue -->
  <FullWidthPool />                    <!-- Pool Feature -->
  <TestimonialHero />                  <!-- S03 Safety Moment + ReviewsBadge -->
  <StylesGrid id="styles" />           <!-- S04 Three Styles -->
  <IncludedGrid />                     <!-- S05 What's Included -->
  <SplitSection id="sapote" />         <!-- S06 Sapote Tree (cream bg) -->
  <SustainabilitySection />            <!-- S07 Sustainability -->
  <SplitSection id="hosts" />          <!-- S08 The Hosts -->
  <PricingSection id="pricing" />      <!-- S06b Pricing (neu aus Mockup) -->
  <FaqAccordion id="faq" />            <!-- S09 FAQ -->
  <ContactForm id="contact" />         <!-- S10 Kontaktformular -->
</BaseLayout>
```

---

## 5. MOBILE-FIRST CSS-STRATEGIE

### Entscheidung: Custom CSS Custom Properties (keine Tailwind-Klassen für Design-Tokens)

Begründung: Das Mockup ist komplett in vanilla CSS + Custom Properties geschrieben. Das ist der Standard. Tailwind v4 wird nur für Utilities genutzt (z.B. `flex`, `grid`, `hidden`) — NICHT für Farben, Fonts, Spacing-Werte.

### global.css Struktur

```css
/* 1. Design Tokens */
:root {
  --color-bg:      #FAFAF7;
  --color-text:    #1A1A18;
  --color-green:   #1D3828;
  --color-gold:    #B5904E;
  --color-neutral: #8C8876;
  --color-cream:   #F2EDE5;
  --color-white:   #FFFFFF;

  --font-serif: 'Cormorant Garamond', Georgia, serif;
  --font-sans:  'DM Sans', system-ui, sans-serif;

  --sp-1: 8px;   --sp-2: 16px;  --sp-3: 24px;  --sp-4: 32px;
  --sp-6: 48px;  --sp-8: 64px;  --sp-10: 80px; --sp-15: 120px;

  --max-content: 1200px;
  --max-text:    760px;
  --gutter:      var(--sp-4);

  --section-py:  var(--sp-10);
  --ease:        cubic-bezier(0.22, 1, 0.36, 1);
}

/* 2. Mobile-First Reset */
/* 3. Shared Components (.eyebrow, .btn-primary, .gold-line, .section-heading) */
/* 4. Media Queries: min-width: 640px (tablet) und min-width: 1024px (desktop) */
```

### Viewport-Breakpoints

| Name | min-width | Was ändert sich |
|------|-----------|----------------|
| Mobile | 375px (Basis) | 1-Spalte, Padding var(--sp-4) |
| Tablet | 640px | 2-spaltige Grids, größere Fonts |
| Desktop | 1024px | Split-Sections 55/45, 3-Col Pricing, Nav-Links sichtbar |
| Wide | 1200px | Max-Content-Breite, Schrift-Maximalgrößen |

---

## 6. DEPLOY-PLAN

### Neuer Container auf 178.104.15.187

Neuer Docker-Container für TJW — kein Coolify (direkt via SSH, wie bei CA-ähnlichen Setups).

```bash
# Container erstellen (einmalig, via SSH)
ssh root@178.104.15.187 "docker run -d \
  --name tjw-website \
  --restart unless-stopped \
  -p 8083:80 \
  nginx:alpine"
```

**Port-Mapping:** 8083 → Container 80 (Ports 8080–8082 vermutlich belegt durch Hardy/Leila/andere)

### nginx.conf (Projekt-Root, nach deploy-standard.md)

```nginx
server {
    listen 80;
    server_name _;
    root /usr/share/nginx/html;
    index index.html;

    gzip on;
    gzip_types text/plain text/css application/javascript image/svg+xml;

    location ~* \.html$ {
        add_header Cache-Control "no-cache, must-revalidate";
    }

    location ~* \.(js|css)$ {
        expires 1d;
        add_header Cache-Control "public, must-revalidate";
    }

    location ~* \.(png|jpg|jpeg|gif|svg|woff2|webp)$ {
        add_header Cache-Control "no-cache";
    }

    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

### Cloudflare (Proxy bereits aktiv laut design-state.md)

- Zone ID: `ca270615206033f4f792b422a7b81a2d`
- Token: `~/.cloudflare/token-tjw`
- DNS: A `@` + `www` → 178.104.15.187 (Proxy aktiv)
- Traefik-Routing: Coolify-Traefik auf 178.104.15.187 routet nach Host-Header → Container tjw-website:8083

**Traefik-Label (beim docker run ergänzen):**
```bash
--label "traefik.enable=true" \
--label "traefik.http.routers.tjw.rule=Host(\`tulumjunglewedding.com\`) || Host(\`www.tulumjunglewedding.com\`)" \
--label "traefik.http.routers.tjw.tls=true" \
--label "traefik.http.routers.tjw.tls.certresolver=letsencrypt" \
--label "traefik.http.services.tjw.loadbalancer.server.port=80"
```

### Deploy-Befehl (nach jedem Build)

```bash
npm run build && \
rsync -az --delete dist/ root@178.104.15.187:/tmp/tjw-dist/ && \
rsync nginx.conf root@178.104.15.187:/tmp/nginx-tjw.conf && \
ssh root@178.104.15.187 "docker cp /tmp/tjw-dist/. tjw-website:/usr/share/nginx/html/ && \
  docker cp /tmp/nginx-tjw.conf tjw-website:/etc/nginx/conf.d/default.conf && \
  docker exec tjw-website nginx -s reload"
```

### astro.config.mjs

```js
import { defineConfig } from 'astro/config';
import tailwind from '@astrojs/tailwind';

export default defineConfig({
  output: 'static',
  integrations: [tailwind()],
  build: {
    assets: '_astro'
  }
});
```

---

## 7. WEB3FORMS — KONTAKTFORMULAR

```astro
<!-- ContactForm.astro -->
<form action="https://api.web3forms.com/submit" method="POST">
  <input type="hidden" name="access_key" value="STEFAN_WEB3FORMS_KEY">
  <input type="hidden" name="subject" value="New Wedding Inquiry — Tulum Jungle Wedding">
  <input type="hidden" name="redirect" value="https://tulumjunglewedding.com/?thanks=1">

  <!-- Felder: First Name, Last Name, Email, Wedding Date, Guest Count, Vision (textarea) -->
</form>
```

**Access Key:** Stefan hat Web3Forms-Account (für CA genutzt) — gleicher Key oder neuer Key für TJW erstellen.

---

## 8. ABWEICHUNGEN VOM MOCKUP

### 1:1 umsetzbar (kein Unterschied)
- Alle Farben, Fonts, Spacing-Werte — exakt aus Mockup übernehmen
- Navigation (Text-Logo + 5 Links + CTA)
- S01 Hero mit Scarcity-Signal und Scroll-Indicator
- S03 Testimonial mit Reviews-Badge
- S04 StylesGrid (asymmetrisch)
- S05 Included-Grid (4 Photo-Cards)
- S07 Sustainability (zentriert)
- S09 FAQ (light-theme details/summary)
- S10 Kontaktformular (2-spaltig ab 1024px)
- Footer (minimal)

### Anpassungen nötig

| Punkt | Mockup | Astro-Build | Begründung |
|-------|--------|-------------|------------|
| Hero-Bild | `images/wedding-2.jpg` als `background-image` | `<Image>` Astro-Komponente mit `object-fit: cover` | Bessere Performance, LCP-Optimierung |
| WeddingGallery | Inline-CSS-Grid mit festen px-Höhen | CSS Grid in Komponente, Höhen als clamp() | Responsiveness |
| Video-Sektion | Nicht im Mockup vorhanden | Optional einbauen: `wedding-video-1080.mp4` vorhanden — `<video autoplay muted loop playsinline>` zwischen Gallery und S02 | Videos sind vorhanden, können als stilles Ambient-Video eingesetzt werden |
| Bilder `images/vg/` | Direktpfade im Mockup | In `src/assets/images/` legen oder aus `public/images/` referenzieren | Astro Image optimization |
| Google Fonts | Via CDN `<link>` im Mockup | `@fontsource/cormorant-garamond` + `@fontsource/dm-sans` als npm-Pakete — oder CDN-Link in BaseLayout | npm-Variante für self-hosting bevorzugen |
| FaqAccordion | Native `<details>/<summary>` | CA-Komponente als Basis anpassen — JS für rotate-Chevron und Accessibility (ARIA) ergänzen | CA-Komponente hat bereits guten Basis-Code |
| PricingSection | Vorhanden im Mockup nach FAQ | Im Plan als S06b zwischen S05 und S06 eingebaut — Reihenfolge gemäß Mockup-Entscheidung aus Phase 3 | Pricing kam nach dem ersten Mockup als Ergänzung dazu |

### Video: Ambient Loop (Optional, Empfehlung: JA einbauen)

`public/wedding-video-1080.mp4` ist vorhanden. Empfehlung: Als Full-Width-Sektion zwischen WeddingGallery und S02 einbauen (autoplay, muted, loop, playsinline, keine Controls). Gibt dem Funnel eine Premium-Qualität die Foto-Wettbewerber nicht haben.

---

## 9. TASK-LISTE FÜR SCHRITT 10

Reihenfolge für den Build (sequenziell, jeder Schritt auf vorherigem aufbauend):

1. **Astro-Projekt initialisieren** — `npm create astro@latest`, Tailwind v4 Plugin, Fontsource-Pakete
2. **global.css** — Design-Tokens, Reset, Shared-Classes (eyebrow, btn-primary, gold-line, section-heading)
3. **BaseLayout.astro** — HTML-Struktur, Fonts, Global CSS, NavBar-Slot, Footer-Slot
4. **NavBar.astro** — Fixed, scroll-behavior (JS), mobile-toggle
5. **HeroSection.astro** — Vollbild, Gradient, Scarcity, Scroll-Indicator
6. **WeddingGallery.astro** — 4-reihiges Grid, alle 8 Fotos (Mockup Row 1–4)
7. **SplitSection.astro** (adapt von CA) — light/dark theme, imagePosition prop
8. **TestimonialHero.astro + ReviewsBadge.astro** (adapt von CA)
9. **StylesGrid.astro** — 1 featured + 2 small
10. **IncludedGrid.astro** — 4 Photo-Cards
11. **FullWidthPool.astro** — Full-Width Image + Overlay
12. **PricingSection.astro** — 3 Karten, Featured-Badge
13. **SustainabilitySection.astro** — einfach
14. **FaqAccordion.astro** (adapt von CA) — light-theme
15. **ContactForm.astro** — Web3Forms
16. **FooterSimple.astro**
17. **index.astro** — alle Komponenten zusammensetzen, Props befüllen
18. **Lokal testen** — npm run dev, alle 5 Viewports prüfen
19. **Build + Deploy** auf 178.104.15.187

---

## 10. WICHTIGE NOTIZEN FÜR DEN BUILD

- **Mockup = visuelle Wahrheit** — kein Design-Entscheid während dem Build. Wenn etwas unklar ist, Mockup aufmachen.
- **Bildreferenzen:** Mockup nutzt `images/...` — im Astro-Build sind diese in `public/images/` (direkte URL-Referenz, kein Astro Image Service nötig wenn Bilder statisch aus public/ geladen werden)
- **CSS-Variablen:** Alle Spacing/Farb-Werte aus Mockup exakt kopieren — kein "ähnlich genug"
- **Keine Abweichungen von Mockup ohne explizite Entscheidung** — Ausnahme: Video-Sektion (optional)
- **Web3Forms Access Key:** Vor ContactForm.astro-Build bei Stefan erfragen oder aus CA-Repo holen
- **Astro Image:** `<Image>` von `astro:assets` für alle `<img>` im Build nutzen (LCP + Core Web Vitals)

---

*Plan Version 1.0 — 2026-04-14*
