# Changelog

## 2026-03-23

- Refined the skills guidance so `.agents/skills/` is documented as the native repo-level Codex location, with `shared/skills/` as shared source material and `.workspace/skills/` as an optional secondary compatibility layer.
- Clarified that third-party orchestration layers and generated agent setup should remain optional local tooling rather than the canonical workspace layout.
- Added `tools/scripts/sync-codex-skills.sh` to preview or sync tracked skill sources into repo `.agents/skills/` folders.
- Added `docs/08-first-run-and-updates.md` plus `tools/scripts/doctor-workspace.sh` to define onboarding questions, setup profiles, and the recommended layered update flow.
- Added a narrow “patterns, not platforms” note for larger agent systems: progressive skill loading, execution modes, and filesystem-backed job artifacts are in scope, while full orchestration remains local-only and optional.
- Added starter skill templates and a selective install-profile example under `tools/templates/skills/`.
- Added generic MCP templates and hygiene guidance: `read-only` by default, explicit `mutating` opt-in, and quiet stdio/logging conventions for future workspace MCP tools.
- Updated `bootstrap-repo.sh` to use package-manager precedence before lockfile fallback, and added `tools/scripts/setup-workspace-profile.sh` as a guided non-destructive profile helper.
- Added optional tracked spec templates, repo-local UI preview guidance, and a local agent-job artifact bundle script for larger or riskier work.
- Added optional local workflow-state guidance, optional `AGENTS.md` composition guidance, repo-group manifest support in `update-all.sh`, and a hash-seeded `audit.jsonl` file in local job bundles.
- Added importable GitHub ruleset JSON for protecting `main` and `v*` release tags without forcing a PR-only workflow.
- Added minimal tracked GitHub Copilot instructions plus a local-only Copilot skeleton for personal prompts, notes, and machine-specific setup.

## 2026-03-22

- Clarified that upstream skill catalogs such as `openai/skills` should be treated as optional sources for selected Codex skills rather than vendored workspace dependencies.
- Added matching guidance in the root README, the cross-agent skills and MCP note, and the Workspace Hub extension guide.

## 2026-03-21

- Added GitHub Discussions support links so repository questions are routed toward Discussions Q&A instead of Issues.
- Added starter GitHub wiki pages under `docs/wiki/` for a thin navigational wiki that points back to the tracked docs set.
- Expanded the public project framing across the root docs to describe the filesystem-first context model, observable retrieval, and tracked-versus-local memory rules more directly.
- Added cross-agent skills and MCP guidance plus a context-cache and retrieval note for generated summaries and provenance.
- Refreshed the README cover path with a versioned asset to avoid stale GitHub image caching.
- Updated the repository social preview artwork to match the current project framing.
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
