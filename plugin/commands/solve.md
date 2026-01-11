---
description: Solve a specific Claude Code problem or implementation question
argument-hint: <problem>
allowed-tools: Task
---

Use the Task tool to spawn a cc-solver agent that will research and solve your Claude Code problem.

**IMPORTANT**: You MUST use the Task tool with these exact parameters:
- `subagent_type`: "cc-solver"
- `prompt`: "Solve this Claude Code problem: $ARGUMENTS"
- `description`: "Solve Claude Code problem"

The cc-solver agent will:
1. Check the changelog for recent changes or fixes
2. Fetch only the 2-4 most relevant documentation pages
3. Provide focused, copy-paste ready solutions

Example Task tool invocation:
```
Task(
  subagent_type="cc-solver",
  prompt="Solve this Claude Code problem: $ARGUMENTS",
  description="Solve Claude Code problem"
)
```

Execute this Task tool call now to solve the problem.
