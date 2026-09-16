---
name: write-skills
description: Create reusable miez skills with clear procedures and independent boundaries.
---

# Write Skills

Use this skill when creating or revising a reusable capability for one or more
miez workers.

## Separation contract

- A skill describes a repeatable capability, method, guardrails, and output.
- A skill does not describe a worker personality or identity.
- A skill does not own workflow phases, handoffs, or worker membership.
- A skill should remain useful when assigned to a different worker.

## Procedure

1. Identify the reusable capability and the situations where it applies.
2. Choose a lowercase kebab-case id and create
   `skills/<skill-id>/SKILL.md`.
3. Add frontmatter with the matching `id`; optional `name` and `description`
   fields may clarify the skill.
4. Describe the purpose, method, guardrails, and expected output.
5. Assign the skill in worker frontmatter only where it is relevant.
6. Run `miez team build .` and inspect the generated catalog.

Do not paste the skill body into a worker and do not add workflow choreography
to the skill.