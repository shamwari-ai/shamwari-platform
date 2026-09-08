# shamwari-platform

The customer console at **platform.shamwari.ai** — API keys, usage and billing.

Astro (SSR) on Cloudflare Workers.

## Status

Not started. This repo is scaffolded fresh rather than extracted from the
monorepo — unlike `shamwari-gateway`, `shamwari-web` and `shamwari-core`,
there is no existing code to lift out.

## Blocked on three Core endpoints

The console needs three endpoints that `shamwari-core` does not serve yet:

| Endpoint | Status |
|---|---|
| Key issuance | **missing** |
| Key revocation | **missing** |
| Per-key usage breakdown | **missing** |

`GET /rollup` and `POST /auth/verify` already exist and cover the rest.
Per the split plan, these three should be added to Core *before* work here
starts, not discovered mid-build.

## Scope

Shows `platform`-scope data about a customer's own account — never
`personal`-scope pod data. That places it outside rule 1 entirely, which
makes it the most straightforward of the active repos to build correctly.

Rust is not warranted here: a console rendering someone else's aggregates
has no CPU-bound work.

## Conventions

- **Astro, not Hono.** Hono is the gateway's routing library for an API with
  no pages; Astro owns page routing and layout here. They are not
  interchangeable — see the split plan's "What not to do".
- `licenseClass` is a cross-cutting invariant. The canonical statement of
  what its values mean lives in the umbrella repo — link to it, don't
  restate it here.

## Related

- [`shamwari`](https://github.com/shamwari-ai/shamwari) — umbrella: architecture, the applied-migration log, repo index
- [`shamwari-core`](https://github.com/shamwari-ai/shamwari-core) — the API this console consumes
- [`docs`](https://github.com/shamwari-ai/docs) — public documentation
