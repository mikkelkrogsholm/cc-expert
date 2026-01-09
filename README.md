# cc-expert

A Claude Code plugin that provides expert-level assistance by thoroughly researching the official documentation and changelog before giving advice.

## Why This Plugin?

Claude Code is evolving rapidly with new features, capabilities, and best practices. This plugin ensures you always get advice based on:

- **Live Documentation**: Fetches the latest docs from code.claude.com
- **Current Changelog**: Checks recent updates for new features and fixes
- **Comprehensive Research**: Doesn't just look at one doc - explores all relevant pages

## Features

### Two Intelligent Skills

#### 1. cc-explorer (Exploratory)
For brainstorming and project planning. Auto-triggers when you ask:
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
For solving specific problems. Auto-triggers when you ask:
- "How do I configure..."
- "Why isn't my hook working..."
- "I'm trying to set up MCP..."
- "Error when creating a skill..."

**What it does:**
1. Checks the changelog first (often has the answer!)
2. Fetches only the 2-4 most relevant docs
3. Provides focused, copy-paste ready solutions

### Explicit Command

#### `/cc-expert:research <topic>`

For when you want to explicitly trigger comprehensive research on a topic.

```
/cc-expert:research hooks
/cc-expert:research MCP servers
/cc-expert:research plugin development
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

# Test locally with --plugin-dir
claude --plugin-dir ./cc-expert
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

### Exploratory Mode
```
You: I want to build a plugin for my team that enforces coding standards.
     What features should I use?

Claude: [Activates cc-explorer skill]
        [Fetches plugins.md, skills.md, hooks.md, slash-commands.md, etc.]
        [Provides comprehensive overview of all options]
```

### Problem-Solving Mode
```
You: My PreToolUse hook isn't blocking the Bash command like I expected.

Claude: [Activates cc-solver skill]
        [Checks changelog for recent hook changes]
        [Fetches hooks.md, hooks-guide.md]
        [Provides specific fix for the issue]
```

### Explicit Research
```
You: /cc-expert:research MCP server authentication

Claude: [Fetches llms.txt, changelog, mcp.md, iam.md, settings.md]
        [Provides complete guide to MCP authentication]
```

## How It Works

Both skills use `context: fork` which means they run in an isolated sub-agent context. This prevents the research from bloating your main conversation while still providing you with comprehensive results.

The skills use the `WebFetch` tool to retrieve:
- `https://code.claude.com/docs/llms.txt` - Documentation index
- `https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md` - Latest changes
- Individual documentation pages as needed

## Plugin Structure

```
cc-expert/
├── .claude-plugin/
│   ├── plugin.json          # Plugin manifest
│   └── marketplace.json     # Marketplace catalog (for GitHub installation)
├── commands/
│   └── research.md          # /cc-expert:research command
├── skills/
│   ├── cc-explorer/
│   │   └── SKILL.md         # Exploratory research skill
│   └── cc-solver/
│       └── SKILL.md         # Targeted problem-solving skill
└── README.md
```

## Contributing

Contributions welcome! Some ideas:
- Add more specialized skills for specific domains
- Improve the research heuristics
- Add caching for frequently accessed docs

## License

MIT
