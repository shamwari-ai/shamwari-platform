# Shamwari Platform

> The customer console — API key issuance, revocation, usage and billing. Astro SSR on Cloudflare Workers.

[![CI](https://github.com/shamwari-ai/shamwari-platform/actions/workflows/ci.yml/badge.svg)](https://github.com/shamwari-ai/shamwari-platform/actions/workflows/ci.yml)
[![Lint](https://github.com/shamwari-ai/shamwari-platform/actions/workflows/lint.yml/badge.svg)](https://github.com/shamwari-ai/shamwari-platform/actions/workflows/lint.yml)
[![License: Apache 2.0](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://www.apache.org/licenses/LICENSE-2.0)
![Astro](https://img.shields.io/badge/Astro-BC52EE?style=flat-square&logo=astro&logoColor=white)

**Status:** not started | **Planned address:** `platform.shamwari.ai` | **API it will consume:** [`shamwari-core`](https://github.com/shamwari-ai/shamwari-core)

---

## What it is

Nothing is implemented here yet. This repo was scaffolded fresh rather than
extracted from the monorepo — unlike
[`shamwari-gateway`](https://github.com/shamwari-ai/shamwari-gateway),
[`shamwari-web`](https://github.com/shamwari-ai/shamwari-web) and
[`shamwari-core`](https://github.com/shamwari-ai/shamwari-core), there is no
existing code to lift out.

When it exists, it is the console a Shamwari Cloud customer logs into: issue an
API key, revoke one, see what it has cost.

## `platform.shamwari.ai` already answers, and it is not this

The name resolves, and a request to it returns `200` — but from **Vercel**,
serving a Next.js app, not from Cloudflare Workers and not from this repo. It
is the same stale pre-pivot Vercel project described in
[`shamwari-web`](https://github.com/shamwari-ai/shamwari-web)'s README.

Do not read that `200` as the console being live, and do not point this repo
at that project. Retiring it is part of the work, not a detail to discover
during the first deploy.

## Blocked on three Core endpoints

The console needs three endpoints that `shamwari-core` does not serve yet:

| Endpoint                | Status      |
| ----------------------- | ----------- |
| Key issuance            | **missing** |
| Key revocation          | **missing** |
| Per-key usage breakdown | **missing** |

`POST /auth/verify`, `GET /rollup` and `GET /guardrails` already exist and
cover the rest. Per `docs/repo-split.md`, these three should be added to Core
_before_ work here starts, not discovered mid-build.

## Scope

It shows `platform`-scope data about a customer's own account — never
`personal`-scope pod data. That places it outside rule 1 entirely, which makes
it the most straightforward of the planned repos to build correctly.

Rust is not warranted here: a console rendering tables of someone else's
aggregates has no CPU-bound work. Rust is kept for
[`shamwari-sandbox`](https://github.com/shamwari-ai/shamwari-sandbox), where
it earns its place.

## Conventions

- **Astro, not Hono.** Hono is the gateway's routing library for an API with
  no pages; Astro owns page routing and layout here. They are not
  interchangeable — see "What not to do" in `docs/repo-split.md`.
- **SSR, unlike the apex site.** `shamwari.ai` is Astro static output with no
  bindings and no secrets. A console cannot be, so this repo is the one Astro
  surface that will hold a deployable server runtime.
- `licenseClass` is a cross-cutting invariant. The canonical statement of what
  its values mean lives in the umbrella repo's `CLAUDE.md` — link to it, don't
  restate it here.

## Ecosystem

- [`shamwari`](https://github.com/shamwari-ai/shamwari) — the umbrella:
  architecture, the applied-migration log, repo index
- [`shamwari-core`](https://github.com/shamwari-ai/shamwari-core) — the API
  this console will consume
- [`docs`](https://github.com/shamwari-ai/docs) — public documentation at
  [docs.shamwari.ai](https://docs.shamwari.ai)
- [Org standards](https://github.com/shamwari-ai/.github/blob/main/ORG_STANDARDS.md)

## Contributing

See the org's
[CONTRIBUTING.md](https://github.com/shamwari-ai/.github/blob/main/CONTRIBUTING.md),
[SECURITY.md](https://github.com/shamwari-ai/.github/blob/main/SECURITY.md) and
[CODE_OF_CONDUCT.md](https://github.com/shamwari-ai/.github/blob/main/CODE_OF_CONDUCT.md).

## Licence

Licensed under the [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0)
— see `LICENSE` and `NOTICE`.

© Bundu Foundation. Shamwari is Bundu Foundation IP, sold commercially under
Nyuchi Africa.
