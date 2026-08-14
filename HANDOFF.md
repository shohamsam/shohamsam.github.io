# Portfolio Site Handoff

## Overview
Shoham Samuel's portfolio site — static HTML/CSS/JS, hosted on GitHub Pages.

- **Live URL:** https://shohamsam.github.io
- **Local repo:** `~/Documents/GitHub/shohamsam.github.io`
- **GitHub Desktop** is used for commits and pushes (personal account: `shohamsam`)
- No build tools, no frameworks — plain HTML files

---

## Repository Structure

```
shohamsam.github.io/
├── index.html                  ← Homepage (card grid, 6 cards)
├── images/
│   └── shoham.png              ← Profile photo (used in hero)
├── .nojekyll                   ← Prevents GitHub Pages from running Jekyll
├── lifecycle-editor/           ← Case study
├── eot-redesign/               ← Case study (End of Trial Redesign)
├── cve-sidecar/                ← Case study
├── network-discovery/          ← Case study (Atera)
├── pricing-pages/              ← Case study (Codefresh self-service checkout) ← BUILT THIS SESSION
│   ├── index.html
│   └── images/
│       ├── hero.png                ← Full product composite (opening image)
│       ├── contact-sales.png       ← The "before" — contact form marketing page
│       ├── pricing-phase-1.png     ← Phase 1 subscription page (usage bars + plan card)
│       ├── pricing-phase-1-checkout.png ← Phase 1 checkout modal (support tier cards)
│       ├── pricing-phase-2-1.png   ← Phase 2 configurator (sliders, presets, live total)
│       ├── pricing-phase-2-2.png   ← Phase 2 configurator (alternate state)
│       ├── pricing-phase-2-3.png   ← Phase 2 checkout modal (2-column layout)
│       ├── isometric.png           ← Isometric 3D render of "Need more Clusters?" card
│       ├── ds-colors.png           ← 6-colour palette strip (2072×340px, horizontal)
│       ├── ds-typography.png       ← Type scale: Heading L–XS
│       ├── ds-icons.png            ← 25 line icons grid on blue-gray background
│       ├── ds-components.png       ← Component library (icons, buttons, toggles, sliders, etc.)
│       ├── ds-components-2.png     ← Component library pt.2 (form controls, table, dialogs)
│       └── ds-light-dark.png       ← Credit card form in light and dark mode side by side
└── runtime-case-study/         ← Case study (Codefresh, moved from separate repo)
    ├── index.html
    ├── support.js
    └── assets/
```

---

## Design Tokens (CSS variables)
Used across ALL case studies — do not deviate from these.

```css
--ink:    #0d1117       /* primary text */
--ink-2:  #3d4550       /* secondary text, body copy */
--ink-3:  #6b7280       /* captions, labels, muted */
--rule:   #e5e7eb       /* borders, dividers */
--bg:     #ffffff
--bg-warm:#fafaf9       /* hero background, image backgrounds */
--bg-gray:#f6f6f6       /* gray band sections */
--accent: #7673fe       /* stat numbers, callout borders */
--f-serif:'Instrument Serif', Georgia, serif
--f-sans: 'Inter', system-ui, sans-serif
```

**h2:** Instrument Serif italic, `clamp(28px, 4vw, 40px)`, weight 400
**p:** 17px, `--ink-2`, line-height 1.75
**nav height:** 60px fixed, frosted glass

---

## Homepage (`index.html`)

### Hero
- "Hello, I'm" greeting → large Instrument Serif name → role text → skill chips
- Profile photo inline with name: `<span class="hero-avatar">` — purple `#7673FE` background, 16px border radius, `height: 0.72em; width: calc(0.72em * 0.924)` (scales with font)
- Photo file: `images/shoham.png`

### Card Grid
**6 case study cards** in a 2-column grid (`max-width: 1060px`). Order:
1. Lifecycle Editor — full-bleed video thumbnail
2. Codefresh Runtime Installation — full-bleed video thumbnail ← links now use relative paths (`runtime-case-study/`)
3. CVE Sidecar — `#0170CD` blue background, image at 80% size
4. End of Trial Redesign — full-bleed screenshot thumbnail
5. Network Discovery — `#f0f4f8` background, image at 80% size
6. **Self-Service Checkout** — `#eef2ff` (light indigo) background, `pricing-phase-2-1.png` at 85% size ← ADDED THIS SESSION

### Hidden section
"There's more / My full portfolio lives in Figma" section has `display: none` — can be re-enabled if needed.

---

## Case Study Nav Pattern
Every case study uses the same nav. **Never add a back link on the right** — that was a duplicate and was removed.

```html
<nav>
  <a class="nav-name" href="/">Works</a>
</nav>
```

---

## Pricing Pages Case Study (`pricing-pages/`) — BUILT THIS SESSION

### Design direction
Inspired by Adham Dannaway's portfolio (https://www.adhamdannaway.com/portfolio/figma-design-system):
- Image-first, editorial, all white background
- Minimal prose — text frames visuals, doesn't replace them
- No alternating gray bands (unlike the old stub)
- Lightbox on all images (click to zoom, Escape to close)

### Structure
Two-part page with section dividers:

