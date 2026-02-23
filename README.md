# Open Circle Agent Skills

Teach AI agents how to use [Valibot](https://valibot.dev) and [Formisch](https://formisch.dev/).

## Contents

- [What are Agent Skills?](#what-are-agent-skills)
- [What These Skills Do](#what-these-skills-do)
- [When to Use These](#when-to-use-these)
- [Examples](#examples)
- [Skills Included](#skills-included)
- [Installation](#installation)
- [Usage](#usage)
- [Skill Structure](#skill-structure)
- [Contributing](#contributing)
- [About Open Circle](#about-open-circle)
- [License](#license)

## What are Agent Skills?

Agent Skills are a lightweight, open format for extending AI agent capabilities with specialized knowledge and workflows. Each skill is a folder containing a `SKILL.md` file with metadata and instructions that help AI agents understand how to use specific tools and libraries.

Learn more at [agentskills.io](https://agentskills.io)

## What These Skills Do

These skills teach agents the correct patterns and best practices for using Valibot and Formisch.

## When to Use These

Use these skills if your agent system needs to:

- Generate, validate, or reason about structured data with Valibot 
- Handle multi-step or stateful form workflows with Formisch 

## Examples

### Valibot Schema

```typescript
import * as v from "valibot";

const UserSchema = v.object({
  name: v.pipe(v.string(), v.nonEmpty("Please enter your name.")),
  email: v.pipe(
    v.string(),
    v.nonEmpty("Please enter your email."),
    v.email("The email address is badly formatted."),
  ),
  age: v.pipe(v.number(), v.minValue(13, "You must be at least 13 years old.")),
});

const result = v.safeParse(UserSchema, data);
if (result.success) {
  console.log(result.output); // { name: string, email: string, age: number }
} else {
  console.log(result.issues);
}
```

### Formisch Form (React)

```tsx
import { Field, Form, useForm } from "@formisch/react";
import type { SubmitHandler } from "@formisch/react";
import * as v from "valibot";

const LoginSchema = v.object({
  email: v.pipe(v.string(), v.email()),
  password: v.pipe(v.string(), v.minLength(8)),
});

export default function LoginPage() {
  const loginForm = useForm({ schema: LoginSchema });

  const handleSubmit: SubmitHandler<typeof LoginSchema> = (output) => {
    console.log(output); // { email: string, password: string }
  };

  return (
    <Form of={loginForm} onSubmit={handleSubmit}>
      <Field of={loginForm} path={["email"]}>
        {(field) => (
          <div>
            <input {...field.props} value={field.input} type="email" />
            {field.errors && <div>{field.errors[0]}</div>}
          </div>
        )}
      </Field>
      <Field of={loginForm} path={["password"]}>
        {(field) => (
          <div>
            <input {...field.props} value={field.input} type="password" />
            {field.errors && <div>{field.errors[0]}</div>}
          </div>
        )}
      </Field>
      <button type="submit">Login</button>
    </Form>
  );
}
```

## Skills Included

| Skill                                    | Purpose                          | When to use                                              |
| ---------------------------------------- | -------------------------------- | -------------------------------------------------------- |
| [valibot-usage](skills/valibot-usage/)   | Schema definition and validation | Validating data structures, API responses, or user input |
| [formisch-usage](skills/formisch-usage/) | Form state handling              | Managing multi-step forms or structured data collection  |

## Installation

> **Compatible with agents that support Agent Skills**

Install the skills using the CLI:

```bash
npx skills add open-circle/agent-skills
npx add-skill open-circle/agent-skills
```

Or copy individual skill folders into your project's `.skills/` directory.

## Usage

Activation behavior varies by agent. Check if your agent supports Agent Skills and refer to its documentation.


## Skill Structure

Each skill folder contains:

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
