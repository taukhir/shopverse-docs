# Backend Engineering Docusaurus Portal

This repository contains the Docusaurus application and its documentation
content. Markdown and MDX live under `docs/` (and the split `docs-*/`
instances), while React components, styling, static assets, and build
configuration remain beside it.

The complete setup, customization, content, image, Mermaid, search,
troubleshooting, and GitHub Pages deployment guide is:

```text
docs/operations/DOCUSAURUS.md
```

The portal is organized as a reusable backend engineering study library.
[Shopverse](https://github.com/taukhir/shopverse) appears as a case study
rather than defining the complete documentation taxonomy. This repository
holds only the documentation site; the platform's own code, service
READMEs, and ADR source-of-truth live in the main `shopverse` repository
and are linked to directly rather than mirrored here.

Reader experience includes local full-text search, Mermaid diagrams, dark
mode, collapsible navigation, a reading-progress indicator, image previews,
reading-time and word-count metadata, share and feedback actions, print-friendly
pages, and a back-to-top control for long technical guides.

## Local Development

```powershell
npm ci
npm start
```

Open `http://localhost:3000/shopverse-docs/`.

## mycheckout documentation

The **mycheckout** navbar and sidebar section starts at
`/shopverse-docs/mycheckout/overview`. Its checked-in pages and assets are a
snapshot of the separate checkout project's documentation; normal builds do
not require that project to exist on the build machine.

To refresh the snapshot explicitly:

```powershell
node scripts/import-mycheckout-docs.mjs "D:\BE Projects\checkout\docs"
npm run check:fast
npm run check:language
npm run build
```

The importer splits long guides into linked parts, maps original heading links,
copies selected diagram/document assets and updates the mycheckout sidebar.
`mycheckout-import-manifest.json` records source hashes, generated pages, assets
and local or stale references that could not become website links. Source code
references remain readable annotations when their files are outside the site.
Chat history, private shortcuts, raw dumps, generators and temporary previews
are excluded. Historical notes retain their original dates; import validation
does not reverify application behavior. Package/hostname examples are anonymized.

## Production Build

```powershell
npm run typecheck
npm run build
npm run serve
```

The generated static site is written to `build/`.

## Automated Verification

Run the same complete gate used by the main and scheduled CI workflows:

```powershell
npm run check
```

The gate validates all source pages, governed terminology, normalized
ownership/lifecycle metadata, sidebar registration, depth and
duplicate-content rules, executable Java and Spring examples, TypeScript,
strict Docusaurus links and anchors, the production build, all generated
routes and assets, performance budgets, accessibility, responsive layout,
images, Mermaid diagrams, reader features, and Chromium, Firefox, and
WebKit behavior.

Service READMEs and other platform-specific source material are **not**
mirrored into this site — pages that reference them link directly to the
canonical file in the `shopverse` repository instead, so there is nothing
here to keep in sync.

Useful narrower commands:

```powershell
npm run check:fast           # changed content and TypeScript
npm run check:content-quality
npm run check:build          # strict build, generated-site crawl, performance
npm run test:changed         # changed/representative routes on desktop + mobile
npm run test:cross-browser   # Firefox + WebKit smoke coverage
npm run test:visual          # committed Chromium screenshot baselines
npm run check:scheduled      # complete gate plus live official-link validation
```

Pull requests run changed-page and representative UI coverage. Pushes and the
weekly schedule run the complete suite. UI/theme changes also trigger visual
regression, and the schedule checks official external references. Browser failure
traces, screenshots, and diffs are uploaded by GitHub Actions.

## Content Rules

- Add reusable project and study material under `docs/`.
- Keep project ADRs under `docs-architecture/adr/` so they are rendered and
  searchable with the rest of the Docusaurus portal.
- Keep service-specific commands and configuration in each service's own
  README in the `shopverse` repository; link to it rather than duplicating it.
- Prefer Mermaid for architecture and sequence diagrams.
- Mark roadmap items as planned rather than implemented.
- For Shopverse-specific pages, separate current runtime behavior from
  production hardening and target design.
- Every Shopverse implementation claim should either link to runnable evidence,
  source/configuration, or the implementation matrix.
- Preserve generic study material as reusable guidance. Do not imply that a
  generic production practice is already implemented by Shopverse unless a
  case-study page marks it implemented.
- Link to source files instead of duplicating implementation code unnecessarily.
