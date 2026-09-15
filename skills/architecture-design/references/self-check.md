# Design Self-Check

Run against the draft `DESIGN.md` and the chosen architecture. Fix what you find.

## 1. Architecture fidelity

The design preserves the selected architecture, control model, LLM/deterministic boundary, state model, and invariants. Watch for drift: single-agent became multi-agent, deterministic workflow became autonomous planning, memory appeared without justification, an LLM took control of a safety gate.

## 2. Contract coverage

Every acceptance criterion in `## Contract` has a concrete mechanism in the design that satisfies it, and an evaluation hook that proves it.

## 3. Component necessity

For every component: what requirement or risk requires this? Flag unnecessary abstractions, speculative infrastructure, redundant components, unjustified agents, premature scalability.

## 4. Control flow completeness

Missing transitions, undefined branches, unclear stopping conditions, circular flows, unbounded loops, missing failure paths.

## 5. Tool contracts

Clear responsibility, defined inputs and outputs, explicit failure behavior, understood side effects. Flag tool interfaces resting on vague natural-language contracts where a structured one is needed.

## 6. State consistency

Hidden dependence on conversation context, state needed across steps but not represented, duplicate sources of truth, unnecessary persistence, unclear ownership.

## 7. LLM / deterministic boundary

Flag the LLM controlling permissions, schema validation, retries, stopping conditions, policy, idempotency, irreversible actions, or success checks. Also flag the reverse: a rigid deterministic path for a task that genuinely needs semantic reasoning.

## 8. Reliability

Bounded execution, timeouts, retry limits, malformed model output, tool failures, repeated actions, partial completion, safe failure. Only require what this system actually needs.

## 9. Testability

Enough is observable to test task success, important state transitions, tool usage, deterministic gates, and failure behavior.

## 10. Vertical slice feasibility

The slice exercises the real architecture end to end on the critical path, and is buildable within the build budget. Flag a slice that is too large to finish or too trivial to prove anything.

## Ready when

The design realizes the chosen architecture faithfully, covers the contract, carries no unjustified component, has bounded and safe failure behavior, and the vertical slice is both real and achievable.
