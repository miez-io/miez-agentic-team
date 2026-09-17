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
- Workers always render as Copilot agents
- Preserve provider frontmatter and use `skills` and MCP `tools` only for miez
   configuration.

## Procedure

1. Identify the worker's durable role, motivation, judgment, and scope.
2. Choose a lowercase kebab-case id and create `workers/<worker-id>.md` —
   the file name is the worker id.
3. Add optional miez fields such as `skills` and `tools`, plus provider fields
   such as `model` and `reasoning-effort` when needed.
4. Set `model` on the agent worker when it needs to override the team default.
5. Write the persona and extract specialized procedures into reusable skills.
6. Assign existing skills explicitly; do not paste their bodies into the
   worker.
7. Register the worker in a workflow only when that membership is explicitly
   requested.
8. Run `miez team build .` and inspect the generated catalog.

Keep workflow behavior in workflow frontmatter and Markdown, not in the
worker persona.