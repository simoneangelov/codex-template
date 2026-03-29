# Complete Issue Workflow

Use when the user invokes `/complete-issue-command` or `/complete-issue`.

## Goal

Finalize reviewed work by confirming human approval, creating and merging the
PR when applicable, posting a completion update, and marking the issue `Done`.

## Execution Rules

- Treat explicit human approval as authoritative.
- Do not modify code during this workflow.
- Do not re-plan, re-implement, or regenerate the review summary.
- If approval is missing or unresolved concerns remain, stop.

## Workflow Steps

### Step 1: Read the Current Review State

Confirm:

- the issue is currently in `In Review`
- a review summary exists
- a human has explicitly approved the work or otherwise indicated it meets
  expectations

If the issue is not in `In Review`, do not proceed.

### Step 2: Create the Pull Request

If a remote workflow is in use:

- create the PR from the feature branch to the main branch
- use conventional commit style for the PR title
- include a short summary, the related issue ID, and the test/validation status

### Step 3: Merge the Pull Request

If the repository workflow allows it:

- merge the PR
- do not delete the implementation branch unless the repo workflow explicitly
  says to do so

If CI or merge requirements block completion, leave the issue in `In Review`
and report the blocker clearly.

### Step 4: Post the Completion Comment

If Linear is available, post a short, factual completion comment that:

- confirms the issue was reviewed and approved
- notes that the PR was merged
- marks the work as complete

### Step 5: Update Linear

Move the issue to `Done`.

## Guardrails

- If approval is missing, stop.
- If the issue is not review-ready, stop.
- If GitHub or Linear integrations are unavailable, report the exact manual
  completion steps remaining.
