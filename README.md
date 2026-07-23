<p align="center">
  <a href="https://gmapsextractor.com">
    <img src="logo.png" alt="G Maps Extractor" width="400">
  </a>
</p>

# Google Maps Scraper MCP server

Give your AI agent live Google Maps business search, review, and photo data through one secure [Model Context Protocol](https://modelcontextprotocol.io/) connection.

This repository is the public listing and manifest for the hosted G Maps Extractor MCP server. The server runs remotely, so there is no package to install and nothing to host locally.

- Website: [gmapsextractor.com](https://gmapsextractor.com)
- Product page: [Google Maps Scraper MCP](https://gmapsextractor.com/google-maps-scraper-mcp)
- Get an API key: [cloud.gmapsextractor.com](https://gmapsextractor.com/google-maps-scraper-mcp)
- MCP endpoint: `https://cloud.gmapsextractor.com/api/mcp`
- Transport: Streamable HTTP
- Authentication: `Authorization: Bearer YOUR_API_KEY`

## What you can do

- Search businesses by keyword and location, including listing details such as names, addresses, phone numbers, websites, ratings, reviews, and photos.
- Retrieve public Google Maps reviews for reputation research and customer feedback analysis.
- Retrieve public business photos and image URLs for listing enrichment and visual audits.

Common workflows include prospecting research, local market analysis, competitor comparisons, CRM enrichment, reputation analysis, and listing audits.

## Connect

Create an API key in the [G Maps Extractor dashboard](https://cloud.gmapsextractor.com), keep it in a secure environment variable or secret store, and register the remote endpoint with your MCP client.

### Claude Code

```bash
claude mcp add --transport http google-maps-scraper-mcp \
  https://cloud.gmapsextractor.com/api/mcp \
  --header "Authorization: Bearer YOUR_API_KEY"
```

### Cursor

Add this to `.cursor/mcp.json` in your project:

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

Add this to `.vscode/mcp.json` in your project:

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

Add this to `~/.codex/config.toml`:

```toml
[mcp_servers.google-maps-scraper-mcp]
type = "http"
url = "https://cloud.gmapsextractor.com/api/mcp"

[mcp_servers.google-maps-scraper-mcp.headers]
Authorization = "Bearer YOUR_API_KEY"
```

### Cline

Add this to your MCP settings:

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

## Tools

### `search_google_maps`

Search for businesses and places on Google Maps in real time.

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `q` | string | Yes | Search query, such as `coffee shops in New York` |
| `ll` | string | No | Coordinates and zoom, such as `@40.7128,-74.0060,11z` |
| `hl` | string | No | Language code; defaults to `en` |
| `gl` | string | No | Country code; defaults to `us` |
| `page` | number | No | Page number; defaults to `1` |
| `extra` | boolean | No | Include emails, social profiles, and extended details |

### `get_place_reviews`

Retrieve public reviews for a place using the `fid` returned by `search_google_maps`.

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `fid` | string | Yes | Google Maps feature ID returned by a search |
| `page` | number | No | Page number; defaults to `1` |
| `max_page` | number | No | Maximum number of pages to retrieve |
| `sort_by` | number | No | `1` relevant, `2` newest, `3` highest rating, `4` lowest rating |

### `get_place_photos`

Retrieve public photos for a place using the `fid` returned by `search_google_maps`.

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `fid` | string | Yes | Google Maps feature ID returned by a search |
| `page` | number | No | Page number; defaults to `1` |
| `max_page` | number | No | Maximum number of pages to retrieve |

## Example prompts

- “Find the top-rated coffee shops in Portland and return their website, phone number, rating, and review count.”
- “Get the newest Google Maps reviews for this place and summarize the recurring customer complaints.”
- “Retrieve public photos for these restaurant FIDs and identify locations with limited visual content.”
- “Compare visible listing signals for dentists in Austin and group the results by rating.”

## Authentication and usage

Every request must include your G Maps Extractor API key:

```http
Authorization: Bearer YOUR_API_KEY
```

Do not commit a real API key to this repository or any client configuration. New accounts can start with the available free monthly requests; higher-volume usage follows the plan attached to the key.

## About this repository

This is a public discovery, configuration, and documentation repository. It contains:

- `server.json` for MCP Registry-compatible server metadata
- `.mcp.json` as a ready-to-customize client configuration
- `llms-install.md` with concise installation instructions for AI agents
- product icons and branding

The hosted MCP implementation remains at `https://cloud.gmapsextractor.com/api/mcp`.

## License

[MIT](LICENSE)
