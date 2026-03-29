# Create Issue Workflow

Use when the user invokes `/create-issue-command` or `/create-issue`.

## Goal

Create a well-formed issue with the minimum back-and-forth necessary while
still capturing enough detail to plan and implement safely later.

## Execution Rules

- Gather all required information before creating the issue.
- Infer smart defaults where the intent is clear.
- Ask only for fields that cannot be inferred safely.
- Do not create a partial issue missing the core problem or acceptance criteria.

## Workflow Steps

### Step 1: Gather the Required Details

Collect or confirm:

- title
- description
- acceptance criteria

### Step 2: Infer Smart Defaults

Infer when possible:

- type: bug, feature, improvement
- priority
- default status
- likely project
- likely assignee when local workflow conventions make it obvious

Ask only when inference would be risky or ambiguous.

### Step 3: Determine Team and Metadata

If Linear tooling is available:

- determine the correct team
- add the appropriate issue type label when supported
- include any explicitly requested labels, assignee, or due date

### Step 4: Create the Issue

Create the issue in Linear when possible.

If Linear tooling is unavailable, produce a ready-to-paste markdown issue draft
that includes the suggested metadata.

## Minimum Issue Shape

- Title
- Description
- Acceptance criteria

## Output

- Confirm the created issue ID and link, or
- Provide a markdown issue draft plus the suggested next command
