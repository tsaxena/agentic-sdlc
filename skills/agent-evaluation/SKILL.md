---
name: agent-evaluation
description: Evaluate whether an implemented agentic system actually performs its intended task, scoring final outputs and trajectory behavior against the Contract acceptance criteria. Use in Stage 5 (Verify) of the agentic SDLC.
---

# Agent Evaluation

Evaluate the agent as a system, not as a collection of functions. The question is whether it does the job, and where it breaks.

## Inputs

`IMPLEMENTATION_PLAN.md` (its `## Contract` is the acceptance standard), the working implementation, the available test environment.

## Method

### 1. Choose evaluation targets

Only dimensions that matter for this system: task success, correctness, completeness, evidence grounding, false positives, false negatives, tool selection, trajectory quality, recovery from failure, unnecessary actions, latency, cost.

Do not measure something merely because it is measurable. Every acceptance criterion in `## Contract` must map to at least one target.

### 2. Build a small case set

Pick from these, keeping only what is relevant:

* **Happy path** - normal input the system should handle
* **Ambiguous input** - the agent must reason before acting
* **Invalid input** - malformed or unsupported
* **Tool failure** - a required tool errors or is unavailable
* **Partial failure** - part of the workflow succeeds, part fails
* **Repeated execution** - the same task again, where duplicate actions would matter
* **Adversarial input** - content designed to mislead the agent or override its instructions
* **Hidden-test-style case** - realistic, and not obviously anticipated by the implementation

Five to eight cases is usually right for an interview. Cover every contract criterion first, then spend what is left on failure modes.

### 3. Define expected behavior before running

For each case, write down first: the input, the expected final output or output shape, the expected trajectory (which tools, roughly how many steps), the expected failure handling, and what counts as pass, partial, and fail.

Writing expectations after seeing output is not evaluation. It is rationalization, and it is the single easiest way to fool yourself about an agent.

### 4. Run and capture

Run each case. Capture the final output, the tool calls made, the number of steps, errors and retries, the termination reason, and anything surprising in the trajectory.

Prefer deterministic assertions. Use LLM-based judgment only where the criterion is genuinely semantic.

### 5. Score

Per case: `PASS | PARTIAL | FAIL`, with the evidence. Then score each `## Contract` acceptance criterion `PASS | PARTIAL | FAIL` from the cases that exercise it.

A case can pass on output while failing on trajectory - an agent that reached the right answer through an unsafe or unbounded path has not passed. Say so explicitly.

### 6. Analyze failures

For each failed or partial case: what actually went wrong, which layer owns it (intent, design, plan, or implementation), whether it is systematic or incidental, and the smallest change that would fix it.

### 7. Prioritize

Rank improvements by contract impact first, then by risk, then by cost to fix.

## Fixing during evaluation

Record failures rather than fixing them, with one exception: a failure that breaks a `## Contract` acceptance criterion gets fixed now. Record the fix and rerun every case it could affect.

Never redefine success criteria after seeing results.

## Guardrails

Do not evaluate only whether the final answer looks good. Do not expand scope. Do not tune the system against the evaluation cases - a system that passes only its own eval set has learned the eval, not the task.

## Output

Feed this into the `## Evaluation` sections of `VERIFY.md`:

* **Evaluation targets** and how they map to contract criteria
* **Cases** - input, expected behavior, actual behavior, score
* **Contract result** - PASS / PARTIAL / FAIL per acceptance criterion
* **Top failure modes** - ranked, with the layer that owns each
* **Highest-value next improvement**
* **Overall** - `MEETS CONTRACT` or `DOES NOT MEET CONTRACT`
