# cc-expert

A Claude Code plugin that provides expert-level assistance by thoroughly researching the official documentation and changelog before giving advice.

## Why This Plugin?

Claude Code is evolving rapidly with new features, capabilities, and best practices. This plugin ensures you always get advice based on:

- **Live Documentation**: Fetches the latest docs from code.claude.com
- **Current Changelog**: Checks recent updates for new features and fixes
- **Comprehensive Research**: Doesn't just look at one doc - explores all relevant pages

## Features

### Two Specialized Agents

#### 1. cc-explorer (Exploratory)
For brainstorming and project planning. Invoke with `/cc-expert:research` or let Claude auto-trigger when you ask:
- "What can Claude Code do for..."
- "How should I set up..."
- "What are my options for..."
- "Best way to structure..."

**What it does:**
1. Fetches the complete documentation index
2. Reads the changelog for latest features
3. Systematically fetches all relevant documentation pages
4. Synthesizes comprehensive, well-researched advice

#### 2. cc-solver (Targeted)
For solving specific problems. Invoke with `/cc-expert:solve` or let Claude auto-trigger when you ask:
- "How do I configure..."
- "Why isn't my hook working..."
- "I'm trying to set up MCP..."
- "Error when creating a skill..."

**What it does:**
1. Checks the changelog first (often has the answer!)
2. Fetches only the 2-4 most relevant docs
3. Provides focused, copy-paste ready solutions

### Slash Commands

#### `/cc-expert:research <topic>`

For comprehensive exploration of a topic:

```
/cc-expert:research hooks
/cc-expert:research MCP servers
/cc-expert:research plugin development
```

#### `/cc-expert:solve <problem>`

For targeted problem-solving:

```
/cc-expert:solve my hook isn't blocking bash commands
/cc-expert:solve MCP server authentication
/cc-expert:solve skill not auto-triggering
```

## Installation

### Option 1: Install from GitHub (Recommended)

Add the marketplace and install the plugin in one go:

```bash
# Add the marketplace (run inside Claude Code)
/plugin marketplace add mikkelkrogsholm/cc-expert

# Install the plugin
/plugin install cc-expert@cc-expert
```

Or using the CLI outside of Claude Code:

```bash
claude plugin marketplace add mikkelkrogsholm/cc-expert
claude plugin install cc-expert@cc-expert
```

### Option 2: Add to Your Project's Settings

Add cc-expert to your project so team members automatically get prompted to install it.

Add to `.claude/settings.json`:

```json
{
  "extraKnownMarketplaces": {
    "cc-expert": {
      "source": {
        "source": "github",
        "repo": "mikkelkrogsholm/cc-expert"
      }
    }
  },
  "enabledPlugins": {
    "cc-expert@cc-expert": true
  }
}
```

### Option 3: Local Development

For testing or contributing:

```bash
# Clone the repository
git clone git@github.com:mikkelkrogsholm/cc-expert.git

# Test locally with --plugin-dir (point to the plugin subdirectory)
claude --plugin-dir ./cc-expert/plugin
```

### Manage the Plugin

```bash
# View installed plugins
/plugin

# Disable without uninstalling
/plugin disable cc-expert@cc-expert

# Re-enable
/plugin enable cc-expert@cc-expert

# Uninstall completely
/plugin uninstall cc-expert@cc-expert

# Update to latest version
/plugin marketplace update cc-expert
```

## Usage Examples

### Using the Research Command
```
You: /cc-expert:research plugin development

Claude: [Spawns cc-explorer agent]
        [Agent fetches plugins.md, skills.md, hooks.md, slash-commands.md, etc.]
        [Agent returns comprehensive overview of all options]
```

### Using the Solve Command
```
You: /cc-expert:solve my PreToolUse hook isn't blocking Bash

Claude: [Spawns cc-solver agent]
        [Agent checks changelog for recent hook changes]
        [Agent fetches hooks.md, hooks-guide.md]
        [Agent returns specific fix for the issue]
```

### Auto-Triggering (if agent descriptions match your question)
```
You: What's the best way to structure a plugin for my team?

Claude: [May auto-trigger cc-explorer based on description match]
```

## How It Works

Both agents run as **subagents** via the Task tool, which means they execute in an isolated context. This:
- Keeps your main conversation clean
- Allows the agent to make multiple WebFetch calls without cluttering your chat
- Returns a synthesized result back to you

The agents use the `WebFetch` tool to retrieve:
- `https://code.claude.com/docs/llms.txt` - Documentation index
- `https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md` - Latest changes
- Individual documentation pages as needed

## Plugin Structure

```
cc-expert/
├── .claude-plugin/
│   └── marketplace.json     # Marketplace catalog (for GitHub installation)
├── plugin/                   # The actual plugin
│   ├── .claude-plugin/
│   │   └── plugin.json      # Plugin manifest
│   ├── commands/
│   │   ├── research.md      # /cc-expert:research command
│   │   └── solve.md         # /cc-expert:solve command
│   ├── agents/
│   │   ├── cc-explorer/
│   │   │   └── AGENT.md     # Exploratory research agent
│   │   └── cc-solver/
│   │       └── AGENT.md     # Targeted problem-solving agent
│   └── skills/              # Legacy skills (kept for auto-discovery)
│       ├── cc-explorer/
│       │   └── SKILL.md
│       └── cc-solver/
│           └── SKILL.md
└── README.md
```

## Version 2.0 Changes

- **Migrated from skills to agents**: Skills with `context: fork` had a known bug. Agents via the Task tool work reliably.
- **Added `/cc-expert:solve` command**: Explicit command for targeted problem-solving.
- **Improved reliability**: Subagents spawn correctly and return results.

## Contributing

Contributions welcome! Some ideas:
- Add more specialized agents for specific domains
- Improve the research heuristics
- Add caching for frequently accessed docs

## License

MIT