**Part 1 — The Work (case study)**
1. Text hero + meta bar
2. `hero.png` (wide-img) — full product composite
3. Context: PLG transition, from contact form to self-serve (2 paragraphs + `contact-sales.png`)
4. Phase 1: Fixed plan + inline checkout (2-column image pair: `pricing-phase-1.png` + `pricing-phase-1-checkout.png`)
5. Phase 2: Live configurator + checkout (`pricing-phase-2-1.png` wide + `pricing-phase-2-3.png`)
6. `isometric.png` — visual transition moment (centered, drop-shadow, no card border)

**Divider:** `── The Design System ──`

**Part 2 — The Design System (UI deep dive)**
7. Colour — `ds-colors.png` (6 swatches: teal, dark navy, blue, silver, sky, near-white)
8. Typography — `ds-typography.png` (Heading L 26px → Label XS 10px)
9. Icons — `ds-icons.png` (25 line icons, utility set)
10. Components — `ds-components.png` + `ds-components-2.png` (stacked)
11. Light & dark — `ds-light-dark.png` (credit card form, both modes)

**Divider:** `── Outcome ──`

12. Outcome text + 3-stat block (+25% customers / First self-serve checkout / 2 phases)

### Key CSS patterns (pricing-pages specific)
```css
/* Two-column image pair */
.img-pair { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; margin: 32px 0; }

/* Isometric image (no card, just shadow) */
.iso-wrap { display: flex; justify-content: center; padding: 40px 24px 64px; }
.iso-wrap img { width: 380px; filter: drop-shadow(0 8px 32px rgba(0,0,0,0.10)); }

/* Section bridge divider */
.section-bridge { display: flex; align-items: center; gap: 20px; max-width: 740px; margin: 0 auto; padding: 0 24px 64px; }
.section-bridge-rule { flex: 1; height: 1px; background: var(--rule); }
.section-bridge-label { font-size: 11px; font-weight: 600; letter-spacing: 0.14em; text-transform: uppercase; color: var(--ink-3); }
```

### Content facts
- Company: Codefresh by Octopus Deploy
- Role: Senior Product Designer
- Phase 1: Fixed plan at $4,170/year — first self-serve checkout
- Phase 2: Live configurator — sliders (clusters + ArgoCD apps), presets (Startup / Growing Company / Multi-Department), annual/monthly toggle (20% discount), total updates live
- Add-ons: $1,500/cluster, $1,500/100 apps, support tiers
- Outcome: 20 → 25 paying customers (+25%) within 6 months of Phase 2 launch
- Codefresh brand primary: teal/green (#00C4A7 approx) — used on CTAs and sliders
- Colours: teal · dark navy · blue · silver · sky · near-white

---

## Network Discovery Case Study (`network-discovery/`)
Reference for style patterns — the canonical style template for other case studies.

Key CSS: `.content { max-width: 740px; margin: 0 auto; padding: 80px 24px; }`, `.wide-img { margin: 36px -120px; }`, `.band { background: var(--bg-gray); border-top/bottom: 1px solid var(--rule); }`

Images: `hero.png`, `atera-logo.png`, `group-1/2/3/4.png`, `scan-results.png`, `select-scan-results.png`

---

## Runtime Case Study (`runtime-case-study/`)
Previously a separate GitHub repo (`shohamsam/runtime-case-study`). Now moved into the main repo.
- Old repo should be **deleted on GitHub** (Settings → Delete repository) — otherwise it still serves the old version
- Homepage card now uses relative paths (`runtime-case-study/`) not absolute URLs ← FIXED THIS SESSION

---

## Git Notes
- **Always use personal account** (`shohamsam`) in GitHub Desktop, not the Octopus work account
- `.nojekyll` file exists in root — required for GitHub Pages to serve HTML without Jekyll
- If git commits fail with lock file errors:
  ```
  pkill -f "git maintenance"; pkill -f "github"; sleep 1; rm -f ~/Documents/GitHub/shohamsam.github.io/.git/index.lock ~/Documents/GitHub/shohamsam.github.io/.git/HEAD.lock; git -C ~/Documents/GitHub/shohamsam.github.io add <files> && git -C ~/Documents/GitHub/shohamsam.github.io commit -m "<message>"
  ```

---

## Pending / To Do
- [ ] Delete the old `shohamsam/runtime-case-study` repo on GitHub (Settings → Delete repository)
- [ ] Check Lifecycle Editor and EOT Redesign case studies for nav consistency (should only have "Works" on left, no back link on right)
- [ ] Consider adding the pricing-pages card thumbnail — currently uses `pricing-phase-2-1.png` at 85%; could replace with a dedicated card thumbnail if one is exported

---

## Figma File
`https://www.figma.com/design/4vLfLaHg6wK30QXS7xKtNi/Screens`

Key nodes used:
- Network Discovery hero: `node-id=18-26692`
- Activity icons order: `node-id=18-26725`
- Profile photo avatar component: `node-id=34638-18732`

---

## Style Reference: Adham Dannaway
https://www.adhamdannaway.com/portfolio/figma-design-system

The pricing pages case study is intentionally styled after this — image-first, editorial, all white, minimal structure. If expanding or adding new case studies in a similar style: short text → big image → short text → big image. Let visuals carry the story.
