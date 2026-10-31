# Digital Gemology cut library (MCP server)

[![mcptry](https://mcptry.com/badge/com.digitalgemology/cut-library)](https://mcptry.com/servers/com.digitalgemology/cut-library)

A remote [Model Context Protocol](https://modelcontextprotocol.io) server for [Digital Gemology](https://digitalgemology.com): search 45 gem cuts and get their ray-traced brilliance, fire and scintillation in seven gemstones, their specifications, and links to the 3D models and GemCad faceting diagrams.

- **Endpoint:** `https://digitalgemology.com/mcp` (Streamable HTTP, stateless)
- **Registry name:** `com.digitalgemology/cut-library` in the [official MCP Registry](https://registry.modelcontextprotocol.io/v0/servers?search=com.digitalgemology)
- **Sign-in:** none. Read-only and free to use.
- **Protocol versions:** 2026-07-28, 2025-11-25, 2025-06-18, 2025-03-26

This repository holds the server's public description, its registry listing and the open data it serves. The server itself runs on digitalgemology.com.

## Tools

| Tool | What it does |
|---|---|
| `search_cuts` | Search the cut library by name, style, shape or use ("square step cut", "round brilliant for moissanite", "historic cushion"). Returns each cut's page, facets, size, price and checkout links; give a gemstone to sort by brilliance, fire and scintillation in that stone. |
| `get_cut` | Everything about one cut: measured specifications (facets, angles, depth, size, index gear), brilliance, fire and scintillation in all seven gemstones, prices and checkout links. |
| `best_cuts_for_gemstone` | The top ten brilliants and top ten jewelry cuts in one gemstone, with the stone's optical constants. |
| `cut_in_gemstone` | How one cut performs in one gemstone: eight measured scores against the T73 round brilliant, with pros and cons. |
| `list_gemstones` | The seven gemstones (diamond, moissanite, cubic zirconia, ruby, sapphire, emerald, amethyst) with refractive index, critical angle, dispersion, hardness and specific gravity. |
| `get_cut_scores` | The [Cut Performance Index](https://digitalgemology.com/learn/cut-performance-index): overall, brilliance, fire, scintillation, tilt, symmetry, spread, shape-norm and leakage, in diamond and in moissanite. |

## Connect

**Claude Code**

```bash
claude mcp add --transport http digital-gemology https://digitalgemology.com/mcp
```

**Claude Desktop, Cursor, VS Code and other clients** that take a JSON config:

```json
{
  "mcpServers": {
    "digital-gemology": {
      "type": "http",
      "url": "https://digitalgemology.com/mcp"
    }
  }
}
```

**Try it with curl**

```bash
curl -s https://digitalgemology.com/mcp \
  -H "Content-Type: application/json" -H "Accept: application/json, text/event-stream" \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"best_cuts_for_gemstone","arguments":{"gemstone":"moissanite"}}}'
```

## Other ways in

- **REST API:** `https://digitalgemology.com/api/cuts`, `/api/cuts/{slug}`, `/api/gemstones`, `/api/cut-index` ([OpenAPI](https://digitalgemology.com/api/openapi.json))
- **A2A agent:** `https://digitalgemology.com/a2a` ([agent card](https://digitalgemology.com/.well-known/agent-card.json))
- **For language models:** [llms.txt](https://digitalgemology.com/llms.txt), and a Markdown copy of every page
- **Docs:** [digitalgemology.com/about/agents](https://digitalgemology.com/about/agents)

## Data

[`data/`](data/) holds the **Digital Gemology Cut Performance Index**: ray-traced light-performance scores for 45 gem cuts, in diamond and in moissanite (90 rows). The method and every column are explained on the [index page](https://digitalgemology.com/learn/cut-performance-index).

- DOI: [10.5281/zenodo.23844870](https://doi.org/10.5281/zenodo.23844870)
- Also on [Kaggle](https://www.kaggle.com/datasets/digitalgemology/digital-gemology-cut-performance-index) and [Hugging Face](https://huggingface.co/datasets/DigitalGemology/cut-performance-index)
- Wikidata: [Q141955945](https://www.wikidata.org/wiki/Q141955945)

## License

The data and this documentation are licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/): use and share freely, with credit to Digital Gemology and a link to https://digitalgemology.com. The 3D models and faceting diagrams the tools link to are sold separately under their own license.

## Contact

support@digitalgemology.com
