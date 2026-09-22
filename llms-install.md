# Installing the JobsPipe MCP server

JobsPipe is a hosted (remote) MCP server. There is nothing to download, build or run locally: add the URL to the client's MCP configuration and connect.

- Server URL: `https://mcp.jobspipe.dev/mcp`
- Transport: streamable HTTP
- Authentication: OAuth 2.0 with dynamic client registration. Clients that support sign-in open the JobsPipe login page on first connect. Clients that cannot sign in send an API key instead: `Authorization: Bearer jp_live_<key>`, created in the JobsPipe dashboard at https://jobspipe.dev/dashboard after a free signup at https://jobspipe.dev/signup.

## Cline

Add to Cline's MCP settings (`cline_mcp_settings.json`), then open the MCP Servers panel and connect:

```json
{
  "mcpServers": {
    "jobspipe": {
      "type": "streamableHttp",
      "url": "https://mcp.jobspipe.dev/mcp",
      "headers": {
        "Authorization": "Bearer jp_live_<key>"
      }
    }
  }
}
```

If the client supports OAuth for remote servers, omit `headers` and sign in when prompted.

## Cursor, VS Code, Claude Code, Gemini CLI

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

Claude Code: `claude mcp add --transport http jobspipe https://mcp.jobspipe.dev/mcp`

Gemini CLI: `gemini extensions install https://github.com/jobspipe/mcp`

## Verify

After connecting, the client should list nine tools: `search`, `fetch`, `search_jobs`, `create_signal`, `list_signals`, `get_account_info`, `detect_company_tech_stack`, `list_pricing_plans`, `search_documentation`. A first call to `list_pricing_plans` needs no credits and confirms the connection.

Docs: https://docs.jobspipe.dev/ai-agents/mcp · Support: support@jobspipe.dev
