# Template Setup

This repository is a Codex template. It includes a complete autonomous development system in `.codex/` — briefs and workflows that power a Linear-driven workflow for planning, implementing, reviewing, and completing issues.

The template is project-agnostic. Follow the steps below to make it yours.

---

## Step 1: Add your product spec

Replace `.codex/docs/SPEC.pdf` with your actual product specification. This is the source of truth the `project-expert` agent will reference when answering planning questions that require product-level understanding.

Your spec should cover what the product does, who it's for, core features and flows, data model, tech stack, V1 scope, and known future plans.

---

## Step 2: Run the setup prompt

Copy the prompt below, fill in the placeholders, and paste it into Codex or Claude Code.

```
I'm setting up a new project using the Codex template.

Project name: [PROJECT_NAME]
One-line description: [ONE_SENTENCE_DESCRIPTION e.g. "a Next.js app that does X for Y"]
Package manager: [e.g. pnpm, npm, yarn]
Tech stack: [e.g. Next.js 14, TypeScript, Prisma, PostgreSQL, Vitest, Playwright]
Test commands: [e.g. pnpm test for unit tests, pnpm test:e2e for E2E]

Please do the following:

1. Read my product spec at .codex/docs/SPEC.pdf.
2. Copy AGENTS-TEMPLATE.md to AGENTS.md — replace [PROJECT_NAME] with the project name, [PROJECT_DESCRIPTION] with the one-line description, and [PACKAGE_MANAGER] with the package manager above. Do not modify AGENTS-TEMPLATE.md.
3. Rewrite .codex/briefs/repo-explorer.md — add the tech stack above so the agent knows what to look for when inspecting the repository.
4. Rewrite .codex/briefs/solution-planner.md — add any architectural constraints or preferences implied by the tech stack and spec (e.g. prefer server components, avoid new dependencies without justification).
5. Rewrite .codex/briefs/test-runner.md — replace the placeholder test tooling section with the actual test framework and commands above.
6. Update .codex/workflows/implement-issue.md — add these git conventions to the branch creation and commit steps:
   - Branch naming: <type>/<issue-id>-short-desc (e.g. feat/CC-123-add-login-page) — types: feat, fix, docs, chore
   - Commit format: <type>(<scope>): <subject> (<Magic-Word> <issue-id>) — types: feat, fix, docs, style, refactor, test, chore
   - Magic words: use "Part of <issue-id>" during implementation, "Closes <issue-id>" on the final commit

Do not modify any other files.
```

---

## What the template includes

**Briefs** — role-scoped instruction files that agents load for specific jobs:
- `linear-issue-analyzer` — extracts requirements and scope from a Linear issue
- `repo-explorer` — maps existing code before implementation begins
- `solution-planner` — generates and evaluates implementation approaches
- `project-expert` — answers planning questions using spec, git history, and codebase
- `test-runner` — writes and runs tests, reports implementation bugs back precisely
- `review-prep` — synthesizes completed work into a review-ready summary

**Workflows** — slash commands that orchestrate the full development lifecycle:
- `/plan-issue` — analyze a Linear issue → propose implementation → post to Linear
- `/implement-issue` — implement the approved plan → commit incrementally → prepare for review
- `/revise-plan` — revise a planning proposal based on new human feedback
- `/complete-issue` — create PR → merge → mark issue Done
- `/create-issue` — guided issue creation with smart defaults
- `/discuss-issue` — explore a Linear issue conversationally