# Intent Self-Check

Run against the draft `INTENT.md` and the original challenge. Fix what you find; do not report a clean bill of health at length.

## 1. Missing requirements

Any requirement in the challenge absent from the draft that would affect scope, architecture, implementation, or evaluation.

## 2. Unsupported assumptions

Assumptions not supported by the challenge, or that unnecessarily constrain the solution. Distinguish a reasonable assumption from an invented requirement.

## 3. Architecture leakage

Any decision that belongs to Stage 2: ReAct, planner/executor, multi-agent, a named framework, a named model, vector databases, component design, tool implementation. The intent says what must be accomplished, never how.

## 4. Contract quality

Each acceptance criterion must be observable, testable, architecture-independent, and tied to a stated requirement. Rewrite anything vague or subjective. Ask of each: what command or assertion proves this?

## 5. Scope creep

Capabilities the draft added that the challenge does not require. A clearly labeled, reasonable assumption is not scope creep.

## 6. Contradictions

Conflicts between the challenge, the requirements, the assumptions, and the contract.

## 7. Material ambiguities

Unresolved questions that affect architecture, safety, system boundaries, evaluation, or feasibility. Do not produce a long list of low-value clarification questions - each one costs human time that the build stage needs.

## Ready when

Every important challenge requirement is represented, assumptions are explicit and reasonable, every acceptance criterion is testable, no architecture decision has leaked in, no material contradiction remains, and Stage 2 could work from this document alone.
