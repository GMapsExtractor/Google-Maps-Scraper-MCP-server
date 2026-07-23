# Installing the Google Maps Scraper MCP server

This is a remote MCP server. There is no package to install and nothing to run locally. Register the endpoint with an MCP client and authenticate with a G Maps Extractor API key.

- Endpoint: `https://cloud.gmapsextractor.com/api/mcp`
- Transport: Streamable HTTP
- Authentication: `Authorization: Bearer YOUR_API_KEY`
- API key: `https://cloud.gmapsextractor.com`

Never commit a real API key. Use an environment variable, secret store, or your client's secure input setting.

## Register the server

### Claude Code

```bash
claude mcp add --transport http google-maps-scraper-mcp \
  https://cloud.gmapsextractor.com/api/mcp \
  --header "Authorization: Bearer YOUR_API_KEY"
```

### Cursor

Add to `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "google-maps-scraper-mcp": {
      "url": "https://cloud.gmapsextractor.com/api/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

### VS Code

Add to `.vscode/mcp.json`:

```json
{
  "servers": {
    "google-maps-scraper-mcp": {
      "type": "http",
      "url": "https://cloud.gmapsextractor.com/api/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

### Codex

Add to `~/.codex/config.toml`:

```toml
[mcp_servers.google-maps-scraper-mcp]
type = "http"
url = "https://cloud.gmapsextractor.com/api/mcp"

[mcp_servers.google-maps-scraper-mcp.headers]
Authorization = "Bearer YOUR_API_KEY"
```

### Cline

Add to your MCP settings:

```json
{
  "mcpServers": {
    "google-maps-scraper-mcp": {
      "type": "streamableHttp",
      "url": "https://cloud.gmapsextractor.com/api/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

After registering the server, call `search_google_maps`, `get_place_reviews`, or `get_place_photos`.

Full product and setup information: `https://gmapsextractor.com/google-maps-scraper-mcp`
