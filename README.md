# Digital Gemology MCP servers: cut library, gem identification, gemology lessons

[![mcptry](https://mcptry.com/badge/com.digitalgemology/cut-library)](https://mcptry.com/servers/com.digitalgemology/cut-library)

Three remote [Model Context Protocol](https://modelcontextprotocol.io) servers from [Digital Gemology](https://digitalgemology.com):

| Server | Endpoint | Registry name | What it does |
|---|---|---|---|
| Cut library | `https://digitalgemology.com/mcp` | `com.digitalgemology/cut-library` | Search 45 gem cuts; ray-traced brilliance, fire and scintillation in seven gemstones; compare cuts; recommend a cut; 3D models and GemCad faceting diagrams |
| Gem identification | `https://digitalgemology.com/mcp/gems` | `com.digitalgemology/gem-identification` | Gemstone properties; match refractive index, birefringence, specific gravity, pleochroism and spectrum lines to seven gemstones; tell two gems apart |
| Gemology lessons | `https://digitalgemology.com/mcp/learn` | `com.digitalgemology/gemology-lessons` | Search, read and quote 53 gemology lessons: the four Cs, diamond anatomy, grading reports, diamond vs moissanite, historic cuts, bow-ties |

- **Transport:** Streamable HTTP, stateless
- **Registry:** [official MCP Registry](https://registry.modelcontextprotocol.io/v0/servers?search=com.digitalgemology)
- **Sign-in:** none. Read-only and free to use.
- **Protocol versions:** 2026-07-28, 2025-11-25, 2025-06-18, 2025-03-26

This repository holds the servers' public description, their registry listings and the open data they serve. The servers run on digitalgemology.com.

## Cut library tools (`/mcp`)

| Tool | What it does |
|---|---|
| `search_cuts` | Search the cut library by name, style, shape or use ("square step cut", "round brilliant for moissanite", "historic cushion"). Returns each cut's page, facets, size, price and checkout links; give a gemstone to sort by brilliance, fire and scintillation in that stone. |
| `get_cut` | Everything about one cut: measured specifications (facets, angles, depth, size, index gear), brilliance, fire and scintillation in all seven gemstones, prices and checkout links. |
| `best_cuts_for_gemstone` | The top ten brilliants and top ten jewelry cuts in one gemstone, with the stone's optical constants. |
| `cut_in_gemstone` | How one cut performs in one gemstone: eight measured scores against the T73 round brilliant, with pros and cons. |
| `list_gemstones` | The seven gemstones (diamond, moissanite, cubic zirconia, ruby, sapphire, emerald, amethyst) with refractive index, critical angle, dispersion, hardness and specific gravity. |
| `get_cut_scores` | The [Cut Performance Index](https://digitalgemology.com/learn/cut-performance-index): overall, brilliance, fire, scintillation, tilt, symmetry, spread, shape-norm and leakage, in all seven gemstones. |
| `compare_cuts` | Two cuts side by side in one gemstone: place in the index, every figure, which cut is ahead on each, and links to buy. |
| `recommend_cut` | The best cuts for a gemstone, ranked by overall, brilliance, fire, scintillation, spread, tilt or leakage; filter by category or shape. |

## Gem identification tools (`/mcp/gems`)

The values that Digital Gemology's free [Refractometer](https://digitalgemology.com/tools/refractometer), [Polariscope](https://digitalgemology.com/tools/polariscope), [Dichroscope](https://digitalgemology.com/tools/dichroscope) and [Spectroscope](https://digitalgemology.com/tools/spectroscope) use, for diamond, moissanite, cubic zirconia, ruby, sapphire, emerald and amethyst. A match is a lead, not an identification: a laboratory report is the proof.

| Tool | What it does |
|---|---|
| `gem_properties` | One gemstone: refractive index, birefringence, dispersion, specific gravity, hardness, crystal system, and what each instrument shows. |
| `identify_gem` | Give any readings (refractive index, birefringence, specific gravity, singly or doubly refractive, pleochroism, a spectrum line, over the refractometer limit). Returns which of the seven stones fit each reading. |
| `compare_gemstones` | Which tests tell two gemstones apart (for example diamond and moissanite), and which do not. |
| `absorption_spectrum` | The lines and bands a gemstone shows in a spectroscope, with their cause. |

## Gemology lessons tools (`/mcp/learn`)

| Tool | What it does |
|---|---|
| `search_lessons` | Find lessons on a topic or question ("what is fire in a diamond"). |
| `get_lesson` | The full text of one lesson as Markdown, by title or URL. |
| `explain_term` | Short passages from the lessons that explain a term ("critical angle", "pavilion angle"), each with its link. |
| `list_courses` | Every course and its lessons. |

## Connect

**Claude Code**

```bash
claude mcp add --transport http digital-gemology https://digitalgemology.com/mcp
claude mcp add --transport http digital-gemology-gems https://digitalgemology.com/mcp/gems
claude mcp add --transport http digital-gemology-learn https://digitalgemology.com/mcp/learn
```

**Claude Desktop, Cursor, VS Code and other clients** that take a JSON config:

```json
{
  "mcpServers": {
    "digital-gemology": { "type": "http", "url": "https://digitalgemology.com/mcp" },
    "digital-gemology-gems": { "type": "http", "url": "https://digitalgemology.com/mcp/gems" },
    "digital-gemology-learn": { "type": "http", "url": "https://digitalgemology.com/mcp/learn" }
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
- **JSON files:** [gem data](https://digitalgemology.com/api/gems.json), [all lessons](https://digitalgemology.com/api/learn.json), [the whole cut library](https://digitalgemology.com/api/catalog.json)
- **A2A agent:** `https://digitalgemology.com/a2a` ([agent card](https://digitalgemology.com/.well-known/agent-card.json))
- **For language models:** [llms.txt](https://digitalgemology.com/llms.txt), and a Markdown copy of every page
- **Docs:** [digitalgemology.com/about/agents](https://digitalgemology.com/about/agents)

## Data

[`data/`](data/) holds the **Digital Gemology Cut Performance Index**: ray-traced light-performance scores for 45 gem cuts in seven gemstones, diamond, moissanite, cubic zirconia, ruby, sapphire, emerald and amethyst (315 rows). Ruby and sapphire are both corundum, so they share one set of figures; color and absorption are not part of the trace. The method and every column are explained on the [index page](https://digitalgemology.com/learn/cut-performance-index).

- DOI: [10.5281/zenodo.23844870](https://doi.org/10.5281/zenodo.23844870)
- Also on [Kaggle](https://www.kaggle.com/datasets/digitalgemology/digital-gemology-cut-performance-index) and [Hugging Face](https://huggingface.co/datasets/DigitalGemology/cut-performance-index)
- Wikidata: [Q141955945](https://www.wikidata.org/wiki/Q141955945)

## License

The data and this documentation are licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/): use and share freely, with credit to Digital Gemology and a link to https://digitalgemology.com. The 3D models and faceting diagrams the tools link to are sold separately under their own license.

## Contact

support@digitalgemology.com
