# P != NP: The Fifty-Year Wall

An interactive research journal about the P versus NP problem, its major barriers, and the consequences of a hypothetical proof. The project combines a long-form article with browser-based visualizations and simulations so that the ideas can be explored rather than only read.

## What is included

- A 3D "Fifty-Year Wall" hero built with the locally vendored Three.js runtime.
- Interactive demonstrations for verification versus search, SAT solving, reductions, complexity barriers, Impagliazzo's five worlds, collapse scenarios, and defensive strategies.
- A full research article rendered inside the demo, covering relativization, natural proofs, algebrization, fine-grained complexity, cryptography, and related topics.
- A static GitHub Pages deployment with no CDN dependency for the main demo experience.
- A Next.js shell and supporting Prisma/database scaffolding for future expansion beyond the current static journal.

## Requirements

- Node.js 22 or newer.
- npm 10 or newer.
- A modern browser with JavaScript enabled. WebGL improves the 3D experience but is not required for reading the article.
- Bun is additionally required only for the `npm start` script.

## Quick start

```bash
npm ci
npm run dev
```

Open [http://localhost:3000](http://localhost:3000). The root route redirects to the interactive journal at `/demo.html`.

For a static-only preview, open `public/demo.html` directly in a browser or serve the project directory with a local static server. Serving it over HTTP is recommended because browser security policies can affect local assets and some interactive behavior.

## Commands

| Command | Purpose |
| --- | --- |
| `npm run dev` | Start the Next.js development server on port 3000. |
| `npm run lint` | Run ESLint across the repository. |
| `npm run build` | Build the application. GitHub Actions produces the static `out/` site; local builds produce a standalone Next.js server bundle. |
| `npm run start` | Run the local standalone production server after a build. Requires Bun. |
| `npm run db:generate` | Generate the Prisma client. |
| `npm run db:push` | Push the Prisma schema to the configured database. This allows destructive changes. |
| `npm run db:migrate` | Create and apply a development Prisma migration. |
| `npm run db:reset` | Reset the development database and apply migrations. |

## Build and deployment

GitHub Pages deployment is defined in `.github/workflows/deploy-pages.yml`.

On every push to `main`, the workflow:

1. Installs dependencies with `npm ci` using Node.js 22.
2. Runs `npm run build` with `GITHUB_ACTIONS=true`.
3. Copies `public/demo.html` to `out/index.html` so the Pages root opens the journal directly.
4. Uploads `out/` as the Pages artifact and deploys it.

To reproduce the Pages output locally:

```bash
GITHUB_ACTIONS=true npm run build
```

The generated `out/` directory is ignored by Git and can be inspected locally after the build.

## Project layout

```text
.
├── build_parts/             Historical HTML source parts for the demo
├── public/
│   ├── demo.html            Shipped interactive journal
│   └── vendor/three.min.js  Local Three.js runtime
├── src/app/                 Next.js entry point, layout, styles, and API route
├── src/components/ui/       Reusable UI primitives
├── src/hooks/               Shared React hooks
├── src/lib/                 Shared utilities and database access
├── prisma/schema.prisma     Prisma data model
├── db/custom.db             Local database fixture for the alternate runtime
├── tests/                   Runtime/build verification scripts
├── .zscripts/               Alternate standalone/container build tooling
└── .github/workflows/       GitHub Pages deployment
```

The current user-facing experience is intentionally concentrated in `public/demo.html`. The Next.js application provides the route shell and the path toward a fuller application architecture.

## Editing the demo

The assembled demo lives in `public/demo.html`. The historical source parts are kept in `build_parts/` for reference and manual reconstruction. The runtime loads Three.js from `public/vendor/three.min.js`, so changes should preserve that relative asset path unless the deployment layout is changed as well.

When changing the interactive page:

1. Run the development server and test the affected interaction in a browser.
2. Check both a desktop viewport and a narrow mobile viewport.
3. Run `npm run build` to verify that the Pages export still completes.
4. Keep generated output, screenshots, logs, and local environment files out of Git.

## Data and environment

Environment files matching `.env*` are ignored. Do not commit credentials or private connection strings.

The Prisma and database files are retained for the project's alternate runtime path, but the current GitHub Pages experience is static and does not require a database connection. Review the Prisma scripts before using them against a shared or production database.

## Current status

The interactive journal is the active deliverable. The production build currently succeeds. ESLint still reports two existing `react-hooks/set-state-in-effect` findings in the reusable carousel and mobile hook files; those findings are unrelated to the static journal cleanup and have not been changed here.

## License and attribution

This project is released under the [MIT License](LICENSE). The project vendors Three.js locally under `public/vendor/` for offline-friendly delivery; preserve its upstream license and attribution requirements when redistributing the repository.
