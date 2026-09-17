# miez-cli

This directory is a miez team authoring package. It contains the source files
that miez validates and turns into a portable GitHub Copilot team.

## Domain model

miez-cli separates four domain artifact roles:

- **Workers** are personas: durable identity, motivation, goals, beliefs,
  judgment, and boundaries. In the target artifact model every worker resolves
  to a selectable GitHub Copilot custom agent.
- **Skills** describe how to solve something: reusable, worker-independent
  know-how, procedures, and guardrails assigned to workers.
- **Tasks** describe what to do: partial reusable todos or worker-neutral work
  objectives that can be applied with different workers and skill sets.
- **Workflows** describe how to chain work: ordered coordination of workers and
  task assignments for more automation. miez renders the coordination; GitHub
  Copilot executes it.

Tasks are part of this package contract and render as worker-neutral Copilot
prompts. Their requirements and invocation design are documented in the
implementation repository's architecture SRS and SDD. Tasks run in a selected
worker agent's context; multi-worker workflows use provider-supported agent
delegation or handoffs rather than nested prompt invocation.

## Quick start

1. Edit `miez.yaml`, the files below `workers/`, `skills/`, `tasks/`, and
  `workflows/`.
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
tasks/<task-id>.md                reusable task objectives rendered as prompts
workflows/<workflow-id>.md        ordered worker/task phases (current worker-only form)
miez.generated.yaml               generated operational catalog
```

The `.github/` directory in this starter package contains authoring support for
GitHub Copilot. It is not scanned as an operational worker, skill, or workflow
and is not added to `miez.generated.yaml`.

## Workers

Every worker renders as a persistent GitHub Copilot custom agent. The worker id
is the file name: `workers/architect.md` becomes `architect`.

A worker can assign reusable skills with `skills: [skill-id]` and may reference
declared MCP servers with `tools: [mcp-id]`. Model selection applies to every
target worker agent.

Keep durable identity, motivation, goals, beliefs, and boundaries in the worker
body. Put repeatable procedures and technology-specific methods in skills.
Keep workflow phases and handoff order in workflow files.

Example:

```markdown
---
skills: [architecture]
model: gpt-5
---
# Architect

Describe the worker's durable persona and decision posture.
```

## Skills and workflows

A skill is reusable and independent of a worker persona. Its id is its
directory name (`skills/<skill-id>/SKILL.md`); do not declare `id` in
frontmatter. Assign it from worker frontmatter or with
the local `miez worker skill add` command after installation.

A workflow's id is its file name; its frontmatter declares `name` and ordered
`phases`. Every phase
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