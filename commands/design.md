---
description: Stage 2 - select an architecture and specify it as DESIGN.md (budget 10 min)
---

# Stage 2 - Design

Read `INTENT.md` and `AGENTS.md`. Do not reread `CHALLENGE.md`. Treat `INTENT.md` as the authoritative problem contract.

This stage does architecture selection and system design together, with one human decision point between them.

## Process

Apply the `architecture-design` skill.

1. **Architecture.** Characterize the problem, generate options only where a genuine alternative exists, recommend one, and present the tradeoffs.
2. **Stop and get the decision.** The AI recommends; the human chooses. Do not write the detailed design until the architecture choice is explicit.
3. **Design.** Specify the chosen architecture well enough to implement: components, control flow, tools, state, LLM/deterministic boundary, failure handling, and the minimal vertical slice.
4. **Self-check.** Run the skill's design self-check and fix what it finds.

## Output

`DESIGN.md`, opening with the `## Contract` section copied verbatim from `INTENT.md`.

## Boundaries

Do not write code or define file-by-file implementation order. If the intent turns out to be wrong, stop and return to Stage 1 rather than reinterpreting it.

## Budget

10 minutes across both halves. If you hit it, ship the design with gaps listed under `## Open Questions`.

## Human Gate

Present `DESIGN.md` for approval. Stop.
