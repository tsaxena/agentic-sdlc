# Writing Agent Design

## Purpose
Turn an approved architecture decision into a concise implementation-ready DESIGN.md.

## Inputs
- CHALLENGE.md
- INTENT.md
- architecture decision supplied by the user

## Procedure

Document:

1. Design thesis
2. High-level architecture
3. Major components
4. Control flow
5. Agent responsibilities
6. Tool interfaces
7. State
8. Deterministic vs LLM responsibilities
9. Failure handling / retries
10. Safety boundaries
11. Observability
12. Evaluation
13. Minimal vertical slice

Use diagrams where they improve clarity.

Make component boundaries explicit.

Call out which decisions are probabilistic and which are deterministic.

## Guardrails
- Preserve the architecture chosen by the user.
- Do NOT silently replace it with another architecture.
- If there is a serious flaw, flag it separately.
- Do NOT start coding.
- Do NOT design speculative future functionality.
- Optimize for an interview prototype rather than production completeness.

## Output
Create DESIGN.md.

Target length: approximately 150–200 lines maximum.