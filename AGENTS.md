# AGENTS.md

This file is a context map for AI agents (and humans) working in this repository. It points to where long-lived project context lives so you don't have to rediscover it by searching across modules.

Flowise is a pnpm + Turborepo monorepo for building AI agents visually. The workspace globs are defined in [`pnpm-workspace.yaml`](pnpm-workspace.yaml), and the build pipeline in [`turbo.json`](turbo.json).

## Where context lives

### Top-level docs

| File | What it covers |
| --- | --- |
| [`README.md`](README.md) | Project overview, quick start, Docker, developer setup, env variables pointer, deployment links. |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | Contribution workflow, step-by-step dev setup, credential definitions, testing, and the canonical [Env Variables](CONTRIBUTING.md#-env-variables) reference. |
| [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md) | Community standards. |
| [`SECURITY.md`](SECURITY.md) | Security policy and vulnerability reporting. |
| [`LICENSE.md`](LICENSE.md) | Apache License 2.0. |
| [`i18n/`](i18n/) | Translated READMEs (繁體中文, 简体中文, 日本語, 한국어). |

### Packages (`packages/*`)

| Package | npm name | Purpose | README |
| --- | --- | --- | --- |
| `server` | `flowise` | Node backend serving API logic. | [`packages/server/README.md`](packages/server/README.md) |
| `ui` | `flowise-ui` | React frontend. | [`packages/ui/README.md`](packages/ui/README.md) |
| `components` | `flowise-components` | Third-party node integrations. | [`packages/components/README.md`](packages/components/README.md) |
| `api-documentation` | `flowise-api` | Auto-generated swagger-ui API docs from express. | [`packages/api-documentation/README.md`](packages/api-documentation/README.md) |
| `agentflow` | `@flowiseai/agentflow` | Embeddable React component for building and visualizing AI agent workflows. | [`packages/agentflow/README.md`](packages/agentflow/README.md) |
| `observe` | `@flowiseai/observe` | Embeddable React components for observing AI agent executions, evaluations, and runtime activity. | [`packages/observe/README.md`](packages/observe/README.md) |

## Environment variables

Env vars are documented authoritatively in [`CONTRIBUTING.md`](CONTRIBUTING.md#-env-variables). Locations of `.env` files:

- **Server:** create `.env` in [`packages/server`](packages/server) (refer to its `.env.example`); set `PORT` and other backend variables.
- **UI (dev):** create `.env` in [`packages/ui`](packages/ui) (refer to its `.env.example`); set `VITE_PORT`.
- **Docker:** copy `.env.example` in [`docker/`](docker/) to `.env` before `docker compose up`.

## Common commands

Run from the repo root:

- `pnpm install` — install all module dependencies.
- `pnpm build` — build all packages.
- `pnpm dev` — development build with hot reload (app on http://localhost:8080).
- `pnpm start` — start the app (http://localhost:3000).

See [`README.md`](README.md#-developers) and [`CONTRIBUTING.md`](CONTRIBUTING.md#-developers) for the full developer setup.

## External documentation

Hosted docs live at <https://docs.flowiseai.com/>.
