# miez-cli

This directory is a miez team authoring package. It contains the source files
that miez validates and turns into a portable GitHub Copilot team.

## Quick start

1. Edit `miez.yaml`, the files below `workers/`, `skills/`, and `workflows/`.
2. Run `miez team build .` to validate the package and generate
   `miez.generated.yaml`.
3. Review the generated catalog, then commit the authored files and the
   generated index to the team repository.
4. Install the published team with `miez team install <github-url>`.

The generated index is derived output. Do not edit it by hand. A failed build
leaves the previous generated index unchanged.

## Package layout

```text
miez.yaml                         team metadata and model/MCP declarations
workers/<worker-id>.md            worker personas and capabilities
skills/<skill-id>/SKILL.md        reusable skills assigned to workers
workflows/<workflow-id>.md        ordered phases and workflow membership
miez.generated.yaml               generated operational catalog
```

The `.github/` directory in this starter package contains authoring support for
GitHub Copilot. It is not scanned as an operational worker, skill, or workflow
and is not added to `miez.generated.yaml`.

## Workers

Every worker needs an `id` and a `kind`. The only valid kinds are:

- `command`: a manually invoked Copilot prompt.
- `agent`: a persistent Copilot custom agent.

Only an `agent` worker may set `model`. A worker can assign reusable skills with
`skills: [skill-id]` and may reference declared MCP servers with `tools:
[mcp-id]`.

Keep durable identity, motivation, goals, beliefs, and boundaries in the worker
body. Put repeatable procedures and technology-specific methods in skills.
Keep workflow phases and handoff order in workflow files.

Example:

```markdown
---
id: architect
kind: agent
model: gpt-5
skills: [architecture]
---
# Architect

Describe the worker's durable persona and decision posture.
```

## Skills and workflows

A skill is reusable and independent of a worker persona. Its frontmatter needs
an `id` matching its directory name. Assign it from worker frontmatter or with
the local `miez worker skill add` command after installation.

A workflow frontmatter declares `id`, `name`, and ordered `phases`. Every phase
lists existing worker ids. Workflow membership belongs only in the workflow;
do not put routing or handoff choreography in a worker or skill.

## Local CLI controls

After installation, the active workspace can select a workflow and adjust local
worker participation, skill assignments, or agent models without changing the
team source:

```bash
miez workflow use <workflow-id>
miez workflow worker enable|disable <worker-id>
miez worker skill add|remove <worker-id> <skill-id>
miez worker model list
miez worker model set <worker-id> <model-id>
miez check
```

The `.miez/` directory stores workspace-local state. The team source remains
the package files and the generated catalog.

## Copilot authoring helpers

- `.github/instructions/miez-team-authoring.instructions.md` is always-on
  guidance for maintaining the package boundaries.
- `.github/prompts/create-worker.prompt.md` and
  `.github/prompts/create-skill.prompt.md` are user-invocable helpers.
- `.github/agents/team-facilitator.agent.md` is a reusable authoring agent.
- `.github/skills/` contains reusable validation and authoring procedures.

Read the relevant helper before changing the team structure. The helpers may
edit source files, but `miez.generated.yaml` must always be regenerated with
`miez team build`.