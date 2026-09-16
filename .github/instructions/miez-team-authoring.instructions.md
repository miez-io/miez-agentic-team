---
applyTo: "**"
---

# Miez team authoring rules

This repository is a miez team package. Keep the authored package contract
valid and keep operational artifacts separate from Copilot authoring support.

## Source and generated files

- Treat `miez.yaml`, `workers/`, `skills/`, and `workflows/` as authored source.
- Treat `miez.generated.yaml` as generated output. Never edit it manually.
- Run `miez team build .` after changing package metadata or artifact
  frontmatter.
- Keep `.github/` authoring helpers separate from the operational source
  directories. They must not be registered as team workers, skills, or
  workflows.

## Worker boundary

- A worker owns durable identity, motivation, goals, beliefs, judgment, and
  boundaries.
- `kind` is either `command` or `agent`.
- Only `kind: agent` may declare `model`.
- Put repeatable procedures, checklists, and technology-specific methods in a
  reusable skill instead of a worker persona.
- Do not put workflow phases, handoff order, or a `Collaboration` section in a
  worker.

## Skill boundary

- A skill is reusable and independent of a worker's personality.
- Store it at `skills/<skill-id>/SKILL.md` with matching `id` frontmatter.
- Describe purpose, method, guardrails, and output.
- Do not put worker persona or workflow choreography in a skill.

## Workflow boundary

- A workflow owns ordered phases and worker membership.
- Every phase must reference an existing worker.
- Do not silently add a worker to a workflow when authoring the worker.
- Keep local enable/disable choices in workspace state rather than changing
  published team source.

When a change crosses these boundaries, split it into the appropriate worker,
skill, or workflow artifact and run the artifact checks before publishing.