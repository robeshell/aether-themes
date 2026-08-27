# Aether repository guide

When asked to build a personal blog with this repository, read [`skills/aether-blog/SKILL.md`](./skills/aether-blog/SKILL.md) and [`STARTER_PROMPT.md`](./STARTER_PROMPT.md) before making changes. The consuming website must live in its own working directory; do not create it inside this theme repository. When maintaining an existing site that already uses Aether, read [`UPDATE_PROMPT.md`](./UPDATE_PROMPT.md) first. Use [`THEME_CONTRACT.md`](./THEME_CONTRACT.md) for markup hooks and [`aether.config.example.mjs`](./aether.config.example.mjs) for theme selection.

Use [`SMOKE_TEST_PROMPT.md`](./SMOKE_TEST_PROMPT.md) only when explicitly asked to validate the Aether package itself. The smoke test is the only workflow that creates `aether-ai-smoke-test`.

Keep the consuming site's content, routes, copy, and asset licenses separate from Aether's CSS. Validate the generated site before delivery. Creating GitHub repositories, pushing commits, or publishing npm packages always requires explicit user approval immediately before the external action.
