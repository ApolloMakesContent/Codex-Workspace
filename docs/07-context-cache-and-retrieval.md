# 07-context-cache-and-retrieval

## Purpose

This note defines a lightweight context model for Codex Workspace and Workspace Hub.

The goal is to make workspace context easier for agents and tooling to find, load, and reason about without turning the workspace into a separate agent platform.

This is intentionally filesystem-first:

- tracked repo docs remain the source of truth
- generated summaries live in `cache/`
- skills stay portable
- local operator memory stays local
- retrieval remains inspectable instead of opaque

## Why this matters

AI-assisted workspaces often accumulate context in too many places:

- repo docs
- manifests
- README files
- screenshots
- local notes
- agent skills
- runtime metadata

When that context is scattered, agents either miss useful information or load too much irrelevant detail too early.

Codex Workspace should avoid that failure mode by treating context as a small, visible filesystem structure rather than as an invisible prompt dump.

## Challenges

In a mixed-repo workspace, the main problems are usually:

- fragmented context across many repos and formats
- too much detail loaded too early
- weak visibility into which files informed a summary or decision
- local-only operator knowledge getting mixed into tracked repo docs
- repo guidance and agent guidance drifting apart

## Our approach

Codex Workspace uses a practical context model built around four ideas:

### 1. Filesystem-shaped context

Useful context should live in normal folders and files that are easy to inspect.

Examples:

- repo `README.md`
- `.workspace/project.json`
- repo-local `.workspace/skills/`
- workspace-wide `shared/skills/`
- generated repo summaries in `cache/context/`

### 2. Layered context loading

Do not load full repo details by default.

Use a three-layer model:

- `L0` abstract: a short summary for quick relevance checks
- `L1` overview: a concise operating view for planning and navigation
- `L2` details: the original docs, manifests, source files, and logs

### 3. Observable retrieval

When a tool or agent uses a summary, it should be possible to see which files fed that summary.

That keeps repo classification, summaries, and recommendations debuggable.

### 4. Local memory stays local

Private notes, secrets, and machine-specific MCP settings should not be folded into tracked project context.

Tracked context should remain portable. Local memory should remain local.

Local memory is still useful, but it should be deliberate, reviewable, and clearly separated from canonical repo facts.

## Context categories

The workspace should treat context as a few explicit categories:

### Resources

Tracked project material such as:

- `README.md`
- `docs/`
- `.workspace/project.json`
- screenshots and covers
- selected config files that explain runtime behaviour

### Skills

Portable workflow guidance such as:

- `shared/skills/`
- `repos/<repo>/.workspace/skills/`

### Local memory

Private operator notes and machine-specific configuration such as:

- `.workspace/project.local.json`
- `docs/*.local.md`
- `tools/local/agents/`

This material should stay untracked by default because it is often private, short-lived, or specific to one machine or operator.

### Runtime state

Generated status or process information such as:

- last known preview URL
- healthcheck state
- process status
- generated context cache metadata

## Cache layout

Use `cache/context/` for generated summaries and retrieval metadata.

Suggested layout:

```text
Codex Workspace/
└── cache/
    └── context/
        ├── workspace/
        │   ├── abstract.md
        │   ├── overview.md
        │   └── sources.json
        └── repos/
            └── workspace-hub/
                ├── abstract.md
                ├── overview.md
                ├── sources.json
                └── retrieval-log.jsonl
```

## File roles

### `abstract.md`

`L0` summary.

Keep this short enough for a quick relevance decision.

Typical contents:

- what the repo is
- its type
- its preferred runtime mode
- its main preview or entry point

### `overview.md`

`L1` summary.

Keep this detailed enough for planning work without forcing a read of the full repo.

Typical contents:

- stack
- key commands
- main directories
- runtime assumptions
- important manifests
- known caveats

### `sources.json`

Retrieval provenance for the current summaries.

Suggested fields:

```json
{
  "version": 1,
  "generatedAt": "2026-03-21T10:30:00Z",
  "repoRoot": "/absolute/path/to/repo",
  "inputs": [
    {
      "path": "README.md",
      "kind": "readme",
      "mtime": "2026-03-20T13:00:00Z"
    },
    {
      "path": ".workspace/project.json",
      "kind": "manifest",
      "mtime": "2026-03-20T13:05:00Z"
    }
  ]
}
```

### `retrieval-log.jsonl`

Optional local log for debugging context usage.

Good entries:

- which repo was queried
- which summaries were read
- which source files were opened next
- whether the cached summaries were stale

Keep this local and disposable.

## Classification provenance

Repo summaries are only part of the story. Repo classification should also be explainable.

Useful provenance to capture or expose includes:

- which detection files were found
- which manifest values overrode inference
- which runtime signals were considered authoritative
- whether local-only overrides influenced the current view

This keeps “why did the tool decide this?” answerable.

## Retrieval flow

The default retrieval path should be simple:

1. check `L0` abstract to see whether the repo or workspace area is relevant
2. if relevant, read `L1` overview for planning context
3. open `L2` source files only when deeper detail is required
4. record the source files used so the result is explainable

This keeps token usage lower and makes context selection easier to debug.

## Source of truth rule

Generated context files are not the source of truth.

The source of truth remains:

- tracked docs
- manifests
- repo files
- explicit local overrides where appropriate

If generated summaries disagree with the repo, regenerate or discard the cache.

Tracked repo facts should win over generated summaries. Local-only operator notes should not silently become shared repo truth.

## Update rules

- write generated context under `cache/`, not into repo docs by default
- keep repo summaries reproducible from tracked files
- never write secrets into `cache/context/`
- do not treat inferred summaries as authoritative when the manifest says otherwise
- prefer regeneration over manual editing of generated files
- keep operator memory reviewable and separate from generated summaries
- promote durable local knowledge into tracked docs instead of letting private notes become the only source

## Workspace Hub scope

For Workspace Hub, the relevant near-term use is modest:

- detect whether context cache files exist
- show whether summaries are fresh or stale
- link to the source files behind a summary
- use cached `L0` and `L1` summaries to reduce repeated full-repo reads
- explain which files and signals drove repo classification when available

Good future enhancements:

- regenerate summaries on demand
- show a summary provenance panel
- explain which detection signals classified a repo

Workspace Hub should not become a mandatory context database service in v1.

## Relationship to skills and MCP

This context cache does not replace the skills and MCP layout.

Use:

- [06-cross-agent-skills-and-mcp.md](06-cross-agent-skills-and-mcp.md) for portable skill and MCP structure
- this file for generated summaries and retrieval visibility

## Practical outcome

This model gives the workspace a simple, inspectable context layer:

- portable tracked context where it belongs
- generated summaries where caches belong
- private operator memory kept private
- better agent navigation without a heavy new platform dependency
- clearer reasoning about how the workspace reached a given summary or classification
