# Abhishek Punna — Portfolio

Personal portfolio site for Abhishek Punna, Azure DevOps Engineer (Chennai, India).
A single static HTML page with no build step, no framework and no dependencies beyond Google Fonts.

Live preview: https://claude.ai/artifact/YSMVNEaj97o4H1AMmEEcT9

## Project structure

```
.
├── index.html        # the whole site: markup, CSS and JS in one file
├── img/
│   ├── hero.png      # hero portrait
│   ├── avatar.png    # nav avatar
│   ├── card.png      # "who am I" photo card
│   ├── azure.png     # Azure logo (hero badge + marquee)
│   └── *.svg         # tool icons for the marquee (Terraform, Docker, Kubernetes, Grafana, SonarQube, Python, Bash)
└── README.md
```

## Sections

1. **Nav** — fixed white top bar: availability pill, centred links with counts (Work [4], Experience [5y+]) and a black "Let's Talk" button.
2. **Hero** — giant outlined + solid name, colour portrait overlapping it, role, blurb, "Let's collaborate" CTA and LinkedIn / Email / Call / Portfolio pills.
3. **Tool marquee** — scrolling strip of the tools used day to day.
4. **Collage panel** — six mock screenshots (pipeline run, `terraform plan`, App Insights, AKS pods, deploy frequency, ACR).
5. **Statement** — positioning line with floating skill pills.
6. **How I Ship** — four-stage pipeline stepper: Code & Review → Build & Test → Provision → Deploy & Monitor.
7. **Highlights** — two role summaries (Charles Technologies, Awan Infotech).
8. **Selected Work** — four project cards.
9. **Who am I** — photo card, bio, career ledger and skill set.
10. **Contact band** — email / phone copy buttons.
11. **Footer** — giant outlined name that fills in as you scroll, then one line with copyright, live Chennai clock and contact links.

## Design

- **Palette:** monochrome. Black (`#111312`) accent on white, light grey tints (`#eef0f2`, `#f5f6f7`) for chips and panels, green (`#22c55e`) only for the availability dot. Portraits keep their natural colour; the lime rim light and backdrops were removed from the PNGs.
- **Dark mode:** follows `prefers-color-scheme`, with blue-tinted neutrals; can be forced with `data-theme="dark"` or `"light"` on `<html>`.
- **Type:** Instrument Serif (display), Plus Jakarta Sans (body), JetBrains Mono (code).
- **Motion:** scroll-reveal, pipeline rail animation, marquee, pointer-tracking hero glow. All respect `prefers-reduced-motion`.
- **Responsive:** single-column layout below 760px, 16px side gutters, no horizontal scroll.

All colours are CSS custom properties on `:root`, so the theme can be changed from the first 40 lines of `index.html`.

## Run locally

Open `index.html` in a browser, or serve the folder:

```powershell
# any static server works, e.g. Python
python -m http.server 8080
# then open http://localhost:8080
```

## Deploy

The site is plain static files, so it can be hosted on GitHub Pages, Azure Static Web Apps, or Azure Storage static website hosting.

**GitHub Pages:** repo *Settings → Pages → Build and deployment → Source: Deploy from a branch → `main` / `/ (root)`*. The site will be served at `https://punnaabhishek.github.io/Portfolio/`.

## Changelog

### 2026-11-22 — Black-and-white redesign of the nav and hero

Switched from the Azure-blue accent to a monochrome black-on-white scheme and rebuilt the top of the page in an editorial layout.

- **Navigation:** replaced the floating glass pill with a full-width fixed top bar: availability pill on the left, centred links (Home, About, Work [4], Experience [5y+], Contact) and a black "Let's Talk" button on the right. It gains a hairline border and shadow once the page scrolls. Links collapse to icons under 640px.
- **Hero:** giant uppercase name with "ABHISHEK" outlined and "PUNNA" solid, portrait overlapping the lettering, role + blurb + "Let's collaborate" on the left and LinkedIn, Email, Call and Portfolio pills on the right.
- **Portrait fix:** removed the pointer-tracking hero glow. The green tint on the face was rim light baked into the PNGs from the original lime theme, so `img/hero.png`, `img/card.png` and `img/avatar.png` were re-processed: lime-hued pixels neutralised and the solid lime backdrops replaced with light grey. Portraits stay in full colour.
- **Palette:** accent tokens renamed from `--lime*` to `--accent*` and set to black / near-black, with light grey tints and a green dot reserved for "available" status. Dark mode inverts to white-on-black.
- Collage panel and footer are light grey on white rather than black, so the whole page reads as white background with black type.
- Collage mock screenshots, pipeline stepper, footer and all greenish greys updated to neutral monochrome values.
- Added the 800 weight of Plus Jakarta Sans for the hero name.
- Removed the "Let's collaborate" button from the hero; the nav "Let's Talk" button is the single call to action.
- The page is light-only now: the automatic dark mode that followed the system setting is gone, so the background is always white. `data-theme="dark"` on `<html>` still works as an explicit opt-in.

