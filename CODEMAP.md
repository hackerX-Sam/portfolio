# Code Map — samirandas.com (folder: bogdankolomiyets.com)

Static portfolio site for **Samiran Das** (samirantsk2020@gmail.com), built in **Webflow** then exported
and post-processed with a Vite-style bundler (hashed asset names, ES modules). Templates originally
from Bogdan Kolomiyets' design. Last Webflow publish: Feb 11 2026. Served with clean URLs
(extensionless files) except `index.html`.

> ⚠️ Folder/robots.txt still mention old domains (`bogdankolomiyets.com` comment, `samirandas.com` sitemap).
> ⚠️ Nav links to `blog` and `portfolio` — **those pages don't exist in this folder** (dead links).

## Pages

| File | Barba namespace | What it contains |
|---|---|---|
| `index.html` (3213 lines) | `home` | Hero ("Building code for real "Impact!""), intro, Selected Projects carousel (4 projects), See-all (05) button, About strip, Testimonials ("They said yes!"), FAQ accordion (7 Qs), CTA, footer. GA4 `G-WX5J84TFY1`. No Webflow CSS duplication cleanup. |
| `about.html` | `about` | Older About page — hero only (minimal). |
| `about` (286 lines) | `about` | **Newer** About page — hero + 2 extra `note-scroller` sections ("Building Beyond The Surface", "An Athlete's Discipline"). Uncommitted edits in git. |
| `contact` (410 lines) | `contact` | Contact form (Netlify-style: `form-name` hidden + bot-field honeypot). Fields: Name, Email, Timeline (4 radios), Budget (4 radios), Message. Validation icons + success/error notifications, all handled by JS. |
| `process` (448 lines) | `process` | "My Proccess" (typo intentional?) — hero, 2 note-scrollers, My System 6 cards, "What you get IS Website that works!" 4 items, Reality check + meme image, CTA. |
| `portfolio/estelle` | `pdp` | **ONETEXT** project page (badges: Design/Architecture/2025). Next → Kivra. |
| `portfolio/shovk-studio` | `pdp` | **Shovk Studio** (redesign). Next → Collection v.1. |
| `portfolio/kivra-architecture` | `pdp` | **Kivra Architecture** (concept). Next → Collection v.2. |
| `portfolio/collection-v-1` | `pdp` | **Collection v.1** personal works (2024). Next → ONETEXT. |
| `portfolio/collection-v-2` | `pdp` | **Collection v.2** explorations (2025). Next → Shovk Studio. |

Every page shares the same skeleton:
`<head>` → Webflow CSS + inline page `<style>` + GA + preloader guard + module scripts →
`<body>` → `.nav_component` (desktop nav) → `aside.nav-floating` (floating nav, full-screen `bold-nav-full` menu)
→ `.loading-container` (preloader with rolling digits) → `main[data-barba=container]` (page content)
→ `footer#site-footer` (Menu/Socials/Say-Hello + giant "SAMIRAN DAS" heading) → `.transition` (page
transition logo SVG) → `<noscript>` CSS fallback.

## Recurring components / classes
- `nav_component`, `nav-floating`, `bold-nav-full` — navs; toggle via `data-navigation-toggle="toggle"`.
- `btn-animate-chars` — buttons animated per-character (`data-button-animate-chars`).
- `section_hero` / `hero_title` / `proccess_hero_image` — page heroes (SplitText word masks).
- `note-scroller` / `section_note` — big text blocks that pin/transition while scrolling.
- `section_cta` — "Ready to hear more yes?" block (`data-theme-section="dark"`).
- `footer` — reused on all pages (`SAMIRAN DAS` giant heading, credits "From Assam with love ❤️").
- `line-mask`, `word-mask` — text-split animation masks written by JS at runtime.
- `text-style-accent is-yes` — accent spans that trigger confetti on click (`data-trigger-confetti="yes"`).

## index.html specifics
- Selected Projects: 4 projects switched by JS while scrolling photo sections:
  1. estelle → **ONETEXT** (`https://home.onetext.com/`)
  2. kivra → **CODE NAKSHATRA 2.0** (`https://codenakshatra2.netlify.app/`)
  3. shovk → **CODE RANGERS** (`portfolio/shovk-studio`)
  4. zapvi → **ZAPVI** (`https://zapvi.in/…`)
