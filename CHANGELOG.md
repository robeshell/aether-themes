# Changelog

## 0.1.4 — 2026-08-27

- Separate the formal user-site setup prompt from the package-maintainer smoke-test prompt.
- Make the formal setup create the site in the current website workspace and refuse to scaffold inside the Aether repository.
- Document `SMOKE_TEST_PROMPT.md` as the only workflow that creates `aether-ai-smoke-test`.

## 0.1.3 — 2026-08-27

- Add `UPDATE_PROMPT.md` with one-line and full workflows for safely updating an existing Aether site through an AI agent.
- Make the starter workflow ask for site identity, content sections, language, and theme choices before creating files.
- Make the update workflow discoverable from `AGENTS.md`, `SKILL.md`, and the README.

## 0.1.2 — 2026-08-27

- Restructure the README as an open-source project guide with badges, quick start, architecture, contributing, and release sections.
- Add repository, homepage, issue tracker, and discovery keywords to the npm metadata.
- Add GitHub Topics for CSS themes, static sites, design systems, and AI-assisted setup.

## 0.1.1 — 2026-08-27

- Add a beginner-friendly `STARTER_PROMPT.md` for creating and building a first Aether site from the current workspace.
- Include the starter prompt in the npm package and link to it from the README.

## 0.1.0 — 2026-08-27

- Extracted the shared foundation and seven visual themes from W.Site.
- Added a documented semantic class contract.
- Made cyber, terminal, and wilds imagery opt-in through CSS custom properties.
- Added the `all.css` convenience entry point.
- Added a package check workflow and publishing notes.
- Added `aether.config.mjs` support and a validated theme-bundle generator.
