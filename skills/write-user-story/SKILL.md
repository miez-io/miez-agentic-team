---
name: write-user-story
description: Write a user story that serves a human on the board, QA including Playwright, and a coding agent from one artifact. Use when turning SRS or SDD content into tickets, slicing a feature into stories, or when asked to write or review a user story, backlog item, or acceptance criteria.
user-invocable: true
disable-model-invocation: false
---

# Write a user story

A user story is the hand-off between architecture and implementation:

```
arc42 / ADR  ->  SRS + SDD  ->  user story  ->  agent task
```

Keep the ticket readable in backlog refinement and useful as an agent prompt.
It has exactly two top-level sections:

1. **User story** contains the outcome and acceptance criteria for humans and
   QA, including criteria that become Playwright tests.
2. **Agent task** contains implementation instructions, necessary technical
   details, and verification steps.

Copy the complete ticket description as the prompt. The agent task may refer
to the acceptance criteria above it instead of repeating them.

Copy structure from [assets/user-story-template.md](assets/user-story-template.md).

Read:

- [references/acceptance-criteria.md](references/acceptance-criteria.md) when
  writing criteria that a human, QA, and an agent read the same way.
- [references/agent-task.md](references/agent-task.md) when writing the
  implementation section.
- [references/story-types.md](references/story-types.md) for the frontend,
  backend, and delivery variants.

## Where to write

Do not assume a path.

1. Use the path given by the invoking agent, prompt, or user.
2. Else search the repository for existing stories (a `stories` or `backlog`
   directory, or files with `## Acceptance criteria`). Add a sibling there.
3. Else ask where stories should go.

Several stories may be concatenated into one Markdown file when an agent needs
the full feature context. Keep each story intact and clearly titled.

## Procedure

1. Read the current SRS, SDD, ADRs, designs, and relevant code. Use them while
  authoring, but do not add repository paths, requirement IDs, or a source
  table to the ticket.
2. Slice one story per user-visible outcome, not per layer, file, or sprint.
3. Write the user story and only the acceptance criteria needed to recognize
  that outcome. For backend and delivery work, use a concise outcome instead
  of a forced user-story sentence.
4. Translate the implementation-relevant parts of the SDD and ADRs into direct
  agent instructions. Embed the necessary facts; do not link back to files
  that may change after the ticket is created.
5. State exact automated tests in the agent task. Use Playwright for
  automatable browser behavior and API or unit tests for backend behavior.
6. Remove optional labels that have no content. Ask when a need is unclear;
  do not add an Open questions section to carry unresolved scope into Jira.

## Avoid duplication

- Put observable behavior in the user story and acceptance criteria.
- Put implementation approach and technical constraints in the agent task.
- Let the agent task say "satisfy the acceptance criteria above" rather than
  restating them.
- Include exact copy, test data, design links, selectors, or exclusions only
  when this ticket actually needs them, in the section whose reader needs them.

## Do not

- Add Context, Scope, Sources, Test notes, Definition of done, or other
  mandatory ceremony around every ticket
- Add repository paths or requirement IDs for traceability
- Restate acceptance criteria in the agent task
- Write criteria that cannot be observed from outside the code
- Put the implementation plan into the acceptance criteria
- Leave the agent task as "implement the story"
- Slice by layer, for example "backend part" and "frontend part", when the
  outcome is one user-visible behavior
- Document history, decisions, or changes in the story
