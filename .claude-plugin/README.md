# Claude Code Marketplace

This directory contains the plugin marketplace configuration for Claude Code.

## Files

- `marketplace.json` — Marketplace catalog listing the `valibot` and `formisch` plugins

Each plugin points to its skill folder in `skills/`, which contains its own `.claude-plugin/plugin.json` manifest next to the `SKILL.md` file.

## Usage

```bash
/plugin marketplace add open-circle/agent-skills
/plugin install valibot@open-circle
/plugin install formisch@open-circle
```

## Validation

```bash
claude plugin validate .
claude plugin validate ./skills/valibot
claude plugin validate ./skills/formisch
```
