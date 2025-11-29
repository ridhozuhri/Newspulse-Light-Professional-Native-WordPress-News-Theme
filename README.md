# Newspulse Light — Professional Native WordPress News Theme

Newspulse Light is a production‑ready, native WordPress theme engineered for modern newsrooms. It focuses on speed, readability, and credibility — no page builders, no external CSS/JS frameworks, and zero plugin dependency required for core UX/SEO.

## Highlights
- Native WordPress, zero plugin dependency for core UX/SEO
- Mobile‑first, performance‑first (small assets, lazy images)
- Next.js‑like navigation (PJAX‑style) with history + fallback
- Modular templates and CSS, minimal vanilla JS (≤ 3 KB)
- Professional newsroom patterns: hero spotlight, ticker, grids, two sidebars (desktop), clean typography

## Theme Structure
```
newspulse-light/
├─ style.css                 # Theme header only
├─ functions.php             # Bootstrap (enqueue, SEO, Customizer, REST)
├─ header.php, footer.php    # Global layout (header utils, social, search)
├─ index.php                 # Home + default listing
├─ single.php, page.php      # Article & page view
├─ archive.php, search.php, 404.php
├─ inc/
│  ├─ setup.php              # add_theme_support, menus, sidebars, image sizes
│  └─ template-functions.php # Helpers (SEO, JSON-LD, meta, breadcrumbs, utils)
├─ template-parts/
│  ├─ layout/
│  │  ├─ header-brand.php
│  │  ├─ header-nav.php      # Responsive nav (+ mobile drawer)
│  │  └─ header-utils.php    # Search popover + social icons
│  ├─ content/
│  │  ├─ hero-simple.php     # Hero spotlight (1 big image + 4 titles)
│  │  ├─ card.php, hero.php (legacy minimal), post-meta.php
│  └─ ui/
│     ├─ ticker.php          # Breaking ticker (home only)
│     └─ share-buttons.php   # Native share links
├─ assets/
│  ├─ css/
│  │  ├─ base.css            # Reset, variables, typography
│  │  ├─ layout.css          # Header, nav, grids, footer, single
│  │  ├─ components.css      # Cards, hero, ticker, widgets, pagination
│  │  └─ pages.css           # Page‑level extras
│  └─ js/
│     ├─ core.js             # PJAX‑style transitions
│     └─ ui.js               # Dropdowns, mobile menu, ticker/live refresh
└─ README.md
```

## Core Features
- 100% native WordPress (no external frameworks)
- SEO & Social
  - Title via `add_theme_support('title-tag')`
  - Automatic meta description
  - Open Graph + Twitter Card
  - Canonical + `amphtml` link
  - JSON‑LD: `WebSite` (sitewide) and `NewsArticle` (single)
  - Clean archive titles, breadcrumbs for single/archive/search
- Accessibility & Responsiveness
  - Mobile‑first, touch targets ≥ 48px, color contrast AA‑oriented
  - Images `loading="lazy"` + descriptive `alt` fallback
- Performance
  - CSS modular, no heavy libraries
  - JS tiny, vanilla only
  - Inter font via Google Fonts `display=swap` (preconnect+preload stylesheet)
- AMP friendliness
  - `add_theme_support('amp')` (non‑invasive)
  - Theme avoids incompatible patterns; JS gracefully no‑ops on `?amp=1`
- Page Transitions (Next.js feel)
  - Intercepts internal links, fetches, swaps `#main-content`, pushes history, updates title
  - Back/forward reloads page; full fallback when JS disabled

## Layout & Components
- Header
  - Brand/logo (Customizer), primary nav with dropdowns
  - Mobile drawer menu + backdrop, colors follow theme accent
  - Search popover (click icon → inline form; responsive full‑width on mobile)
  - Social icons (SVG inline) header (white) and footer (black)
- Breaking Ticker (Home only)
  - Sticky bar above header, auto‑scroll marquee, pause on hover
  - REST refresh every 5 minutes (`/wp-json/newspulse/v1/breaking`)
- Hero Section (Home)
  - “Hero Simple”: 1 big image (16:9) with overlay headline inside image
  - Category badge inside image (breaking badge suppressed as requested)
  - Below hero: list of 4 titles (no images) with hover highlight
- News Grid
  - 1‑column full (desktop & mobile) with breathable padding on desktop
  - Cards: 16:9 thumb, bold title (2‑line clamp), meta “Oleh … • Tanggal”, excerpt (20 words)
  - Hover: gentle shadow + image micro‑zoom (0.2s)
