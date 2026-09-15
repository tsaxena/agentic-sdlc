---
description: Stage 5 - review the implementation and evaluate it against the contract (budget 15 min)
---

# Stage 5 - Verify

Read `IMPLEMENTATION_PLAN.md`, the current implementation, and the existing tests. The `## Contract` section at the top of the plan is the acceptance standard.

This stage does implementation review and system evaluation together, producing one artifact.

## Process

1. Apply the `implementation-review` skill. It covers plan fidelity, correctness, agent boundaries, reliability, state, tool handling, unnecessary complexity, and test gaps.
2. Fix P0 blockers with the smallest targeted change, then rerun the affected tests.
3. Apply the `agent-evaluation` skill. Define expected behavior for each case **before** running it, then run the system and score against the `## Contract`.
4. Write `VERIFY.md`.

## Fixing during evaluation

Record failures rather than fixing them, with one exception: a failure that breaks a `## Contract` acceptance criterion gets fixed now, and the fix is recorded in `VERIFY.md` along with which cases were rerun after it.

Deferring a contract-breaking bug to "a later pass of the SDLC" means shipping a system that does not meet its own stated bar.

## Boundaries

Do not redesign, expand scope, implement P1, refactor broadly, or fix stylistic issues. Do not redefine success criteria after seeing results.

## Budget

15 minutes. Prioritize: contract criteria first, then failure modes, then everything else.

## Output

`VERIFY.md` containing:

* `## Contract` (copied verbatim from `IMPLEMENTATION_PLAN.md`)
* `## Review` - P0 status per item, blockers with evidence, fixes applied, plan deviations
* `## Test Gaps` - what is untested that matters
* `## Evaluation` - cases run, expected vs actual, score per case
* `## Contract Result` - PASS / PARTIAL / FAIL per acceptance criterion
* `## Top Failure Modes`
* `## Highest-Value Next Improvement`

End with exactly one status line: `MEETS CONTRACT` or `DOES NOT MEET CONTRACT`.
