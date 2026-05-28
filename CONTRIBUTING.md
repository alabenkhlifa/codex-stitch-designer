# Contributing

Thanks for improving Codex Stitch Designer.

## Useful Contributions

- Better Stitch MCP workflows and edge cases.
- Prompt examples for real product categories.
- Installation and troubleshooting notes.
- Design critique rubrics.
- Implementation handoff templates.
- Bug reports from actual Codex or Stitch sessions.

## Development

Validate the plugin before opening a PR:

```bash
python3 /path/to/plugin-creator/scripts/validate_plugin.py plugins/stitch-designer
python3 -m json.tool .agents/plugins/marketplace.json >/dev/null
python3 -m json.tool plugins/stitch-designer/.codex-plugin/plugin.json >/dev/null
```

Test install in a temporary Codex home:

```bash
mkdir -p /tmp/codex-stitch-test
CODEX_HOME=/tmp/codex-stitch-test codex plugin marketplace add .
CODEX_HOME=/tmp/codex-stitch-test codex plugin list --marketplace codex-stitch-designer
CODEX_HOME=/tmp/codex-stitch-test codex plugin add stitch-designer@codex-stitch-designer
```

## Pull Requests

- Keep changes focused.
- Prefer direct technical wording.
- Include the command output or manual verification you used.
- Do not include private Stitch project IDs, API keys, screenshots with confidential content, or customer data.
