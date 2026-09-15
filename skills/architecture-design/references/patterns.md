# Agency Spectrum

Work down this list and stop at the first pattern that satisfies the contract.

## Deterministic workflow

Steps are known in advance, branching is limited, the tool sequence is predictable, and reproducibility matters more than flexibility.

This is the right answer far more often than it gets chosen.

## Single ReAct agent

The next action depends on the last observation, investigation is open-ended, tool selection must happen dynamically, and lightweight replanning is sufficient.

## Planner / executor

The task benefits from an explicit multi-step plan, steps have dependencies, progress needs tracking, and execution is structured once the plan exists.

## Planner with replanning

Initial plans are likely to become invalid, observations materially change the path, and long-horizon work requires adaptation.

Costs a full extra reasoning loop. Justify it with a concrete case where the first plan breaks.

## Router + specialists

Requests fall into distinct categories that need meaningfully different tools or expertise, and a cheap routing decision isolates the workflows.

## Multi-agent / supervisor

Justify against all of: tasks are meaningfully separable, specialization improves quality, independent work can run in parallel, separate context windows or tool permissions are useful, and the coordination overhead is worth it.

If only some of those hold, the answer is usually one agent with more tools.

## Hybrid

Some reasoning must stay flexible while control, validation, or side effects stay deterministic. Most production-shaped answers land here.

---

# State Models

Pick the least of: none, per-run, resumable, shared across workers, long-term memory.

Do not introduce databases, queues, or vector stores without a concrete requirement from the contract.

---

# Architectural Invariants

Identify the small number of constraints the design and implementation must preserve. Keep them architectural rather than implementation-specific. Examples:

* execution is bounded
* external side effects require deterministic validation
* tool failures are observable
* retrieved or repository content is untrusted
* duplicate actions are prevented
* human approval precedes a high-impact action

---

# Anti-Patterns

* Architecture by buzzword. Every component must solve a requirement or mitigate a named risk.
* Generating three options when there is really one.
* Multi-agent as a default.
* Persistent memory with no requirement behind it.
* An LLM holding a guarantee that deterministic code could enforce.
