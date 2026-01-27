# Open Circle Agent Skills

This repository contains Agent Skills for Open Circle projects. Skills help AI agents work effectively with Valibot, Formisch, and other tools in the Open Circle ecosystem.

## Available Skills

- **valibot-usage** — Schema validation with Valibot
- **formisch-usage** — Form handling with Formisch

## How to Use

When working on tasks involving Open Circle projects, consult the relevant skill in the `skills/` directory. Each skill contains a `SKILL.md` with detailed instructions.

## Skill Format

Each skill follows the [agentskills.io](https://agentskills.io) specification:

```
skill-name/
├── SKILL.md          # Required: instructions + metadata
├── scripts/          # Optional: executable code
├── references/       # Optional: documentation
└── assets/           # Optional: templates, resources
```

## Guidelines

1. **Check skill metadata** — The `description` field indicates when to use each skill
2. **Follow instructions** — Each skill contains step-by-step guidance
3. **Use examples** — Skills include code examples and patterns
4. **Reference documentation** — Skills link to official docs when needed
