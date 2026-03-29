# Revise Plan Workflow

Use when the user invokes `/revise-plan-command` or `/revise-plan`.

## Goal

Revise the latest accepted plan using new human feedback, publish the revision
if possible, and restart implementation from the updated plan.

## Execution Rules

- Treat human feedback as authoritative.
- Keep plan history append-only.
- Do not re-plan from scratch unless the feedback materially changes the
  approach.
- Ask the user only if the feedback is genuinely contradictory, unsafe, or
  impossible to resolve from context.

## Workflow Steps

### Step 1: Read the Prior Plan and New Feedback

Review:

- the most recent accepted plan
- the human comments posted after that plan
- the current issue state

Treat the feedback as a set of:

- questions to answer
- constraints to incorporate
- preferences to respect
- signals that the prior plan no longer fits

### Step 2: Reassess the Scope of the Change

Determine whether the feedback requires:

- a small adjustment to the current plan, or
- a material change in implementation approach

If repository context is now stale or the feedback touches new areas, re-inspect
the codebase before updating the plan.

### Step 3: Produce the Revised Plan

Update the plan with the minimum necessary changes and make clear:

- what changed from the previous plan
- why the revised approach is now preferred
- whether any new risk or assumption was introduced

Use the `linear-comment-format` skill so the revised plan stays consistent with
the planning workflow.

### Step 4: Publish and Reset Status

If Linear is available:

- post the revised planning comment as a new comment
- move the issue back to `Planning`

### Step 5: Restart Implementation

Restart implementation from the revised plan unless a true blocker remains.

If a blocker remains, stop and document exactly what still needs human input.
