# Contributing to Open Circle Agent Skills

Thank you for your interest in contributing! This document provides guidelines for contributing to the Open Circle Agent Skills repository.

## Getting Started

1. Fork the repository
2. Clone your fork locally
3. Create a new branch for your contribution

## Adding a New Skill

### 1. Create the Skill Directory

Create a new folder in `skills/` with your skill name (lowercase, hyphen-separated):

```
skills/your-skill-name/
└── SKILL.md
```

### 2. Write the SKILL.md

Your `SKILL.md` must include YAML frontmatter with required fields:

```yaml
---
name: your-skill-name
description: A clear description of what this skill does and when to use it. Include keywords that help agents identify when this skill is relevant.
license: MIT
metadata:
  author: your-github-username
  version: "1.0"
---

# Your Skill Name

## When to use this skill

Describe the scenarios where this skill should be activated.

## Instructions

Provide step-by-step guidance for the agent.

## Examples

Include code examples demonstrating usage.
```

### 3. Skill Requirements

- **name**: 1-64 characters, lowercase alphanumeric + hyphens, must match directory name
- **description**: 1-1024 characters, describe what the skill does and when to use it
- **Content**: Keep under 500 lines / 5000 tokens for the main SKILL.md

### 4. Optional Directories

If needed, you can add:

- `scripts/` — Executable code (Python, Bash, JavaScript)
- `references/` — Additional documentation files
- `assets/` — Templates, images, data files

## Style Guidelines

- Use clear, concise language
- Include practical code examples
- Document common edge cases
- Use relative paths for file references
- Keep content focused and actionable

## Testing Your Skill

Before submitting, validate your skill structure:

```bash
npx skills-ref validate ./skills/your-skill-name
```

## Submitting Changes

1. Commit your changes with a clear message
2. Push to your fork
3. Open a Pull Request against the `main` branch
4. Describe your changes and the skill's purpose

## Code of Conduct

Please be respectful and constructive in all interactions. We're building tools to help developers and AI agents work together effectively.

## Questions?

Open an issue if you have questions about contributing or need help with your skill.
