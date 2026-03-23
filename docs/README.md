# Docs

This folder is the canonical home for the Codex Workspace documentation set.

Use [../README.md](../README.md) as the public-facing project entrypoint, then use this folder for the detailed workspace and handover material.

## Core pack

Read these in order:

1. `00-overview.md`
2. `01-codex-workspace-handover.md`
3. `02-local-runtime-handover.md`
4. `03-workspace-hub-build-spec.md`
5. `04-build-order-and-dod.md`
6. `05-examples-and-templates.md`
7. `06-cross-agent-skills-and-mcp.md`
8. `07-context-cache-and-retrieval.md`
9. `08-first-run-and-updates.md`
10. `HANDOVER.md`
11. `CHANGELOG.md`

## What Lives Here

- `00-overview.md` to `05-examples-and-templates.md` define the handover pack.
- `06-cross-agent-skills-and-mcp.md` defines the cross-agent portability layout for skills and MCP.
- `07-context-cache-and-retrieval.md` defines the layered context-cache model and retrieval visibility rules.
- `08-first-run-and-updates.md` defines the recommended onboarding questions, setup profiles, and update flow.
- `HANDOVER.md` summarizes the current state of the workspace after the initial build.
- `CHANGELOG.md` records notable workspace-level changes.

## Related Locations

- `tools/bin/` holds small wrappers or launch helpers.
- `tools/scripts/` holds reusable workspace scripts.
- `tools/templates/` holds starter metadata templates.
- `tools/manifests/` holds source lists and supporting manifests for scripts.
- `docs/wiki/` holds starter content for the optional GitHub wiki surface.
- `repos/workspace-hub/docs/` holds repo-local documentation for Workspace Hub itself.

Useful maintenance scripts:

- `tools/scripts/bootstrap-repo.sh` previews or runs repo-native install/setup using manifest `installCommand` first, then package-manager precedence such as env override, manifest `packageManager`, `package.json`, and lockfiles.
- `tools/scripts/doctor-workspace.sh` runs a non-destructive environment and readiness check for the workspace, Workspace Hub, mixed-stack tooling, and Codex-related setup.
- `tools/scripts/cleanup-sync-noise.sh` removes macOS and sync-client noise files such as `Icon\r` and `._*`, including the broken-ref cases when they leak into `.git/`.
- `tools/scripts/init-agent-job-bundle.sh` previews or creates a local cache/context bundle for longer-running agent jobs under `cache/context/agents/jobs/`.
- `tools/scripts/setup-workspace-profile.sh` provides a guided, non-destructive profile check for `core`, `hub`, `mixed-stack`, `wordpress`, `agent-enhanced`, `workflow-state`, `spec-driven`, and `ui-previews`.
- `tools/scripts/sync-codex-skills.sh` previews or syncs tracked workspace skill sources into repo `.agents/skills/` folders, with dry-run mode by default.
- `tools/scripts/trim-git-repos.sh` performs safe Git maintenance across `repos/` by cleaning `.git` sync noise, expiring older reflog entries, and running `git gc` with a conservative prune window.
- `tools/scripts/update-all.sh` can now fast-forward all repos or only a named repo group from a JSON manifest via `--group`.

Useful template locations:

- `tools/templates/skills/` holds starter skill packs, execution-mode conventions, and a selective install-profile example.
- `tools/templates/mcp/` holds starter MCP profiles for `read-only` versus `mutating` capability tiers and stdio/logging hygiene.
- `tools/templates/openspec/` holds lightweight tracked spec and change templates for larger work.
- `tools/templates/ui-previews/` holds guidance for repo-local component preview tooling.
- `tools/templates/artifacts/` holds the local artifact-bundle convention for longer-running agent jobs.
- `tools/templates/workflow-state/` holds guidance for optional local workflow-state layers such as `.cognetivy/`.
- `tools/templates/agents-md/` holds guidance for optional `AGENTS.md` composition when plain single-file authoring stops scaling.

## Shared Metadata

The `shared/` folder is reserved for workspace-facing metadata such as `shared/repo-index.json` and `shared/standards.md`.

## Recommended machine-level tools

- Core: `git`, `gh`, `jq`, `rg`, `fd`, `tree`
- Node: a version manager plus `npm`, `pnpm`, and `yarn` where legacy repos need it
- Python: `python3`, `pip`, optional `uv`
- PHP: `composer`, `wp`, optional ServBay or Local

## Shared cache targets

- npm: `cache/npm`
- pnpm: `cache/pnpm-store`
- yarn: `cache/yarn`
- pip: `cache/pip`
- Homebrew downloads: `cache/homebrew`

Map package-manager caches here where practical, but keep project installs inside each repo.
