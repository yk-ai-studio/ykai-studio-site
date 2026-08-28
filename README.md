# YK AI Studio — Website

A single-page, static site. No build step, no framework, no CMS.
This is intentional — see "Why no framework" below.

## Files

```
ykai-studio-site/
  index.html            ← the entire site (production — this is what gets deployed)
  artifact-preview.html ← same design, body-only, used only for Claude's own preview
                           tool. Not part of the deployed site — excluded via .gitignore.
  assets/
    YK_Logo.png          ← official logo, used in the header
    og-image.jpg          ← (not yet added — see STEP 7)
  README.md
```

## STEP 6 — Responsive behavior

Already built in, nothing to configure:
- Layout uses `clamp()` for type sizes and spacing, so it scales fluidly
  between ~360px (small phones) and large desktop screens, no fixed
  breakpoint jumps for most values.
- The two hard breakpoints are `720px` (label/content column stacks to
  one column) and `820px` (the Work card image drops below the text).
- Test by resizing the browser window, or open dev tools' device toolbar.

## STEP 7 — SEO / OGP / favicon

Already set in `<head>` of `index.html`:
- `<title>`, meta description
- Open Graph + Twitter Card tags
- A minimal inline SVG favicon (a plain "YK" monogram) — works immediately,
  no external file needed

`assets/og-image.jpg` (1200×630px) exists and is wired up via the
`og:image` / `twitter:image` tags. It was generated from
`og-card-source.html` (not part of the deployed site — a local-only build
source, ignored by git) rendered at exact 1200×630 resolution via
Playwright, using the site's real fonts/colors and the untouched logo
file. To regenerate after a copy change: edit `og-card-source.html`,
serve the folder locally, screenshot it at 1200×630, and re-export as
`assets/og-image.jpg`.

Once "First Light" is finished, you may prefer to swap this for a still
from the actual film — that's a judgment call, not a requirement.

## STEP 8 — Links checked

- Email: `mailto:yuki@ykai.studio` — confirmed working format
- Instagram: currently linked as `https://instagram.com/ykai.studio` in two
  places (Contact section + footer). **This is a placeholder handle and has
  not been confirmed against the real account.** Before going live, search
  `index.html` for `instagram.com/ykai.studio` and replace both occurrences
  with the real profile URL.
- All internal nav links (`#work`, `#approach`, `#create`, `#about`,
  `#contact`) are anchor-scrolled, already working

## STEP 9 — Adding a new piece of work

Find the `<div class="work-card">` block inside `<section id="work">` in
`index.html`. Duplicate that whole block (from `<div class="work-card">`
to its closing `</div>`) directly below the existing one, then edit:

- `.work-tag` → project name (e.g. "Vaelume")
- `.work-title` → piece title (e.g. "Second Light")
- `.work-subtitle` → one-line mood description
- `.work-desc` → 1–2 sentence description
- `.work-meta` → category — length — status (e.g. "Beauty — 15 sec — 2026")
- `.work-visual` → once you have a real finished video/still, replace the
  `<canvas>` placeholder with a real `<video>` or `<img>` tag pointing at
  a file in `assets/`

Once "First Light" itself is finished, do the same edit on the existing
entry: swap its `<canvas>` placeholder for the real video/thumbnail, and
change `Fragrance — 15 sec — In Production` to the finished status.

## Why no framework (Next.js / Astro etc.)

At 0–5 pieces of work, a static-generator or CMS adds build tooling and
maintenance cost without solving a problem you have yet. Every new piece
is a copy-paste block in one HTML file — genuinely faster than authoring
a CMS entry. Revisit this once the Work section holds ~10+ pieces and
copy-pasting blocks starts feeling repetitive; at that point, migrating
the same content into Astro's content collections is a half-day job, not
a rewrite.

## Deployment (Cloudflare Pages)

1. Push this folder to a new GitHub repo (or use direct upload)
2. Cloudflare dashboard → **Workers & Pages** → **Create application** →
   **Pages** → connect the repo (or "Upload assets" for a no-git deploy)
3. Build settings: leave build command empty, output directory `/`
4. Once deployed, go to the Pages project → **Custom domains** →
   add `ykai.studio` (since the domain's nameservers are already on
   Cloudflare, this is a one-click connection, no DNS record copying
   needed)

## Logo

- **Header**: uses the real logo file, `assets/YK_Logo.png`, at a fixed
  1:1 aspect ratio (`.brand-logo`), scaled responsively via `clamp()`.
- **Hero**: still the styled-text lockup (`YK AI STUDIO`), unchanged.
- **Footer**: intentionally typography-only (`YK AI STUDIO` as text), not
  the image. The source PNG has an opaque white background baked in (no
  transparency), which reads as a white badge against the footer's dark
  background — worse than plain type. If a transparent-background version
  of the mark is produced later, the footer can be switched to the image
  the same way the header was; until then, typography is the more
  polished choice.
