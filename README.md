# agent-memory-doc

The **documentation-generation cluster** for the [agent-memory](https://github.com/alvseek/agent-memory-system) framework: five doc generators, the shared discovery contract they all read, and the components and templates they carry.

Extracted from the coding overlay on **2026-10-12**. These procedures lived in `agent-memory-project` before that, and moved because they change for their own reasons: a new doc lens has nothing to do with push/pull or with tending a session, and they are the overlay's one concern that produces artifacts rather than memory.

## Relationship to the framework

- **Standalone, independent repo** — a *peer* of the memory core ([`agent-memory-system`](https://github.com/alvseek/agent-memory-system) / `control-files`), the coding overlay ([`agent-memory-project`](https://github.com/alvseek/agent-memory-project)), the fleet ([`agent-memory-fleet`](https://github.com/alvseek/agent-memory-fleet)), the wizards ([`agent-memory-wizards`](https://github.com/alvseek/agent-memory-wizards)) and the localization lane ([`agent-memory-local`](https://github.com/alvseek/agent-memory-local)).
- **One-way dependency**: this repo references the core; the **core never references this repo by name**.
- **It is a leaf.** Nothing calls it, so it declares no access of its own and carries no access declaration.

## Contents

| Path | What it holds |
|---|---|
| `procedures/` | the six procedures: `generate-readme`, `generate-docs` (the cross-lens orchestrator), `generate-architecture-docs`, `generate-domain-docs`, `generate-flow-docs`, and `discovery-contract` |
| `components/` | `compute-doc-placement` and `present-doc-for-review`, inlined into a generator at compile time so an installed skill never points at a file the agent cannot reach |
| `templates/` | the six doc templates the generators copy into the target repository by path |
| `setup-scripts/` | the compile and install tooling |

## How generation works

A generator is entered three ways. **Bare** runs discovery: it lists that lens's units marked documented-versus-not, and stops for the human's pick. A **named unit** runs one deep-dive. The **`[M]` pick** synthesizes that lens's whole-system artifact. `generate-docs` is the cross-lens `[M]`: it delegates to all four map paths and reports the whole documentation surface in one table.

Discovery lists from **disk alone**, and every generated artifact carries `doc_type` frontmatter so an indexer can classify it. Nothing here reads or writes the orientation map: the map indexes docs on its own scan.

## Setup

Install the **memory core first**, then this repo:

```bash
python setup-scripts/setup-all-opencode.py      # -> ~/.config/opencode/skills
```

It honours `AGENT_MEMORY_TARGET_DIR`, keeps its own manifest (`.agent-memory-doc-opencode-manifest`), and protects every sibling's in the same skills directory, so re-installing any layer leaves the others intact.

## Status

Extracted from the coding overlay on 2026-10-12; the decision is recorded in [ADR-024](https://github.com/alvseek/agent-memory-project/blob/main/docs/adr/2026-10-12-hermod-doc-extraction-and-hermod-server.md). Installs OpenCode-only for now.

The procedures are markdown that an agent *executes*, so the license covers them as source: copying a procedure into your own fleet, adapting it, or shipping it inside a commercial product is all permitted, provided you keep the notice.

## License

Licensed under the Apache License 2.0, the same license the memory core carries. See [LICENSE](LICENSE) and [NOTICE](NOTICE).
