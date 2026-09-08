# Comunicate.top — MCP server & public API

Remote **MCP server** and **HTTP API** for [Comunicate.top](https://comunicate.top), a
Romanian platform for publishing press releases, advertorials and SEO articles on a
network of **3,800+ online publications** (Romania, Italy and other European markets).

Prices and turnaround times are printed in the catalogue and are the same for everyone —
there is no request-for-quote and no negotiation, so an assistant can read a price and
act on it.

| | |
|---|---|
| MCP endpoint | `https://app.comunicate.top/mcp` (Streamable HTTP) |
| Auth | OAuth 2.1 + PKCE, dynamic client registration — or an API key |
| OpenAPI 3.1 | <https://comunicate.top/openapi.json> |
| APIs.json | <https://comunicate.top/apis.json> |
| Docs | <https://comunicate.top/en/documentatie-api> |
| Free, no key | `https://app.comunicate.top/api/v1/public/*` |

---

## Connect the MCP server

The server speaks Streamable HTTP and authenticates with OAuth 2.1 (PKCE, S256).
Clients register themselves — there is nothing to copy and paste, you just approve the
connection in a browser window.

**Claude Code**

```bash
claude mcp add --transport http comunicate-top https://app.comunicate.top/mcp
```

**Claude Desktop, Cursor, VS Code and anything else that reads `mcpServers`**

```json
{
  "mcpServers": {
    "comunicate-top": {
      "type": "http",
      "url": "https://app.comunicate.top/mcp"
    }
  }
}
```

**With an API key instead of OAuth** (for CI, or a client without OAuth support): issue a
key under *Integrations* in your account and send it as a bearer token.

```json
{
  "mcpServers": {
    "comunicate-top": {
      "type": "http",
      "url": "https://app.comunicate.top/mcp",
      "headers": { "Authorization": "Bearer bk_live_…" }
    }
  }
}
```

OAuth discovery follows RFC 9728: an unauthenticated request returns `401` with
`WWW-Authenticate: Bearer resource_metadata="https://app.comunicate.top/.well-known/oauth-protected-resource/mcp"`.

### Tools

Twenty tools, in the order you would normally call them.

| Tool | What it does |
|---|---|
| `whoami` | The organisation behind the key, its permissions, and whether assistants are allowed to order and publish. Call it first. |
| `get_balance` | Credits per package and the cash balance. |
| `search_catalog` | Search the network: niche, language, authority, price, turnaround. |
| `get_site` | One publication in full: price per campaign type, rules, turnaround. |
| `list_campaign_types` | What each campaign type means and what the text must or must not contain. |
| `list_articles` / `get_article` | The organisation's drafts and published articles. |
| `create_article` / `update_article` | Write and revise a draft. |
| `check_article_seo` | What the article still needs to pass publication checks. |
| `check_article_fit` | Whether the text meets a campaign type's requirements. |
| `list_campaigns` / `create_campaign` / `update_campaign` | Editorial plans: goal, budget, allowed sites. |
| `list_publications` / `get_publication` | Status and live URL of each publication. |
| `order_publication` | Orders a publication. **Spends credits or money.** |
| `order_writing` | Orders an article to be written. **Spends credits or money.** |
| `list_writing_orders` | Status of writing orders and delivered articles. |
| `report_summary` | Publications, successes, failures, distinct sites, spend over a period. |

Ordering is gated twice: the organisation has a switch for whether AI assistants may
spend at all, and every order is checked against the balance before anything is written.

---

## Free public API — no key, no account

Four read-only routes, open to anyone, CORS enabled. They are described in the same
OpenAPI document as the rest of the API, with `security: []`.

```bash
# How big the network is
curl 'https://app.comunicate.top/api/v1/public/stats'
# → {"publications":3822,"niches":21}

# The niches, with publication counts and average authority
curl 'https://app.comunicate.top/api/v1/public/niches?locale=en'

# One niche, with sample publications: domain, DA, PA, turnaround, price, ad label
curl 'https://app.comunicate.top/api/v1/public/niches/stiri?locale=en'

# Market statistics: authority distribution, turnaround, price per campaign type
curl 'https://app.comunicate.top/api/v1/public/statistici-piata'
```

There is deliberately **no public route that returns the whole publication list**, and no
public route writes anything. Everything else — catalogue with prices, articles, orders,
publications, campaigns, reports, webhooks — needs a key issued from an account.

---

## Despre, pe scurt (RO)

Comunicate.top publică advertoriale, comunicate de presă și articole SEO pe o rețea de
peste 3.800 de publicații. Prețul și termenul fiecărei publicații sunt scrise în catalog,
publice și identice pentru toți. Serverul MCP de mai sus le dă asistenților AI acces la
catalog, la articole și la comenzi, cu OAuth și cu un comutator prin care organizația
decide dacă asistenții au voie să cheltuiască. Rutele `/public/*` sunt gratuite, fără
cheie și numai de citire.

Documentație: <https://comunicate.top/ro/documentatie-api> ·
Ce poate face serverul MCP: <https://comunicate.top/ro/mcp>

---

## This repository

Documentation and the registry manifest only — the platform itself is closed source.
`server.json` is what is published to the [official MCP registry](https://registry.modelcontextprotocol.io)
under the `top.comunicate` namespace, verified by the key at
<https://comunicate.top/.well-known/mcp-registry-auth>.

Questions or bug reports about the API: [open an issue](https://github.com/adrianncraciun-cmd/public-mcp/issues) or write to
contact@comunicate.top.

## Licence

The contents of this repository (documentation and manifest) are released under the MIT
licence. Use of the API and the MCP server is governed by the
[terms of service](https://comunicate.top/ro/legal/termeni).