### 2026-11-22 — Statement section rebuilt around a skill dial

- Replaced the floating-pill statement with a skill dial: the sentence on top, five skill pills either side, a low-poly dodecahedron in the middle (Three.js r128 from cdnjs) and a detail card underneath.
- Each of the ten skills owns one pentagon. The face shows the real tool logo on a white tile with the name beneath (Azure DevOps, Docker, Terraform, Kubernetes, Git, Grafana, Key Vault, Python + Bash, Azure, SonarQube); two spare faces carry the AP monogram and "5+ years on Azure". Added `img/git.svg`, `img/azuredevops.svg` and `img/keyvault.svg`; all logo SVGs now carry an intrinsic 24px size so they draw cleanly onto canvas textures.
- The face turned to the front is the selected skill. The card shows its proof sentence, tools and where it was used, with a dot strip to jump between skills.
- The dial follows the mouse anywhere over the statement section, tilting toward the cursor without any dragging. That tilt is layered on top of the dial's own state, so idle stepping (next skill every few seconds), drag with inertia, and hover or tap on a pill or face all still work. On desktop the pills drift toward the cursor too.
- Rendering pauses off screen; auto-stepping respects reduced-motion; on phones the dial sits above the pills and card.

### 2026-11-22 — Footer replaced with a giant name reveal

- Removed the status-panel footer (brand blurb, link columns, status card). Its contents were duplicates of the nav and hero.
- The page now ends with "ABHISHEK PUNNA" set full-width in outlined capitals, mirroring the hero. As the footer scrolls into view the letters fill solid one by one, and empty again on the way back up. Letters lift slightly on hover.
- Beneath it, one line: copyright and role, the live Chennai clock, and LinkedIn / Email / Call pills plus a back-to-top button.

### 2026-11-22 — Navigation jumps fixed

