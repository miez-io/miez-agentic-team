# Story types

The structure is the same for every story. What changes is the story sentence,
where the criteria are observed, and who verifies them.

## Frontend

- Story sentence: the full "As a … I want … so that …" form. The role is a real
  user role with a scope.
- Criteria: observed in the browser. Quote user-visible text verbatim in the
  product language. Cover loading, empty, error, and permission states, not
  only the happy path.
- Agent task: name the implementation approach and exact Playwright coverage.
  Add routes, roles, seed data, design links, or stable selectors only when the
  story needs them.

## Backend

- Story sentence: one outcome paragraph instead of the user sentence. Name the
  consumer, for example the web client, a worker, or an external partner.
- Criteria: observed at the service boundary. Use request and response,
  persisted record, emitted event, or job state. Include the failure and
  concurrency cases, because they are the ones that are skipped otherwise.
- Agent task: carry the exact contract. Schema fields and types, endpoint and
  method, status codes, error bodies, index changes, migration order, limits,
  timeouts, test setup, and the API or unit tests to add.

## Delivery

Pipelines, infrastructure, and release mechanics.

- Story sentence: the outcome paragraph. The consumer is usually the team or an
  environment.
- Criteria: observed from the pipeline run or the target system. Name the
  trigger and the artifact.

> WHEN a pull request is opened THEN the image is built and no push to the
> registry occurs.
> WHEN a commit is merged to the default branch THEN the image is pushed
> tagged with the short commit hash.
> WHEN a tag is pushed THEN the image is pushed tagged with that tag name.

- Agent task: name the workflow file, the runner, the registry, the
  authentication method, and the required secrets by name, never by value.

## Mixed slices

When one user-visible outcome needs backend and frontend work, keep one story.
Order the Agent task so the contract is created before it is consumed. Split
into two stories only when the halves ship separately.
