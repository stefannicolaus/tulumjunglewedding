# Design-Workflow: tulumjunglewedding.com
Gestartet: 2026-04-13
Aktueller Schritt: 12
Typ: onepager
Client-Typ: Stefan/eigenständig — Luxury Wedding Venue für Casa Arkaana

## Gates
- [x] Style Guide approved (2026-04-13)
- [x] Mockup approved (2026-04-14)

## Schritte
- [x] 1 Discovery (Kontext in dieser Datei vollständig)
- [x] 2 Niche Research (bereits abgeschlossen, siehe Entscheidungslog)
- [x] 3 Architecture
- [x] 4 Testimonials + Voice
- [x] 5 Style Guide
- [x] 6 Mockup
- [x] 7 Copy
- [x] 8 Taste-Skill
- [x] 9 Implementierungsplan
- [x] 10 Build
- [x] 11 Staging Deploy
- [ ] 12 Visual Iteration
- [ ] 13 QC-Loop
- [ ] 13.5 UX-Roast (Top 1% Audit — Pflicht)
- [ ] 14 Accessibility + Metadata
- [ ] 15 Copy-Polish + Launch

## Pfade
Style Guide: public/tulumjunglewedding-style-guide.html
Mockup Homepage: public/tulumjunglewedding-homepage-mockup.html
Staging URL: http://178.104.15.187:8083/ (Container: tjw-website · DNS pending: Cloudflare NS noch nicht bei Hetzner Registrar eingetragen)
Projekt-Root: ~/code/tulumjunglewedding/

## Design-Tokens (aus Niche Research + Stefan-Entscheidung)
Basis: #FAFAF7 (Warm-Weiß)
Text: #1A1A18 (Fast-Schwarz)
Grün: #1D3828 (Dunkelgrün/Dschungel — tief, satt, Regenwald bei Nacht)
Gold: #B5904E (Champagner-Gold — matt, dezent, nie als Fläche)
Neutral: #8C8876 (Warm-Grau — Subtext, Captions)
Cream: #F2EDE5 (Karten-BG, sanfte Trenner)
Fonts: Cormorant Garamond 300/400/500 + DM Sans 300/400
Stil: Editorial Luxury, Nacht-im-Dschungel-Motive als Akzent auf weißem Grund
Anti-Pattern: KEIN durchgehend dunkler Hintergrund, kein Hochglanz-Wedding-Kitsch, kein Stock-Photo-Feeling

## Entscheidungslog

### Phase 1: Strategie

#### Discovery (Schritt 1)
- **Projekt:** tulumjunglewedding.com — separater Funnel für CA Wedding-Angebote
- **Verhältnis zu CA:** Eigene Domain, eigene Marke, können aufeinander verweisen. Zielgruppe komplett anders als CA-Retreat-Zielgruppe.
- **Stack:** Astro + Tailwind v4, Deploy Hetzner/Coolify
- **CA-Komponenten adaptieren:** PageHero, GalleryGrid, TestimonialCard, FaqAccordion, SplitSection, Footer, Header, Button
- **Kontaktformular:** Web3Forms

**Content (von casaarkaana.com/weddings gescrapt):**
- Headline: "A Jungle Wedding Venue for Sacred, Soulful Celebrations in Tulum"
- 3 Wedding-Stile: Retreat-Stil / Boho Jungle / Festival under the Stars
- Package: Venue 16–24 Uhr, 3 Nächte Unterkunft, String Lights, Lagerfeuer, Holztanzfläche, Altar, Welcome Drink etc.
- USP Sustainability: "3 Tage Feier — nur 2 Müllbeutel"
- Testimonial: "B & A 2024" — echtes Zitat vorhanden (Wortlaut aus CA-Site)
- Voice/Audience Research: "burned out", "soul family", "nervous system reset", "I almost didn't go" — Safety-Angst direkt ansprechen

**CA Brand-Details (aus memory/):**
- Pool aus Cenoten-Wasser — geografisch einmalig
- Temazcal vorhanden
- Living farm-acy (Mayas Begriff für Kräutergarten)
- Google Reviews: 55/56 Fünf-Sterne
- Bestes Testimonial (Alec): "I was a lost soul before arriving. I left with a second chance at life." (für allg. CA relevant, nicht Wedding-spezifisch)

