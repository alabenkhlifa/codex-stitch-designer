# Codex Stitch Designer

GitHub Pages: <https://alabenkhlifa.github.io/codex-stitch-designer/>

Codex Stitch Designer is a Codex and Claude Code plugin package for designing high-quality UI screens with Google Stitch MCP.

It helps an AI coding assistant act like a practical product designer for Stitch: pick or create the right Stitch project, inspect existing screens and design systems, write strong prompts, generate variants, critique output, and prepare implementation handoffs.

Keywords: Codex plugin, Claude Code plugin, Claude plugin, Claude skills, Claude agents, Google Stitch, Stitch MCP, MCP design tool, UI design, UX design, frontend design, product design, design systems, AI design workflow, AI design assistant.

## Why Use It

- choosing whether to reuse an existing Stitch project or create a new one
- inspecting Stitch projects, screens, and design systems before editing
- writing concrete prompts for mobile apps, web apps, dashboards, landing pages, and games
- generating and refining Stitch screens
- creating useful variants instead of random reskins
- critiquing output for hierarchy, contrast, accessibility, and implementation risk
- preparing implementation handoffs from Stitch designs

## Good Fit

Use this plugin when you want Codex or Claude Code to:

- create new Stitch screens from a product brief
- match the design language of an existing Stitch project
- convert screenshots or rough ideas into concrete Stitch prompts
- generate conservative, distinctive, and experimental variants
- review a Stitch result before implementation
- produce a clean frontend implementation handoff

The Claude Code package ships the same design workflow as a Claude plugin with a skill and a subagent.

## Requirements

- Codex with plugin support
- Claude Code with plugin support, if you use the Claude package
- Google Stitch MCP configured and available in your assistant session
- A Stitch API key and MCP setup from the official docs:
  <https://stitch.withgoogle.com/docs/mcp/setup>

## Install For Codex

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

## Install For Claude Code

Add this repository as a Claude Code plugin marketplace:

```bash
claude plugin marketplace add alabenkhlifa/codex-stitch-designer
claude plugin install stitch-designer@stitch-designer
```

For a local development checkout, validate and install from the repo path:

```bash
claude plugin validate .
claude plugin validate ./claude/stitch-designer
claude plugin marketplace add ./
claude plugin install stitch-designer@stitch-designer
```

The Claude package is isolated under `claude/stitch-designer/`, so it does not change the Codex plugin files.

## Usage

Ask Codex or Claude Code to use the Stitch Designer plugin:

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
- Include your Codex or Claude Code version, install command, Stitch project shape, and screenshots when relevant.

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
- It does not replace product design judgment. It gives your assistant a better workflow for using Stitch.

## Repository Layout

```text
.agents/plugins/marketplace.json
.claude-plugin/marketplace.json
plugins/stitch-designer/.codex-plugin/plugin.json
plugins/stitch-designer/skills/stitch-designer/SKILL.md
plugins/stitch-designer/agents/stitch-designer.toml
plugins/stitch-designer/examples/
claude/stitch-designer/.claude-plugin/plugin.json
claude/stitch-designer/skills/stitch-designer/SKILL.md
claude/stitch-designer/agents/stitch-designer.md
```

## Troubleshooting

- If Stitch tools are missing, verify your MCP setup and restart/reload your assistant.
- If the plugin installs but the skill is not visible, reload plugins or restart the client.
- If Stitch generation times out, inspect the project before retrying; the operation may have completed.
- If project matching is ambiguous, provide the Stitch project ID directly.
- If GitHub Discussions is unavailable, use Issues for feedback until Discussions is enabled.
