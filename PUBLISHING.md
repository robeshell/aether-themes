# Publishing Aether

This repository is intentionally ready to publish, but publishing is a separate explicit step from local extraction.

## First GitHub release

Create an empty public repository named `aether-themes`, then push this repository's `main` branch:

```sh
git remote add origin https://github.com/robeshell/aether-themes.git
git push -u origin main
```

## Package release

After checking the package contents and confirming the package name is available:

```sh
npm login
npm publish --access public
```

The first package is `aether-themes@0.1.0`; the current release is `aether-themes@0.1.5`. Use a version bump for every later published change.

## Switching W.Site to the published package

Once the package is available, replace the site's local CSS snapshot imports with package imports and keep `src/styles/site-assets.css` as the site-owned asset override. Remove the temporary `sync:aether` script only after the package dependency is stable in GitHub Actions.
