# Frontend publication

The only maintained UI source is `kryptostesmoiras/KryptosTesMoiras`, branch `main`, directory `github/pages/`.

The workflow `.github/workflows/publish.yml` checks out that directory, installs its locked npm dependencies, checks TypeScript, builds the React application, and publishes only the generated output here. Files under `assets/`, `index.html` and `favicon.svg` are build artifacts, not a second set of UI sources. Do not edit them manually.

## Automatic updates

GitHub Actions checks the canonical frontend every five minutes. GitHub can delay scheduled runs; this is not an instantaneous cross-repository push hook. A change to the frontend tree or publishing workflow triggers a build. Changes elsewhere in the source repository do not rebuild the UI. The workflow also runs when its own configuration changes, and can be started manually from Actions > Publish React frontend > Run workflow. Use `force` to rebuild an unchanged source tree.

No cross-repository token is required while the source repository is public. The workflow uses this repository's built-in `GITHUB_TOKEN` to publish generated files. It explicitly requests a Pages build because commits made with that token do not automatically trigger Pages. It checks that the published Pages commit matches the generated build; a failure is retried on the next run.

GitHub can disable scheduled workflows in public repositories after 60 days without repository activity. If that happens, re-enable the workflow in Actions and run it manually. A direct source-push trigger would require a separately authorized cross-repository credential; none is assumed or embedded.

## Repository settings

GitHub Pages must retain its existing branch publication setting: **Deploy from a branch**, branch **main**, directory **/ (root)**. GitHub Actions must be enabled, and repository rules must allow the built-in token to commit the generated files. The workflow has `contents: write` and `pages: write`; it does not need a personal token or an onion address.

This uses Actions to synchronize and build the application, and the existing branch-based Pages service to serve it. Do not change the Pages source to “GitHub Actions” without migrating the final publication step to the Pages artifact/deployment actions as well.

`deployment.json` records the canonical source commit, frontend tree and workflow revision for the generated build. The workflow preserves `CNAME`, `.github/`, this documentation and other owner-managed configuration. It removes obsolete portal files and never generates sample projects.

## Local verification

In the canonical source checkout:

```sh
cd github/pages
npm ci
npm run build
npm run preview
```

The browser entry file is generated HTML, loading the compiled React/TSX application and local assets. The presence of `index.html` does not mean that the former authored HTML portal is still in use.
