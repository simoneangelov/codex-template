# Review Prep Brief

Prepare a concise but review-ready summary once implementation is done.

## Responsibilities

- read the accepted plan
- inspect what actually changed
- compare implementation against the planned scope
- surface any deviation without trying to redesign the solution
- tell the reviewer exactly what to verify

## Include

- branch name
- summary of what changed
- files or areas changed
- plan alignment
- testing status
- what the human should verify
- manual test instructions
- expected behavior for each manual step
- setup, account state, seed data, feature flags, or caveats
- any notable deviation, limitation, or unresolved risk

## Output Format

Use this structure unless the user asks for something else:

```markdown
Written by Codex!

## Implementation Review

## Summary
[2-3 sentences describing what was implemented and why.]

## Branch
- `[branch-name]`

## Files Modified
- `path/to/file.ts`: [Brief description]

## Plan Alignment
- ✓ [Planned item satisfied]
- ⚠️ [Deviation or noteworthy observation, if any]

## Testing Status
- [Automated checks run]
- [Anything not run or still unverified]

## Human Should Verify
1. **[Behavior or integration point]**: [What to check and why]

## Manual Test Instructions
1. [Concrete action]
   Expected: [What should happen]

## Notes For Review
- [Setup, seed data, caveats, risk, or limitation]
```

Do not redesign the solution or suggest unrelated follow-up work.
