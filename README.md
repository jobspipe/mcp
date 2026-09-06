# JobsPipe MCP Server

[![LightNow](https://lightnow.ai/badge/dev.jobspipe/mcp)](https://lightnow.ai/servers/dev.jobspipe/mcp)

The hosted [Model Context Protocol](https://modelcontextprotocol.io) server for [JobsPipe](https://jobspipe.dev): live job postings from 30+ ATS feeds and job boards, normalized into one schema, queryable by AI agents.

There are two servers. **Live job results come only from the authenticated one.**

- **Live endpoint (authenticated):** `https://mcp.jobspipe.dev/mcp` — remote, streamable HTTP; nothing to run locally. Requires a Bearer API key (free tier: 100 credits/month at [jobspipe.dev/signup](https://jobspipe.dev/signup)).
- **Demo endpoint (no key):** `https://jobspipe.dev/mcp` — for trying the protocol out. Its `search_jobs` returns the REST call to run for your query, **not** live postings.
- **Server card:** [`/.well-known/mcp/server-card.json`](https://jobspipe.dev/.well-known/mcp/server-card.json)
- **Docs:** https://docs.jobspipe.dev
- **Agent skills:** [`npx skills add jobspipe/skills`](https://skills.sh/jobspipe/skills) - the official JobsPipe skill collection (job search, stack scan, MCP setup, webhooks, agent discovery)

## Tools

Live server (`mcp.jobspipe.dev/mcp`, Bearer key required):

| Tool | What it does |
|---|---|
| `search_jobs` | Search live, normalized job postings by title, skill/tech, country, remote, seniority, employment type and recency. Returns the postings. |
| `list_pricing_plans` | List JobsPipe plans with monthly USD price, request quota and features |

Demo server (`jobspipe.dev/mcp`, no key):

| Tool | What it does |
|---|---|
| `search_jobs` | Returns the REST call to run for your query — not live postings |
| `list_job_sources` | List the ATS and job-board sources JobsPipe normalizes, with coverage and freshness notes |
| `list_pricing_plans` | List JobsPipe plans with monthly USD price, request quota and features |
| `search_upwork_jobs` | Search live Upwork postings with budget, skills and client signals |

## Setup

Claude Code:

```bash
claude mcp add --transport http jobspipe https://mcp.jobspipe.dev/mcp \
  --header "Authorization: Bearer jp_live_YOUR_KEY"
```

Generic client config (Cursor, Windsurf, and others):

```json
{
  "mcpServers": {
    "jobspipe": {
      "url": "https://mcp.jobspipe.dev/mcp",
      "headers": {
        "Authorization": "Bearer jp_live_YOUR_KEY"
      }
    }
  }
}
```

Keys start with `jp_live_` and come from the dashboard (Settings -> API Keys). An `x-api-key` header also works.

### Trying it without a key

Point any MCP client at `https://jobspipe.dev/mcp` — the discovery tools work fully, and `search_jobs` hands back the exact REST request to run instead of the postings. For sample job data in the live schema without a key, use the REST sandbox instead:

```bash
curl -X POST https://api.jobspipe.dev/v1/sandbox/jobs/search \
  -H "Content-Type: application/json" \
  -d '{"job_title_or":["software engineer"],"remote":true}'
```

## Related

- [jobspipe-cli](https://github.com/jobspipe/jobspipe-cli): CLI and agent skill wrapping the same API
- [jobspipe-python](https://github.com/jobspipe/jobspipe-python): official Python SDK
- [REST API reference](https://docs.jobspipe.dev)
