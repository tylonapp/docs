# Documentation project instructions

## About this project

- Documentation for **Tylon**, built on [Mintlify](https://mintlify.com)
- Pages are MDX files with YAML frontmatter; configuration lives in `docs.json`
- **Two languages, and the folder is the language.** English lives under
  `en/`, Brazilian Portuguese under `pt-br/`, and every page exists in both.
  A link inside a page stays inside its own language: `/en/screens/board` from
  an English page, `/pt-br/screens/board` from a Portuguese one. Adding a page
  means adding it in both and in both `navigation.languages` entries
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

## Writing the Portuguese

Brazilian Portuguese, and a translation of the English page rather than a
different page — same headings, same order, same claims.

Two habits, taken from the product's own `pt.ts`:

- **The words a developer actually says stay as they are.** *Branch*, *pull
  request*, *commit*, *deploy*, *merge*, *push*, *release*, *trunk*,
  *workspace*, *card*. "Ramificação" is a correct translation and nobody on a
  Brazilian team has said it out loud.
- **The product's own words for its own screens.** *Quadro* for the board,
  *Caixa de entrada* for the inbox, *Fluxo*, *Estágio*, *Papel*, *Segredo* for
  a credential's secret, *Membro* / *Mantenedor* / *Dono* / *Observador* for
  the roles. If a screenshot shows a word, the page uses that word.

Screenshots come in a Portuguese set of their own — `/images/pt-light/` and
`/images/pt-dark/`, taken with `DEMO_LOCALE=pt`. A Portuguese page never
points at `/images/light/`. What the demo *data* says — card titles, stage
names, page names — stays English, because that is what the seed writes and
what a Brazilian team writing its repository in English actually sees.

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
