# Membrane (latent-io)

**Membrane: treating model I/O as a selective membrane between latent reasoning
and the external world — pushing the token boundary out to where it is actually
needed.**

## What this is

Current LLM and VLM systems do everything interesting in continuous latent
space, yet every I/O operation — retrieval, tool use, code execution, reading a
file — forces a hard round-trip through tokens: full serialization out, full
re-encoding in. Tokens are load-bearing at *commitment* boundaries and at the
edge of external tools; everywhere else they may be scaffolding. The research
bet is that moving the token boundary outward buys both efficiency and
capability. Four design moves, in rough order of ambition: latent queries
against a latent index, spliced back into the residual stream without
tokenizing; a continuous uncertainty signal as the retrieval trigger;
retrieval as a layer rather than a prompt-time step; and action–observation
traces kept latent between commitments. RETRO, Atlas, and kNN-LM are partial
prior art; the move is to make latent I/O primary rather than a soft assist.
`concepts/` holds the atomic ideas; `NOTES.md` has the framing history.

Personal research project. See `CLAUDE.md` for the agent-facing orientation
and `~/.claude/CLAUDE.md` for the framework's durable principles.

## Quick start

```sh
make env       # uv sync
make lint      # orphan/dead-link check
```

## Layout

- `raw/` — immutable sources (papers, repos, web captures).
- `literature/` — processed notes.
- `concepts/` / `mocs/` — knowledge graph.
- `experiments/` — runs, each dated and slugged.
- `docs/decisions/` — ADRs.
- `journal/` — per-session log.
- `_meta/` — index, log, templates.
