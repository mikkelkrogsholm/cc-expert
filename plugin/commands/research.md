---
description: Comprehensively research Claude Code documentation for a specific topic
argument-hint: <topic>
model: sonnet
allowed-tools: WebFetch, Read, Grep, Glob, Bash
---

# Claude Code Documentation Research

You are being asked to perform comprehensive research on Claude Code documentation for the topic: **$ARGUMENTS**

## Your Mission

Thoroughly research the Claude Code documentation to provide expert-level guidance on the requested topic.

## Research Steps

### 1. Fetch the Documentation Index

First, get the complete list of available documentation:

```
WebFetch: https://code.claude.com/docs/llms.txt
```

### 2. Fetch the Changelog

Get the latest updates and features:

```
WebFetch: https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md
```

### 3. Fetch ALL Relevant Documentation

Based on the topic "$ARGUMENTS", identify and fetch ALL documentation pages that could be relevant. Be thorough - fetch at least 5-10 relevant pages. Don't just pick one or two.

For each relevant page from the index:
```
WebFetch: https://code.claude.com/docs/en/[page-name].md
```

### 4. Synthesize Your Findings

After reading all the documentation, provide a comprehensive response that includes:

## Response Format

```
## Executive Summary
[3-5 sentence overview of the topic and key findings]

## Core Concepts
[Explain the fundamental concepts related to this topic]

## Available Features
[Comprehensive list of relevant features with brief descriptions]

## Recommended Implementation
[Step-by-step guide for the most common use case]

## Configuration Reference
[Relevant settings, file paths, and configuration options]

## Code Examples
[Practical, copy-paste ready examples]

## Advanced Usage
[More sophisticated patterns and techniques]

## Recent Updates
[Relevant changes from the changelog]

## Common Pitfalls
[Issues to watch out for, based on documentation]

## Related Features
[Other features that work well with this topic]

## Documentation Sources
[List all documentation pages you consulted]
```

## Guidelines

- Fetch documentation liberally - the user wants comprehensive information
- Include specific code examples and configurations
- Reference exact file paths and settings names
- Note version requirements if mentioned in changelog
- If something isn't supported, clearly state that
- Cross-reference related features when relevant