**Content-Status:** 1 Wedding-Testimonial (B&A 2024) bestätigt. Weitere Quellen zu prüfen: ~/Obsidian/Stefan/, CA memory/MAYA-MEMORY.md, CA website src/.

#### Niche Research (Schritt 2) — bereits abgeschlossen
- **Azulik.com:** Monochrom, Serif "Freight Display", Luxus durch Understatement. Editorial.
- **Papaya Playa:** Beige + Schwarz, "Barefoot Luxury", Dschungel durch Minimalismus.
- **Northbound (lexingtonthemes.com/templates/northbound):** Editorial-Struktur ohne Wedding-Kitsch — Inspiration (kein Kauf)
- **Anti-Patterns (explizit verboten):**
  - Durchgehend dunkler Hintergrund — Stefan: "überwiegend klassisch weiß"
  - Hochglanz-Wedding-Kitsch (florale Ornamente, Schmetterlings-Icons, Roségold)
  - Symmetrische 3-Karten-Grids
  - Stock-Photo-Feeling
  - Generische "Book your dream wedding"-Sprache
- **Gewählte Richtung:** Editorial Luxury auf weißem Grund — Azulik-Understatement trifft Northbound-Struktur. Dschungel-Elemente als texturale Akzente, nicht als Hintergrundfarbe.

#### Architecture (Schritt 3)

**Onepager — 10 Sektionen (S01–S10)**

| # | Name | Conversion-Zweck | CA-Komponente |
|---|------|-----------------|---------------|
| S01 | **Hero — "A Jungle Wedding. Nothing Like Anything Else."** | Sofortiger Pattern-Break: kein Standard-Wedding-Kitsch, sondern Nacht-Dschungel-Editorial. Primärer CTA oben. | PageHero.astro (Vollbild, Titel links, CTA absolut unten) |
| S02 | **The Venue — Was hier anders ist** | Vertrauen durch Einzigartigkeit: Dschungel, Lagerfeuer, Holztanzfläche, Sapote-Baum — kein Hotel, kein Resort. | SplitSection.astro (Foto links, Text rechts) |
| S03 | **Safety Moment — "I Almost Didn't Go"** | Direkte Ansprache der Safety-Angst: Mexico-Bedenken, Abgeschiedenheit. Testimonial B&A als sozialer Beweis HIER. | TestimonialHero.astro (großes Zitat, kein Karten-Grid) |
| S04 | **The Three Styles** | Zeige dass CA 3 verschiedene Visionen bedienen kann — Retreat-Stil / Boho Jungle / Festival under the Stars. Kein Paketkauf nötig, nur Anfragen. | GalleryGrid.astro (3 Bilder mit Stil-Label) |
| S05 | **What's Included** | Konkretes Package-Vertrauen aufbauen: Venue 16–24h, 3 Nächte, String Lights, Feuer, Tanzfläche, Altar, Welcome Drink. | SectionWrapper + FactCard.astro (Icon-Liste, kein Tabellen-Grid) |
| S06 | **The Sapote Tree** | Emotionaler Höhepunkt — der älteste Baum auf dem Gelände als Zeremonieort. Story verkauft, kein Preis. Sekundärer CTA hier. | SplitSection.astro (Baum-Foto, Zitat in Large Serif) |
| S07 | **Sustainability Story** | USP-Differenzierung: "3 Tage Feier — nur 2 Müllbeutel." Spricht die Anti-Convention-Wedding Zielgruppe direkt an. | EyebrowLabel + kurze Text-Sektion, kein eigenes Komponenten-Container nötig |
| S08 | **The Hosts — Maja & Asdru** | Gesichter und Geschichte: Mexikaner, Dschungel-Aufbauer, keine anonymen Venue-Manager. Baut finales Vertrauen vor CTA. | SplitSection.astro (Foto, persönliches Statement) |
| S09 | **FAQ** | Nimmt 5 konkrete Einwände weg (Anreise, Gruppensize, Catering, Ceremony-Optionen, Preis-Transparenz). | FaqAccordion.astro |
| S10 | **Kontaktformular — Primärer CTA** | Conversion-Endpunkt: einfaches Inquiry-Formular (Name, Datum, Gästezahl, Vision), kein Buchungssystem. | SectionWrapper + Web3Forms |

