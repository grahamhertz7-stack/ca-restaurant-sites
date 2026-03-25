# Restaurant Site Style Guide
## Reference: MexiNica Taco Truck (`mexicanica-taco-truck.html`)

All new sites should match this design system. When rebuilding existing sites, migrate them to this standard.

---

## Design Philosophy
- **Light background, not dark.** Body bg: `#fafaf8` (--white), not black.
- **Typography-first.** Big, bold display headings with serif italics for personality.
- **Premium but approachable.** Clean whitespace, subtle shadows, no loud neon.
- **Bilingual (EN/ES) by default** for Spanish-speaking restaurant audiences.

---

## Fonts (Google Fonts)
```html
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=Instrument+Serif:ital@0;1&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
```
- **Syne** — headings, nav logo, section titles, stats (bold/800)
- **Instrument Serif italic** — accent words in titles, quotes, taglines
- **DM Sans** — body copy, buttons, labels, meta text

---

## Color Tokens
```css
:root {
  --white: #fafaf8;
  --black: #111110;
  --red: #c93030;        /* primary accent — swap per restaurant's vibe */
  --green: #2a6e3f;      /* secondary (unused in MexiNica but available) */
  --mist: #f2f2f0;       /* alternate section bg */
  --mid: #777772;        /* muted text */
  --border: rgba(17,17,16,0.08);
}
```
**Per-restaurant accent color:** swap `--red` to match the restaurant's cuisine/culture. Examples:
- Mexican/Latin: `#c93030` (red) or `#d97706` (warm amber)
- Seafood: `#0e7490` (teal/ocean)
- BBQ/soul food: `#92400e` (burnt orange/brown)
- Korean: `#7c3aed` (deep purple) or `#dc2626` (red)
- Caribbean/Jamaican: `#059669` (green) + `#f59e0b` (gold)

---

## Page Structure (in order)
1. **Fixed Nav** — logo + links + "Find Us" CTA button + optional lang toggle
2. **Hero** — 2-col grid: left (headline + subtitle + CTAs), right (feature card with emoji + quote)
3. **Scrolling Strip** — black bar, marquee of keywords (rating, cuisine, location, price, tagline)
4. **About Section** — 2-col: left (eyebrow + title + body + phone CTA + stats), right (pull quote block)
5. **Menu Section** — mist bg, 3-col card grid (emoji + name + desc + price tag)
6. **Reviews Section** — white bg, 3-col cards (stars + italic quote + author)
7. **CTA / Visit Section** — black bg, big headline, call + maps buttons, info strip (hours/service/location/price)
8. **Footer** — logo + tagline + copyright

---

## Key Components

### Fixed Nav
```html
<nav> <!-- position: fixed; backdrop-filter: blur(16px) -->
  <div class="nav-logo">Name<span>Accent</span></div>
  <ul class="nav-links">...</ul>
  <div class="lang-toggle">EN / ES buttons</div>
</nav>
```

### Hero
- Left col: `hero-tag` pill → big `hero-title` (Syne 800, clamp 3rem–6rem) → subtitle (DM Sans 300) → action buttons
- Right col: `hero-card` with oversized emoji, card title, body text, location dot strip
- Hero right column is `display: none` on mobile (<900px)
- Fade-up entrance animations on load

### Scrolling Strip
- `overflow: hidden`, `animation: stripScroll 22s linear infinite`
- Duplicate items (2x) for seamless loop
- Items: rating · cuisine · location · price range · signature dish

### Section Headers
```html
<p class="section-eyebrow">SHORT LABEL</p>  <!-- uppercase, tracked, --red -->
<h2 class="section-title">Main <em>Title</em></h2>  <!-- Syne 800, em = Instrument Serif italic -->
```

### Menu Cards (3-col grid)
```html
<div class="menu-card">
  <span class="menu-emoji">🌮</span>
  <div class="menu-name">Category Name</div>
  <p class="menu-desc">Items with prices</p>
  <span class="menu-tag">From $X</span>
</div>
```

### Review Cards (3-col grid)
```html
<div class="review-card">
  <div class="review-stars">★★★★★</div>
  <p class="review-text">"Quote in Instrument Serif italic"</p>
  <div class="review-author">Name · Source</div>
</div>
```

### CTA Info Strip
```html
<div class="info-block">
  <div class="info-lbl">LABEL</div>
  <div class="info-val">Value</div>
</div>
```

---

## Bilingual Setup
- All user-facing text elements get `data-en` and `data-es` attributes
- JS `setLang(lang)` swaps innerHTML from the correct attribute
- Two toggle buttons (nav + floating bottom-right)
- For restaurants where Spanish isn't relevant, the toggle can be omitted

---

## Scroll Reveal Animation
```css
.reveal { opacity: 0; transform: translateY(20px); transition: opacity 0.7s ease, transform 0.7s ease; }
.reveal.visible { opacity: 1; transform: translateY(0); }
.reveal-delay-1 { transition-delay: 0.1s; }
.reveal-delay-2 { transition-delay: 0.2s; }
```
```js
const observer = new IntersectionObserver(...);
document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
```

---

## Buttons
| Class | Style |
|-------|-------|
| `.btn-primary` | Black bg, white text → hover: red + lift |
| `.btn-secondary` | Transparent, border → hover: black border + lift |
| `.btn-white` | White bg, black text → hover: red bg |
| `.btn-outline-white` | Transparent, white border → hover: solid white border |

---

## Responsive Breakpoints
- `< 900px`: hide nav links, stack hero to 1-col, hide hero right card, stack about/menu to 1-col, reviews to 1-col
- `< 600px`: menu grid to 1-col

---

## Existing Sites to Rebuild
These currently use the old dark template and should be migrated:
- [x] nakas-broiler.html
- [x] las-islas-marias.html
- [x] callos-la-rosca.html
- [x] pupuseria-la-ceiba.html
- [x] mis-amigos-tacos.html
- [x] submarine-crab.html
- [x] don-chema.html
- [x] dominguez-tacos.html
- [x] honduras-mi-sabor.html
- [x] ten-raku-korean-bbq.html
- [x] mexicanica-taco-truck.html ← reference design

---

## Per-Site Checklist
- [ ] Correct accent color for cuisine type
- [ ] Real phone number in `tel:` links
- [ ] Real Google Maps link (place_id or address search)
- [ ] Real Google Photos carousel images (Places API)
- [ ] Real reviews (3 minimum, pulled from Google)
- [ ] Accurate menu items with prices
- [ ] Accurate hours
- [ ] Bilingual EN/ES on all user-facing text
- [ ] Scroll reveal on section content
- [ ] Mobile responsive
