# agentic-sdlc

A reusable, stage-gated SDLC for designing and building agentic systems with AI assistance - built for time-constrained work such as engineering interviews.

The human owns problem interpretation, architecture, tradeoffs, and scope. The AI does analysis, documentation, implementation, review, and evaluation. Every stage ends at an explicit human gate.

## What's in here

| Path | Purpose |
| --- | --- |
| `AGENTS.md` | Global instructions: stage boundaries, design principles, artifact precedence. Loaded by every stage. |
| `prompts/01-07*.md` | One prompt per SDLC stage. These are what you paste/run to drive a stage. |
| `skills/*/SKILL.md` | Natively loadable skills the stage prompts invoke by name (e.g. `intent-generation`, `design-review`). |

## The seven stages

| # | Stage | Prompt | Output artifact |
| --- | --- | --- | --- |
| 1 | Understand | `prompts/01-understand.md` | `INTENT.md` |
| 2 | Architecture | `prompts/02-architecture.md` | `ARCHITECTURE.md` |
| 3 | Design | `prompts/03-design.md` | `DESIGN.md` |
| 4 | Plan | `prompts/04-plan.md` | `IMPLEMENTATION_PLAN.md` |
| 5 | Build | `prompts/05-build.md` | working P0 slice + `BUILD_SUMMARY.md` |
| 6 | Review | `prompts/06-review.md` | `REVIEW.md` |
| 7 | Evaluate | `prompts/07-evaluate.md` | `EVAL_RESULTS.md` |

Each stage reads only the artifact from the stage before it. That is deliberate: the upstream artifact is the contract, so context does not accumulate and decisions do not silently drift.

## Setup

Copy this framework into the project you are working on:

```bash
# from the root of your project
cp -R /path/to/agentic-sdlc/AGENTS.md .
cp -R /path/to/agentic-sdlc/prompts .
cp -R /path/to/agentic-sdlc/skills/* .claude/skills/
```

Each skill carries `name` / `description` frontmatter, so dropping them in `.claude/skills/` (project scope) or `~/.claude/skills/` (all projects) makes them load natively - the stage prompts can then invoke them by bare name.

If your agent reads `CLAUDE.md` rather than `AGENTS.md`, symlink it:

```bash
ln -s AGENTS.md CLAUDE.md
```

Then write the problem statement into `CHALLENGE.md` at the project root. That file is the only input to Stage 1.

## Running a stage

Start a session in your project directory and run the stage prompt. In Claude Code:

```
Follow prompts/01-understand.md
```

The stage will read `AGENTS.md` plus its declared input, do the work, and stop at its human gate.

Review the artifact it produced. If it is right, approve it explicitly and move on:

```
Approved. Follow prompts/02-architecture.md
```

Repeat through Stage 7. Do not skip a stage, and do not start the next stage before approving the current artifact - the gates are the control mechanism.

Recommended: start each stage in a **fresh context**. The prompts are written to be self-contained precisely so a clean session works, and it keeps a stale earlier decision from leaking past a gate.

## Handling conflicts and iteration

Artifact precedence when documents disagree:

1. Explicit user decision
2. `CHALLENGE.md`
3. `INTENT.md`
4. Approved architecture decision
5. `DESIGN.md`
6. `IMPLEMENTATION_PLAN.md`
7. Generated implementation

If a later stage discovers that an earlier decision is wrong, it must stop and hand the decision back to that stage rather than patching around it. Fix the implementation to match the upstream artifact, not the other way around.

Evaluation failures in Stage 7 are recorded, not fixed in place. Each fix starts a new pass of the SDLC at whichever stage actually owns the problem.

## Typical interview run

```
CHALLENGE.md
  -> 01-understand   INTENT.md            (approve)
  -> 02-architecture ARCHITECTURE.md      (you pick the architecture)
  -> 03-design       DESIGN.md            (approve)
  -> 04-plan         IMPLEMENTATION_PLAN.md - P0 / P1 / out of scope (approve)
  -> 05-build        P0 vertical slice + BUILD_SUMMARY.md
  -> 06-review       REVIEW.md -> "READY FOR EVALUATION"
  -> 07-evaluate     EVAL_RESULTS.md
```

Build P0 end-to-end before anything else. A thin working system beats several half-built components. Target roughly 45 minutes for the Stage 5 vertical slice.

## Using the skills directly

The skills are normally invoked by the stage prompts, but once installed in `.claude/skills/` each is usable on its own when you want one specific pass:

```
/test-gap-analysis
/debugging-loop
```

`debugging-loop` in particular is meant to be reached for mid-build whenever a step fails, rather than at a stage boundary.
