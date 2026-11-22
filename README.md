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
11. **Footer** — brand, links, live clock and availability status.

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
- Idle: the dial steps to the next skill every few seconds. Drag to browse with inertia, hover or tap a pill or a face to jump to it, and on desktop the pills drift toward the cursor.
- Rendering pauses off screen; auto-stepping respects reduced-motion; on phones the dial sits above the pills and card.

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
