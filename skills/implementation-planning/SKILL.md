---
name: implementation-planning
description: Turn an approved DESIGN.md into a small, ordered IMPLEMENTATION_PLAN.md that delivers a working end-to-end vertical slice, split into P0 / P1 / out of scope, and self-check it before presenting. Use in Stage 3 (Plan) of the agentic SDLC.
---

# Implementation Planning

Turn an approved `DESIGN.md` into the smallest ordered plan that reaches a working end-to-end system.

## Input

`DESIGN.md`. Its design, interfaces, invariants, and vertical slice are authoritative.

## Method

### 1. Find the end-to-end path

The minimum path from real input to real output that proves the design works. Include only the components on it.

### 2. Set priorities

* **P0** - everything necessary for a working end-to-end system.
* **P1** - useful, but not needed to prove the architecture.
* **Out of scope** - explicitly deferred.

Size P0 against the build budget, not against completeness. When in doubt, move it to P1.

### 3. Break P0 into ordered steps

Per step: objective, files or modules affected, key interface, expected behavior afterward, and how to verify it. Prefer steps that leave the repository runnable.

### 4. Order for early feedback

Respect dependencies, but favor an order that reaches end-to-end execution soonest and exposes the riskiest unknown first. The step most likely to fail should not be the last one.

### 5. Plan incremental verification

Every meaningful step gets a concrete verification action: run a function, run a CLI command, execute a focused test, inspect structured output, exercise one tool call, run the slice. Never postpone all testing to the end.

### 6. Name the blocking risks

Only risks likely to block implementation: auth, external APIs, unclear tool behavior, model output parsing, environment setup, state handling, side effects. Each gets the simplest mitigation or fallback.

### 7. Define done

Exactly what must work before the build stage is complete, tied to the vertical slice and to the acceptance criteria in `## Contract`.

## Guardrails

Do not change the architecture, redesign components, add features absent from `DESIGN.md`, introduce speculative infrastructure, optimize prematurely, promote P1 into P0 without justification, or write code.

Prefer thin vertical slices, simple interfaces, incremental verification, and working end-to-end behavior over completeness.

## Self-Check Before Presenting

Run `references/self-check.md` against the draft and fix what it finds. Report fixes applied, scope moved out of P0, any design drift (or `None`), and any decision needing human scope judgment (or `None`).

## Output

`IMPLEMENTATION_PLAN.md`:

```
# Implementation Plan
## Contract              (copied verbatim from DESIGN.md)
## Vertical Slice
## P0 - Required
## P1 - If Time Allows
## Out of Scope
## Implementation Steps  (per step: goal, files, key interface, verification)
## Risks and Mitigations
## Definition of Done
```
