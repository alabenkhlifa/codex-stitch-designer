# Codex Stitch Designer

Codex Stitch Designer is a Codex plugin for designing high-quality UI screens with Google Stitch MCP.

It helps Codex act like a practical product designer for Stitch: pick or create the right Stitch project, inspect existing screens and design systems, write strong prompts, generate variants, critique output, and prepare implementation handoffs.

Keywords: Codex plugin, Google Stitch, Stitch MCP, UI design, frontend design, design systems, AI design workflow.

## Why Use It

- choosing whether to reuse an existing Stitch project or create a new one
- inspecting Stitch projects, screens, and design systems before editing
- writing concrete prompts for mobile apps, web apps, dashboards, landing pages, and games
- generating and refining Stitch screens
- creating useful variants instead of random reskins
- critiquing output for hierarchy, contrast, accessibility, and implementation risk
- preparing implementation handoffs from Stitch designs

## Good Fit

Use this plugin when you want Codex to:

- create new Stitch screens from a product brief
- match the design language of an existing Stitch project
- convert screenshots or rough ideas into concrete Stitch prompts
- generate conservative, distinctive, and experimental variants
- review a Stitch result before implementation
- produce a clean frontend implementation handoff

## Requirements

- Codex with plugin support
- Google Stitch MCP configured and available in the Codex session
- A Stitch API key and MCP setup from the official docs:
  <https://stitch.withgoogle.com/docs/mcp/setup>

## Install From This Marketplace

Add this repository as a Codex plugin marketplace:

```bash
codex plugin marketplace add https://github.com/alabenkhlifa/codex-stitch-designer.git
codex plugin list --marketplace codex-stitch-designer
codex plugin add stitch-designer@codex-stitch-designer
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

## Example Prompts

Mobile app:

```text
Use stitch-designer to create a mobile home screen for a habit tracking app. Ask whether to reuse an existing Stitch project or create a new one.
```

Dashboard:

```text
Use stitch-designer to generate three variants for an incident operations dashboard: conservative, distinctive, and experimental.
```

Design language match:

```text
Use stitch-designer to inspect my existing Stitch project and create a billing settings screen that matches its current design language.
```

Critique:

```text
Use stitch-designer to critique this Stitch screen for hierarchy, contrast, accessibility, and implementation risk.
```

## Feedback

Feedback is welcome.

- Open an issue for install problems, MCP workflow bugs, or unclear behavior.
- Open a discussion or issue for design workflow ideas, prompt improvements, and examples from real projects.
- Include your Codex version, install command, Stitch project shape, and screenshots when relevant.

Issue tracker:
<https://github.com/alabenkhlifa/codex-stitch-designer/issues>

Discussions:
<https://github.com/alabenkhlifa/codex-stitch-designer/discussions>

## Roadmap

- More example prompts for ecommerce, fintech, education, internal tools, and games.
- A deeper implementation handoff template for React, React Native, and Tailwind.
- More troubleshooting notes for Stitch MCP setup and timeout behavior.
- Optional screenshots or short videos showing the full install and design flow.
- A companion workflow for turning Stitch output into frontend code.

## What This Plugin Does Not Do

- It does not configure your Stitch MCP server for you.
- It does not turn Stitch output into production code unless you ask for a separate implementation step.
- It does not create persistent Stitch projects without your confirmation.
- It does not replace product design judgment. It gives Codex a better workflow for using Stitch.

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
- If GitHub Discussions is unavailable, use Issues for feedback until Discussions is enabled.
