# Comparing Agent Architectures

## Purpose
Generate and compare plausible architectures for an agentic system.

## Inputs
- CHALLENGE.md
- INTENT.md

## Procedure

First characterize the task:

- Is the workflow predictable or open-ended?
- Does the system need dynamic replanning?
- Are tasks independent enough for parallelism?
- Is long-lived state required?
- How many tools are involved?
- Are actions reversible?
- Are there high-risk actions requiring deterministic gates?
- What kinds of failures must be recoverable?

Then consider only architectures relevant to the problem, such as:

- deterministic workflow
- ReAct
- planner/executor
- planner + replanning
- router + specialist agents
- supervisor / multi-agent
- hybrid deterministic + agentic system

For each plausible option describe:

- control flow
- strengths
- weaknesses
- failure modes
- implementation complexity
- suitability for a 45-minute prototype

Recommend an option and explain why.

## Guardrails
- Do NOT implement anything.
- Do NOT create DESIGN.md.
- Do NOT assume multi-agent is better than single-agent.
- Prefer the simplest architecture satisfying the requirements.
- The final architecture decision belongs to the user.

## Output
Provide 2–3 realistic options with a concise comparison.
End with a recommendation, not a decision.