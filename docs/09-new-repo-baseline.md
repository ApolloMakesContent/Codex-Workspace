# New Repo Baseline

Use this document as the default baseline for any repository added under `repos/` in the Codex Workspace.

This is not meant to force every repo into one shape. The goal is to keep each repo independently runnable while making workspace behaviour predictable.

## What every new repo should preserve

- Keep the repo independently runnable on its own terms.
- Do not merge unrelated repos into one shared dependency install.
- Use shared caches under workspace `cache/` where that helps, but keep installs local to the repo.
- Do not make ServBay mandatory unless the repo genuinely needs proxy or mapped-host behaviour.
- Prefer the repo's native runtime and package manager.

## Default runtime expectations

### Static, Vite, Three.js, WebGL, and similar frontend repos

- Default to `direct` runtime.
- Prefer running on the repo's own local port.
- Do not force these repos behind ServBay by default.

### WordPress repos

- Default to `external` runtime.
- Keep existing Local-managed projects on Local unless there is a clear reason to move them.
- Use ServBay only when it adds practical value and does not become a hidden requirement.

### Other server-side repos

- Use repo-native runtime first.
- Add proxy or mapped-host support only when it solves a real local workflow problem.

## Recommended files for new repos

When useful, add small explicit metadata instead of hidden assumptions:

- `.workspace/project.json` for runtime mode, launch command, preview URL, or notes
- `README.md` for setup and run instructions
- `HANDOVER.md` when the repo needs a resumable state document
- repo-level `AGENTS.md` only when the repo genuinely needs rules beyond the workspace baseline

## `.workspace/project.json` guidance

Add `.workspace/project.json` when runtime behaviour is not obvious from the repo files alone.

Typical reasons:

- the repo can run in more than one mode
- the startup command is non-obvious
- the preview URL is not inferable
- the repo should be treated as `external`

Keep the manifest lightweight. It should clarify runtime behaviour, not become a second config system.

## Safe defaults for setup work

- Classify conservatively when repo type is unclear.
- Do not auto-run heavy install steps without a clear reason.
- Do not assume one package manager across all repos.
- Do not hard-code machine-specific paths inside repos when a relative or inferred path will do.

## Minimal onboarding expectation

For a repo to feel workspace-ready, it should ideally have:

1. a clear way to run or preview it
2. a known runtime mode: `direct`, `external`, or explicit repo-native server mode
3. enough docs that another person can resume work without guessing

## Override rule

If a repo has its own `AGENTS.md` or clearer local docs, those should refine this baseline rather than duplicate it.
