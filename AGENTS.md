# Codex Workflow Instructions

You are helping build **[PROJECT_NAME]**, [PROJECT_DESCRIPTION].

## Core Behavior

- Prefer small, scoped changes.
- Never refactor unrelated files.
- Never modify config files or `.env*` files without explicit instruction.
- Never commit secrets or copy local credentials into Codex config.
- Re-read touched files before editing to avoid duplication or drift.
- Verify behavior, not just appearance.
- Do not add enhancements that were not requested or approved.
- Think methodically before coding.
- Re-check task scope before concluding work.

## Source Of Truth

- Product behavior: `.codex/docs/product-spec.md`
- Development workflow: [add path if you have one]
- Test guidance: [add path if you have one]

Load the minimum relevant file before acting when the task touches product behavior, issue workflow, or testing strategy.

## Project Defaults

- Single-owner repository
- Package manager: `[PACKAGE_MANAGER]`
- Prefer existing repository patterns over invention
- When external APIs or libraries are involved, verify against official docs if the API may have changed

## Command-Style Workflow

If the user invokes any of the following command-style prompts, treat them as workflow entry points and load the matching file in `.codex/workflows/` before proceeding:

- `/create-issue-command` or `/create-issue`
- `/discuss-issue-command` or `/discuss-issue`
- `/plan-issue-command` or `/plan-issue`
- `/revise-plan-command` or `/revise-plan`
- `/implement-issue-command` or `/implement-issue`
- `/complete-issue-command` or `/complete-issue`

The workflow docs define the expected behavior, outputs, and status transitions. Follow them unless the user explicitly asks for a different flow.

## Linear-Centric Mode

When the user is working from a Linear issue:

- Treat the Linear issue and its latest approved plan as the source of truth.
- Keep status transitions aligned with the workflow.
- Use concise, factual Linear comments.
- If Linear or GitHub integrations are unavailable in the current Codex environment, continue with the same reasoning flow locally and clearly state what must be completed manually.

## Delegation

When delegation would help, prefer narrow sub-tasks and mirror these role briefs:

- Issue analysis: `.codex/briefs/linear-issue-analyzer.md`
- Repository discovery: `.codex/briefs/repo-explorer.md`
- Ambiguity resolution: `.codex/briefs/project-expert.md`
- Planning synthesis: `.codex/briefs/solution-planner.md`
- Testing: `.codex/briefs/test-runner.md`
- Review summary: `.codex/briefs/review-prep.md`

Use them as prompt templates for spawned agents. Keep ownership clear and avoid duplicate work.

## Practical Rules

- Ask the user only when a decision is truly blocking or risky.
- If a workflow references unavailable tooling, fall back gracefully instead of stopping early.
- Do not copy local-only hooks, permissions, or secret-bearing settings into shared repo config.
