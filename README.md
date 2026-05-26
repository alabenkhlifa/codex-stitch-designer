# Codex Stitch Designer

Codex plugin for designing UI screens with Google Stitch MCP.

It gives Codex a structured workflow for:

- choosing whether to reuse an existing Stitch project or create a new one
- inspecting Stitch projects, screens, and design systems before editing
- writing concrete prompts for mobile apps, web apps, dashboards, landing pages, and games
- generating and refining Stitch screens
- creating useful variants instead of random reskins
- critiquing output for hierarchy, contrast, accessibility, and implementation risk
- preparing implementation handoffs from Stitch designs

## Requirements

- Codex with plugin support
- Google Stitch MCP configured and available in the Codex session
- A Stitch API key and MCP setup from the official docs:
  <https://stitch.withgoogle.com/docs/mcp/setup>

## Install From This Marketplace

Add this repository as a Codex plugin marketplace:

```bash
codex plugin marketplace add https://github.com/alabenkhlifa/codex-stitch-designer.git
codex plugin list --source codex-stitch-designer
codex plugin install stitch-designer --source codex-stitch-designer
```

If your Codex client requires sparse paths, use:

```bash
codex plugin marketplace add \
  https://github.com/alabenkhlifa/codex-stitch-designer.git \
  --sparse '.agents/plugins' \
  --sparse 'plugins'
```

## Usage

Ask Codex to use the Stitch Designer plugin:

```text
Use stitch-designer to create a mobile onboarding screen in Stitch.
```

```text
Use stitch-designer to redesign this dashboard and generate conservative, distinctive, and experimental variants.
```

```text
Use stitch-designer to inspect my existing Stitch project and create a settings screen that matches its design language.
```

If you do not provide a Stitch project ID, the plugin should ask whether to:

- reuse an existing Stitch project
- create a new Stitch project
- work without Stitch and produce a design spec or handoff

## What This Plugin Does Not Do

- It does not configure your Stitch MCP server for you.
- It does not turn Stitch output into production code unless you ask for a separate implementation step.
- It does not create persistent Stitch projects without your confirmation.

## Repository Layout

```text
.agents/plugins/marketplace.json
plugins/stitch-designer/.codex-plugin/plugin.json
plugins/stitch-designer/skills/stitch-designer/SKILL.md
plugins/stitch-designer/agents/stitch-designer.toml
plugins/stitch-designer/examples/
```

## Troubleshooting

- If Stitch tools are missing, verify your MCP setup and restart/reload Codex.
- If the plugin installs but the skill is not visible, reload plugins or restart the client.
- If Stitch generation times out, inspect the project before retrying; the operation may have completed.
- If project matching is ambiguous, provide the Stitch project ID directly.
