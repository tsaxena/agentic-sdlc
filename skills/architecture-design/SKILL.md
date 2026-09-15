---
name: architecture-design
description: Select the simplest architecture that satisfies an approved INTENT.md, get the human decision, then specify that architecture as an implementation-ready DESIGN.md and self-check it. Use in Stage 2 (Design) of the agentic SDLC.
---

# Architecture and Design

One stage, two halves, one human decision between them.

## Input

`INTENT.md`. Treat it as the authoritative problem contract. Do not reread the original challenge.

---

## Part A - Choose the Architecture

### 1. Characterize the problem

Only the characteristics that actually move the decision: how predictable the workflow is, whether the task is a fixed sequence, whether dynamic replanning is required, how many external systems are involved, whether long-lived or shared state is needed, which actions are irreversible or expensive, what failures the system must recover from, and what the latency, cost, and implementation-time constraints are.

Do not infer complexity the intent does not require.

### 2. Determine the required level of agency

Ask whether an agent is necessary at all. `references/patterns.md` lists the spectrum from deterministic workflow through multi-agent, with the conditions that justify each. Greater agency is not better architecture.

### 3. Generate options

Two or three, and only where a genuinely meaningful alternative exists. Never generate a third option for symmetry. For each: control flow, where LLM reasoning happens, where deterministic logic happens, state requirements, failure modes, implementation complexity.

### 4. Recommend one

Compare against requirement coverage, simplicity, failure recovery, deterministic guarantees, testability, and whether a working vertical slice is reachable in the time available.

Prefer the least complex architecture that satisfies the contract. Explain why a simpler option is insufficient, why a more complex one is unnecessary, the main tradeoff accepted, and the biggest risk.

### 5. Stop

Present the recommendation and tradeoffs. The human decides. Do not begin Part B until the choice is explicit.

---

## Part B - Specify the Design

Preserve the chosen architecture exactly. Specify:

1. **Design thesis** - the architecture and core implementation idea in 2-4 sentences.
2. **Components** - the minimum set. For each: responsibility, inputs, outputs, boundaries. Every component solves a concrete requirement; no speculative components.
3. **Control flow** - input to output, including reasoning steps, tool interactions, deterministic gates, state transitions, stopping conditions, and side effects. A simple diagram helps.
4. **Agent responsibilities** - exactly what the LLM may decide, and what it must not control.
5. **Tools** - per important tool: purpose, input, output, side effects, failure modes. Success and failure must be distinguishable from the result.
6. **State** - the minimum that must survive across steps. Explicit, single-owner. No persistent storage without a requirement.
7. **LLM / deterministic boundary** - LLM for semantic judgment; deterministic code for validation, permissions, schemas, state transitions, retries, stopping conditions, idempotency, irreversible actions, and success checks.
8. **Failure handling** - tool failure, timeout, malformed model output, invalid arguments, repeated actions, retry exhaustion, partial completion, no-progress. Every agent loop is bounded and fails safely.
9. **Safety boundaries** - untrusted inputs, high-impact actions, permissions. Deterministic gates where it matters.
10. **Observability** - the minimum needed to understand one run: major decisions, tool calls, results, errors, retries, final status. Not a production platform.
11. **Evaluation hooks** - what Stage 5 can assert against each acceptance criterion in the contract.
12. **Minimal vertical slice** - the smallest end-to-end implementation that exercises the real architecture: real input, core reasoning, essential tools, critical gates, final output.

## Guardrails

Do not change the chosen architecture, add agents or planners or memory or databases or queues or frameworks without justification, design speculative production infrastructure, write code, or define file-by-file implementation order.

If the approved architecture contains a blocking flaw, surface it for human review instead of quietly fixing it.

## Self-Check Before Presenting

Run `references/self-check.md` against the draft and fix what it finds. Report fixes applied, any architecture drift (or `None`), and any issue needing architecture-level human judgment (or `None`).

## Output

`DESIGN.md`:

```
# Design
## Contract               (copied verbatim from INTENT.md)
## Architecture Decision  (options considered, selection, rationale, who approved)
## Design Thesis
## Components
## Control Flow
## Agent Responsibilities
## Tools
## State
## LLM vs Deterministic Boundary
## Failure Handling
## Safety Boundaries
## Observability
## Evaluation Hooks
## Key Invariants
## Minimal Vertical Slice
## Major Risks
## Open Questions         (only if the stage ran out of budget)
```
