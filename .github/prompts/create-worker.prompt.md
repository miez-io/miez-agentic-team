---
name: create-worker
description: Create or revise one miez worker with valid frontmatter and a durable persona.
agent: Team Facilitator
argument-hint: Describe the worker's role, responsibility, and whether it is a command or agent.
---

Create or revise exactly one miez worker in `workers/<worker-id>.md`.

Before editing, inspect the existing package, the always-on authoring rules, and
the worker template. Use a lowercase kebab-case id and choose exactly one
frontmatter kind: `command` or `agent`. Add `model` only for an agent. Assign
existing reusable skills instead of copying their bodies into the worker.

Write a persona with identity, motivation, core goals, beliefs, judgment, and
boundaries. Keep workflow phases, handoffs, and collaboration choreography out
of the worker. Do not silently add the worker to a workflow; ask the author or
leave it unassigned.

Run `miez team build .` after the edit and report the resulting validation.