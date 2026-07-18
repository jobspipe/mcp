# JobsPipe MCP Server

[![smithery badge](https://smithery.ai/badge/jobspipe/jobspipe-mcp)](https://smithery.ai/servers/jobspipe/jobspipe-mcp)

The hosted [Model Context Protocol](https://modelcontextprotocol.io) server for [JobsPipe](https://jobspipe.dev): live job postings from 30+ ATS feeds and job boards, normalized into one schema, queryable by AI agents.

- **Endpoint:** `https://jobspipe.dev/mcp` (remote, streamable HTTP; nothing to run locally)
- **Server card:** [`/.well-known/mcp/server-card.json`](https://jobspipe.dev/.well-known/mcp/server-card.json)
- **Docs:** https://jobspipe.dev/docs
- **Agent skills:** [`npx skills add jobspipe/skills`](https://skills.sh/jobspipe/skills) - the official JobsPipe skill collection (job search, stack scan, MCP setup, webhooks, agent discovery)

## Tools

| Tool | What it does |
|---|---|
| `search_jobs` | Search live, normalized job postings by title, skill/tech, country, remote, seniority, employment type and recency |
| `list_job_sources` | List the ATS and job-board sources JobsPipe normalizes, with coverage and freshness notes |
| `list_pricing_plans` | List JobsPipe plans with monthly USD price, request quota and features |
| `search_upwork_jobs` | Search live Upwork postings with budget, skills and client signals |

## Setup

Claude Code:

```bash
claude mcp add --transport http jobspipe https://jobspipe.dev/mcp
```

Generic client config (Cursor, Windsurf, and others):

```json
{
  "mcpServers": {
    "jobspipe": {
      "url": "https://jobspipe.dev/mcp"
    }
  }
}
```

Discovery tools work without a key. For authenticated job-search results, pass your API key (free tier: 100 credits/month at [jobspipe.dev/signup](https://jobspipe.dev/signup)):

```json
{
  "mcpServers": {
    "jobspipe": {
      "url": "https://jobspipe.dev/mcp",
      "headers": {
        "Authorization": "Bearer jp_live_YOUR_KEY"
      }
    }
  }
}
```

## Related

- [jobspipe-cli](https://github.com/jobspipe/jobspipe-cli): CLI and agent skill wrapping the same API
- [jobspipe-python](https://github.com/jobspipe/jobspipe-python): official Python SDK
- [REST API reference](https://jobspipe.dev/docs)
