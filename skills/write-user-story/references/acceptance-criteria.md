# Acceptance criteria

Criteria are the shared contract between the human reader, QA, and the agent.
Write them once in the User story section. The Agent task refers to them by
their short IDs instead of copying them.

## Form

Reuse the EARS shapes from the SRS, phrased as a check:

| Shape | Use for |
|---|---|
| WHEN `<event>` THEN `<observable result>` | An action and its result |
| WHILE `<state>` THEN `<observable result>` | Behavior that holds during a state |
| IF `<unwanted condition>` THEN `<observable result>` | Errors and rejections |
| WHERE `<feature is enabled>` THEN `<observable result>` | Optional or flagged behavior |

Rules:

- One criterion, one check. Split on "and" when both halves can fail apart.
- Observable from outside the code: UI state, API response, file, event, exit
  code, or stored record. Never "the service uses X internally".
- Deterministic: name the exact text, status code, count, or state, not
  "appropriate" or "correct".
- Use short IDs `AC1`, `AC2`, and so on. Tests may reference these IDs.

Do not annotate every criterion with its source or test type. Put the tests to
create under Verification in the Agent task. If nothing can verify a
criterion, make it observable or move it to the Agent task as a technical
requirement.

## Playwright-ready phrasing

A criterion that a Playwright test can be generated from names:

- the entry point: route, role, and precondition;
- the interaction: a user-level action, not a selector chain;
- the assertion: a role-, label-, or `data-testid`-addressable element and its
  expected state or text.

Write:

> WHEN a signed-in partner opens `/checks/new` and submits the form without a
> title THEN the form is not submitted and `data-testid="title-error"` shows
> "Titel ist erforderlich".

Do not write:

> WHEN the form is invalid THEN a proper error is shown.

If a criterion needs an element with no stable handle, put the selector to add
under Technical requirements in the Agent task.

## Visual and copy criteria

Exact user-visible text is part of the contract. Quote it verbatim, in the
product language, and mark the language when the repository is mixed.

Layout and spacing belong in a design link, not in long prose. Include the link
only when it is needed for this ticket. Anything that must hold regardless of
the design, such as sticky behavior or independent skeleton states, gets its
own criterion.

## Scoping criteria to the slice

Criteria describe only this story. When a screen shows elements that a later
story owns, state their presence and explicitly exclude their behavior:

> WHEN the page loads THEN four product placeholders are rendered. Placeholder
> interaction is out of scope, see `<story id>`.

## Anti-patterns

| Anti-pattern | Fix |
|---|---|
| "The usual pipeline" | Name each observable step |
| "Works as expected" | Name the expectation |
| A criterion that describes a code change | Move it to the Agent task |
| A bullet list of UI fields with no checkable state | Say what must be visible, with its text |
| Criteria copied mechanically from the SRS | State only this slice's observable result |
