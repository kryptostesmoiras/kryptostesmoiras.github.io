# Documentation and Discussions publication

This repository publishes only the project's Markdown documentation and its public GitHub Discussions space. It does not publish the source-search portal, a private workspace, accounts, desktop binaries or sample projects.

## Single source and build

The canonical Markdown files and React/TSX document reader live in `kryptostesmoiras/KryptosTesMoiras`. The workflow `.github/workflows/publish.yml` checks out that repository, generates the document collection from all tracked `.md`/`.markdown` files, checks TypeScript and builds `github/pages/`.

The root `index.html`, `assets/`, `documents.json`, `discussions.json`, `favicon.svg` and `deployment.json` are generated publication files. Do not maintain copies of document content or UI code here by hand. `CNAME`, `.github/`, this documentation and other owner-managed configuration are preserved.

## Synchronization

Actions checks for changes every five minutes. It rebuilds if the source tree, publisher workflow or Discussions snapshot changed. GitHub can delay scheduled runs; this is not an instantaneous cross-repository push hook. A manual run is available in Actions > Publish documentation > Run workflow, with a `force` option.

No cross-repository token is required for the public source. The built-in token commits the generated files here and explicitly requests the existing branch-based Pages build. The workflow verifies that Pages built the expected commit, and retries on a later run after a failure.

GitHub may disable scheduled workflows in public repositories after 60 days without repository activity. Re-enable the workflow in Actions if this occurs.

## Discussions

The workflow checks this repository's Discussions feature and attempts to enable it. If GitHub denies that change to `GITHUB_TOKEN`, the repository owner must enable **Settings > General > Features > Discussions** once. The documentation deployment continues; the site reports Discussions as unavailable until activation is confirmed.

When enabled, the site lists up to 30 recently updated real discussions from the repository and links to GitHub for reading, replying and creating topics. Each document links to a Discussions search for its path. Counts and topic titles come from GitHub, not generated examples. This is native GitHub Discussions, not an embedded account or comment service: participation uses a GitHub account. No credentials, fake comments or private application accounts are collected by the documentation site.

## Pages settings

Keep **Deploy from a branch**, branch **main**, directory **/ (root)**. Actions must be enabled and repository rules must permit its token to commit generated files. Required workflow permissions are `contents: write` `pages: write` and `discussions: read`. The old React search portal is not an input to publication.

Local preview from the canonical repository:

```sh
cd github/pages
npm ci
npm run dev
```

Use `npm run build` and `npm run preview` to verify the production document reader. English Markdown remains in its source language; the navigation retains twenty UI languages and four themes plus system mode.
