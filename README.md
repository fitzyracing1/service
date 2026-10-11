# .service file type

## What it is

A plain-text `.service` file lets a robot keep a local, offline-readable manifest of services it may need. Before any remote API call the robot opens the matching `.service` file, evaluates the PRECHECK against the local filesystem, and only then decides whether to call the network.

## Why it helps

- Organizes local checks, cache paths, and fallback rules in one place
- Robots can decide without network access
- Simple text format — easy to generate, edit, or version on a phone or embedded controller
- Clear separation between local state and remote endpoint

## Keys used

| Key      | Meaning                                      |
|----------|----------------------------------------------|
| SERVICE  | Short name of this service entry             |
| LOCAL    | Path to the local file or status the robot should examine |
| API      | Relative or absolute endpoint to call if needed |
| METHOD   | HTTP method (GET, POST, …)                   |
| CACHE    | Where to write the response if the call succeeds |
| PRECHECK | Condition that must be true to skip or proceed (`exists`, `fresh:N`, `match:pattern`, `always`) |
| FALLBACK | What to do if PRECHECK fails (`use_cache`, `call_api`, `skip`) |
| NOTES    | Human-readable reminder                      |

## Quick start

1. Copy `sample.service` into the robot’s workspace.
2. Edit LOCAL and CACHE paths to match the robot’s local storage.
3. Before an API call, the robot reads the file, finds the SERVICE entry, evaluates PRECHECK, and follows FALLBACK.

## Declaration

See `service.kind` for the full kind specification (structure, parse rules, write rules).
