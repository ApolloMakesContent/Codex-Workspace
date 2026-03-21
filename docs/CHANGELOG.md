# Changelog

## 2026-03-21

- Moved the canonical workspace handover docs from `tools/docs/` to the root `docs/` folder.
- Removed the duplicated documentation links from `shared/` so it acts as a metadata-only layer.
- Rewrote the repo root `README.md` to behave more like a public project homepage.
- Added `LICENSE`, `.github/CONTRIBUTING.md`, and a scaffolded `.github/FUNDING.yml`.
- Normalized workspace docs away from the old machine-specific path assumptions.

## 2026-03-17

- Moved the six canonical workspace handover docs from the workspace root into `tools/docs/`.
- Repointed `shared/` handover links to the new canonical doc location.
- Updated workspace docs so `tools/docs/` is the source of truth and `shared/` acts as the compatibility and metadata layer.
- Added `tools/docs/HANDOVER.md`.
- Added `tools/docs/CHANGELOG.md`.
- Added or updated repo-root `.gitignore` files across detected repos for macOS metadata and Google Drive icon files.

## 2026-03-16

- Built the workspace foundation and shared tooling structure.
- Created the standalone `repos/workspace-hub/` application.
- Implemented repo discovery, conservative classification, and summary APIs.
- Added core repo actions including open, preview, runtime start, stop, and restart.
- Added persisted repo metadata overrides under `repos/workspace-hub/data/`.
- Added manifest authoring and repo-native preset support in `workspace-hub`.
- Added `repos/workspace-hub/docs/` with repo-local documentation guidance and a manifest guide.
