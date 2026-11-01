# Website and project documentation publication

The two destinations are distinct:

| URL | Purpose |
| --- | --- |
| `https://kryptostesmoiras.github.io/` | Public React website: horizontal banner, project search interface and planned desktop application information. |
| `https://kryptostesmoiras.github.io/KryptosTesMoiras/` | Project Markdown reader, license and public Discussions. |

The sole maintained UI source is `kryptostesmoiras/KryptosTesMoiras`, branch `main`, under `github/pages/`. Vite builds two TSX entry points. The Markdown collector adds all tracked `.md`/`.markdown` files and `License` to the documentation subsite. Generated document and discussion JSON live only under `KryptosTesMoiras/`.

The publishing workflow retrieves the source repository, installs locked dependencies, builds both entries, and publishes the complete `dist/` output to this repository's existing Pages `main` / root source. Do not edit generated root assets or the generated project subfolder manually. `CNAME`, `.github/`, this documentation and other owner-managed configuration are preserved.

## Automatic synchronization

Actions checks every five minutes for changes in the canonical source, workflow or Discussion metadata. GitHub may delay scheduled runs. Manual runs, including forced rebuilds, are available under Actions > Publish website and project documentation.

The built-in token commits generated output and explicitly requests the branch Pages build; token-authenticated commits do not trigger Pages automatically. The workflow verifies that the expected commit was built and retries on a subsequent run after a failure. No cross-repository personal token is required for the public source.

GitHub may disable scheduled workflows in public repositories after 60 days without repository activity. Re-enable the workflow in Actions if this occurs.

## Discussions

The project subsite displays recent real topics from this hosting repository's public GitHub Discussions and links to GitHub for reading and participation. Each document links to its path's discussion search. No fake comments, public-site account service or credentials form is provided.

The workflow checks and attempts to enable Discussions. If the built-in token cannot change that setting, the owner must enable Settings > General > Features > Discussions once. The documentation view reports unavailability until activation is confirmed. Participation uses a GitHub account, separate from the platform's planned anonymous accounts.

## Pages settings and preview

Keep **Deploy from a branch**, branch **main**, directory **/ (root)**. Actions must be enabled and its token must be allowed to commit generated files. Workflow permissions are `contents: write`, `pages: write`, and `discussions: read`.

From the canonical repository:

```sh
cd github/pages
npm ci
npm run dev
```

Preview `/` for the website and `/KryptosTesMoiras/` for documentation. `npm run build` builds both; `npm run preview` serves the production result. Root `deployment.json` records the source revision used for both destinations.

## Existing project Pages site

The project repository also has its own Pages site, which can take precedence over the generated fallback folder at `/KryptosTesMoiras/`. Its `Publish project documentation` workflow builds the standalone document reader (`npm run build:docs`) and publishes it through that project’s existing Pages branch and directory. It preserves Markdown and owner-managed files and does not require a Pages setting change. The root website remains published by this hosting repository.