**CTA-Positionen:**
- Primärer CTA: S01 Hero ("Start Planning Your Wedding") + S10 Formular
- Sekundärer CTA: S06 Sapote ("Tell Us Your Vision") — für Paare die noch browsen

**Komponenten-Mapping (5 wichtigste):**
1. PageHero.astro → S01 Hero (anpassen: helles Bild nachts, Titel Cormorant Garamond weight 300, CTA-Button btn-primary in Champagner)
2. TestimonialHero.astro → S03 Safety Moment (B&A Zitat groß, kein Karten-Layout)
3. SplitSection.astro → S02 + S06 + S08 (3× verwenden, abwechselnde Bildseiten)
4. FaqAccordion.astro → S09 FAQ (minimal Restyling nötig, hell statt dunkel)
5. GalleryGrid.astro → S04 Three Styles (3-spaltig mit Style-Labels als Overlay-Text)

#### Content + Testimonials (Schritt 4)

**Wedding-spezifische Testimonials:**

| # | Text | Quelle | Typ | Verwenden |
|---|------|--------|-----|-----------|
| 1 | "Choosing Casa Arkaana was the best decision. From the very beginning, Mila, Maja, and Asdrubal welcomed us and supported us in bringing our vision to life. The closeness to nature made the wedding truly magical. The experience was unique -- we spent three days there, enjoying the jungle, and left feeling renewed. If we had the chance, we would do it all over again." | B & A 2024 — aus `research/website-content-audit-2026-04-02.md` | Person→Klient (direkt übernehmen) | S03 Safety Moment, Hauptzitat |

**Allgemeine CA Testimonials (relevant für Wedding-Kontext):**

| # | Text | Quelle | Typ | Verwenden |
|---|------|--------|-----|-----------|
| 2 | "The best place to have a wonderful ceremony in the Maloka and to rest and digest near the pool. You will feel the love they put in the place." | Google Maps Review — `research/google-maps-reviews-2026-02.md` | Person→Klient | S08 Hosts oder FAQ-Sektion |
| 3 | "Had a beautiful weekend of ceremony at Casa Arkaana! The accommodations were lovely, the nature with bird sounds, the temple space, food they provided was delicious. Asdrubal and Maya are such great hosts and had a really warm welcome to their home." | Google Maps Review — `research/google-maps-reviews-2026-02.md` | Person→Klient | S08 Hosts oder S02 Venue |

**Asdru-Zitate (aus Brainstorming — Voice of Owner, für Copy-Basis):**
- "We've had two weddings without promoting them. People just look for a place — a micro wedding in the jungle — and we tend to be affordable for them." → Belegt organische Nachfrage, für S02 oder FAQ nutzbar
- "If weddings were bringing 10 or 20 percent of your income, then why not having this channel? But maybe it makes sense to have two websites — and then the wedding website gets so much more clarity. It's easier to target. It's easier to canalize. Absolutely." → Strategische Bestätigung des separaten Funnels (intern, nicht publizieren)

**Voice-Status:**
- MAYA-MEMORY.md: kein wedding-spezifischer Content vorhanden (zu allgemein)
- daniel-retreat-strategy.md: kein wedding-relevanter Content
- voc-online-research-2026-02.md: Audience-Voice vorhanden (Retreat, nicht Wedding)
- google-maps-reviews-2026-02.md: 2 nutzbare allgemeine Testimonials gefunden
- brainstorming-10-03-2026-2-3-analysis.md: Owner-Voice zum Wedding-Thema gefunden
- website-content-audit-2026-04-02.md: B&A 2024 — EINZIGES echtes Wedding-Testimonial

**Content-Status:** 1 Wedding-Testimonial (B&A 2024, direkt nutzbar) + 2 allgemeine CA Testimonials + Owner-Voice (Asdru-Zitat für Copy-Inspiration). Keine weiteren Wedding-Testimonials in Obsidian oder CA Repo gefunden. Für Mockup reicht B&A 2024 als Hauptzitat.