- Nav targets (About, Work, Experience, Contact) now land just below the fixed bar instead of under it (`scroll-margin-top` equal to the nav height, 76px desktop / 64px mobile).
- On screens wider than 640px each target section is at least one viewport tall with its content vertically centred, so clicking a nav item shows that section on its own rather than the top of the next one.
- Fixed a regression from that change: the About collage rendered blank because the centred grid let its wrapper shrink to zero width (the panel's screenshots are absolutely positioned). `.wrap` now has an explicit 100% width.
- Collage goes to a single column of screenshots under 480px.

### 2026-11-22 — Mobile pass (verified with headless Edge at 320 / 360 / 390 px)

- The dial hint line was `white-space: nowrap` and 547px wide, which pushed the page out to 461px and clipped every section on phones. It now wraps on mobile and the "follows your mouse" part is desktop-only. `html` also clips horizontal overflow as a safety net.
- Two class-name collisions fixed: the hero's "PUNNA" span used `.solid`, the same class as the 3D dial container, so it inherited a square aspect ratio and left a 250px gap above the portrait (dial container renamed to `.dial`, hero span to `.fill`). The highlight cards' author block used `.who`, the same class as the Experience section, so it inherited 40px / 90px section padding (section rules scoped to `section.who`).
- Result: zero elements wider than the viewport at 320, 360 and 390px; hero, collage, dial, pills, card, stepper, work cards, ledger, CTA and footer all stack correctly.

### 2026-11-22 — Phone layout rework (≤ 760px)

A dedicated phone stylesheet block replaces the earlier patchwork of per-section tweaks. Verified by rendering at 390px.

- **Hero:** name scaled up to about 13vw with the portrait overlapping it like desktop; role and blurb centred; contact links in an equal-width 2 × 2 grid.
- **Nav:** five icons spread evenly with the round "Let's Talk" button on the right.
- **Collage:** the six mock screenshots are a horizontal swipe carousel with scroll-snap and a "swipe for more" hint, instead of a 1200px-tall stack.
- **Statement:** dial capped at 300px, "drag to browse" hint only, skills in a tidy two-column grid of equal pills, then the detail card.
- **Spacing:** one rhythm across sections (32 to 56px), smaller kicker and headings, tighter stepper nodes and cards.
- **Who / footer:** photo card no longer tilted on phones; footer name flush left on both lines with a compact contact row.

### 2026-11-22 — Brand-colour contact icons

- LinkedIn, email and phone icons across the site (hero pills, photo card, contact band, footer) now use real logos in their own colours: LinkedIn blue "in" tile (`img/linkedin.svg`), the Gmail "M" (`img/gmail.svg`) and a green phone tile (`img/phone.svg`), instead of monochrome line icons.

### 2026-11-22 — Bug sweep before push

- Static: tag balance, anchor targets, image paths, script element ids and duplicate ids all verified clean.
- Runtime (headless Edge, 1280 and 390px): Three.js loads, dial reacts to pill hover and dot clicks, nav highlight and sticky bar work, clock and year populate, zero console errors.
- Fixed: the footer name only filled 9 of 13 letters at the bottom of a desktop-height page; the fill now completes once the name is fully in view.

### 2026-11-22 — Fewer contact links

Email, phone and LinkedIn each appeared four or five times. Now each has one clear home.

- **Hero:** the four contact pills are replaced by three proof stats (5+ years on Azure, 3 environments run, 24/7 NOC coverage).
- **Photo card:** the LinkedIn / email icons give way to a small "Chennai, India" label.
- **Contact band:** one big black button with the email address, plus a quiet line for the phone number and LinkedIn. This is the contact section.
- **Footer:** LinkedIn and back-to-top only.
- **Nav:** "Let's Talk" stays as the always-visible way to email.
- Removed the dead copy-to-clipboard script that targeted buttons no longer in the page.

### 2026-11-22 — Contact panel, nav button removed, dial and footer fixes

- **Hero:** two proof stats (5+ years on Azure, 3 environments run); the 24/7 one is gone.
- **Nav:** the "Let's Talk" button is removed; the Contact link leads to the contact panel.
- **Dial:** camera moved back so the solid and its labels never clip at the top and bottom on smaller windows.
- **Contact panel:** replaces the plain band. A light rounded panel with a cursor-following spotlight: on the left a kicker, headline, short pitch, availability dot and a live Chennai clock; on the right a card with Email (primary, black), Call and LinkedIn rows that lift on hover.
- **Footer:** the contact section no longer forces a full screen height, so the empty space above the giant name is gone; footer top padding reduced; filled letters flip back to outline when hovered.

### 2026-11-22 — Finish and depth pass

**Finish**
- Share-ready: page description, "AP" monogram favicon, canonical URL, Open Graph and Twitter cards with a rendered 1200×630 preview (`img/og.png`) pointing at the GitHub Pages URL.
- Images: photo card is now a 640px JPEG (952 KB → 43 KB) and the hero portrait is 800px wide (1.8 MB → 1.2 MB); hero loads with high priority, the photo card lazily. Unused `img/avatar.png` removed.
- Résumé row added to the contact card, hidden until `Abhishek-Punna-Resume.pdf` is placed in the repo root.
- About section gets a kicker, heading and one-line intro above the collage.
- Skills regrouped into five labelled rows: Cloud, CI / CD, Containers & IaC, Observability, Security & Automation.
- Hero portrait fades softly into the page at the bottom.
- LinkedIn links point to the real profile.

**Depth**
- Hero name letters draw in one by one on first load.
- Collage screenshots drift at different depths as the cursor moves.
- Work cards tilt toward the cursor in 3D.
- Nav links get an animated underline; the marquee pauses on hover; a 2px scroll-progress line runs along the top.
- Contact card: the three rows share one white style and invert to black on hover; the duplicate "Available for new opportunities" line is removed from the panel (it lives in the nav pill).

### 2026-11-22 — Things you can feel

- One clock: the live Chennai time stays in the contact panel and leaves the footer line.
- Custom cursor on desktop: a dot with a lagging ring that grows over anything clickable, shrinks on press, and turns into a white "drag" badge over the dial and a "tilt" badge over work cards. Inverts over dark surfaces. Off for touch devices and reduced-motion.
- Hero reacts to the mouse: the portrait and the name drift in opposite directions, and each outlined letter of ABHISHEK fills black while the pointer is over it.
- Numbers count up the first time they scroll into view (hero stats and the figures inside the mock screenshots).
- Section headings wipe in from the top as their block reveals.
- Hero portrait: removed the drop shadow. Its soft halo beside the shoulders read as a faint grey box on some monitors; the image itself was verified fully transparent around the figure.

### 2026-11-22 — Résumé and content from the CV

- `Abhishek-Punna-Resume.pdf` added to the repo root and the "Download CV" row in the contact card switched on.
- Highlight cards rebuilt as honest role cards: company, title, dates, and five bullets each taken from the résumé (Charles Technologies 2025 → now, Awan Infotech 2021 → 2025). The quote-mark and tick styling that made them look like testimonials is gone.
- Work card descriptions expanded with the résumé's specifics: Azure CLI steps, Entra ID service connections, pull-request workflow for infrastructure, App Store and Play Store release automation, root-cause analysis.
- Skills: new "Platforms & ITSM" row (Rackspace, SendGrid, Ivanti) and a "Languages" row (English, Telugu).

### 2026-11-22 — Mobile polish round

- Phone nav is a labelled tab bar: icon plus a small label for Home, About, Work, Experience and Contact.
- Hero name on touch screens: since there is no hover, the outlined letters ink in and fade out once, letter by letter, after the entrance.
- Collage carousel shows position dots under it; tap a dot to jump to that screenshot.
- Phones download a 480px portrait (`img/hero-480.png`, 430 KB) via `srcset` instead of the 800px one.

### 2026-11-22 — Structure, signature details, feel, hygiene

**Structure**
- The standalone "Track record" section is gone. Its two role cards now live in the Experience section in place of the plain job rows, so pipelines and tooling are no longer described in five places.
- Process and Work use an editorial header: kicker and title on the left, a lead sentence on the right. About, the statement and Experience stay centred, so the variety is deliberate.
- Process and Experience sit on a light paper band; everything else stays white. Chips inside the bands are white so they keep their contrast.

**Signature details**
- The collage screenshots come alive when scrolled into view: pipeline steps complete one by one with a pulsing running step, the Terraform plan has a blinking cursor, the pending pod turns green-for-go (black), the grey pod blinks, the deploy bars grow in sequence, the availability line draws itself and the ACR log reveals line by line. The work-card screenshots animate the same way.
- Two faint orbit rings sit behind the dial, and a dotted hairline connects the active skill pill to the solid (desktop).

**Feel**
- Smooth, weighted scrolling via Lenis on desktop pointers; nav anchors scroll through it and account for the fixed bar. Off on touch and reduced-motion.
- A quiet "scroll" cue with a sliding line under the hero copy.
- Lead paragraphs step up to 1.1rem.

**Hygiene**
- "Skip to content" link for keyboard users; proper `</head>` and `<body>` tags.
- Preconnect to the font file host.
- Branded `404.html` for GitHub Pages.

### 2026-11-22 — Education lens cards

- The two education rows are now photo cards (college and senior secondary) with the institution image, degree, place and years.
- Hover (or tap on touch) fires a one-shot camera moment: eight aperture blades close over the photo and reopen, the image pulls focus (blur in, sharp out), viewfinder corner marks settle in, and a small EXIF-style caption with the years appears. Built with CSS custom-property animation (`@property`), no library.
- Real campus photos supplied by Abhishek (`img/edu-scsvmv.jpg` 1400×614, `img/edu-kcp.jpg` 980×475). The cards moved out of the narrow text column into a full-width two-up row under the Experience grid, with 16:9 photos, and the university is named in full: Sri Chandrasekharendra Saraswathi Viswa Mahavidyalaya (SCSVMV University).

### 2026-11-21 — Azure blue palette

Replaced the original lime / neon-yellow accent with Microsoft Azure blue to match the Azure DevOps positioning.

- Swapped the accent tokens (`--lime`, `--lime-deep`, `--lime-soft`) to Azure blue values and added `--lime-glow` (soft wash colour) and `--on-lime` (text colour on accent).
- Hero glow and contact band now use the softer sky-blue wash so headline text stays readable.
- Text on accent surfaces (pipeline step nodes, highlight icons, hover states, back-to-top button) changed from dark to white for contrast.
- Hardcoded lime inside the collage mock screenshots (pipeline dots, done lines, deploy bars, sparkline fill, AKS pod grid, chips) updated to blue.
- Footer panel changed to deep navy with light-blue links, status dot and glow.
- Dark-mode neutrals shifted from greenish to blue-tinted greys.
- Shadows re-tinted from green to blue.

### 2026-11-21 — Initial build

- Single-page portfolio with the eleven sections above.
- Floating glass navigation with active-section tracking.
- Collage of six animated mock screenshots of Azure DevOps, Terraform, App Insights, AKS and ACR.
- Four-stage "How I Ship" pipeline stepper.
- Light and dark themes, reduced-motion support, mobile layout.
- Copy-to-clipboard contact buttons and live IST clock in the footer.

## Contact

- Email: punnaabhishek9@gmail.com
- Phone: +91 99125 11744
