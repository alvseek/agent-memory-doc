# Migration: the documentation-generation cluster moved here

**Date**: 2026-10-12

This repository was created by extracting the documentation-generation cluster out of
`agent-memory-project` (`hermod-project`). No procedure's behaviour changed on the way; they
moved, and the overlay stopped carrying them.

## What moved here

| From `agent-memory-project` | To |
|---|---|
| `procedures/discovery-contract.md` | `procedures/` |
| `procedures/generate-readme.md` | `procedures/` |
| `procedures/generate-docs.md` | `procedures/` |
| `procedures/generate-architecture-docs.md` | `procedures/` |
| `procedures/generate-domain-docs.md` | `procedures/` |
| `procedures/generate-flow-docs.md` | `procedures/` |
| `components/compute-doc-placement.md` | `components/` |
| `components/present-doc-for-review.md` | `components/` |
| `templates/readme-template.md` | `templates/` |
| `templates/architecture-doc-template.md` | `templates/` |
| `templates/domain-doc-template.md` | `templates/` |
| `templates/flow-doc-template.md` | `templates/` |
| `templates/domain-context-map-template.md` | `templates/` |
| `templates/flow-journey-map-template.md` | `templates/` |

## What changed on the way

- **The path placeholder** is now `[path-to-agent-memory-doc]`.
- **The installed identity**: folder prefix `agent-doc-`, manifest
  `.agent-memory-doc-opencode-manifest`, and its own marker UUIDs, so no installed folder or
  global-instruction definition can be shared with a sibling layer.
- **The orientation map left these procedures.** Discovery lists from disk alone; the stale-map
  flag, the status join and the map's `--rescan` pointer are gone. The map indexes docs on its
  own scan and reads `doc_type` frontmatter, so an artifact stays classifiable without these
  procedures knowing about the map at all. Six template lines and 18 generator lines carried
  that relationship and were removed with it.

## What stayed in the overlay

The shell (`awaken-coder`, `project-wrap-up`), project memory (`update-project-context`,
`load-project-context`), the orientation map itself (`map-orientation`), and push/pull
(`push-project`, `pull-project`, `push-all`, `pull-all`). `dockerize` also left the overlay,
but it went to `agent-memory-wizards`, not here.

## Lineage

The original `agent-memory-coding-skill` repository split five ways: `agent-memory-project`
(the shell and the project surface), **this repo**, `agent-memory-local`, `agent-memory-fleet`
and `agent-memory-wizards`.
