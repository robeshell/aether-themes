# Aether theme contract

Aether is a CSS layer, not a page generator. The consuming site keeps ownership of markup, content, routes, and interaction logic. Themes style the following semantic hooks.

## Required hooks

- `.site-header`, `.site-name`, `.site-header nav`, `.site-header nav a`, `.header-tools`, `.about`
- `.theme-menu`, `.theme-menu summary`, `.theme-panel`, `.theme-options`, `.theme-option`, `.theme-preview`
- `.intro`, `.intro h1`, `.intro p`
- `.page-header`, `.page-header h1`, `.page-header p`
- `.home-section`, `.home-section-header`, `.home-section-header h2`
- `.entry-list`, `.entry-list li`, `.entry-list a`, `.entry-list h2`, `.entry-list p`, `.entry-arrow`, `.list-meta`
- `.entry`, `.entry-header`, `.back-link`, `.entry-header h1`, `.entry-description`, `.entry-meta`, `.prose`
- `.about-page`, `.footer-meta`, `.footer-meta-end`, `.footer-settings`

## Content hooks

Rich article content can use the existing `.prose` descendants: `h2`, `h3`, `p`, `img`, `blockquote`, `code`, `pre`, `.media-figure`, `.media-gallery`, `.audio-player`, `.formula-block`, and `.media-note`.

## Theme activation

Set one of these values on `<html data-theme="...">`:

`minimal`, `magazine`, `terminal`, `cyber`, `island`, `wilds`, `persona`

Themes are ordered after the foundation so the same semantic markup can move between visual systems. A consumer can add a local override stylesheet after Aether for brand colors, imagery, or site-specific components.

## Compatibility policy

- New theme rules should target these semantic hooks instead of page-specific routes.
- New markup hooks should be additive and documented here.
- Theme-specific assets should be opt-in through CSS custom properties.
- Keep the foundation free of content data and franchise assets.
