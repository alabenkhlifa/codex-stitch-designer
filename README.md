<div align="center">

# Codex Stitch Designer

Design Google Stitch screens from Codex or Claude Code.

[Website](https://alabenkhlifa.github.io/codex-stitch-designer/) |
[Install](#install) |
[Usage](#usage) |
[Feedback](#feedback)

![GitHub release](https://img.shields.io/github/v/release/alabenkhlifa/codex-stitch-designer?label=release)
![License](https://img.shields.io/github/license/alabenkhlifa/codex-stitch-designer)
![Codex](https://img.shields.io/badge/Codex-plugin-111827)
![Claude Code](https://img.shields.io/badge/Claude_Code-plugin-191919)
![Google Stitch](https://img.shields.io/badge/Google_Stitch-MCP-4285F4)

</div>

Codex Stitch Designer is a plugin package that gives Codex and Claude Code a practical workflow for Google Stitch MCP: choose or create the right Stitch project, inspect existing screens and design systems, write stronger prompts, generate variants, critique output, and prepare implementation handoffs.

## Why Use It

| Need | What the plugin does |
| --- | --- |
| Start a new UI direction | Creates Stitch-ready prompts for mobile apps, web apps, dashboards, landing pages, and games. |
| Match an existing product | Inspects the current Stitch project before generating screens that follow the same design language. |
| Explore options | Generates conservative, distinctive, and experimental variants with the same functional requirements. |
| Improve a weak result | Critiques hierarchy, contrast, inactive states, accessibility, density, and implementation risk. |
| Move toward code | Produces a frontend handoff with tokens, components, states, localization notes, and risks. |

## Install

### Requirements

- Codex with plugin support, for the Codex package.
- Claude Code with plugin support, for the Claude package.
- Google Stitch MCP configured in your assistant session.
- A Stitch API key and MCP setup from the official docs: <https://stitch.withgoogle.com/docs/mcp/setup>.

### Codex

```bash
codex plugin marketplace add https://github.com/alabenkhlifa/codex-stitch-designer.git
codex plugin list --marketplace codex-stitch-designer
codex plugin add stitch-designer@codex-stitch-designer
```

If your Codex client requires sparse paths:

```bash
codex plugin marketplace add \
  https://github.com/alabenkhlifa/codex-stitch-designer.git \
  --sparse '.agents/plugins' \
  --sparse 'plugins'
```

### Claude Code

```bash
claude plugin marketplace add alabenkhlifa/codex-stitch-designer
claude plugin install stitch-designer@stitch-designer
```

For local development:

```bash
claude plugin validate .
claude plugin validate ./claude/stitch-designer
claude plugin marketplace add ./
claude plugin install stitch-designer@stitch-designer
```

The Claude package is isolated under `claude/stitch-designer/`, so it does not change the Codex plugin files.

## Usage

Ask Codex or Claude Code to use `stitch-designer`:

```text
Use stitch-designer to create a mobile onboarding screen in Stitch.
```

```text
Use stitch-designer to inspect my existing Stitch project and create a billing settings screen that matches its current design language.
```

```text
Use stitch-designer to generate three variants for an incident operations dashboard: conservative, distinctive, and experimental.
```

If you do not provide a Stitch project ID, the plugin should ask whether to reuse an existing project, create a new project, or work without Stitch and produce a design spec or handoff.

## What It Includes

| Package | Path | Contents |
| --- | --- | --- |
| Codex marketplace | `.agents/plugins/marketplace.json` | Marketplace entry for Codex. |
| Codex plugin | `plugins/stitch-designer/` | Skill, agent metadata, examples, and Codex manifest. |
| Claude marketplace | `.claude-plugin/marketplace.json` | Marketplace entry for Claude Code. |
| Claude plugin | `claude/stitch-designer/` | Claude Code skill, subagent, and plugin manifest. |

## Verify

Useful checks for contributors:

```bash
claude plugin validate .
claude plugin validate ./claude/stitch-designer
python3 -m json.tool .agents/plugins/marketplace.json >/dev/null
python3 -m json.tool plugins/stitch-designer/.codex-plugin/plugin.json >/dev/null
```

To confirm Claude Code sees the installed package:

```bash
claude plugin details stitch-designer@stitch-designer
```

Expected inventory:

```text
Skills (1)  stitch-designer
Agents (1)  stitch-designer
```

## Troubleshooting

| Problem | Check |
| --- | --- |
| Stitch tools are missing | Verify the Stitch MCP setup and restart or reload your assistant. |
| Plugin installs but skill is not visible | Reload plugins or restart the client. |
| Stitch generation times out | Inspect the project before retrying; the operation may have completed. |
| Project matching is ambiguous | Provide the Stitch project ID directly. |

## Feedback

Feedback is welcome:

- Install problems: <https://github.com/alabenkhlifa/codex-stitch-designer/issues>
- Design workflow ideas: <https://github.com/alabenkhlifa/codex-stitch-designer/discussions>

Please include your Codex or Claude Code version, install command, Stitch project shape, and screenshots when relevant.

## Roadmap

- More examples for ecommerce, fintech, education, internal tools, and games.
- A deeper implementation handoff template for React, React Native, and Tailwind.
- More troubleshooting notes for Stitch MCP setup and timeout behavior.
- Optional screenshots or short videos showing the full install and design flow.
- A companion workflow for turning Stitch output into frontend code.

## Scope

This plugin does not configure Stitch MCP for you, convert Stitch output into production code by itself, or create persistent Stitch projects without confirmation. It gives your assistant a better workflow for using Stitch.

<details>
<summary>Search terms</summary>

Codex plugin, Claude Code plugin, Claude plugin, Claude skills, Claude agents, Google Stitch, Stitch MCP, MCP design tool, UI design, UX design, frontend design, product design, design systems, AI design workflow, AI design assistant.

</details>
