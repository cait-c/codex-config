---
name: research-codebase
description: Comprehensive codebase research for architecture, system design, patterns, and end-to-end feature understanding. Use when the user asks to research, investigate, explore, or understand a codebase; when documenting how features work or where functionality is implemented; or when preparing context before making changes. Always invoke this skill for codebase research requests and do not use the default plan mode or default plan agent.
---

# Research Codebase

## Overview

Conduct thorough, multi-angle codebase research using parallel sub-agents, then synthesize findings into a structured research document.

## Workflow

### 1. Read mentioned files first and classify request

- Read any explicitly mentioned files fully (no limit/offset) before spawning tasks.
- Determine whether the request is:
  - General research request: Understand the repo/system purpose, core components, interactions, and external dependencies.
  - Specific research request: Do everything in general research, plus deep dives into components tied to the specific feature/question.

### 2. Decompose the research question

- Break the request into composable, independent research areas.
- Identify components, patterns, concepts to investigate.
- Create a research plan (use a TodoWrite-style plan tool if available) with concrete investigation tasks.
- Add extra tasks for specific research requests to cover feature-specific components and interactions.

### 3. Spawn parallel sub-agents

- Use `codebase-locator` agents to find relevant files and directories.
- Use `codebase-analyzer` agents for deep dives on promising components.
- Use `codebase-pattern-finder` to surface existing patterns and examples.
- Run multiple agents in parallel for efficiency.

### 4. Synthesize results

- Wait for all sub-agents to finish.
- Prioritize live codebase evidence over prior knowledge or documentation.
- Include file paths and line numbers for all references.
- Highlight patterns, architectural decisions, and design rationale.

### 5. Generate the research document

- Output path: `./YYYY-MM-DD-<description>.md`.
- Use the template at `~/assets/research-template.md`.
- Add GitHub permalinks if on `main` branch or pushed to remote.

### 6. Present findings to the user

- Summarize key discoveries.
- Highlight anything surprising or noteworthy.
- Note open questions or areas needing further investigation.

## Notes

- Do not use the default plan mode or plan agent for research requests.
- Use the named sub-agents as the primary mechanism for discovery and analysis.
