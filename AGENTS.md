# Agent instructions

Guidance for AI-assisted development in this repository. All commands are non-interactive and intended to be copy-pasted from the repo root.

## Prerequisites

- Node.js `^20`
- pnpm `^10.26.0`

```bash
pnpm install
```

## Monorepo layout

pnpm workspace (`pnpm-workspace.yaml` → `packages/*`), orchestrated by Turbo.

| Path | Package name | Role |
| --- | --- | --- |
| `packages/server` | `flowise` | Node backend (API, CLI) |
| `packages/ui` | `flowise-ui` | React frontend |
| `packages/components` | `flowise-components` | Third-party node integrations |
| `packages/agentflow` | `@flowiseai/agentflow` | Embeddable agent-flow canvas |
| `packages/observe` | `@flowiseai/observe` | Embeddable observability UI |
| `packages/api-documentation` | `flowise-api` | Auto-generated Swagger docs |

Tests are co-located with source (`Foo.test.ts` next to `Foo.ts`). See [CONTRIBUTING.md](./CONTRIBUTING.md) for PR workflow, env vars, and credential security rules.

## Build

Full monorepo build (may require extra heap on large machines):

```bash
NODE_OPTIONS=--max-old-space-size=4096 pnpm build
```

Build a single package:

```bash
NODE_OPTIONS=--max-old-space-size=4096 pnpm --filter flowise build
NODE_OPTIONS=--max-old-space-size=4096 pnpm --filter flowise-ui build
NODE_OPTIONS=--max-old-space-size=4096 pnpm --filter flowise-components build
NODE_OPTIONS=--max-old-space-size=4096 pnpm --filter @flowiseai/agentflow build
NODE_OPTIONS=--max-old-space-size=4096 pnpm --filter @flowiseai/observe build
NODE_OPTIONS=--max-old-space-size=4096 pnpm --filter flowise-api build
```

Alternative path filter (useful when package names collide):

```bash
NODE_OPTIONS=--max-old-space-size=4096 pnpm --filter "./packages/server" build
```

Force clean rebuild:

```bash
pnpm build-force
```

Docker-oriented build (excludes agentflow and observe):

```bash
pnpm build:docker
```

## Lint

Lint entire repo:

```bash
pnpm lint
```

Auto-fix:

```bash
pnpm lint-fix
```

Lint a single package:

```bash
pnpm --filter flowise-components lint
pnpm --filter @flowiseai/agentflow lint
pnpm --filter @flowiseai/observe lint
pnpm --filter flowise-api lint
```

## Test

Run all package tests:

```bash
pnpm test
```

Run with coverage:

```bash
pnpm test:coverage
```

Run tests for one package:

```bash
pnpm --filter flowise-components test
pnpm --filter @flowiseai/agentflow test
pnpm --filter @flowiseai/observe test
pnpm --filter flowise-ui test
pnpm --filter "./packages/server" test
```

Coverage for one package:

```bash
pnpm --filter flowise-components test:coverage
pnpm --filter @flowiseai/agentflow test:coverage
pnpm --filter "./packages/server" test:coverage
```

## Dev and run

Development (hot reload on `http://localhost:8080`; copy `.env.example` → `.env` in `packages/ui` and `packages/server` first):

```bash
pnpm dev
```

Production start after build:

```bash
pnpm start
```

After changes under `packages/components`, rebuild before testing server/UI:

```bash
NODE_OPTIONS=--max-old-space-size=4096 pnpm --filter flowise-components build
```

## Safe conventions for agents

- Make minimal, targeted edits; do not remove unrelated code.
- Do not commit secrets (`.env`, API keys, credentials). Never change credential field types from `password`/`url` to `string` — see [CONTRIBUTING.md](./CONTRIBUTING.md#adding-or-modifying-credential-definitions).
- Prefer package-scoped commands (`pnpm --filter <name> …`) when working in one area to save time.
- Place new tests beside the source file they cover.
- Run lint and relevant tests before finishing work; use `NODE_OPTIONS=--max-old-space-size=4096` if builds fail with heap OOM (exit code 134).
