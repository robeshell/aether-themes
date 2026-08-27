# Aether

[![npm version](https://img.shields.io/npm/v/aether-themes?logo=npm)](https://www.npmjs.com/package/aether-themes)
[![npm downloads](https://img.shields.io/npm/dm/aether-themes?logo=npm)](https://www.npmjs.com/package/aether-themes)
[![Check package](https://github.com/robeshell/aether-themes/actions/workflows/check.yml/badge.svg)](https://github.com/robeshell/aether-themes/actions/workflows/check.yml)
[![License](https://img.shields.io/npm/l/aether-themes)](./LICENSE)

**A small, framework-agnostic theme layer for content-first personal sites.**

Aether gives a blog, notebook, photo journal, or music archive a distinct visual atmosphere without coupling the theme to one person's content, routes, or framework. It is the visual layer extracted from [W.Site](https://robeshell.github.io/).

[Browse the demo site](https://robeshell.github.io/) · [Read the AI starter prompt](./STARTER_PROMPT.md) · [View the npm package](https://www.npmjs.com/package/aether-themes)

## Why Aether

- **Seven swappable themes** using one semantic markup contract.
- **Selective loading** so a site only ships the themes it offers.
- **Framework-agnostic CSS** that works with Astro, Eleventy, plain HTML, and other static-site tools.
- **AI-ready onboarding** through a repository-discoverable skill and a copy-and-paste starter prompt.
- **No runtime dependencies** and no bundled franchise artwork or scraped assets.

## Themes

| Theme | Direction |
| --- | --- |
| `minimal` | Quiet whitespace and editorial order |
| `magazine` | Paper, columns, and print rhythm |
| `terminal` | Phosphor green, grids, and command-line cues |
| `cyber` | Hazard yellow, cyan diagnostics, and hard panels |
| `island` | Bright island life and soft rounded surfaces |
| `wilds` | Earth tones, ruins, and wide landscape space |
| `persona` | Red-black cut-paper poster composition |

All themes style the same semantic hooks. Change the root attribute to switch the visual system:

```html
<html data-theme="persona">
```

## Quick start

Install the package in your site:

```sh
npm install aether-themes
```

Import the foundation first, then the themes you want:

```css
@import 'aether-themes/foundation.css';
@import 'aether-themes/themes/minimal.css';
@import 'aether-themes/themes/persona.css';
```

If your site offers every built-in theme, use the convenience bundle:

```css
@import 'aether-themes/all.css';
```

The package only provides the visual layer. Your site owns the HTML, content, routes, theme picker, and interaction logic.

## Load only the themes you need

Copy [`aether.config.example.mjs`](./aether.config.example.mjs) to your site as `aether.config.mjs`, then remove themes you do not want:

```js
export default {
  themes: ['minimal', 'persona'],
  defaultTheme: 'minimal',
};
```

Generate an import bundle for that configuration:

```sh
npx aether-themes \
  --config aether.config.mjs \
  --output src/styles/aether-themes.css
```

The generator validates theme names, duplicate entries, and `defaultTheme`. Use the same `themes` array for your theme picker so disabled themes are not offered in the UI. Keep labels and descriptions in the consuming site so Aether stays content-agnostic.

## Build a site with an AI agent

For a guided, from-scratch setup, give this repository to an AI coding agent and ask it to read [`skills/aether-blog/SKILL.md`](./skills/aether-blog/SKILL.md). The root [`AGENTS.md`](./AGENTS.md) makes the entry point discoverable in agents that support the convention.

If you are new to terminal-based development, copy [`STARTER_PROMPT.md`](./STARTER_PROMPT.md). It tells the agent to create a disposable test site inside the current workspace, install Aether, configure selected themes, render representative content, run the build, and report the result without modifying the theme source.

## Markup contract

Aether styles semantic hooks rather than page-specific routes. Read [`THEME_CONTRACT.md`](./THEME_CONTRACT.md) for the required hooks and rich-content hooks, including images, video, audio, code, formulas, and galleries.

The consuming site owns:

- content collections and frontmatter;
- routes and page structure;
- theme-picker state and persistence;
- site copy and labels;
- asset licensing and site-specific overrides.

## Optional imagery

Aether does not ship scraped or franchise-owned imagery. The `cyber`, `terminal`, and `wilds` themes expose optional image variables instead:

```css
:root[data-theme="cyber"] {
  --aether-cyber-dots-image: url('/assets/cyber/dots-yellow.png');
}

:root[data-theme="terminal"] {
  --aether-terminal-rain-image: url('/assets/terminal/matrix-rain.svg');
}

:root[data-theme="wilds"] {
  --aether-wilds-header-image: url('/images/wilds-header.png');
}
```

These variables default to `none`, so the themes work without extra assets. Only add imagery that you own or have permission to redistribute.

## Development

The package has no runtime dependency. Review the publish contents locally with:

```sh
npm pack --dry-run
```

The same check runs in [GitHub Actions](https://github.com/robeshell/aether-themes/actions/workflows/check.yml) for every push and pull request.

## Contributing

Changes should target the semantic hooks in [`THEME_CONTRACT.md`](./THEME_CONTRACT.md), keep the foundation content-agnostic, and preserve the consuming site's ability to opt into only the themes it needs. Before opening a pull request, run `npm pack --dry-run` and check the generated package contents.

For release steps, see [`PUBLISHING.md`](./PUBLISHING.md). Every published change needs a version bump.

## License

MIT. See [`LICENSE`](./LICENSE).
