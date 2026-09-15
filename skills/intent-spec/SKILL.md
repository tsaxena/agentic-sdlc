---
name: intent-spec
description: Convert an ambiguous engineering challenge or CHALLENGE.md into a concise, architecture-neutral INTENT.md with a testable Contract block, then self-check it before presenting. Use in Stage 1 (Understand) of the agentic SDLC, before any architecture work.
---

# Intent Spec

Turn an ambiguous challenge into a problem specification that downstream stages can work from without rereading the original.

## Input

The original challenge or `CHALLENGE.md`.

## Method

Extract, in this order:

1. **Goal** - the primary outcome, 1-2 sentences.
2. **Functional requirements** - externally observable capabilities ("the system must..."). Never implementation.
3. **Non-functional requirements** - correctness, reliability, safety, latency, cost, auditability. Only what is stated or clearly implied.
4. **Constraints** - time, tools, required platforms or APIs, provided data, environment, technology restrictions.
5. **Assumptions** - where the challenge is underspecified, decide and label it. Keep each minimal and avoid assumptions that constrain architecture.
6. **Contract** - see below.
7. **Ambiguities** - only questions that materially affect scope, architecture, safety, evaluation, or feasibility. Anything a reasonable assumption can settle belongs in assumptions, not here.

## The Contract Block

`## Contract` is the one section every downstream artifact copies verbatim. It holds:

* **Acceptance criteria** - observable, testable, architecture-independent conditions that determine whether the solution works.
* **Hard constraints** - the boundaries that cannot be traded away.

Write each criterion so Stage 5 can score it PASS or FAIL by running something. "Handles errors gracefully" is not a criterion. "A tool returning a 500 produces a recorded failure and terminates the run within the step budget" is.

Keep it short. Five criteria you can test beat fifteen you cannot.

## Guardrails

Do not propose an architecture, choose between ReAct / workflows / planners / multi-agent, select frameworks or models, design tools, define components, or write code.

Do not invent requirements without labeling them as assumptions. Do not encode a preferred solution into the intent.

## Self-Check Before Presenting

Run `references/self-check.md` against your draft and fix what it finds. Report only:

* fixes you applied
* ambiguities that genuinely need a human decision (or `None`)

## Output

`INTENT.md`, approximately one page:

```
# Intent
## Goal
## Functional Requirements
## Non-Functional Requirements
## Constraints
## Assumptions
## Contract
### Acceptance Criteria
### Hard Constraints
## Ambiguities
## Open Questions   (only if the stage ran out of budget)
```
