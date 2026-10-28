# pi-add-9router — standalone capability-discovery fork

Adapter-only fork of [arhen/pi-extensions](https://github.com/arhen/pi-extensions),
extracted from `packages/add/pi-add-9router` version **1.0.2** at fork snapshot
`267bbdbc142942f9741ffd21287b94d77a52bb1f`. Upstream release tag:
[`@arhen/pi-add-9router@1.0.2`](https://github.com/arhen/pi-extensions/tree/%40arhen%2Fpi-add-9router%401.0.2).
Original author attribution and [MIT license](LICENSE) are retained. This fork is
installed from git; it is not the published `@arhen/pi-add-9router` npm release.

## Install

Requires the [pi coding agent](https://github.com/earendil-works/pi) — install it first: `npm install -g @earendil-works/pi-coding-agent`.

```sh
# Remove the old adapter first: duplicate provider registrations are unsafe.
pi remove npm:@arhen/pi-add-9router@1.0.1
# Substitute the reviewed immutable 40-character commit from Shikumi's stack.json.
pi install git:github.com/giovannirandykusuma/pi-add-9router@<commit>
```

Pi Coding Agent extension for 9router — AI routing proxy (default `http://localhost:20128`).

Registers 9router as a Pi provider with dynamic model discovery. **Provider only, no web tools** — use [pi-web-access](https://github.com/nicobailon/pi-web-access) for web search/fetch.

## Features

- Auto-discovers models and combos from 9router `/v1/models` on startup
- Registers `9router` provider with dynamic base URL + API key
- Cached discovery (fast startup, credential-fingerprinted)
- models.dev metadata enrichment (context window, max tokens, input modalities)
- Per-model `capabilities.thinkingLevels` discovery at startup and `/9router-reload`
- Advertised Pi levels map to `reasoning_effort`; `max` is enabled only when advertised
- Explicit `reasoning:false` and the global reasoning-off toggle override advertised levels
- Older servers retain the legacy map through `xhigh`, never inferred `max`; malformed or empty level metadata fails closed
- This changes capability discovery, not visible reasoning-summary delivery
- Commands: `/9router-status`, `/9router-models`, `/9router-config`, `/9router-reasoning`, `/9router-reload`

## Environment

| Variable                       | Default                  | Description                          |
| ------------------------------ | ------------------------ | ------------------------------------ |
| `NINE_ROUTER_BASE_URL`         | `http://localhost:20128` | 9router endpoint                     |
| `NINE_ROUTER_API_KEY`          | —                        | API key if 9router requires auth     |
| `NINE_ROUTER_ENABLE_REASONING` | —                        | `1`/`true` to expose thinking levels |

Config persists to `~/.pi/agent/9router-config.json` (or `$PI_CODING_AGENT_DIR/9router-config.json`), shared across Pi instances.

## Commands

| Command              | Purpose                                |
| -------------------- | -------------------------------------- |
| `/9router-config`    | Configure base URL, API key, reasoning |
| `/9router-status`    | Connection status, model counts        |
| `/9router-models`    | Browse models/combos and switch        |
| `/9router-reasoning` | Toggle thinking levels                 |
| `/9router-reload`    | Re-discover models                     |

## Why not pi-9router-ext?

[pi-9router-ext](https://github.com/irfansofyana/pi-9router-ext) bundles the same provider **plus** web tools (`ninerouter_web_search`, `ninerouter_web_fetch`) and web-route discovery (~1.2K tokens extra in context). This package is the provider flow only — same config file format, same env vars, so they're drop-in interchangeable.

## License

MIT
