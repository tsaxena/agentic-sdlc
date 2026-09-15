---
description: Stage 4 - implement and verify the P0 vertical slice (budget 45 min)
---

# Stage 4 - Build

Read `IMPLEMENTATION_PLAN.md` and `AGENTS.md`. Do not reread `DESIGN.md`, `INTENT.md`, or `CHALLENGE.md`. Treat the plan as the implementation contract.

## Process

Apply the `implementation-execution` skill.

1. Execute P0 steps in plan order.
2. Run the plan's verification after each meaningful step. Never batch several components before running anything.
3. On any failure, apply the `debugging-loop` skill.
4. Continue until the P0 path works end to end, or a blocking upstream issue appears.
5. Run the full P0 slice once more, cleanly.

Record what you built, what you verified, known limitations, and any deviation from the plan. Keep this in the conversation - Stage 5 reads the code and the plan, not a summary document.

## Boundaries

If implementation requires changing the approved plan or design, stop, explain the conflict, and return the decision to the owning stage. Do not silently redesign. Do not start P1 until the user approves.

Never hard-code an output to make a run look successful.

## Budget

45 minutes. At 35 minutes, stop adding and make whatever exists run end to end. A thin slice that works beats a wide one that does not.

## Output

Working P0 implementation plus the tests you wrote along the way. Stop before the formal review.
