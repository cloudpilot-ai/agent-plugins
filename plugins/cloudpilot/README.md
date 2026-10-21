# CloudPilot Plugin (Preview)

This package contains one shared knowledge skill, Codex and Claude Code
manifests, and a production MCP connection. For customer installation, see the
[repository guide](https://github.com/cloudpilot-ai/agent-plugins#install).

## Contents

- `skills/cloudpilot-knowledge/SKILL.md`: retrieval and read-only reasoning.
- `.codex-plugin/plugin.json`: Codex compatibility manifest.
- `.claude-plugin/plugin.json`: Claude Code manifest.
- `.mcp.json`: production connection to `https://mcp.cloudpilot.ai/mcp`.
- `assets/logo.svg`: official [CloudPilot logo](https://assets.cloudpilot.ai/favicon/favicon.svg), bundled for Codex plugin branding.
- `evaluation.md`: generic manual cases and acceptance boundaries.
- `testing/mcp.local.json`: optional developer-only localhost connection.

Product documentation is retrieved from MCP rather than copied into the package.
The skill distinguishes fetched guidance from live observations and inference.
This milestone does not validate configuration-recommendation strategies.
The read-only workflow is not a replacement for server-side authorization.

## Local testing

Use a separate staging copy of this repository. Before registering that copy's
marketplace, replace only its plugin `.mcp.json` with `testing/mcp.local.json`.
The resulting endpoint must be `http://127.0.0.1:8787/mcp`; start a compatible
local backend separately. Do not change the tracked production configuration.

Register the staging repository by its local path with
`codex plugin marketplace add /absolute/path/to/staging-repository` or
`claude plugin marketplace add /absolute/path/to/staging-repository`, then install
CloudPilot using the respective client's plugin flow. Authorize the selected
local connection and inspect its tools. Do not fall back to production if the
local service or knowledge tools are unavailable. Use a fresh conversation and
the [evaluation cases](evaluation.md); do not load a second standalone skill.

## Validate and package

Validate both the plugin and marketplace with Claude Code before submitting:

```sh
claude plugin validate /absolute/path/to/repository/plugins/cloudpilot
claude plugin validate /absolute/path/to/repository
```

Also check both catalogs resolve to this package and the Codex manifest resolves
its skill and MCP paths. These structural checks do not prove runtime behavior
or production knowledge-tool availability.

For a ZIP, run from the plugin directory, placing the archive outside the repo:

```sh
python3 -m zipfile -c /absolute/path/to/output/cloudpilot-0.1.1.zip \
  .codex-plugin .claude-plugin .mcp.json assets skills README.md evaluation.md
python3 -m zipfile -t /absolute/path/to/output/cloudpilot-0.1.1.zip
```

Build customer archives only from a clean production-configured checkout.
Verify the archived endpoint is the production URL. Do not include `testing/`,
local configuration, authentication state, generated outputs, or transcripts.
There are no install hooks, executable helpers, or bundled credentials.
