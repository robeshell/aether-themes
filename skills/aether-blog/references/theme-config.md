# Theme configuration reference

The consuming site owns `aether.config.mjs`:

```js
export default {
  themes: ['minimal', 'persona'],
  defaultTheme: 'minimal',
  themeMeta: {
    minimal: { label: '留白', description: '极简与秩序' },
    persona: { label: '预告信', description: '红黑与斜切' },
  },
};
```

`themes` is the enabled-theme allowlist. The order controls the order shown by the picker. `defaultTheme` must be one of its values. `themeMeta` is optional package-independent UI copy; if omitted, a consumer can fall back to the theme key.

Generate a bundle after changing the config:

```sh
node node_modules/aether-themes/tools/generate-theme-css.mjs \
  --config aether.config.mjs \
  --output src/styles/aether-themes.css
```

For a site that keeps a committed local CSS snapshot, use `--source local` and import the generated file from the site's layout. For a published package, use the default `package` source. The generator rejects unknown names, duplicate themes, an empty list, and a default that is not enabled.

Available keys:

`minimal`, `magazine`, `terminal`, `cyber`, `island`, `wilds`, `persona`
