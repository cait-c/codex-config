# Usage

This pulls from agents & skills introduced here: https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/ace-fca.md -- specifically this section.

Also pulled from https://github.com/carterbs/agent-config and https://github.com/tausman/claude-config

This is a WIP to utilize dedicated skills and agents to create a workflow that accomplishes work more efficiently.

# Research

Always start with a clear context. Use the `$research-codebase` skill, which will spawn agents to understand the problem space. You can create a `PROMPT.md` file along the lines of:

```
I want to understand X. Can you give me a high-level overview of the important components and how this particular section Y works? Write your findings to RESEARCH.md.
```

You can continue to add to the research by asking follow-up questions. If this is a multi-service or multi-repo change, it can be worth having multiple `RESEARCH.md` files.

This research phase is just as important for the human in the loop as it is for the agent. This part should require the most brainpower. Being lazy here will lead to not understanding the plan or implementation and will likely lead to poor results.

# Plan

The research step should have clarified anything that you did not understand, if you are still unclear then go back to the research step.
Clear the context. Use the `$create-plan` skill and add the `RESEARCH.md` file(s) to the context. Describe the outcome that you want to achieve. Add a jira ticket (if it is well scoped) and add pictures/diagrams if you can. If you know specific areas of code or components that need to be modified, refer to the files or methods by name to guide the agent. If this is a multi-repo or multi-service change, be sure the agent has access to all the code. Be sure to tell the agent to write the plan to a `PLAN.md` file.

Additionally, prompt the agent with something like:

```
Break the task down into phases. Each phase should be a commit. Before a commit is made, new tests should be added for the new code paths. Before a commit is made, run all tests to make sure they are passing. If tests are failing, keep iterating until they succeed. If you cannot run tests or they are failing, stop and ask for guidance.
```

It is important for the agent to work on small, specific pieces of work and a feedback/validation loop.

Review the plan. You can either iterate on the plan or start over if things do not look right. It is challenging to modify the plan once the agent starts implementation, so you want this to be as accurate as possible.

# Implement

The final step is to clear the context and run `$implement-plan`. Open the branch to watch and follow along. If the code or problem is not well understood, or there are a lot of phases in the plan, it is likely that there will be some human intervention.

You can pause the main agent, start a new session, investigate code changes, and ask the new agent for assistance. Then, inform the main agent of changes, tell it to update the plan (add or edit a phase), and have it continue where it left off.

If there are large changes, modifying the plan live is not always effective. If live modification is not working, the two approaches you can take are: take your learnings and try again from step 1 or 2, or let the agent complete its work and clean up afterwards with the help of additional agents.

If you do not get the desired results, there is nothing wrong with going back to the planning stage or even the research stage. Part of software development is learning by doing, and agentic development just lets us do this much faster. We can find pitfalls or missed edge cases within hours instead of days.

# Codex Skills Setup

To add a skill to your global Codex install, copy (or paste) each skill folder into `~/.codex/skills/`.

Then:

1. Restart Codex after adding skills to the global Codex config.
2. Start the Codex CLI by running `codex`.
3. List skills with `/skills`, or invoke a skill by name using a dollar sign, e.g. `$create-plan`.

# Codex Agents Setup

Place `AGENTS.md` at the root of `~/.codex/`.

For up-to-date documentation, always reference:

- https://developers.openai.com/codex/config-basic