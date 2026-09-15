# Plan Self-Check

Run against the draft plan and `DESIGN.md`. Fix what you find.

## 1. Design fidelity

The plan implements the design without changing architecture, component responsibilities, control flow, important interfaces, deterministic boundaries, or invariants.

## 2. P0 completeness

P0 contains everything required for the minimum end-to-end slice. Trace the path from input to output and confirm no step on it is missing.

## 3. Scope control

Work in P0 that is not required to prove the design: unnecessary abstractions, premature infrastructure, production hardening, optional features, speculative extensibility. Move it to P1 or out of scope.

## 4. Order

Dependencies respected, runnable increments, failures exposed early, no large disconnected pieces, end-to-end execution reached quickly.

## 5. Verification quality

Every meaningful step has a verification whose success is observable. Flag any step where "done" is a judgment call.

## 6. Feasibility

Is P0 realistic within the build budget? Count the steps and be honest about the ones involving an external API or auth. A plan that is obviously too large should be cut now, not discovered at minute 40.

## 7. Definition of done

Concrete, tied to the vertical slice, and traceable to the acceptance criteria in `## Contract`.

## Ready when

P0 is the smallest complete path, every step is verifiable, the order surfaces risk early, and the whole thing fits the budget.
