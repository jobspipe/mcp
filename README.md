# JobsPipe MCP Server

[![smithery badge](https://smithery.ai/badge/jobspipe/jobspipe-mcp)](https://smithery.ai/servers/jobspipe/jobspipe-mcp)

The hosted [Model Context Protocol](https://modelcontextprotocol.io) server for [JobsPipe](https://jobspipe.dev): live job postings from 30+ job boards, ATS feeds and public employment services, normalized into one schema and queryable by AI agents. Nothing to run locally.

This repository is also the [Cursor Marketplace](https://cursor.com/marketplace) plugin for JobsPipe.

- **Server:** `https://mcp.jobspipe.dev/mcp` — remote, streamable HTTP. Sign in with OAuth on first connect (the default in Cursor, Claude, ChatGPT, VS Code and Codex), or send a Bearer API key from a script.
- **Try it without an account:** `https://jobspipe.dev/mcp` — a smaller no-key server with real postings for evaluating the protocol.
- **Server card:** [`/.well-known/mcp/server-card.json`](https://jobspipe.dev/.well-known/mcp/server-card.json)
- **Docs:** https://docs.jobspipe.dev/ai-agents/mcp
- **Agent skills:** [`npx skills add jobspipe/skills`](https://skills.sh/jobspipe/skills)

## Install in Cursor

1. Open **Cursor Settings → Plugins**.
2. Search for **JobsPipe**.
3. Click **Install**, then complete the JobsPipe sign-in prompt.

Or run `/add-plugin jobspipe` in chat.

Without the marketplace, add the server by hand to `mcp.json`:

```json
{
  "mcpServers": {
    "jobspipe": {
      "type": "http",
      "url": "https://mcp.jobspipe.dev/mcp"
    }
  }
}
```

Auth is OAuth 2.0 against JobsPipe with dynamic client registration; Cursor prompts for sign-in when the plugin connects, and there is no API key to configure. A JobsPipe account is free to create at [jobspipe.dev/signup](https://jobspipe.dev/signup).

## Tools

| Tool | What it does |
|---|---|
| `search` | Search live postings by role, place and date; returns results to cite, each with an id, a title and a link |
| `fetch` | Read one posting in full by the id a `search` result carried |
| `search_jobs` | The same corpus with every filter exposed: location, salary, seniority, skills, visa stance, language, work arrangement, source and more |
| `create_signal` | Save a search and be notified of new matches by email, Slack or webhook, instead of polling |
| `list_signals` | List the signals saved on the connected account |
| `get_account_info` | Show the connected account, its plan and remaining credits |
| `detect_company_tech_stack` | Detect the technologies a company serves on its domain |
| `list_pricing_plans` | List JobsPipe plans with monthly price, job quota and limits |
| `search_documentation` | Search the JobsPipe API documentation for filter names, accepted values and limits |

Searches draw on the connected account's plan; evaluating a signal costs no job credits.

## Other clients

Gemini CLI (this repository is also a Gemini CLI extension):

```bash
gemini extensions install https://github.com/jobspipe/mcp
```

Claude Code:

```bash
claude mcp add --transport http jobspipe https://mcp.jobspipe.dev/mcp
```

Claude, ChatGPT, VS Code, Codex and any client that supports remote MCP with OAuth: add `https://mcp.jobspipe.dev/mcp` as a connector and sign in. For a script or a client without sign-in, send `Authorization: Bearer jp_live_<key>` with a key from the [dashboard](https://jobspipe.dev/dashboard).

The server is also listed in the official [MCP Registry](https://registry.modelcontextprotocol.io) as `dev.jobspipe/mcp` (`server.json` in this repository).

## Support

- Email: support@jobspipe.dev
- Docs: https://docs.jobspipe.dev
- Terms and privacy: https://jobspipe.dev/terms · https://jobspipe.dev/privacy

Logo is the JobsPipe app icon (three white bars on the purple gradient tile) from https://jobspipe.dev/brand/app-icon/app-icon-gradient.svg.

## License

MIT
