# The agent task block

The Agent task is the second half of the ticket. Together with the User story
above it, the complete Jira description is a ready-to-paste agent prompt.

## Contract

A task answers "how should the agent implement and verify this story?" It does
not repeat the outcome or acceptance criteria and does not redefine the
persona, skills, or workflow.

Required parts:

| Part | Rule |
|---|---|
| Steps | Ordered, each a verifiable move, ending with verification |
| Technical requirements | Only contracts and constraints needed here; omit when empty |
| Verification | Tests and checks that prove the acceptance criteria |

Do not make the Agent task stand alone by copying the User story into it. Copy
the complete ticket when invoking a worker.

## Steps

Steps are the approach, not a line-by-line diff. Aim for three to seven.

Write:

1. Add `leaseExpiresAt` and `attempt` to the job document and the index.
2. Implement `claimJob` so a claim is atomic against a live lease.
3. Expose the claim through the worker loop and keep the existing retry path.
4. Add a concurrency test that two workers never claim one live lease.

Do not write:

1. Open `job.go`.
2. On line 42 add a field.

A step that is only "write tests" is missing its assertion. Name what the test
proves.

## Technical requirements

Translate only the values needed to build: field names, status enums, routes,
limits, headers, error codes, and naming conventions. Embed those facts in the
ticket instead of linking to changing architecture files.

Include ticket-local technical facts that exist nowhere else:

- `data-testid` values to add, so QA automation has a stable handle;
- fixtures or seed data to create;
- migration and rollout order;
- feature-flag name and default.

State what stays untouched as a technical requirement when it matters:

- Do not change the public response shape of `<endpoint>`.
- Do not introduce a new container or transport.
- Keep the existing `<library>` usage; replacing it is out of scope.

## Verification

Name the tests and checks to create or run. Keep them objectively checkable:

- [ ] Playwright spec `checks-create.spec.ts` covers AC2 and AC3
- [ ] `make test` and lint pass

Do not add a generic Definition of done checklist. The team's shared process
already owns it.
