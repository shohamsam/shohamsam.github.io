# Portfolio Site Handoff

## Overview
Shoham Samuel's portfolio site — static HTML/CSS/JS, hosted on GitHub Pages.

- **Live URL:** https://shohamsam.github.io
- **Local repo:** `~/Documents/Portfolio Website` (connected folder, edited via Cowork/Claude)
- **Cowork/Claude** handles edits, commits, and pushes directly in this folder (personal account: `shohamsam`); GitHub Desktop is no longer the primary workflow but still works if used
- No build tools, no frameworks — plain HTML files

---

## ⚠️ Before Laptop Wipe — Back These Up
These folders are NOT in the git repo and will be lost if not backed up:

1. **`Pricing page assets/`** — all source images and videos for the pricing-pages case study, including the `Extra images/` subfolder
2. **`.claude/skills/`** — custom Cowork skills (octopus-slides, octopus-deploy-knowledge, octopus-writing-guide, brand-guidelines, etc.)

Back both up to Google Drive or iCloud before wiping.

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
├── pricing-pages/              ← Case study (Codefresh self-service checkout)
│   ├── index.html
│   └── images/
│       ├── hero.png                ← Hero image (1283x1274px)
│       ├── contact-sales.png       ← The "before" — contact form marketing page
│       ├── pricing-phase-1.png     ← Phase 1 subscription page
│       ├── pricing-phase-1-checkout.png ← Phase 1 checkout modal
│       ├── pricing-phase-2-1.png   ← Phase 2 configurator
│       ├── pricing-phase-2-2.png   ← Phase 2 configurator alternate state
│       ├── pricing-phase-2-3.png   ← Phase 2 checkout modal
│       ├── isometric-large.png     ← Wide isometric (5384x1912px, #F1F5FE bg) — closing image + homepage card thumbnail
│       ├── ds-colors.png           ← 6-colour palette strip
│       ├── ds-typography.png       ← Type scale
│       ├── ds-icons.png            ← 25 line icons
│       ├── ds-components-2.png     ← Component library (updated)
│       ├── ds-color-analysis.png   ← Colour token annotations
│       ├── ds-light-dark-2.png     ← Light/dark form comparison (2512x1370px)
│       └── plan-interaction.mov    ← Phase 2 interaction video (autoplay, controls, loop, muted)
└── runtime-case-study/         ← Case study (moved from separate repo)
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
--bg-warm:#fafaf9       /* image card backgrounds */
--bg-gray:#f6f6f6
--accent: #7673fe       /* stat numbers, callout borders */
--f-serif:'Instrument Serif', Georgia, serif
--f-sans: 'Inter', system-ui, sans-serif
```

**h2:** Instrument Serif italic, `clamp(28px, 4vw, 40px)`, weight 400  
**p:** 17px, `--ink-2`, line-height 1.75  
**nav height:** 60px fixed, frosted glass

---

## Homepage (`index.html`)

### Card Grid — Order
1. Lifecycle Editor — video thumbnail
2. Codefresh Runtime Installation — video thumbnail
3. **Self-Service Checkout** — isometric-large.png, `#F1F5FE` bg, `object-fit: cover`
4. CVE Sidecar — `#0170CD` blue bg, 80% contain
5. Purchase Pages Redesign (EOT) — `#C8E0FC` bg, 85% contain
6. Network Discovery — `#f0f4f8` bg, 80% contain

---

## Pricing Pages Case Study (`pricing-pages/index.html`)

### Hero
- Background: `linear-gradient(270deg, #CFF0ED 0%, #ffffff 100%)` (teal right → white left)
- Image: `hero.png` (1283×1274px) — `position: absolute; right: 0; top: 0; width: 62%`
- Image fades in from left: `-webkit-mask-image: linear-gradient(to right, transparent 0%, black 22%)`
- Text column: left 44%, padding `80px 0 80px 8%`
- `min-height: 892px`
- Stat block: `+40%` in large Instrument Serif italic + "growth in paying customers" label
- Current hero image: `Hero image 01.png` from Extra images (exported from Figma at 1283×1274px)

### Meta Bar
Company · Role · Focus · Year · **Outcome (+40% growth in paying customers)**

### Page Structure

**Part 1 — The Work**
1. Context: text + `contact-sales.png` (stacked, `.full-img`)
2. Phase 1: `.img-pair` (wide bleed `-120px`) — `pricing-phase-1.png` + `pricing-phase-1-checkout.png`
3. Phase 2: text → `.trio-wrap` (1280px wide) with `pricing-phase-2-1/2/3.png` → `plan-interaction.mov` video (autoplay, controls, loop, muted)

**Divider:** `── The Design System ──`

**Part 2 — The Design System**
4. Colour — `ds-colors.png` (wide bleed)
5. Typography & Icons — `.ds-pair` side by side (no card background)
6. Colour tokens — `ds-color-analysis.png` (wide bleed)
7. Components — `ds-components-2.png` (wide bleed)
8. Light & dark — `ds-light-dark-2.png` (wide bleed)

**Divider:** `── Outcome ──`

9. Outcome text + 3-stat block (+40% / First / 2 phases)
10. Closing isometric — `isometric-large.png`, full-width, `background: #F1F5FE`

### Key CSS Classes
```css
/* Wide bleed images */
.wide-img      { margin: 32px -120px; background: var(--bg-warm); border/shadow }
.img-pair      { display: grid; 1fr 1fr; gap: 16px; margin: 32px -120px; }
.trio-wrap     { max-width: 1280px; margin: 0 auto; padding: 0 24px 80px; }
.img-trio      { display: grid; 1fr 1fr 1fr; gap: 16px; }

/* DS images — no background/border */
.ds-img        { width: 100%; margin: 32px 0; }
.ds-img--wide  { margin: 32px -120px; width: auto; }
.ds-pair       { display: grid; 1fr 1fr; gap: 24px; margin: 32px 0; }

/* Closing section */
.iso-wrap      { background: #F1F5FE; line-height: 0; }
.iso-wrap img  { width: 100%; display: block; }
```

### Content Facts
- Company: Codefresh by Octopus Deploy
- Role: Senior Product Designer, 2024
- Phase 1: Fixed plan at $4,170/year — first ever self-serve checkout
- Phase 2: Live configurator — sliders (clusters + ArgoCD apps), presets, annual/monthly toggle
- Outcome: **+40%** growth in paying customers within 6 months of Phase 2 launch
- Em dashes replaced with hyphens throughout (`—` → `-`)

---

## Style Reference
- **Adham Dannaway** (https://www.adhamdannaway.com/portfolio/figma-design-system) — inspiration for the design system section: image-first, editorial, all white, minimal text
- DS images are frameless (no warm card background) — images have their own backgrounds baked in

---

## Nav Pattern (all case studies)
```html
<nav>
  <a class="nav-name" href="/">Works</a>
</nav>
```
No back link on the right — was removed as duplicate.

---

## Git Notes
- Always use personal account (`shohamsam`) for git ops (via Cowork/Claude or GitHub Desktop), not Octopus work account
- `.nojekyll` file exists in root — required for GitHub Pages
- If git lock errors occur:
  ```
  pkill -f "git maintenance"; pkill -f "github"; sleep 1
  rm -f ~/Documents/Portfolio\ Website/.git/index.lock
  git -C ~/Documents/Portfolio\ Website add <files>
  git -C ~/Documents/Portfolio\ Website commit -m "<message>"
  ```

---

## Recent Changes (last session)
- Replaced hero image with `Hero image 01.png` (same 1283×1274px dimensions)
- Hero image now anchored `right: 0; top: 0` — flush to top-right corner, no clipping
- Hero image fades in from left using CSS mask gradient (transparent → opaque over 22%)
- Added `plan-interaction.mov` video below Phase 2 trio (autoplay, controls, loop, muted)
- Changed +25% outcome stat to **+40%** throughout (hero, meta bar, outcome section, body text)
- Moved Self-Service Checkout to card #3 on homepage; thumbnail uses `isometric-large.png`
- Replaced all em dashes (—) with hyphens (-) throughout the case study
- Skills are stored inside Claude app's internal session folders — not user-accessible, not worth backing up

## Laptop Wipe Notes
- **Code is safe** once pushed to GitHub — all HTML, images, and videos are in the repo
- **`Pricing page assets/`** folder contains original source files — back up to iCloud/Drive if you want the originals (not strictly needed since exported versions are in the repo)
- **Skills** are stored in Claude app internals, not user-accessible — don't worry about them; rebuild on new machine as needed
- On new machine: connect the target folder in Cowork/Claude and clone `shohamsam/shohamsam.github.io` into it

## Pending / To Do
- [x] Delete old `shohamsam/runtime-case-study` repo on GitHub (Settings → Delete repository)
- [x] Export new hero images from Figma at 1283×1274px when updating
