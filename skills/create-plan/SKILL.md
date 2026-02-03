---
name: create-plan
description: Create detailed implementation plans with thorough research and iteration. Use when starting significant features spanning multiple files, planning refactors affecting architecture, working on multi-phase projects with milestones, establishing success criteria before coding, breaking down complex work, or documenting approach for non-trivial technical decisions.
---

# Create Implementation Plan (Generic)

## Workflow

### 1. Understand The Requirement

- Read all mentioned files completely (no partial reads)
- Present an informed understanding with specific `file:line` references
- Ask focused questions only about what research could not clarify
- Do not ask questions answerable through code exploration

### 2. Decompose And Plan Research

- Break the task into composable research areas
- Identify components, patterns, and concepts to investigate
- Use TodoWrite to track subtasks
- Think through underlying patterns and constraints

### 3. Spawn Parallel Sub-Agents

**Codebase research**
- Use `codebase-locator` to find where files and components live
- Use `codebase-analyzer` to understand how existing code works
- Use `codebase-pattern-finder` to find similar implementations

**Agent tips**
- Start with locator work to map the terrain
- Use analyzer on promising locations
- Run multiple agents in parallel when possible
- Tell agents what you are looking for, not how to search

### 4. Wait And Synthesize

After all sub-agents complete:
- Compile results and prioritize the live codebase as source of truth
- Include file paths and line numbers
- Highlight patterns, connections, and architectural decisions
- Answer open questions with concrete evidence

### 5. Propose Plan Structure

Present an outline and get explicit approval before detailed planning:

```
## Overview
[1-2 sentence summary]

## Implementation Phases:
1. [Phase Name] - [What this accomplishes]
2. [Phase Name] - [What this accomplishes]
3. [Phase Name] - [What this accomplishes]
```

### 6. Write The Plan

Save to `./YYYY-MM-DD-plan.md`.

**Plan structure**
- Overview
- Current State Analysis (with `file:line` refs, constraints, gaps)
- Desired End State
- Key Discoveries (with `file:line` refs)
- What We Are Not Doing
- Implementation Approach

**Per phase**
- Overview
- Required changes (files and specifics)
- Success criteria
- Confirmation gate
- Ensure current tests pass
- Add new tests as needed

**End with**
- Testing Strategy (unit, integration, manual)
- References (tickets, research, code refs)

## Success Criteria Format

**Automated**: Tests, type check, lint, build  
**Manual**: Feature works, performance acceptable, edge cases handled

## Key Principles

- Use `file:line` references and measurable criteria
- Define phases with confirmation gates
- Research before proposing
- Consider backward compatibility
- Avoid open questions; research or ask first

## Common Implementation Patterns

**Database changes**  
Schema → Store/Repository methods → Business logic → API endpoints → Client code

**New features**  
Research patterns → Data model → Backend implementation → API → UI/Frontend

**Refactoring**  
Document current state → Incremental changes → Maintain backward compatibility → Migration strategy

**API changes**  
Document current behavior → Deprecation plan → New implementation → Migration guide → Old code removal
