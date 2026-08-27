# Aether

Expressive, swappable CSS themes for personal sites.

Aether is the visual layer extracted from [W.Site](https://github.com/robeshell/robeshell.github.io). It gives a content-first personal site a small set of distinct atmospheres without coupling the theme package to one person's articles, routes, or content model.

## Included themes

| Theme | Direction |
| --- | --- |
| `minimal` | quiet whitespace and editorial order |
| `magazine` | paper, columns, and print rhythm |
| `terminal` | command line and Matrix-like green phosphor |
| `cyber` | hazard yellow, cyan diagnostics, and hard panels |
| `island` | bright island life and soft rounded surfaces |
| `wilds` | quiet ruins, earth tones, and wide landscape space |
| `persona` | red-black cut-paper poster composition |

## Usage

Import the foundation once, then import the themes you want after it. Aether themes activate through the `data-theme` attribute on the root element:

```css
@import 'aether-themes/foundation.css';
@import 'aether-themes/themes/minimal.css';
@import 'aether-themes/themes/persona.css';
```

```html
<html data-theme="persona">
```

For a site that offers every built-in theme, import `aether-themes/all.css` instead.

For AI-assisted site setup, give the repository to an agent and point it to [`skills/aether-blog/SKILL.md`](./skills/aether-blog/SKILL.md). The root [`AGENTS.md`](./AGENTS.md) makes this entry point discoverable in repositories that support the convention.

If you are new to Aether, copy the complete [initial install and build prompt](./STARTER_PROMPT.md) to an AI agent. It creates a disposable test site inside the current directory, installs the package, configures selected themes, renders representative content, and runs the build without touching the repository source.

### Select only the themes you need

Copy [`aether.config.example.mjs`](./aether.config.example.mjs) to your site as `aether.config.mjs`, remove the themes you do not want, and generate a small import bundle:

```sh
npx aether-themes \
  --config aether.config.mjs \
  --output src/styles/aether-themes.css
```

The generator validates theme names, duplicate entries, and `defaultTheme`. The generated file imports only the selected themes; your theme picker can use the same `themes` array to hide the rest. Keep labels and descriptions in the consuming site's config so Aether remains content-agnostic.

The CSS is framework-agnostic. It expects the semantic class contract documented in [`THEME_CONTRACT.md`](./THEME_CONTRACT.md), so you can use Astro, Eleventy, plain HTML, or another static-site tool.

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

They default to `none`, so the themes work without any additional assets. Only add imagery that you own or have permission to redistribute.

## Development

```sh
npm pack --dry-run
```

The package intentionally has no runtime dependency. Keep content, routes, and site-specific copy in the consuming site.

## License

MIT. See [`LICENSE`](./LICENSE).
