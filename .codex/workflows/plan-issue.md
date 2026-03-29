# Plan Issue Workflow

Use when the user invokes `/plan-issue-command` or `/plan-issue`.

## Goal

Analyze the issue thoroughly, resolve as much ambiguity as possible from repo
and issue context, publish a concrete implementation plan, move the issue into
`Planning` when possible, and continue into implementation unless a real blocker
remains.

## Execution Rules

- Treat the issue description, acceptance criteria, and the latest relevant
  human comments as the source of truth.
- Prefer issue context and repository evidence before loading extra skills.
- Resolve ambiguities autonomously whenever repo context, issue history, git
  history, or project skills can answer them.
- Ask the user only when the remaining ambiguity is contradictory, safety
  critical, or impossible to resolve from available context.
- Load only the minimum relevant skills needed to plan correctly.
- Do not invent requirements that are not supported by the issue, repo, or
  project specification.

## Workflow Steps

### Step 1: Read the Issue

Extract and document:

- the core problem being solved
- acceptance criteria
- constraints and non-goals
- scope and complexity
- ambiguities or missing information

Use the `linear-issue-analyzer` brief when it would help keep this analysis
structured.

### Step 2: Resolve Ambiguities

Before proposing an approach, resolve open questions using:

- repository context
- issue comment history
- git history
- relevant project skills

Use the `project-expert` brief for focused questions that would otherwise turn
into guesswork. The goal is to post a planning comment with few or no open
questions.

### Step 3: Inspect the Repository

Inspect the existing implementation before proposing changes. Identify:

- relevant files and entry points
- existing patterns and conventions
- dependencies and coupling
- technical risks or missing infrastructure
- nearby tests that establish current behavior

Use the `repo-explorer` brief when a dedicated discovery pass would help.

### Step 4: Load Specification Context Only When Needed

Load the minimum relevant skills when correctness depends on product rules,
workflow rules, or test expectations that are not obvious from code alone.

Typical cases:

- `/product-spec` for product behavior, UX expectations, and data semantics
- `/test-spec` when the likely implementation affects test scope
- `/dev-workflow` for branch, commit, PR, and done criteria

### Step 5: Produce the Recommended Plan

Synthesize the issue context and repository findings into a single recommended
approach. Include:

- a concise problem summary
- the proposed implementation approach
- why this approach is preferred
- expected behavior before and after the change
- risks, assumptions, and dependencies
- open questions only if they truly remain unresolved

Use the `solution-planner` brief when tradeoffs are non-trivial.

### Step 6: Format and Post the Plan

Format the plan using the `linear-comment-format` skill.

If Linear tooling is available:

- post the planning comment
- move the issue to `Planning`

If Linear tooling is unavailable, still produce a review-ready plan in the same
shape so it can be posted manually.

### Step 7: Continue Into Implementation

If no blocking ambiguity remains, continue into the implementation workflow.

If uncertainty remains but implementation is still safe:

- document the uncertainty explicitly in the plan
- state any assumptions being made

If the ambiguity would make coding unsafe:

- stop before implementation
- state exactly what is unresolved and why it blocks coding

## Planning Philosophy

- Prefer clarity over verbosity
- Favor small, scoped changes
- Respect existing patterns and constraints
- Surface risks and assumptions explicitly
- Make the plan concrete enough that implementation can begin without
  reinterpretation
