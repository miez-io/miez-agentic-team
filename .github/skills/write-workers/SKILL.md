---
name: write-workers
description: Create persona-first miez workers and assign reusable skills without mixing workflow behavior into personas.
---

# Write Workers

Use this skill when creating or revising a miez worker and its reusable skill
assignments.

## Separation contract

- A worker describes identity, motivation, goals, beliefs, judgment, and
  boundaries.
- A skill describes a repeatable capability and contains no worker persona.
- A worker does not contain workflow phases, handoff sequencing, or a
  `Collaboration` section.
- `kind: command` versus `kind: agent` is frontmatter configuration.

## Procedure

1. Identify the worker's durable role, motivation, judgment, and scope.
2. Choose a lowercase kebab-case id and create `workers/<worker-id>.md`.
3. Add frontmatter with `id`, `kind`, and optional `skills`, `model`, and
   `tools`. Use only `command` or `agent` for `kind`.
4. Set `model` only when `kind: agent`.
5. Write the persona and extract specialized procedures into reusable skills.
6. Assign existing skills explicitly; do not paste their bodies into the
   worker.
7. Register the worker in a workflow only when that membership is explicitly
   requested.
8. Run `miez team build .` and inspect the generated catalog.

Keep workflow behavior in workflow frontmatter and Markdown, not in the
worker persona.