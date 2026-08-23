# Documentation project instructions

## About this project

- Documentation for **Tylon**, built on [Mintlify](https://mintlify.com)
- Pages are MDX files with YAML frontmatter; configuration lives in `docs.json`
- The site covers the two ways something reaches a board without a browser:
  the **public API** (`api-reference/`) and the **MCP server** (`mcp/`), plus
  the product vocabulary both of them lean on (`concepts/`)

## What Tylon is

Git's control panel. A board whose columns are real branches: moving a card
cuts a branch, opens a pull request, or merges one. It is not a project
management tool that happens to link to GitHub, and writing about it as one is
the mistake to avoid.

## Terminology

- **card**, not "issue" or "ticket"
- **board**, and its columns are **stages** of a **flow**
- **workspace** is a board's home; a workspace holds **projects**
- **credential** for the API's client id and secret — never "API key", which
  suggests one opaque string
- **connection** for what an editor holds over MCP
- **forge**, or the provider's name, for GitHub and GitLab — the checks and
  the reviews live there, not here

## Style preferences

- Use active voice and second person ("you")
- Keep sentences concise — one idea per sentence
- Use sentence case for headings
- Bold for UI elements: Click **Settings**
- Code formatting for file names, commands, paths, and code references

## Content boundaries

**Do not document behaviour that has not been checked against the code.**

This site began as a scaffold describing a product that did not exist: rate
limits by plan tier, HMAC webhook signatures, endpoints for Integrations,
Events and Users. All of it read as documentation and none of it was true.
Every number, endpoint, header and status code here should be traceable to
something in `tylonapp/tylon`.

That applies to example responses too. The `/v1/board` example was written
from memory and had the wrong shape — `{status: {...}}` instead of
`{statusId, name, kind, minRole, tasks}` — which broke exactly the two fields
a script needs before it can promote anything. Copy example bodies from a real
call.

Specifically, as of the last check:

- The public API is addressed **by id**. No slug or name appears in any
  request; the board is chosen with `X-Tylon-Workspace`.
- Writes need the `write` scope **and** an `Idempotency-Key`.
- Approving an agent's proposal and granting board access are deliberately
  absent from the API. If that changes, the reason it was refused should
  change first.

Do not document internal admin features or anything behind a feature flag.
