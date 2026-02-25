````skill
---
name: formisch
description: Form handling with Formisch, the type-safe form library for modern frameworks. Use when the user needs to create forms, handle form state, validate form inputs, or work with Formisch.
license: MIT
metadata:
  author: open-circle
  version: "1.1"
---

# Formisch

This skill helps AI agents work effectively with [Formisch](https://formisch.dev/), the schema-based, headless form library for modern frameworks.

## When to Use This Skill

- When the user asks about form handling with Formisch
- When managing form state and validation
- When working with React, Vue, Solid, Preact, Svelte, or Qwik forms
- When integrating Valibot schemas with forms

## Introduction

Formisch is a schema-based, headless form library that works across multiple frameworks. Key highlights:

- **Small bundle size** — Starting at ~2.5 kB
- **Schema-based validation** — Uses Valibot for type-safe validation
- **Headless design** — You control the UI completely
- **Type safety** — Full TypeScript support with autocompletion
- **Framework-native** — Native performance for each supported framework

### Supported Frameworks

| Framework | Package            | Hook/Primitive |
| --------- | ------------------ | -------------- |
| React     | `@formisch/react`  | `useForm`      |
| Vue       | `@formisch/vue`    | `useForm`      |
| SolidJS   | `@formisch/solid`  | `createForm`   |
| Preact    | `@formisch/preact` | `useForm`      |
| Svelte    | `@formisch/svelte` | `createForm`   |
| Qwik      | `@formisch/qwik`   | `useForm$`     |

## Installation

### 1. Install Valibot (peer dependency)

```bash
npm install valibot
```

### 2. Install Formisch for your framework

```bash
npm install @formisch/react   # React
npm install @formisch/vue     # Vue
npm install @formisch/solid   # SolidJS
npm install @formisch/preact  # Preact
npm install @formisch/svelte  # Svelte
npm install @formisch/qwik    # Qwik
```

## Core Concepts

### Schema-First Design

Every form starts with a Valibot schema. Types are automatically inferred from the schema.

```ts
import * as v from "valibot";

const LoginSchema = v.object({
  email: v.pipe(
    v.string("Please enter your email."),
    v.nonEmpty("Please enter your email."),
    v.email("The email address is badly formatted."),
  ),
  password: v.pipe(
    v.string("Please enter your password."),
    v.nonEmpty("Please enter your password."),
    v.minLength(8, "Your password must have 8 characters or more."),
  ),
});
```

### Form Store

The form store manages all form state. Access it via the framework-specific hook/primitive.

**Form Store Properties:**

- `isSubmitting` — Form is currently being submitted
- `isSubmitted` — Form has been successfully submitted
- `isValidating` — Validation is in progress
- `isTouched` — At least one field has been touched
- `isDirty` — At least one field differs from initial value
- `isValid` — All fields pass validation
- `errors` — Root-level validation errors

### Field Store

Each field has its own reactive store with:

- `path` — Path array to the field
- `input` — Current field value
- `errors` — Field-specific errors
- `isTouched` — Field has been focused and blurred
- `isDirty` — Field value differs from initial value
- `isValid` — Field passes validation
- `props` — Props to spread onto input elements
- `onChange` (React) / `onInput` (other frameworks) — Sets the field input value programmatically. Use this when the field cannot be connected to a native HTML element.

### Dirty Tracking

Formisch tracks two inputs per field:

- **Initial input** — Baseline for dirty tracking (server state)
- **Current input** — What the user is editing (client state)

`isDirty` becomes `true` when current input differs from initial input.

## Framework Examples

### React Example

```tsx
import { Field, Form, useForm } from "@formisch/react";
import type { SubmitHandler } from "@formisch/react";
import * as v from "valibot";

const LoginSchema = v.object({
  email: v.pipe(v.string(), v.email()),
  password: v.pipe(v.string(), v.minLength(8)),
});

export default function LoginPage() {
  const loginForm = useForm({
    schema: LoginSchema,
  });

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
      <button type="submit" disabled={loginForm.isSubmitting}>
        {loginForm.isSubmitting ? "Submitting..." : "Login"}
      </button>
    </Form>
  );
}
```

### Vue Example

```vue
<script setup lang="ts">
import { Field, Form, useForm } from "@formisch/vue";
import type { SubmitHandler } from "@formisch/vue";
import * as v from "valibot";

const LoginSchema = v.object({
  email: v.pipe(v.string(), v.email()),
  password: v.pipe(v.string(), v.minLength(8)),
});

const loginForm = useForm({
  schema: LoginSchema,
});

const handleSubmit: SubmitHandler<typeof LoginSchema> = (output) => {
  console.log(output);
};
</script>

<template>
  <Form :of="loginForm" @submit="handleSubmit">
    <Field :of="loginForm" :path="['email']" v-slot="field">
      <div>
        <input v-bind="field.props" v-model="field.input" type="email" />
        <div v-if="field.errors">{{ field.errors[0] }}</div>
      </div>
    </Field>
    <Field :of="loginForm" :path="['password']" v-slot="field">
      <div>
        <input v-bind="field.props" v-model="field.input" type="password" />
        <div v-if="field.errors">{{ field.errors[0] }}</div>
      </div>
    </Field>
    <button type="submit">Login</button>
  </Form>
</template>
```

### SolidJS Example

```tsx
import { Field, Form, createForm } from "@formisch/solid";
import type { SubmitHandler } from "@formisch/solid";
import * as v from "valibot";

const LoginSchema = v.object({
  email: v.pipe(v.string(), v.email()),
  password: v.pipe(v.string(), v.minLength(8)),
});

export default function LoginPage() {
  const loginForm = createForm({
    schema: LoginSchema,
  });

  const handleSubmit: SubmitHandler<typeof LoginSchema> = (output) => {
    console.log(output);
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

### Svelte Example

```svelte
<script lang="ts">
  import { createForm, Field, Form } from '@formisch/svelte';
  import type { SubmitHandler } from '@formisch/svelte';
  import * as v from 'valibot';

  const LoginSchema = v.object({
    email: v.pipe(v.string(), v.email()),
    password: v.pipe(v.string(), v.minLength(8)),
  });

  const loginForm = createForm({
    schema: LoginSchema,
  });

  const handleSubmit: SubmitHandler<typeof LoginSchema> = (output) => {
    console.log(output);
  };
</script>

<Form of={loginForm} onsubmit={handleSubmit}>
  <Field of={loginForm} path={['email']}>
    {#snippet children(field)}
      <div>
        <input {...field.props} value={field.input} type="email" />
        {#if field.errors}
          <div>{field.errors[0]}</div>
        {/if}
      </div>
    {/snippet}
  </Field>
  <Field of={loginForm} path={['password']}>
    {#snippet children(field)}
      <div>
        <input {...field.props} value={field.input} type="password" />
        {#if field.errors}
          <div>{field.errors[0]}</div>
        {/if}
      </div>
    {/snippet}
  </Field>
  <button type="submit">Login</button>
</Form>
```

### Qwik Example

```tsx
import { Field, Form, useForm$ } from "@formisch/qwik";
import { component$ } from "@qwik.dev/core";
import * as v from "valibot";

const LoginSchema = v.object({
  email: v.pipe(v.string(), v.email()),
  password: v.pipe(v.string(), v.minLength(8)),
});

export default component$(() => {
  const loginForm = useForm$({
    schema: LoginSchema,
  });

  return (
    <Form of={loginForm} onSubmit$={(output) => console.log(output)}>
      <Field
        of={loginForm}
        path={["email"]}
        render$={(field) => (
          <div>
            <input {...field.props} value={field.input.value} type="email" />
            {field.errors.value && <div>{field.errors.value[0]}</div>}
          </div>
        )}
      />
      <Field
        of={loginForm}
        path={["password"]}
        render$={(field) => (
          <div>
            <input {...field.props} value={field.input.value} type="password" />
            {field.errors.value && <div>{field.errors.value[0]}</div>}
          </div>
        )}
      />
      <button type="submit">Login</button>
    </Form>
  );
});
```

## Form Configuration

```ts
const form = useForm({
  // Required: Valibot schema
  schema: MySchema,

  // Optional: Initial values (partial allowed)
  initialInput: {
    email: "user@example.com",
  },

  // Optional: When first validation occurs
  // Options: 'initial' | 'blur' | 'input' | 'submit' (default)
  validate: "submit",

  // Optional: When revalidation occurs after first validation
  // Options: 'blur' | 'input' (default) | 'submit'
  revalidate: "input",
});
```

## Field Paths

Paths are type-safe arrays that reference fields in your schema.

```tsx
// Top-level field
<Field of={form} path={['email']} />

// Nested field (schema: { user: { email: string } })
<Field of={form} path={['user', 'email']} />

// Array item field (schema: { todos: [{ label: string }] })
<Field of={form} path={['todos', 0, 'label']} />

// Dynamic array index
{items.map((item, index) => (
  <Field of={form} path={['todos', index, 'label']} key={item} />
))}
```

## Form Methods

All methods follow a consistent API pattern:

- **First parameter**: Form store
- **Second parameter**: Config object

### Reading Values

```ts
import { getInput, getErrors, getAllErrors } from "@formisch/react";

````
