# ykai.studio

Personal site for **YK AI** — freelance software & AI engineering, based in Japan.
Bilingual (JA / EN). Single static `index.html`, no build step, no framework.

## Files

```
index.html   ← the entire site (this is what gets deployed)
README.md
.gitignore
```

Everything is inline: styles in a `<style>` block, the logo and favicon as
inline SVG, no image assets, no dependencies except Google Fonts
(Archivo, IBM Plex Sans, IBM Plex Mono).

## Editing

- **Copy** lives directly in `index.html`. Every translatable string is two
  sibling `<span>`s: `<span class="i18n-ja">…</span><span class="i18n-en">…</span>`.
  CSS shows one based on `html[data-lang]`; a small script sets the initial
  language (saved choice → browser language → Japanese default) and the
  `JA / EN` button in the nav toggles it.
- **Sections**: hero, `#services`, `#approach`, `#stack`, `#about`,
  `#contact`. Alternating sections carry `class="block panel"` for the
  raised background.
- **Accent colour**: `--accent` (`#0d9488` light / `#19b8ab` dark), defined
  once in `:root` and the `prefers-color-scheme: dark` block. The teal
  cursor in the logo SVG is hard-coded `#0d9488` in three places (nav mark,
  favicon data-URI, and it inherits elsewhere).
- **Stack list** (`#stack`) is placeholder-ish — keep it matched to what
  you actually take on.

## OG image

There is no `og:image` right now (the old one was removed). Link previews
fall back to title + description. To add one later: create a 1200×630
image, drop it at `assets/og-image.jpg`, and re-add the
`og:image` / `twitter:image` meta tags (and switch `twitter:card` back to
`summary_large_image`).

## Deployment (Cloudflare Pages)

1. Push to the connected repo (or upload `index.html` directly).
2. Build settings: no build command, output directory `/`.
3. Custom domain `ykai.studio` is already connected via Cloudflare.

## Why plain HTML

One page, occasional edits. A framework or CMS would add build tooling and
maintenance for a problem this site doesn't have. Revisit only if it grows
into something with many pages or frequently-changing content.