### Phase 2: Design System
- Farb-Entscheidungen: BG #FAFAF7 (warm, organisch), Text #1A1A18 (weich statt reines Schwarz), Grün #1D3828 (Regenwald bei Nacht — tiefer als CA's #1e2018, mehr grün), Gold #B5904E (matter Champagner — dezenter als CA's #b49c6e), Neutral #8C8876 (warm-grau, kein kühles Grau)
- Font-Entscheidungen: Cormorant Garamond (Emotion, Eleganz, weight 300 als Basis) + DM Sans (Lesbarkeit, modern, weight 300)
- Design-Principles: R01 Weißraum, R02 Serif/Sans-Rollen, R03 Grün als Pause, R04 Gold nur als Linie, R05 Foto hat Vorrang
- Style Guide Feedback: [leer — wartet auf Stefan]

### Phase 3: Mockup
- Mockup-Methode: Direkt gebaut (HTML)
- Struktur-Entscheidungen: S04 asymmetrisch (1 featured Boho Jungle + 2 klein), S03 Großzitat statt Card-Grid, max 2 dunkle Sections (Hero + S06 Sapote)
- Taste-Skill Findings: (1) Buttons: transform translateY(-2px) + gold box-shadow auf allen hover-States (btn-primary, btn-primary--light, form__submit). (2) S03 Testimonial: font-size von clamp(22px) auf clamp(28px) angehoben, Attribution auf 11px/letter-spacing 0.18em/uppercase. (3) Nav-Links: Underline-Animation via ::after pseudo-element (width 0→100% on hover). (4) S04 Three Styles: small-pair auf grid-template-rows: 1fr 1fr gesetzt damit beide Items die volle Spalten-Höhe füllen. (5) S05 Included Header: Von single-col auf 2-col editorial Layout (Heading links, Sub rechts auf gleicher Baseline). (6) S07 Sustainability: Generische cream border-top/border-bottom entfernt. S06 Sapote: box-shadow inset als Übergangs-Signal zum weißen Bereich. Split-Sections: 55/45 statt 50/50 für mehr visuelle Asymmetrie.
- Mockup Feedback: [leer — wartet auf Stefan]
- Competitor Research Additions (2026-04-13): (1) Scarcity signal in Hero — "3 dates still available for 2026" with green pulse dot below CTA. (2) Google Reviews badge after B&A testimonial — "55 of 56 reviews · Google" in bordered widget. (3) Pricing section (new S06) after What's Included: 3 tiers — The Roots $2,500–3,000 / The Tree $4,500–5,500 (featured) / The Bloom $7,000–9,000. Inspired by Kima Tulum + Azulik transparent-tier strategies. "Packages" added to nav.

### Phase 4: Build

#### Implementierungsplan (Schritt 9) — 2026-04-14

**Plan:** `docs/superpowers/plans/2026-04-14-tjw-build-plan.md`

**21st.dev Ergebnis (bu-scout, 2026-04-14):**
- ADOPT: Clean Testimonial (lucasheriques) + Scroll Media Expansion Hero (aceternity-style)
- ADAPT: FAQ Accordion (originui) + Masonry Gallery + Minimal Nav
- BUILD: Pricing Cards (3-Tier Featured) + Contact Form (Web3Forms)
- Details: docs/superpowers/plans/2026-04-14-tjw-build-plan.md Sektion 1

**Shared Components (16 Dateien in src/components/):**
- NavBar.astro — neu (scroll-behavior, Text-Logo)
- HeroSection.astro — neu (Vollbild, Scarcity-Signal)
- EyebrowLabel.astro — adapt CA
- WeddingGallery.astro — neu (4-reihiges Custom-Grid)
- SplitSection.astro — adapt CA (light-theme)
- TestimonialHero.astro — adapt CA (light-theme)
- ReviewsBadge.astro — adapt CA GoogleReviewsBadge
- StylesGrid.astro — neu (1 featured + 2 small)
- IncludedGrid.astro — neu (4 Photo-Cards)
- FullWidthPool.astro — neu (Full-Width Image + Overlay)
- PricingSection.astro — neu (3 Tiers, Featured-Badge)
- SustainabilitySection.astro — neu (einfach)
- FaqAccordion.astro — adapt CA (light-theme)
- ContactForm.astro — neu (Web3Forms)
- FooterSimple.astro — neu (minimal)
- GoldLine.astro — Utility (oder als CSS-Klasse)

