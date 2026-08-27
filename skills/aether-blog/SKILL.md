---
name: aether-blog
description: "Set up, configure, and publish a content-first personal blog with Aether themes; use when an AI needs to turn a repository into a maintainable blog site."
---

# Aether Blog Builder

Use this skill to establish or maintain a personal blog without coupling the site's content to its visual theme package.

## Workflow

1. Inspect the repository before changing it. Preserve existing content, routes, framework choices, and uncommitted work. If no site exists, scaffold a small static site (Astro is the default) with semantic hooks from [`THEME_CONTRACT.md`](../../THEME_CONTRACT.md).
2. Create `aether.config.mjs` from [`aether.config.example.mjs`](../../aether.config.example.mjs). Keep only the themes the owner wants, ensure `defaultTheme` is enabled, and keep labels/descriptions in the consuming site.
3. Generate the selected CSS bundle with `generate-theme-css.mjs`. Make the theme picker read the same `themes` array so disabled themes are not offered in the UI.
4. Keep content in a collection or Markdown directory separate from theme code. A typical entry has `title`, `description`, `date`, and `section` frontmatter. Use the site's existing content model when one exists.
5. Build pages around reading order: home, section indexes, entry details, and an about page. Add rich media only when the repository has real or clearly marked sample assets; never invent a user's biography, achievements, or external imagery.
6. Validate with the site's build/check command, confirm every enabled theme activates, and check desktop and narrow layouts for overflow. Respect reduced-motion preferences.
7. For GitHub setup and publishing, read [`github-pages.md`](./references/github-pages.md). Creating a remote repository, pushing commits, or publishing a package requires explicit user approval immediately before the external mutation.

## Boundaries

- Aether owns CSS foundation and theme rules; the consuming site owns content, routes, copy, asset licenses, and interaction logic.
- Do not load every theme merely because it exists. The config and generated import bundle are the source of truth for enabled themes.
- Do not copy Nintendo, SEGA, CDPR, Persona, or other franchise artwork into a generated public starter. Use original CSS treatments or user-owned assets.
- Keep GitHub instructions actionable, but stop before creating or pushing anything when approval is missing.

## References

- Read [`theme-config.md`](./references/theme-config.md) when editing theme selection, labels, or generated imports.
- Read [`github-pages.md`](./references/github-pages.md) when creating a repository, configuring Pages, or preparing a release.