- Article (Single)
  - Max width 720px, full‑width featured image
  - H1 title, read‑time line (⏱️ X menit baca)
  - Meta: author, date (format internasional: `j F Y`), categories (internal links)
  - Native share buttons (WA, Twitter/X, Facebook)
  - Related posts (3), small card grid
- Sidebars & Footer
  - Desktop: dual sidebars (left 300px, right 320px) on listing pages (archive/search/index)
  - Mobile: sidebars hidden (focus on content)
  - Footer: 3 columns (about/links/social) + copyright bar with accent color

## Widgets (Dashboard → Appearance → Widgets)
Built‑in professional widgets (limit 3 per sidebar; search/recent‑comments filtered out):
- Newspulse: Iklan (300×250 / 300×600)
- Newspulse: Trending 7 Hari (views rolling meta)
- Newspulse: Artikel Populer (comment count)
- Newspulse: Topik Utama (kategori)
- Newspulse: Newsletter CTA (title + text + button)
- Newspulse: Editor Picks (sticky posts or chosen category)
- Newspulse: Terbanyak Komentar (last 30 days)
- Newspulse: Video Terbaru (post format video)
- Newspulse: Ikuti Kami (uses theme social links)

Activation defaults (if sidebars empty):
- Right: Ad 300×250, Trending 7 Hari, Categories
- Left: Categories, Artikel Populer, Ad 300×250

## Customizer
- Logo (custom‑logo)
- Accent Color (CSS var `--accent`)
- Footer Description / titles and Copyright text
- Social Links (Twitter/X, Facebook, YouTube, Instagram)

## Image Sizes
- `newspulse-hero` 1200×630 (16:9, hard crop)
- `newspulse-card` 600×338 (16:9)
- `newspulse-thumb-sm` 80×50 (sidebar list)
- `newspulse-4x3` 240×180 (secondary list)

## JavaScript
- `core.js` (PJAX):
  - Intercepts internal links → fetch → swap `#main-content` → pushState → scroll to top
  - Back/forward triggers reload for robustness
- `ui.js` (UI glue):
  - Dropdown menus (tap/hover), click‑outside close
  - Mobile menu drawer (toggle, ESC/backdrop close)
  - Search popover toggle (desktop & responsive mobile bar)
  - Breaking ticker refresh (5 min), Live updates refresh (60 s)

## REST Endpoints
- `GET /wp-json/newspulse/v1/breaking` → latest 5 posts in category `breaking`
- `GET /wp-json/newspulse/v1/live` → latest 5 posts in category `live` (for hero sidebar live feed)

## SEO & Schema
- Meta description (auto), Canonical, Open Graph, Twitter Card
- JSON‑LD `WebSite` + `NewsArticle`
- Archive titles cleaned; breadcrumbs on single/archive/search

## Styling (CSS)
- Variables in `base.css` (`--accent`, `--bg`, `--text`, etc.)
- Layouts in `layout.css` (header/nav/footer/grids/single)
- Components in `components.css` (cards, hero, ticker, widgets, pagination)
- Page‑specific in `pages.css`

## Accessibility
- Color contrast mindful; text shadows only for overlay readability
- `sr-only` labels for icon‑only links (social/search)
- Touch targets ≥ 48×48 px

## Mobile Behavior
- Sidebars hidden, content full width
- Search popover becomes fixed bar below header
- Nav becomes drawer with backdrop

## How to Use
1. Activate the theme (Appearance → Themes → Newspulse Light)
2. Assign menus to “Primary Menu” and “Footer Quick Links”
3. Customize (Appearance → Customize): Logo, Accent Color, Footer text, Social URLs
4. Create categories (including `breaking` and optional `live`)
5. Add widgets to “Sidebar Kiri” and “Sidebar Utama” (desktop only)

## Notes
- Breaking badge is intentionally hidden for category `breaking` (requested behavior)
- Hero Simple is default: 1 image + 4 titles; lightweight, non‑intrusive
- Grid is 1 column by design (can be extended to 2/3 easily)

## Editing & Extending
- Modify hero behavior: `template-parts/content/hero-simple.php`
- Add/adjust widgets: `inc/setup.php` (widget classes)
- Helpers/SEO: `inc/template-functions.php`
- Page transitions: `assets/js/core.js`

## License
This theme does not include a license header by default. Add your preferred license and attribution as required by your project or organization.

