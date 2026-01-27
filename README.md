# Open Circle Agent Skills

A collection of [Agent Skills](https://agentskills.io) for [Open Circle](https://opencircle.dev) projects. These skills help AI agents work effectively with Valibot, Formisch, and other Open Circle ecosystem tools.

## What are Agent Skills?

Agent Skills are a lightweight, open format for extending AI agent capabilities with specialized knowledge and workflows. Each skill is a folder containing a `SKILL.md` file with metadata and instructions that help AI agents understand how to use specific tools and libraries.

Learn more at [agentskills.io](https://agentskills.io)

## Available Skills

| Skill                                    | Description                    |
| ---------------------------------------- | ------------------------------ |
| [valibot-usage](skills/valibot-usage/)   | Schema validation with Valibot |
| [formisch-usage](skills/formisch-usage/) | Form handling with Formisch    |

## Installation

You can install these skills using th `skills` or `add-skill` CLI:

```bash
npx skills add open-circle/agent-skills
npx add-skill open-circle/agent-skills
```

Or copy individual skill folders into your project's `.skills/` directory.

## Usage

Once installed, AI agents will automatically discover and use these skills when relevant tasks are detected. Each skill contains:

- **SKILL.md** — Instructions and metadata for the agent
- **references/** — Additional documentation (optional)
- **scripts/** — Executable code (optional)
- **assets/** — Templates and resources (optional)

## Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## About Open Circle

[Open Circle](https://opencircle.dev) is a GitHub organization serving as a shared home for open-source projects that share a philosophy around modularity, type safety, and developer experience.

### Projects

- **[Valibot](https://valibot.dev)** — The modular and type safe schema library for validating structural data
- **[Formisch](https://formisch.dev/)** — The modular and type-safe form library for any framework

## License

This repository is licensed under the [MIT License](LICENSE.md).
