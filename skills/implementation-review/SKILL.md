---
name: implementation-review
description: Determine whether the implementation faithfully executes IMPLEMENTATION_PLAN.md and is tested well enough for system-level evaluation, focusing on correctness, reliability, test gaps, and unnecessary complexity. Use in Stage 5 (Verify) of the agentic SDLC.
---

# Implementation Review

Decide whether the P0 implementation is correct and sufficiently tested to evaluate. Behavior over style.

## Inputs

`IMPLEMENTATION_PLAN.md` (including its `## Contract`), the current implementation, the existing tests.

## Method

### 1. P0 status

For each P0 item, classify `PASS | PARTIAL | FAIL | NOT VERIFIED` using evidence from code, tests, or an actual run. Code existing is not evidence that it works.

### 2. Plan fidelity

Missing P0 functionality, changed interfaces, changed control flow, skipped deterministic gates, unexpected components, unrequested P1 work, undocumented deviations.

Not every deviation is wrong, but every meaningful one should be understood.

### 3. Correctness on critical paths

Incorrect assumptions, logic errors, invalid state transitions, malformed output handling, mishandled tool results, failures treated as success, unsafe side effects.

"Failure treated as success" is the highest-yield thing to look for in an agentic system, because it is the one the happy-path demo cannot reveal.

### 4. Agent boundaries

Where LLM reasoning is used, verify it has not taken control of stopping conditions, validation, permissions, retries, success checks, idempotency, or irreversible actions.

### 5. Reliability

Bounded execution, retry limits, timeouts, tool failures, malformed model output, repeated actions, partial failure, safe termination. Only what the approved plan actually needs.

### 6. State

Important state is explicit, consistently updated, owned by a clear component, and available when later steps need it. Watch for hidden dependence on conversational context and accidental globals.

### 7. Tool boundaries

Inputs validated, outputs checked, errors propagated or handled, side effects understood, retries safe, success verified.

### 8. Complexity

Unused abstractions, dead code, speculative extensibility, duplicate logic, unnecessary frameworks. Do not request cleanup for aesthetics.

### 9. Test gaps

Run `references/test-gaps.md`. Confidence in critical behavior, not coverage percentage.

## Output

Feed this into the `## Review` and `## Test Gaps` sections of `VERIFY.md`:

* **P0 status** per item
* **Blockers** - must fix before evaluation. Each with issue, evidence, impact, smallest fix.
* **Important issues** - non-blocking, worth doing if time remains
* **Plan deviations** - or `None`
* **Simplification opportunities** - only significant unnecessary complexity
* **Test gaps** - critical behavior not covered, and the minimal test that would cover it

## Guardrails

Do not redesign, broaden scope, add features, refactor for style, or treat every code-quality issue as a blocker. Prefer small targeted fixes.
