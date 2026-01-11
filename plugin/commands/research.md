---
description: Comprehensively research Claude Code documentation for a specific topic
argument-hint: <topic>
allowed-tools: Task
---

Use the Task tool to spawn a cc-explorer agent that will thoroughly research Claude Code documentation.

**IMPORTANT**: You MUST use the Task tool with these exact parameters:
- `subagent_type`: "cc-explorer"
- `prompt`: "Research Claude Code documentation for: $ARGUMENTS"
- `description`: "Research Claude Code docs"

The cc-explorer agent will:
1. Fetch the complete documentation index from code.claude.com
2. Read the changelog for latest features
3. Systematically fetch all relevant documentation pages
4. Synthesize comprehensive, well-researched advice

Example Task tool invocation:
```
Task(
  subagent_type="cc-explorer",
  prompt="Research Claude Code documentation for: $ARGUMENTS",
  description="Research Claude Code docs"
)
```

Execute this Task tool call now to begin the research.
