# agentic-sdlc

A stage-gated SDLC for designing and building agentic systems with AI assistance, sized for a clock - engineering interviews in particular.

The human owns problem interpretation, architecture, tradeoffs, and scope. The AI does analysis, documentation, implementation, review, and evaluation. Every stage ends at an explicit human gate.

## The five stages

| # | Stage | Command | Output | Budget |
| --- | --- | --- | --- | --- |
| 1 | Understand | `/understand` | `INTENT.md` | 5 min |
| 2 | Design | `/design` | `DESIGN.md` | 10 min |
| 3 | Plan | `/plan` | `IMPLEMENTATION_PLAN.md` | 5 min |
| 4 | Build | `/build` | working P0 slice + tests | 45 min |
| 5 | Verify | `/verify` | `VERIFY.md` | 15 min |

Roughly 80 minutes, with more than half of it in build. Architecture selection and system design share Stage 2, with one human decision between the halves. Implementation review and system evaluation share Stage 5.

Each stage reads only the artifact from the stage before it. The upstream artifact is the contract, so context does not accumulate and decisions do not silently drift.

## The Contract block

`INTENT.md` carries a `## Contract` section holding the acceptance criteria and hard constraints. Every downstream artifact copies it verbatim.

That is what makes the one-artifact-back rule safe. Stage 5 scores the built system against the original acceptance criteria without ever rereading `CHALLENGE.md`, and no stage can quietly soften the bar it will later be judged against.

Write each criterion so it can be scored by running something.

## Install

As a plugin:

```bash
/plugin marketplace add /path/to/agentic-sdlc
/plugin install agentic-sdlc
```

Or copy it into a project directly:

```bash
cp /path/to/agentic-sdlc/AGENTS.md .
cp -R /path/to/agentic-sdlc/commands/* .claude/commands/
cp -R /path/to/agentic-sdlc/skills/*   .claude/skills/
```

If your agent reads `CLAUDE.md` rather than `AGENTS.md`:

```bash
ln -s AGENTS.md CLAUDE.md
```

## Run

Write the problem statement into `CHALLENGE.md`. That file is the only input to Stage 1.

```
/understand
```

Review the artifact. If it is right, approve it and move on:

```
Approved.
/design
```

Repeat through `/verify`. The gates are the control mechanism - do not start a stage before approving the previous artifact.

Start each stage in a **fresh context**. The commands are self-contained so a clean session works, and it stops a stale earlier decision from leaking past a gate.

## Time discipline

Budgets are in the table above and enforced by convention, not by tooling. When a stage runs over: ship the artifact as-is, list what is open under `## Open Questions`, and move on.

Over-budget upstream stages cost build time, and build is the only stage that produces a working system.

## Iteration and conflicts

Artifact precedence is defined in [AGENTS.md](AGENTS.md#artifact-precedence).

If a later stage finds that an earlier decision is wrong, it stops and hands the decision back to the stage that owns it rather than patching around it. Fix the implementation to match the upstream artifact, not the reverse.

Stage 5 records failures rather than fixing them, with one exception: a failure that breaks a `## Contract` acceptance criterion gets fixed immediately, with the fix and the reruns recorded. Everything else starts a new pass at whichever stage owns the problem.

## Scaling up

For real project work rather than an interview, split Stage 2 into separate architecture and design stages with a gate on each, and split Stage 5 into review and evaluation. The skills are already separable along those lines - `architecture-design` has a part A and part B, and `/verify` runs two independent skills.

Keep the Contract block either way. It is the part that does the work.

## Skills

Seven skills, invoked by the stage commands:

| Skill | Stage |
| --- | --- |
| `intent-spec` | 1 |
| `architecture-design` | 2 |
| `implementation-planning` | 3 |
| `implementation-execution` | 4 |
| `debugging-loop` | 4, on any failure |
| `implementation-review` | 5 |
| `agent-evaluation` | 5 |

Each is usable on its own when you want one specific pass. `debugging-loop` is meant to be reached for mid-build the moment a step fails, not at a stage boundary.

Long checklists live in each skill's `references/` and load only when needed, so a stage does not pull hundreds of lines of instructions before doing any work.
