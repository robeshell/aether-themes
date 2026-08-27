# GitHub Pages setup and release guide

Use this guide when the owner wants to publish a generated site. Treat every remote mutation as an approval boundary.

## Prepare locally

1. Confirm the site builds locally and inspect `git status`.
2. Set the Astro `site` URL and, when publishing under a project path, the `base` path.
3. Add a GitHub Actions workflow that installs dependencies, runs the build, uploads `dist/`, and deploys with the official Pages actions.
4. Check that assets use root paths compatible with the chosen `base` path.

## Create the repository

Ask the owner whether the repository should be public or private and what exact name to use. The normal user flow is:

1. Create an empty repository on GitHub without adding a second README or license.
2. Add the exact remote URL locally and push the chosen branch only after approval.
3. In repository settings, set Pages to **GitHub Actions**.
4. Wait for the workflow, then verify the deployed URL on desktop and mobile.

Do not assume a repository name, organization, visibility, custom domain, or permission to push. Do not put tokens in the repository or workflow logs.

## Aether package release

For Aether itself, run `npm pack --dry-run`, review the tarball contents, create the public GitHub repository, push `main`, and publish `aether-themes` only after the owner confirms the final package name and npm account. Bump the version for every published change.
