# Implement Issue Workflow

Use when the user invokes `/implement-issue-command` or `/implement-issue`.

## Goal

Implement the accepted plan, validate the work thoroughly, commit cleanly, and
prepare the issue for efficient human review with a review-ready summary.

## Execution Rules

- Treat the latest accepted plan as authoritative.
- Implement only the approved scope unless human feedback explicitly narrows it
  further.
- If the implementation reveals a material flaw in the plan, stop and route to
  the revise-plan workflow instead of silently changing direction.
- Commit in small, logical steps using the git conventions below.
- Consult project skills to fill gaps in the approved plan, not to redesign it.
- When external library behavior may have changed, verify against official docs
  before relying on memory.

## Workflow Steps

### Step 1: Read the Issue and Accepted Plan

Review:

- the issue description and acceptance criteria
- the latest accepted planning comment
- the current status
- any human comments posted after the latest review summary

### Step 2: Determine the Implementation Mode

#### If the issue is in `Planning`

- move the issue to `In Progress` if Linear is available
- create the implementation branch using this convention: `<type>/<issue-id>-short-desc` (e.g. `feat/CC-123-add-login-page`) — types: `feat`, `fix`, `docs`, `chore`
- reconfirm the planned scope before writing code

#### If the issue is in `In Review`

- read the human feedback posted after the latest review summary
- address only the requested fixes
- reuse the existing implementation branch when possible
- if the feedback materially changes the plan, stop and route to the
  revise-plan workflow
- move the issue back to `In Progress` while fixes are in progress if Linear is
  available

#### If the issue is in any other status

- do not proceed with implementation
- state what status the issue is in
- explain that implementation should begin from `Planning` or return from
  `In Review` for targeted fixes

### Step 3: Implement the Approved Scope

When implementing for the first time:

- follow the approved plan incrementally
- preserve existing patterns
- keep changes scoped to the issue

When fixing review feedback:

- focus only on the requested fixes
- do not expand scope or add unrelated improvements
- reference the reviewer feedback when deciding what to change

For all implementation work:

- use a tight loop of code, test, and adjust
- re-read touched files before editing to avoid drift
- consult `/product-spec` when product behavior, UX flow, or data semantics are
  not fully specified in the plan

### Step 4: Validate Incrementally

As implementation progresses:

- run relevant checks and tests for the areas being changed
- add or update tests when the change affects behavior
- prefer validating real user-impacting flows, not just static output
- if Playwright or equivalent E2E coverage exists in the repo for the affected
  area, use it for user-facing flows when practical

If validation reveals a material mismatch with the plan:

- pause implementation
- document the mismatch
- route to the revise-plan workflow instead of improvising

### Step 5: Testing Phase

After implementation is complete and before marking the issue review-ready:

- run a focused test pass using the `test-runner` brief or equivalent local test
  process
- provide changed files, feature context, and the implementation approach so
  testing can target likely failure modes

Testing should:

- analyze the changed code
- follow the `/test-spec` skill
- cover happy path, failure path, and important edge cases
- report implementation bugs precisely rather than hiding them

When deciding the testing scope:

- run comprehensive testing for first-time implementation
- run targeted testing for narrow review-fix follow-ups
- skip new tests only when the change is genuinely trivial or explicitly
  documented as not requiring tests

### Step 6: Handle Test Results

If tests pass:

- store the test results clearly for the review summary

If tests fail because implementation is wrong:

- fix the implementation
- rerun the relevant tests
- repeat until the work passes or a real blocker is identified

If testing cannot be completed:

- document exactly what could not be run and why
- do not claim the work is fully verified

### Step 7: Prepare Review State

Once the planned work is complete:

- ensure all changes are committed using this format:
  - During implementation: `<type>(<scope>): <subject> (Part of <issue-id>)`
  - Final commit: `<type>(<scope>): <subject> (Closes <issue-id>)`
  - Types: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`
- push the branch if remote workflow is active
- confirm acceptance criteria appear satisfied
- move the issue to `In Review` if Linear is available

## Validation Standard

Do not call the task review-ready until:

- acceptance criteria appear satisfied
- relevant tests pass, or any test gap is explicitly documented
- no known blocker remains
- the remaining reviewer work is primarily verification, not discovery

## Review Summary Standard

Use the `review-prep` brief to prepare the implementation review summary.

The review summary should include:

- branch name
- what changed
- which files or areas changed
- how the work aligns with the approved plan
- any deviations from scope or noteworthy observations
- testing and validation status
- what the human should verify
- a `Manual Test Instructions` section with concrete steps to follow
- the expected behavior or outcome for each manual verification step
- any setup, seed data, account state, feature flag, or environment prerequisite
  needed to test the change
- any known limitation, remaining risk, or intentionally unverified area

When returning from `In Review` for fixes, the updated summary should also make
clear:

- which reviewer comments were addressed
- what changed in response
- what should be re-verified specifically
