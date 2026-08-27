---
name: aether-blog
description: "Use Aether's AI-first, template-driven workflow to build and maintain a customizable personal blog."
---

# Aether Blog Builder

Use this skill to let an AI agent establish or maintain a customizable personal blog without coupling the site's content to its visual theme package. The agent works by creating or updating the consuming site's editable templates; Aether itself remains a CSS theme layer and has no AI runtime dependency.

## Workflow

1. Inspect the working directory before changing it. Preserve existing content, routes, framework choices, and uncommitted work. If maintaining an existing Aether site, read [`UPDATE_PROMPT.md`](../../UPDATE_PROMPT.md) before changing the dependency or generated CSS. If no site exists and the owner has not supplied a brief, ask the setup questionnaire in [`STARTER_PROMPT.md`](../../STARTER_PROMPT.md), summarize the proposed site, and wait for confirmation before scaffolding the formal site directly in the current website workspace (Astro is the default) with semantic hooks from [`THEME_CONTRACT.md`](../../THEME_CONTRACT.md).

   The Aether theme repository is a reference/package repository, not the consuming site's workspace. If the current directory is the Aether repository, do not scaffold a website there and do not create a test subdirectory; ask the owner to open or create a separate website directory. Use [`SMOKE_TEST_PROMPT.md`](../../SMOKE_TEST_PROMPT.md) only when the owner explicitly asks to validate the package itself.
2. Create `aether.config.mjs` from [`aether.config.example.mjs`](../../aether.config.example.mjs). Keep only the themes the owner wants, ensure `defaultTheme` is enabled, and keep labels/descriptions in the consuming site.
3. Generate the selected CSS bundle with `generate-theme-css.mjs`. Make the theme picker read the same `themes` array so disabled themes are not offered in the UI.
4. Keep content in a collection or Markdown directory separate from theme code. A typical entry has `title`, `description`, `date`, and `section` frontmatter. Use the site's existing content model when one exists.
5. Build pages around reading order: home, section indexes, entry details, and an about page. Add rich media only when the repository has real or clearly marked sample assets; never invent a user's biography, achievements, or external imagery.
6. Validate with the site's build/check command, confirm every enabled theme activates, and check desktop and narrow layouts for overflow. Respect reduced-motion preferences.
7. For GitHub setup and publishing, read [`github-pages.md`](./references/github-pages.md). Creating a remote repository, pushing commits, or publishing a package requires explicit user approval immediately before the external mutation.

## Boundaries

- Aether owns CSS foundation and theme rules; the consuming site owns content, routes, copy, asset licenses, and interaction logic.
- The consuming site is created in its own workspace. `aether-ai-smoke-test` is reserved for package-maintainer smoke tests and must not be used as the default user-site destination.
- Do not load every theme merely because it exists. The config and generated import bundle are the source of truth for enabled themes.
- Do not copy Nintendo, SEGA, CDPR, Persona, or other franchise artwork into a generated public starter. Use original CSS treatments or user-owned assets.
- Keep GitHub instructions actionable, but stop before creating or pushing anything when approval is missing.

## References

- Read [`theme-config.md`](./references/theme-config.md) when editing theme selection, labels, or generated imports.
- Read [`github-pages.md`](./references/github-pages.md) when creating a repository, configuring Pages, or preparing a release.
