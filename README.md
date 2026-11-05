# Comunicate.eu — MCP server & public API

[Citește în română](README.ro.md)

Remote **MCP server** and **HTTP API** for [Comunicate.eu](https://comunicate.eu), a Romanian platform for publishing press releases, advertorials and SEO articles on a catalogue of **3,800+ online publications**, in Romania, Italy and other European markets.

Prices are printed in the catalogue and are the same for everyone. There is no request for a quote and no negotiation, so an assistant can read a price and act on it.

| | |
|---|---|
| MCP endpoint | `https://app.comunicate.eu/mcp` (Streamable HTTP) |
| Without an account | Catalogue search, budget plans, niches, campaign types |
| With an account | API key, or OAuth 2.1 with PKCE for approved assistants |
| OpenAPI 3.1 | <https://comunicate.eu/openapi.json> |
| APIs.json | <https://comunicate.eu/apis.json> |
| API docs | <https://comunicate.eu/en/documentatie-api> |
| MCP guide | <https://comunicate.eu/en/mcp> |
| Public API, no key | `https://app.comunicate.eu/api/v1/public/*` |

---

## What you can ask

These work with no account:

1. How much does an advertorial cost on a Romanian news site?
2. I run a travel site and have 500 lei. Where can I publish 5 articles with dofollow backlinks?
3. I run a dental clinic in Cluj and have a budget of 2,000 lei. Which sites do you recommend?
4. I run an online furniture shop. How do I run a backlink campaign with 1,000 lei?
5. Where can I publish a press release online, and what must it contain to be accepted?
6. Which travel sites accept advertorials, and which are the cheapest?
7. How can an NGO publish free press releases in the online press?

---

## Connect

No key and no sign-in are needed to connect or to read the catalogue.

**Server address:** `https://app.comunicate.eu/mcp`

Menus and plan limits change often, so check your assistant's help pages if a step looks different.

### Claude

On claude.ai or in the desktop app, open **Settings → Connectors → Add custom connector**, name it `Comunicate.eu` and paste the server address. On Team and Enterprise plans, an owner adds it for the organisation first.

### ChatGPT

Open **Settings → Apps & Connectors → Advanced** and turn on **Developer mode**, then create a connector with the server address. Choose **No authentication** to read the catalogue, or **OAuth** to work in your account. Availability depends on your plan, and on Business or Enterprise an admin may have to enable it.

### Perplexity

On a paid plan, open **Settings → Connectors**, add a custom connector with the server address and the Streamable HTTP transport, and choose no authentication to read the catalogue, or OAuth to work in your account.

### Gemini

Use [Gemini CLI](https://github.com/google-gemini/gemini-cli):

```bash
gemini extensions install https://github.com/adrianncraciun-cmd/public-mcp
```

Or add the server yourself:

```bash
gemini mcp add --transport http comunicate-eu https://app.comunicate.eu/mcp
```

You can also add this to `~/.gemini/settings.json`:

```json
{
  "mcpServers": {
    "comunicate-eu": {
      "httpUrl": "https://app.comunicate.eu/mcp"
    }
  }
}
```

### Claude Code

```bash
claude mcp add --transport http comunicate-eu https://app.comunicate.eu/mcp
```

Or install it as a plugin from this repository:

```
/plugin marketplace add adrianncraciun-cmd/public-mcp
/plugin install comunicate-eu@comunicate-eu
```

### Codex

```bash
codex mcp add comunicate-eu --url https://app.comunicate.eu/mcp
codex mcp login comunicate-eu
```

The second command signs you in with OAuth, for the account tools. Skip it if you only need the catalogue.

### Cursor

Add to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "comunicate-eu": {
      "type": "http",
      "url": "https://app.comunicate.eu/mcp"
    }
  }
}
```

### VS Code

Run **MCP: Add Server** from the Command Palette and paste the server address, or add it for all projects to `~/.copilot/mcp-config.json`:

```json
{
  "mcpServers": {
    "comunicate-eu": {
      "type": "http",
      "url": "https://app.comunicate.eu/mcp"
    }
  }
}
```

For a single project, `.vscode/mcp.json` uses `servers` instead:

```json
{
  "servers": {
    "comunicate-eu": {
      "type": "http",
      "url": "https://app.comunicate.eu/mcp"
    }
  }
}
```

### Windsurf

Add to `~/.codeium/windsurf/mcp_config.json`:

```json
{
  "mcpServers": {
    "comunicate-eu": {
      "serverUrl": "https://app.comunicate.eu/mcp"
    }
  }
}
```

### Devin Desktop, Devin CLI

Add to `~/.config/devin/mcp_config.json`:

```json
{
  "mcpServers": {
    "comunicate-eu": {
      "url": "https://app.comunicate.eu/mcp",
      "transport": "http"
    }
  }
}
```

### Zed

Add to Zed's `settings.json`:

```json
{
  "context_servers": {
    "comunicate-eu": {
      "url": "https://app.comunicate.eu/mcp"
    }
  }
}
```

### Anything else that reads `mcpServers`

```json
{
  "mcpServers": {
    "comunicate-eu": {
      "type": "http",
      "url": "https://app.comunicate.eu/mcp"
    }
  }
}
```

### With an account

Issue an API key under *Integrations* and send it as a bearer token. The key ties the server to your organisation, so it can see the balance, write drafts and, if you allow it, place orders.

```json
{
  "mcpServers": {
    "comunicate-eu": {
      "type": "http",
      "url": "https://app.comunicate.eu/mcp",
      "headers": { "Authorization": "Bearer bk_live_…" }
    }
  }
}
```

### OAuth

Claude, ChatGPT, Perplexity, VS Code, Cursor (desktop and web), Mistral Le Chat and Vibe, Raycast, Microsoft Copilot Studio, Coda, Zapier, Make and Glama can connect with OAuth 2.1 (PKCE S256) and approve the connection in the browser. Clients that run on your own machine, such as Claude Code, Codex, Gemini CLI, Zed, Goose and Cline, sign in the same way through a local address. Authorization codes go only to these approved clients. Any other client uses an API key.

An account tool called without credentials returns `401` with:

```
WWW-Authenticate: Bearer resource_metadata="https://app.comunicate.eu/.well-known/oauth-protected-resource/mcp"
```

---

## Where to find it

- [Official MCP registry](https://registry.modelcontextprotocol.io/v0.1/servers?search=eu.comunicate): `eu.comunicate/publishing`
- [Glama](https://glama.ai/mcp/connectors/eu.comunicate/publishing)
- [cursor.directory](https://cursor.directory/plugins/comunicatetop)
- [mcptry](https://mcptry.com/servers/eu.comunicate/publishing)
- Claude Code plugin and Gemini CLI extension: this repository

---

## Tools

Twenty-seven tools.

**No account needed**

| Tool | What it does |
|---|---|
| `how_it_works` | How publishing works, subscriptions, payment, and the free programme for NGOs and institutions. |
| `plan_budget` | Packages for a budget, by niche, topic and city, with totals with and without VAT. Call it again with `exclude` for other options. |
| `search_catalog` | Search the catalogue by text, niche, campaign type, authority and price. |
| `get_site` | One publication: price and links per campaign type, rules and conditions. |
| `catalog_stats` | How many publications and niches the catalogue has. |
| `list_niches` / `get_niche` | The niches, with descriptions and examples. |
| `list_campaign_types` | What each campaign type means and what the text must or must not contain. |
| `list_own_network` / `get_own_publication` | The Comunicate.eu network, on explicit request. |

**Account needed**

| Tool | What it does |
|---|---|
| `whoami` | The organisation behind the key and what it may do. |
| `get_balance` | Credits per package and the cash balance. |
| `list_articles` / `get_article` | The organisation's drafts and published articles. |
| `create_article` / `update_article` | Write and revise a draft. |
| `check_article_seo` | How well the text is written as an SEO article. |
| `check_article_fit` | Whether the text meets a campaign type's requirements and has no blanks left. |
| `list_campaigns` / `create_campaign` / `update_campaign` | Editorial plans: goal, budget, allowed sites. |
| `list_publications` / `get_publication` | Status and live URL of each publication. |
| `order_publication` | Orders a publication. **Spends credits or money.** |
| `order_writing` | Orders an article to be written. **Spends money.** |
| `list_writing_orders` | Status of writing orders and delivered articles. |
| `report_summary` | Publications, sites and spend over a period. |

Ordering is off by default. The organisation has a switch for whether AI assistants may spend, and it applies to OAuth tokens on the API as well. Every order is also checked against the balance.

---

## Public API

Read-only routes, open to anyone, with rate limits. They are described in the same OpenAPI document as the rest of the API, with `security: []`.

```bash
# Catalogue size
curl 'https://app.comunicate.eu/api/v1/public/stats'
# → {"publications":3809,"niches":22}

