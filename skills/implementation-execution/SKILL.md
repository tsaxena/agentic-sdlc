---
name: implementation-execution
description: Implement an approved IMPLEMENTATION_PLAN.md as a working P0 vertical slice, verifying incrementally and preserving the approved design. Use in Stage 4 (Build) of the agentic SDLC.
---

# Implementation Execution

Execute the plan incrementally, verify continuously, and reach a working P0 vertical slice before adding anything optional.

## Input

`IMPLEMENTATION_PLAN.md`, the authoritative implementation contract. Do not reinterpret the original challenge or redesign the system.

## Method

### 1. P0 only

Implement nothing outside P0 until the end-to-end slice runs.

### 2. Work one step at a time

Read the step objective, make the smallest change that satisfies it, run the plan's verification, inspect the actual result, fix blocking failures, confirm, continue.

Never implement several major components before running anything. The cost of a wrong assumption compounds with every step built on top of it.

### 3. Preserve design contracts

Respect component responsibilities, interfaces, state ownership, control flow, LLM/deterministic boundaries, safety gates, and stopping conditions. If implementation requires changing one, stop and surface the conflict. Do not silently redesign.

### 4. Keep interfaces explicit

Structured inputs, structured outputs, clear error results, explicit state transitions. Never rely on hidden conversational state where program state is required.

### 5. Validate external actions

For side-effecting tools: inspect the result, verify success, handle errors, and avoid duplicate execution on retry. A tool call that returned is not a tool call that worked.

### 6. Keep the code simple

Small modules, explicit control flow, minimal dependencies, readable code, direct abstractions.

Avoid unnecessary frameworks, speculative extensibility, premature scalability infrastructure, complex inheritance, and any abstraction used once. The implementation has to be explainable out loud.

### 7. Test critical paths early

At minimum: the normal end-to-end path, critical deterministic gates, important tool failure behavior, and termination behavior.

### 8. Stop at P0

When the slice works: rerun the end-to-end path clean, record known limitations, and list the P1 work left undone. Do not keep adding features on momentum.

## Guardrails

Never modify the architecture without approval, change the design silently, expand scope, implement P1 before P0 runs, accept generated code without running it, hide a failing test, or replace broken behavior with a hard-coded demo output.

If the upstream artifacts are inconsistent with implementation reality, surface the problem rather than working around it.

## When Something Fails

Apply the `debugging-loop` skill rather than guessing. Reach for it the moment a step fails, not after three speculative fixes.

## Complete When

The P0 vertical slice runs end to end, critical deterministic checks work, expected outputs are produced, blocking runtime failures are resolved, and known limitations are written down.

## Report

In the conversation, not in a document:

* what was implemented and verified, with the actual command output
* known limitations
* P1 not implemented
* deviations from the plan, or `None`

Stage 5 reads the code and the plan directly, so a build summary artifact would only add a lossy layer between them.
