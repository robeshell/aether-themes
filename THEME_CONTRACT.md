# Aether theme contract

Aether is the visual layer for AI- or developer-built sites with editable templates. It ships CSS plus optional framework-agnostic snippets; it is not a page generator or an adapter for arbitrary hosted-blog markup. The consuming site keeps ownership of markup, content, routes, and interaction chrome such as the theme picker UI and persistence. Themes style the following semantic hooks.

## Required hooks

- `.site-header`, `.site-name`, `.site-header nav`, `.site-header nav a`, `.header-tools`, `.about`
- `.theme-menu`, `.theme-menu summary`, `.theme-panel`, `.theme-options`, `.theme-option`, `.theme-preview`
- `.intro`, `.intro h1`, `.intro p`
- `.page-header`, `.page-header h1`, `.page-header p`
- `.home-section`, `.home-section-header`, `.home-section-header h2`
- `.entry-list`, `.entry-list li`, `.entry-list a`, `.entry-list h2`, `.entry-list p`, `.entry-card-shell`, `.entry-arrow`, `.entry-arrow--wilds`, `.list-meta`
- `.island-divider`, `.island-divider--line-brown`, `.island-divider--line-teal`, `.island-divider--line-yellow`, `.island-divider--wave-yellow`, `.island-divider--dashed-brown`
- `.entry`, `.entry-header`, `.back-link`, `.entry-header h1`, `.entry-description`, `.entry-meta`, `.prose`
- `.about-page`, `.footer-meta`, `.footer-meta-end`, `.footer-settings`

## Content hooks

Rich article content can use the existing `.prose` descendants: `h2`, `h3`, `p`, `img`, `blockquote`, `code`, `pre`, `.media-figure`, `.media-gallery`, `.audio-player`, `.formula-block`, and `.media-note`.

## Theme activation

Set one of these values on `<html data-theme="...">`:

`minimal`, `magazine`, `terminal`, `cyber`, `island`, `wilds`, `persona`

Themes are ordered after the foundation so the same semantic markup can move between visual systems. A consumer can add a local override stylesheet after Aether for brand colors, imagery, or site-specific components.

## Optional runtime

Most themes are CSS-only. These hooks need markup or a small script that CSS cannot invent:

- Persona titles: wrap matching headings into `.p5-title` with per-character `<span>` children. Import `applyThemeEnhancements(theme)` from `aether-themes/scripts/persona-titles.js` and call it whenever `html[data-theme]` changes.
- Dividers: include `.island-divider` with the matching variant class. Path constants and `createDivider(variant)` live in `aether-themes/scripts/markup.js`.
- Entry list arrows: keep both `.entry-arrow` and `.entry-arrow--wilds` in the list item; themes show or hide them. Paths are `ENTRY_ARROW_PATH` and `ENTRY_ARROW_WILDS_PATH`.
- Persona list cards: keep an empty `.entry-card-shell` inside each list link.

Example list item:

```html
<a href="...">
  <span class="entry-card-shell" aria-hidden="true"></span>
  <h2>Title</h2>
  <span class="entry-arrow" aria-hidden="true"><svg viewBox="0 0 24 24"><path d="…" /></svg></span>
  <span class="entry-arrow entry-arrow--wilds" aria-hidden="true"><svg viewBox="0 0 10 18"><path d="…" /></svg></span>
  <div class="list-meta">…</div>
  <p>…</p>
</a>
```

## Compatibility policy

- New theme rules should target these semantic hooks instead of page-specific routes.
- New markup hooks should be additive and documented here.
- Theme-specific assets should be opt-in through CSS custom properties.
- Keep the foundation free of content data and franchise assets.
