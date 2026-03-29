# Discuss Issue Workflow

Use when the user invokes `/discuss-issue-command` or `/discuss-issue`.

## Goal

Answer questions about an issue naturally without planning, implementing, or
modifying project state.

## Execution Rules

- Fetch only the minimum issue context first.
- Ask what the user wants to understand before loading more context.
- Gather code, comments, git history, or related issues only as needed to answer
  the specific question.
- Keep the conversation read-only and focused.

## Workflow Steps

### Step 1: Fetch Basic Issue Info

Load:

- title
- description
- status
- assignee when available

### Step 2: Ask What the User Wants To Discuss

Show the basic issue context, then ask what they want to understand or evaluate.

### Step 3: Gather Context On Demand

Based on the question, load only the relevant context:

- code when they ask about implementation
- comments when they ask about discussion or decisions
- git history when they ask what changed
- related issues when they ask about dependencies or broader scope

### Step 4: Answer Naturally

Respond directly to what they asked. Do not proactively plan or implement
unless they ask to move from discussion into action.

## Important

- Do not change code.
- Do not change issue state.
- Suggest the planning or implementation workflow only if the user wants to
  transition from discussion into execution.