# Niches, with publication counts and average authority
curl 'https://app.comunicate.eu/api/v1/public/niches?locale=en'

# Catalogue search: at most 20 per page and the first 120 per search
curl 'https://app.comunicate.eu/api/v1/public/catalog?niche=sanatate&campaign=PRESS_RELEASE&sort=PRICE_ASC&limit=5'

# Budget plan: packages for 1,000 lei in a niche and a city
curl 'https://app.comunicate.eu/api/v1/public/plan?bugetLei=1000&nise=sanatate&zona=Cluj'

# What each campaign type requires
curl 'https://app.comunicate.eu/api/v1/public/campaign-types'
```

Prices are set by each publisher, in bani (1 leu = 100 bani), without VAT. VAT is 21%. A budget plan covers publication only, and we recommend a unique text for each publication. No public route writes anything. Articles, orders, campaigns, reports and webhooks need a key issued from an account.

---

## Free programme for NGOs and institutions

NGOs, schools, universities, hospitals and city halls can publish public interest press releases for free through the [Comunicate de interes public](https://comunicate.eu/ro/comunicate-de-interes-public) programme: up to 8 publications a month, on 19 publications, with nofollow links. Commercial and electoral content is excluded.

---

## This repository

Documentation, the registry manifest and the plugin manifests for Claude Code, Cursor and Gemini CLI only. The platform itself is closed source. `server.json` is what is published to the [official MCP registry](https://registry.modelcontextprotocol.io) under the `eu.comunicate` namespace, verified by the key at <https://comunicate.eu/.well-known/mcp-registry-auth>.

Questions or bug reports about the API: [open an issue](https://github.com/adrianncraciun-cmd/public-mcp/issues) or write to contact@comunicate.eu.

## Licence

The contents of this repository (documentation and manifest) are released under the MIT licence. Use of the API and the MCP server is governed by the [terms of service](https://comunicate.eu/en/legal/termeni).
