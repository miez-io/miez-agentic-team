---
name: create-skill
description: Create or revise one reusable miez skill with valid frontmatter and clear procedures.
agent: Team Facilitator
argument-hint: Describe the repeatable capability, guardrails, and expected output.
---

Create or revise exactly one reusable skill at
`skills/<skill-id>/SKILL.md`.

Use a lowercase kebab-case id matching the directory name. Keep the skill
independent of any worker personality and workflow order. Describe its purpose,
method, guardrails, and expected output. Do not put a worker's identity,
motivation, or workflow handoff choreography in the skill.

Inspect existing workers before assigning the skill. Assign it explicitly in
worker frontmatter only when the capability is relevant. Do not silently add a
worker to a workflow.

Run `miez team build .` after the edit and report the resulting validation.