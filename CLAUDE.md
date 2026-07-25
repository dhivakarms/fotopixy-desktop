# Fotopixy — desktop

Fotopixy is a multi-tenant billing + print/delivery tracking system for photo studios in India, connecting **Studio** organizations and **Lab** organizations. This repo is a **thin Electron shell** — it does not duplicate any Angular code.

Sibling repos (same overall app, split for independent deployment):
- Frontend (Angular — this shell loads its build output): https://github.com/dhivakarms/fotopixy-frontend
- Backend (FastAPI): https://github.com/dhivakarms/fotopixy-backend

## What this repo is
`main.js` creates a `BrowserWindow` that loads `http://localhost:4200` in dev or the frontend repo's built `dist/frontend/browser/index.html` in production. `preload.js` is reserved for future native integrations (printer, cash drawer) via Electron's context bridge/IPC — currently empty, nothing wired up yet.

There is intentionally **no separate Angular app here** — all UI code lives in the frontend repo. This repo only exists to package that app as a native desktop installer and provide a place for native OS integrations the browser can't do (direct printer access, cash drawer, etc.).

## Tech stack
Plain Electron project (`package.json` + `electron` devDependency), no monorepo tooling. Node pinned via `.nvmrc` (24.18.0), matching the frontend repo.

## Skills
None yet — no list/form/detail concept applies to a thin shell. If desktop-specific patterns emerge (e.g. IPC handler conventions), they'd go in `.claude/skills/` here.

## Distribution
Not part of the Render server deployment — this is a downloadable installer, not a hosted service. Plan is to attach packaged builds (`.dmg`/`.exe` via `electron-builder`, not yet configured) to GitHub Releases on this repo for studio owners to download directly.

## User context
Building this with someone who's an experienced Angular developer but completely new to Python (not directly relevant to this repo, but shapes how the overall project is explained). They explicitly prioritize doing things step by step: implement one concrete piece at a time and check in, rather than chaining many steps autonomously. Prefer plain, standard tooling over opinionated scaffolding frameworks.
