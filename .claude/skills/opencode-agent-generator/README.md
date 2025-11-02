# OpenCode Agent Generator

Creates OpenCode agents in project folders with proper configuration and permissions.

## Usage
Ask Claude to create an OpenCode agent:
```
Create an OpenCode agent for code review with restrictive permissions
```

## What it does
- Generates proper YAML frontmatter
- Sets appropriate tool permissions
- Creates focused system prompts
- Validates agent configuration

## Agent location
Agents are created in `.opencode/agent/` (project-local, not global)