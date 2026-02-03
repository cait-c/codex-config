---
name: implement-plan
description: Implement technical plans with verification and phase gates. Use when a completed implementation plan is ready to execute systematically, including multi-phase work, success criteria tracking, explicit confirmation between phases, and prescribed testing procedures or file:line references.
---

# Implement Plan

## Overview

Execute a completed technical plan phase by phase with verification, explicit phase gates, and clear reporting. Track success criteria and testing requirements as written in the plan.

## Workflow

### 1. Load The Plan

- Ask for the plan path if it is not provided
- Read the full plan and extract phases, success criteria, dependencies, and prerequisites
- Run pre-flight checks: `git status`, `git log -1`
- Note any assumptions or prerequisites called out in the plan

### 2. Create Branches For All Repos

- If implementation has not started:
  - Create a feature branch from the base repo
  - Use `feature/<work_name>` based on the plan or ticket
  - Example:
```bash
cd /Users/caitlin.ciaramella/grata/<repo_name>
git checkout main
git checkout -b feature/<work_name>
```
- If implementation has already started:
  - Find the existing branch that matches the `work_name`
  - If repo or branch cannot be found, stop and ask before continuing
- Work only on a non-main branch

### 3. Execute Each Phase

For each phase in order:

**Implement**
- Make changes exactly per plan (honor file:line references)
- Follow existing patterns
- Update the plan to mark phase progress
- Ensure tests pass before committing
- Make a single commit for the phase with a descriptive message

Example commit message:
```
Phase 1: Add configuration validation layer

- Implement ConfigValidator class (config/validator.ts)
- Add unit tests for validation rules
- Ref: ./2025-12-23-config-refactor.md
```

**Verify Automatically**
- Run the tests specified by the plan
- If the plan is silent, run the repo’s standard test command

**Report Results**
- Summarize passes
- Include full error output on failures
- Call out any unexpected failures

**Manual Verification**
- Follow plan testing steps
- Verify every success criterion, edge case, and error handling requirement

### 4. Phase Gate

After success criteria are met, report and wait for explicit confirmation:

```
✓ Phase [N]: [Phase Name]

Implemented:
- [specific changes made]
- [files modified]

Verification Results:
- Automated checks: All passing
- Manual verification: Complete

Commits: [hash(es)]

Proceed to Phase [N+1]? (waiting for confirmation)
```

- Do not proceed without confirmation
- Ensure the plan is marked complete for the phase

### 5. Final Verification

After all phases:

1. Run the full automated validation suite again
2. Perform end-to-end testing for the entire feature
3. Document completion:

```
✅ Implementation Complete: [Feature Name]

Plan: ./[filename]

Phases Executed:
- Phase 1: [Name] ✓ [commit hash]
- Phase 2: [Name] ✓ [commit hash]

Success Criteria Verified:
- Automated: All passing
- Manual: All verified

Files modified: [count]
Commits: [count] | Branch: [name]

Next Steps:
- [Follow-up items]
```

## Handling Issues

**Automated checks fail**
1. Show complete error output
2. Analyze cause
3. Propose solutions or ask for guidance
4. Ask: “Fix this, troubleshoot further, or try different approach?”

**Manual testing reveals problems**
1. Document the issue clearly
2. Determine if it is in scope for the current phase
3. Fix immediately or note as follow-up

**Plan unclear**
1. Quote the ambiguous text
2. Propose an interpretation
3. Wait for confirmation before proceeding

## Key Principles

- Complete one phase at a time
- Reference the plan continuously and flag deviations
- Verify automatically before manual testing
- Require explicit confirmation between phases
- Document issues immediately