- Wiring: `data-project-content="{id}" data-content-type="title|accent|description|button"` +
  `data-project-section="{id}"` on photo wrappers; `[data-falling-image][data-speed]` parallax photos;
  SVG `.fall-line` strokes draw in.
- Testimonials: `data-staking-card` + `[data-staking-cards-container]` (4 cards: Khris, Clara, Ariel, Mattias —
  still contain original template text praising "Bogdan"!).
- FAQ: `data-accordion-close-siblings css accordion` (7 items Q1–Q7).

## assets/
- `main-BjxpTroB.css` (183 KB) — full site CSS (Webflow + custom), loaded async via `media=print` trick.
- `main-jKaaXVz_.js` (185 KB, ES module, minified) — custom site code. Imports GSAP/Lenis/Barba.
  Behaviors keyed off data attributes: preloader, nav, barba transitions, smooth scroll, text-split,
  falling-image parallax, project carousel, staking cards, accordion, form validation,
  bunny.net HLS video players (`data-bunny-background-init`, `data-player-src` .m3u8), confetti
  (bundles tsParticles), momentum hover, 3D perspective hover, flip cards.
- `gsap-DdEwfv-Y.js`, `lenis-Bu7sAdyK.js`, `barba-CQlRLqFM.js` — vendored libraries.
- Images: template leftovers (col1-*, shovk-*, estelle-*, Serene-*, etc.) + `favicon-DrVmsY45.ico`, fonts
  (PPNeueMontreal, Lektorat, tentang-nanti.woff2).
- **Remote media**: many images/videos are hot-linked from `ik.imagekit.io/logicsync/…` (ImageKit) and
  `vz-e59da973-cb0.b-cdn.net` (bunny.net HLS) — local copies don't exist.

## Key inline CSS/JS in each page
- `sessionStorage visited` check hides preloader on repeat visits.
- `visibility:hidden` on `.hero_title`, `.loading__*`, `#floating-nav`, project titles etc. — JS (GSAP)
  reveals them; if JS fails the page stays invisible for those parts.
- `.line-mask` padding fixes for SplitText bounce animations.
- index-only overrides: hero image heights, `nav_logo` sized 3.5rem, `hero_description` uses League Spartan.
- Elements with `data-*` hooks that main-jKaaXVz_.js reads:
  `data-barba`, `data-navigation-toggle`, `data-theme-section`, `data-theme-nav`,
  `data-project-content`, `data-project-section`, `data-falling-image`, `data-staking-card(s-container)`,
  `data-accordion-*`, `data-form-validate`, `data-validate`, `data-submit`, `data-radiocheck-group`,
  `data-trigger-confetti`, `data-3d-hover-target`, `data-momentum-hover-*`, `data-flip-element`,
  `data-hero`, `data-ignore-trail`, `text-split`, `text-split="words"`,
  `data-bunny-*-init/player-*` (HLS video), `data-ratio` (project image ratios).

## Text content to know when editing
- Taglines: "Engineering Solutions that Work", "Building code for real Impact".
- About strip (index): "I build modern, high-impact websites for tech communities… cybersecurity…".
- Skills line: "National-level badminton player and armwrestler, state-level swimmer, music lover".
- Footer credit: "©2026 SAMIRAN DAS", "From Assam with love ❤️".
- Contact email/login everywhere: `samirantsk2020@gmail.com`.
- Socials: instagram.com/samiran.das, linkedin.com/in/samirandas, dribbble.com/samirandas.

## Gotchas when making changes
1. Shared blocks (nav, footer, preloader, transition, head scripts) are **duplicated in all 9 pages** —
   a change must be repeated in every file (or at least in the page you care about).
2. `about.html` vs `about` are different versions — `about` is the newer one; keep them in sync or delete the old one.
3. Many attributes/elements are animated by JS reading exact `data-*` hooks and class names — renaming
   classes (e.g. `hero_title`, `selected-projects_*`) can silently break animations.
4. Headless JS: content inside `[data-project-content]`, `.hero_description`, `.loading__*` etc. is
   `visibility:hidden` until GSAP shows it.
5. Form posting is Netlify-style (`form-name`); on any other host the contact form needs a backend.
6. GA4 id `G-WX5J84TFY1`; og images point to `samirandas.com/og/og-*.jpg`.
