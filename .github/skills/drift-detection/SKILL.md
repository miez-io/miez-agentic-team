---
name: drift-detection
description: Check a miez team for worker, skill, generated-index, and separation drift.
---

# Drift Detection

Use this skill after changing team artifacts or before publishing a generated
team index. It is read-only and reports the smallest repair for each finding.

## Checks

1. Read `miez.yaml` and `miez.generated.yaml`; collect worker, skill, model,
   and workflow ids.
2. Confirm every generated worker path exists and its frontmatter id matches.
3. Confirm every assigned skill exists at `skills/<skill-id>/SKILL.md` and its
   frontmatter id matches the directory and assignment.
4. Confirm worker, skill, workflow, phase, and model ids are unique and valid.
5. Confirm every workflow phase references an existing worker.
6. Inspect workers for workflow phases, handoff choreography, or a
   `Collaboration` section that belongs in workflow configuration.
7. Inspect skills for worker-specific persona information or workflow
   instructions that should be reusable boundaries instead.
8. Confirm specialized procedures are skills rather than duplicated personas.
9. Run `miez check` when the CLI and an installed team are available.

## Output

Report `clean`, `blocked`, or `drift`. For every finding, name the file, the
violated boundary, and the smallest repair. Do not rewrite files during this
check.