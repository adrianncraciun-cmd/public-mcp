# Comunicate.eu — server MCP și API public

[Read in English](README.md)

**Server MCP** și **API HTTP** pentru [Comunicate.eu](https://comunicate.eu), platforma românească de publicare a comunicatelor de presă, advertorialelor și articolelor SEO, cu un catalog de **peste 3.800 de publicații online** din România, Italia și alte piețe europene.

Prețurile sunt scrise în catalog și sunt aceleași pentru toți. Nu se cere ofertă și nu se negociază, deci un asistent AI poate citi prețul și poate lucra cu el.

| | |
|---|---|
| Server MCP | `https://app.comunicate.eu/mcp` (Streamable HTTP) |
| Fără cont | Căutare în catalog, planuri pe buget, nișe, tipuri de campanie |
| Cu cont | Cheie de API sau OAuth 2.1 cu PKCE, pentru asistenții aprobați |
| OpenAPI 3.1 | <https://comunicate.eu/openapi.json> |
| APIs.json | <https://comunicate.eu/apis.json> |
| Documentație API | <https://comunicate.eu/ro/documentatie-api> |
| Ghid MCP | <https://comunicate.eu/ro/mcp> |
| API public, fără cheie | `https://app.comunicate.eu/api/v1/public/*` |

---

## Ce poți întreba

Merg fără cont:

1. Cât costă un advertorial pe un site de știri din România?
2. Am un site de turism și 500 de lei. Unde pot publica 5 articole cu backlink dofollow?
3. Am o clinică stomatologică în Cluj și un buget de 2.000 de lei. Pe ce site-uri îmi recomanzi să public?
4. Am un magazin online de mobilă. Cum îmi fac o campanie de backlinkuri cu 1.000 de lei?
5. Unde pot publica un comunicat de presă online și ce trebuie să conțină ca să fie acceptat?
6. Ce site-uri de turism acceptă advertoriale și care sunt cele mai ieftine?
7. Cum poate publica un ONG comunicate de presă gratuite în presa online?

---

## Conectare

Pentru conectare și pentru citirea catalogului nu ai nevoie de cheie sau de cont.

**Adresa serverului:** `https://app.comunicate.eu/mcp`

Meniurile și limitele planurilor se schimbă des, deci verifică paginile de ajutor ale asistentului dacă un pas arată altfel.

### Claude

Pe claude.ai sau în aplicația desktop, deschide **Settings → Connectors → Add custom connector**, numește conectorul `Comunicate.eu` și lipește adresa serverului. Pe planurile Team și Enterprise, un proprietar îl adaugă întâi pentru organizație.

### ChatGPT

Deschide **Settings → Apps & Connectors → Advanced**, pornește **Developer mode**, apoi creează un conector cu adresa serverului. Alege **No authentication** pentru citirea catalogului sau **OAuth** ca să lucrezi în cont. Disponibilitatea depinde de plan, iar pe Business sau Enterprise e posibil să trebuiască pornit de un administrator.

### Perplexity

Pe un plan plătit, deschide **Settings → Connectors**, adaugă un conector personalizat cu adresa serverului și transportul Streamable HTTP, apoi alege fără autentificare pentru citirea catalogului sau OAuth ca să lucrezi în cont.

### Gemini

Folosește [Gemini CLI](https://github.com/google-gemini/gemini-cli):

```bash
gemini extensions install https://github.com/adrianncraciun-cmd/public-mcp
```

Sau adaugă serverul manual:

```bash
gemini mcp add --transport http comunicate-eu https://app.comunicate.eu/mcp
```

Poți adăuga și în `~/.gemini/settings.json`:

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

Sau instalează-l ca plugin din acest depozit:

```
/plugin marketplace add adrianncraciun-cmd/public-mcp
/plugin install comunicate-eu@comunicate-eu
```

### Codex

```bash
codex mcp add comunicate-eu --url https://app.comunicate.eu/mcp
codex mcp login comunicate-eu
```

A doua comandă te conectează prin OAuth, pentru uneltele de cont. Sari peste ea dacă îți trebuie doar catalogul.

### Cursor

Adaugă în `~/.cursor/mcp.json`:

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

Rulează **MCP: Add Server** din Command Palette și lipește adresa serverului, sau adaugă-l pentru toate proiectele în `~/.copilot/mcp-config.json`:

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

Pentru un singur proiect, `.vscode/mcp.json` folosește `servers`:

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

Adaugă în `~/.codeium/windsurf/mcp_config.json`:

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

Adaugă în `~/.config/devin/mcp_config.json`:

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

Adaugă în `settings.json` din Zed:

```json
{
  "context_servers": {
    "comunicate-eu": {
      "url": "https://app.comunicate.eu/mcp"
    }
  }
}
```

### Orice alt client care citește `mcpServers`

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

### Cu cont

Emite o cheie de API din *Integrări* și trimite-o ca bearer token. Cheia leagă serverul de organizația ta, deci poate vedea soldul, poate scrie ciorne și, dacă îi dai voie, poate comanda.

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

Claude, ChatGPT, Perplexity, VS Code, Cursor (pe desktop și pe web), Mistral Le Chat și Vibe, Raycast, Microsoft Copilot Studio, Coda, Zapier, Make și Glama se pot conecta prin OAuth 2.1 (PKCE S256), iar conectarea o aprobi în browser. Clienții care rulează pe calculatorul tău, cum sunt Claude Code, Codex, Gemini CLI, Zed, Goose și Cline, se conectează la fel, printr-o adresă locală. Codurile de autorizare pleacă doar spre acești clienți aprobați. Orice alt client folosește o cheie de API.

---

## Unde îl găsești

- [Registrul oficial MCP](https://registry.modelcontextprotocol.io/v0.1/servers?search=eu.comunicate): `eu.comunicate/publishing`
- [Glama](https://glama.ai/mcp/connectors/eu.comunicate/publishing)
- [cursor.directory](https://cursor.directory/plugins/comunicatetop)
- [mcptry](https://mcptry.com/servers/eu.comunicate/publishing)
- Pluginul pentru Claude Code și extensia pentru Gemini CLI: acest depozit

---

## Unelte

Douăzeci și șapte de unelte.

**Fără cont**

| Unealtă | Ce face |
|---|---|
| `how_it_works` | Cum se publică, abonamentele, plata și programul gratuit pentru ONG-uri și instituții. |
| `plan_budget` | Pachete pentru un buget, după nișă, subiect și oraș, cu totalul cu și fără TVA. Se cheamă din nou cu `exclude` pentru alte variante. |
| `search_catalog` | Caută în catalog după text, nișă, tip de campanie, autoritate și preț. |
| `get_site` | O publicație: preț și linkuri pe tip de campanie, reguli și condiții. |
| `catalog_stats` | Câte publicații și nișe are catalogul. |
| `list_niches` / `get_niche` | Nișele, cu descrieri și exemple. |
| `list_campaign_types` | Ce înseamnă fiecare tip de campanie și ce e obligatoriu sau interzis în text. |
| `list_own_network` / `get_own_publication` | Rețeaua Comunicate.eu, la cerere explicită. |

**Cu cont**

| Unealtă | Ce face |
|---|---|
| `whoami` | Organizația din spatele cheii și ce are voie să facă. |
| `get_balance` | Creditele pe pachete și soldul. |
| `list_articles` / `get_article` | Ciornele și articolele publicate. |
| `create_article` / `update_article` | Scrie și modifică o ciornă. |
| `check_article_seo` | Cât de bine e scris textul ca articol SEO. |
| `check_article_fit` | Dacă textul respectă cerințele tipului de campanie și nu are locuri necompletate. |
| `list_campaigns` / `create_campaign` / `update_campaign` | Planuri editoriale: obiectiv, buget, site-uri permise. |
| `list_publications` / `get_publication` | Starea și adresa fiecărei publicări. |
| `order_publication` | Comandă o publicare. **Cheltuie credite sau bani.** |
| `order_writing` | Comandă redactarea unui articol. **Cheltuie bani.** |
| `list_writing_orders` | Starea comenzilor de redactare și articolele livrate. |
| `report_summary` | Publicări, site-uri și cheltuieli într-o perioadă. |

Comenzile sunt oprite implicit. Organizația are un comutator prin care decide dacă asistenții AI pot cheltui, valabil și pentru tokenurile OAuth folosite direct pe API. Fiecare comandă e verificată și față de sold.

---

## API public

Rute de citire, deschise oricui, cu limite de cereri. Sunt descrise în același document OpenAPI ca restul API-ului, cu `security: []`.

```bash
# Mărimea catalogului
curl 'https://app.comunicate.eu/api/v1/public/stats'
# → {"publications":3809,"niches":22}

# Nișele, cu numărul de publicații și autoritatea medie
curl 'https://app.comunicate.eu/api/v1/public/niches?locale=ro'

# Căutare în catalog: cel mult 20 pe pagină și primele 120 pe o căutare
curl 'https://app.comunicate.eu/api/v1/public/catalog?niche=sanatate&campaign=PRESS_RELEASE&sort=PRICE_ASC&limit=5'

# Plan pe buget: pachete pentru 1.000 de lei, într-o nișă și un oraș
curl 'https://app.comunicate.eu/api/v1/public/plan?bugetLei=1000&nise=sanatate&zona=Cluj'

# Ce cere fiecare tip de campanie
curl 'https://app.comunicate.eu/api/v1/public/campaign-types'
```

Prețurile sunt stabilite de fiecare publisher, în bani (1 leu = 100 de bani), fără TVA. TVA-ul e 21%. Un plan pe buget acoperă doar publicarea și recomandăm un text unic pentru fiecare publicație. Nicio rută publică nu scrie nimic. Articolele, comenzile, campaniile, rapoartele și webhook-urile cer o cheie emisă dintr-un cont.

---

## Program gratuit pentru ONG-uri și instituții

ONG-urile, școlile, universitățile, spitalele și primăriile pot publica gratuit comunicate de interes public prin programul [Comunicate de interes public](https://comunicate.eu/ro/comunicate-de-interes-public): până la 8 publicări pe lună, pe 19 publicații, cu linkuri nofollow. Conținutul comercial și cel electoral nu intră în program.

---

## Acest depozit

Conține doar documentația, manifestul pentru registru și manifestele de plugin pentru Claude Code, Cursor și Gemini CLI. Platforma nu e open source. `server.json` e publicat în [registrul oficial MCP](https://registry.modelcontextprotocol.io) sub spațiul `eu.comunicate`, verificat prin cheia de la <https://comunicate.eu/.well-known/mcp-registry-auth>.

Întrebări sau probleme legate de API: [deschide un issue](https://github.com/adrianncraciun-cmd/public-mcp/issues) sau scrie la contact@comunicate.eu.

## Licență

Conținutul acestui depozit (documentație și manifest) e publicat sub licența MIT. Folosirea API-ului și a serverului MCP e guvernată de [termenii de utilizare](https://comunicate.eu/ro/legal/termeni).
