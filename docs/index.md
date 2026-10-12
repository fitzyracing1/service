# .service file type

`.service` is a plain-text manifest (kind `service`, version 1, MIME `application/x-service`). A robot reads it before any remote API call so it can check local state first and decide offline whether to call the network.

The repo contains only the specification and a sample. It has no parser or code:

| File | Content |
|---|---|
| `service.kind` | full spec: structure, parse rules, write rules |
| `sample.service` | example with three entries (`status`, `inventory`, `command`) |
| `README.md` | overview and key table |

## Format summary (from `service.kind`)

- Line 1 must be `# service v1`. Optional YAML frontmatter (`api_base`, `timeout`, `robot_id`) can follow.
- Entries are separated by blank lines, and each starts with `SERVICE: <name>`.
- Allowed keys: `LOCAL`, `API`, `METHOD`, `CACHE`, `PRECHECK`, `FALLBACK`, `NOTES`.
- `PRECHECK` takes one of: `exists`, `missing`, `fresh:N` (seconds), `match:pattern`, `always`.
- `LOCAL` and `CACHE` must be relative paths. If a `SERVICE` name repeats, the last entry wins.
- The `FALLBACK` values used in the sample are `use_cache`, `call_api`, and `skip`. The spec does not list a closed set.

## Getting started

1. Copy `sample.service` into the robot's workspace.
2. Edit the `LOCAL` and `CACHE` paths.
3. Before an API call, find the `SERVICE` entry, evaluate `PRECHECK`, and follow `FALLBACK`.

Copyright (c) 2026 Joshua Almeida
