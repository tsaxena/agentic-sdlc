# Test Gap Analysis

Do the existing tests give enough confidence in critical behavior to move to system evaluation? Critical behavior, not test count.

## 1. Identify critical behaviors

Extract from the plan what must work for P0: the end-to-end happy path, critical deterministic gates, tool failures, stopping conditions, state transitions, and externally visible side effects.

## 2. Map existing tests

Classify each critical behavior as COVERED, PARTIALLY COVERED, or NOT COVERED.

## 3. Prioritize gaps

Missing tests that could reveal an incorrect success condition, an unhandled tool failure, malformed model output, unsafe repeated execution, an unsafe side effect, an excessive or infinite loop, or invalid state.

Skip exhaustive edge-case enumeration. In an interview the budget buys three or four tests.

## 4. Recommend minimal tests

Per gap: the scenario, the expected behavior, and why the test matters. A few high-value tests beat broad coverage.

## Do not

Optimize for coverage percentage, test trivial getters and plumbing, require production-scale test infrastructure, or test beyond approved P0 behavior.

## Report

`SUFFICIENT FOR EVALUATION` or the specific gaps that must be closed first.
