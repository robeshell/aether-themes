# Aether

[English](./README.md) · [简体中文](./README.zh-CN.md) · [日本語](./README.ja.md)

[![npm version](https://img.shields.io/npm/v/aether-themes?logo=npm)](https://www.npmjs.com/package/aether-themes)
[![npm downloads](https://img.shields.io/npm/dm/aether-themes?logo=npm)](https://www.npmjs.com/package/aether-themes)
[![Check package](https://github.com/robeshell/aether-themes/actions/workflows/check.yml/badge.svg)](https://github.com/robeshell/aether-themes/actions/workflows/check.yml)
[![License](https://img.shields.io/npm/l/aether-themes)](./LICENSE)

**An AI-first, template-driven theme kit for customizable personal sites.**

Aether combines a swappable CSS theme layer with AI-guided setup and maintenance workflows. It helps an agent create or update editable site templates without coupling the visual system to one person's content, routes, or framework. The theme layer was extracted from [W.Site](https://robeshell.github.io/).

[Browse the demo site](https://robeshell.github.io/) · [Read the AI starter prompt](./STARTER_PROMPT.md) · [View the npm package](https://www.npmjs.com/package/aether-themes)

## What Aether is (and is not)

Aether is an AI-first, template-driven theme kit, not a complete blog theme, site generator, or CMS. It combines two layers:

1. **Theme layer** — framework-agnostic CSS, design tokens, and a semantic markup contract.
2. **AI builder layer** — prompts and a Skill that ask for the site's requirements, create or update editable templates, configure themes, and validate the result.

It does not provide routes, a content model, an admin panel, or ready-made templates for every blogging platform. The generated site remains a normal project that can run without an AI service at runtime.

Aether is intended for sites whose templates can be edited by an AI agent or a developer. It is not a universal adapter that can restyle arbitrary hosted-blog markup without template access.

The guided starter workflow uses Astro by default. The package itself has no Astro runtime dependency and can be integrated with any framework or static-site generator that can load global CSS, emit HTML, and add the semantic hooks documented in [`THEME_CONTRACT.md`](./THEME_CONTRACT.md).

| Environment | Integration level |
| --- | --- |
| Astro | First-class starter and template workflow |
| Eleventy or plain HTML | Direct CSS integration |
| Other HTML-producing frameworks or static-site generators | Compatible after mapping templates to the contract |
| Existing CMS or blog markup | Not drop-in; requires a template adapter or local overrides |

In other words, Aether is portable, but it is not universally plug-and-play. The consuming site remains responsible for its markup, content, routes, and interactions.

## Why Aether

- **Seven swappable themes** using one semantic markup contract.
- **Selective loading** so a site only ships the themes it offers.
- **Framework-agnostic CSS** that works with Astro, Eleventy, plain HTML, and other static-site tools.
- **AI-first setup and maintenance** through a repository-discoverable Skill and copy-and-paste prompts.
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

For a guided, from-scratch setup, open an empty directory that will become your website and give the AI agent this repository as a reference. Do not open the Aether theme repository as the website's working directory: Aether is the dependency and visual layer, while your website owns its files, content, routes, and configuration.

The agent's job is to create or modify the site's editable templates so they use Aether's semantic hooks. Aether does not infer arbitrary markup or rewrite a locked-down hosted blog automatically.

The root [`AGENTS.md`](./AGENTS.md) and [`skills/aether-blog/SKILL.md`](./skills/aether-blog/SKILL.md) make the setup entry point discoverable in agents that support repository conventions.

If you are new to terminal-based development, copy [`STARTER_PROMPT.md`](./STARTER_PROMPT.md). It asks a short setup questionnaire about the site name, description, author, sections, language, and themes, then creates the formal website directly in the current workspace after you confirm the plan. It refuses to create files when the current workspace is the Aether theme repository.

The shortest handoff message is:

```text
Read https://github.com/robeshell/aether-themes/blob/main/STARTER_PROMPT.md. Ask me the setup questions first, wait for my confirmation, then create and start the formal website directly in the current workspace. Do not create `aether-ai-smoke-test` or any other test directory. If the current workspace is the `aether-themes` repository, stop and ask me to switch to a separate website directory.
```

If you are maintaining the Aether package itself, use [`SMOKE_TEST_PROMPT.md`](./SMOKE_TEST_PROMPT.md). It creates an isolated `aether-ai-smoke-test/site` inside the repository for package and generator checks; it is not a user-site setup workflow.

If you already have an Aether site, use [`UPDATE_PROMPT.md`](./UPDATE_PROMPT.md). It gives the agent a one-line update command plus a cautious full workflow that preserves content, configuration, local snapshots, and uncommitted work before rebuilding and checking the site.

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
