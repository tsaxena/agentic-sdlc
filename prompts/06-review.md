# Stage 6 — Review

Read:

* `IMPLEMENTATION_PLAN.md`
* `BUILD_SUMMARY.md`
* current implementation
* existing tests
* `AGENTS.md`

Do not reread `DESIGN.md`, `ARCHITECTURE.md`, `INTENT.md`, or `CHALLENGE.md`.

Treat `IMPLEMENTATION_PLAN.md` as the implementation contract and `BUILD_SUMMARY.md` as the record of what was built.

## Goal

Determine whether the P0 implementation is correct and sufficiently tested to proceed to system-level evaluation.

## Process

1. Apply the `implementation-review` skill.
2. Apply the `test-gap-analysis` skill.
3. Identify only blockers that must be resolved before evaluation.
4. Apply targeted fixes for approved blockers.
5. Rerun the relevant focused tests.
6. Repeat review only for the affected areas.
7. Produce `REVIEW.md`.

## Boundaries

Do not:

* redesign the system
* expand scope
* implement P1 functionality
* perform broad refactoring
* fix purely stylistic issues

If review reveals a problem requiring a design or architecture change, stop and return the issue to the appropriate earlier stage.

## Output

Create `REVIEW.md`.

It should capture:

* what was reviewed
* acceptance criteria results
* blockers found, with evidence, impact, and the smallest fix
* fixes applied during this stage
* test gaps that matter before evaluation
* important non-blocking issues
* meaningful deviations from `IMPLEMENTATION_PLAN.md`
* issues returned to an earlier stage, if any

End `REVIEW.md` with exactly one status line:

`READY FOR EVALUATION`

or

`FIX BLOCKERS FIRST`

## Human Gate

Present `REVIEW.md` for human approval.

Do not proceed to evaluation unless the status is `READY FOR EVALUATION` and the user approves.

Stop after Stage 6.