**Deploy:** Neuer Container `tjw-website` auf 178.104.15.187, Port 8083, Traefik-Labels für tulumjunglewedding.com

#### Build-Entscheidungen (Schritt 10) — 2026-04-14

**Stack:** Astro 6 (minimal template), statischer Export, kein Tailwind — vanilla CSS + Custom Properties exakt aus Mockup.

**16 Komponenten gebaut:**
- NavBar.astro — scroll-behavior JS, Text-Logo, 5 Links, sticky
- HeroSection.astro — Vollbild, Gradient, Scarcity-Dot (Puls), Scroll-Indicator
- WeddingGallery.astro — 4-reihiges Custom-Grid, 8 Fotos, responsive Höhen
- VenueSection.astro — Split 55/45, Image+Label, Detail-List
- PoolSection.astro — Full-Width, Gradient-Caption
- TestimonialSection.astro — Großzitat, ::before Anführungszeichen, Reviews-Badge
- StylesGrid.astro — 1 featured (3fr) + 2 small (2fr), background-image
- IncludedGrid.astro — 7 Photo-Cards, 2-col mobile / 4-col desktop
- AvailabilityStrip.astro — Dark green Banner
- PricingSection.astro — 3 Tiers, Featured-Badge, Gold-Divider
- SapoteSection.astro — Split reversed (Text links / Bild rechts), Cream-BG
- SustainabilitySection.astro — Zentriert, Serif-Stat, Gold-Line
- HostsSection.astro — Split mit Pull-Quote Box
- FaqSection.astro — details/summary, Chevron-Rotation, FAQPage Schema
- ContactForm.astro — Web3Forms (STEFAN_WEB3FORMS_KEY Placeholder), 2-col ab 1024px
- FooterSimple.astro — Dark Footer, 6 Links, CA-Backlink

**Abweichungen vom Mockup:**
- Video-Sektion: NICHT eingebaut — `drone-web.mp4` nicht vorhanden, nur `wedding-video-1080.mp4` in public/. Empfehlung: in Schritt 12 als Optional einbauen.
- Google Fonts: CDN-Link (wie Mockup) statt npm-Package — Build-Zeit kürzer, kein self-hosting.

**Deploy:** Container `tjw-website` auf 178.104.15.187:8083, Traefik-Labels für tulumjunglewedding.com gesetzt.
**DNS-Blocker:** tulumjunglewedding.com löst noch auf Hetzner-Registrar (88.198.219.246). Cloudflare NS (bella + guss) müssen bei Hetzner Registrar eingetragen werden → dann läuft HTTPS über Traefik.

### Phase 5: Polish
[AUSSTEHEND]

## Domain + Hosting
- Domain: tulumjunglewedding.com ✅ registriert (Hetzner)
- Cloudflare Zone ID: ca270615206033f4f792b422a7b81a2d
- Cloudflare Token: ~/.cloudflare/token-tjw
- DNS: A-Records @ + www → 178.104.15.187 ✅ (Cloudflare Proxy aktiv)
- Nameserver: bella.ns.cloudflare.com + guss.ns.cloudflare.com ← MUSS bei Hetzner eingetragen werden
- Deploy: Hetzner/Coolify, neuer Container nötig (nach Style Guide Approval)

## SEO-Ziele
- Primary Keywords: "tulum jungle wedding", "jungle wedding tulum"
- Secondary: "destination wedding mexico", "destination wedding tulum"
- Schema: WeddingBusiness + FAQPage (astro-seo-schema npm package)
- Domain: tulumjunglewedding.com (noch zu registrieren)

## Technische Basis
- CA-Astro-Komponenten vorhanden in: ~/code/CasaArkaana/website/src/components/
- Verfügbar: PageHero, GalleryGrid, TestimonialCard, FaqAccordion, SplitSection, Footer, Header, Button, SectionWrapper, EyebrowLabel, ParallaxDivider
