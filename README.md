<div style="display: flex; align-items: flex-start; gap: 28px;">
  <img
    width="460"
    height="690"
    alt="Algorithmic industry-research expert"
    src="https://github.com/user-attachments/assets/20d1e3ea-b5b5-47ea-bd7a-7084c8c8f493"
    style="flex: 0 0 auto; max-width: 40%; height: auto;"
  />

  <div style="flex: 1;">
    <p>
      This repository is a self-contained Claude Code plugin and marketplace
      for sector- and industry-level investment research. The repository root
      is also the plugin root. It exposes 39 industry modules across 11 sectors
      as searchable MCP tools and resources, plus a routing skill that helps
      Claude apply the right module during company and security research.
    </p>
    
  </div>
</div>

## Project structure

```text
.
├── .claude-plugin/
│   ├── marketplace.json
│   └── plugin.json
├── .mcp.json
├── server/
├── skills/
│   └── industry-research/
│       ├── SKILL.md
│       └── references/
│           └── <sector>/
│               └── <industry>.md
├── package.json
└── README.md
```

The marketplace entry uses `"source": "./"`, so Claude Code copies this repository root as the plugin. The immutable marketplace slug is `industry-expertise`; its user-facing label is controlled by `displayName`.

## Install from a Claude Code marketplace

After this repository is hosted on GitHub, add it as a marketplace and install the plugin:

```text
/plugin marketplace add <owner>/<repository>
/plugin install industry-expertise@subject-level-expertise
/reload-plugins
```

For local development, replace `<owner>/<repository>` with this repository's absolute path:

```text
/plugin marketplace add /absolute/path/to/SubjectLevelExpertise
/plugin install industry-expertise@subject-level-expertise
/reload-plugins
```

Use `/mcp` to confirm that `industry-expertise` is connected. A Git repository is required for remote marketplace installation; the manifests do not publish or host the repository by themselves.

## Use

Ask Claude naturally, for example:

- “Use the industry expertise layer to analyze a semiconductor equipment company.”
- “What drives margins and capacity in the hotel industry?”
- “Search across industries for exposure to water scarcity.”

Or invoke the plugin skill directly:

```text
/industry-expertise:industry-research "Analyze the industry context for a regional bank"
```

The MCP server exposes:

- `list_industries` — lists the supported sector/industry taxonomy.
- `get_industry_expertise` — retrieves a full module or section with character pagination.
- `search_industry_expertise` — searches all modules or a selected sector/industry.
- `industry-expertise://<sector>/<industry>` resources — provides each complete Markdown module.
- `investigate-industry` — an MCP prompt for starting an industry-grounded investigation.

The modules are an orientation layer. Time-sensitive facts, policies, market data, and company information should still be verified against current primary sources.

## Develop and validate

Requirements: Node.js 18 or newer and Claude Code for manifest validation.

```bash
npm test
npm run validate:plugin
npm run check
```

Run the MCP server directly with `npm start`. The plugin version appears in `package.json`, `.claude-plugin/plugin.json`, and `.claude-plugin/marketplace.json`; bump all three when publishing a release because Claude Code uses the declared plugin version to detect updates.

The marketplace layout follows Anthropic's [plugin marketplace documentation](https://code.claude.com/docs/en/plugin-marketplaces), and the bundled server follows the current [Model Context Protocol specification](https://modelcontextprotocol.io/specification/2025-11-25).
