# Update the installed CloudPilot plugin

Load this workflow only for an explicit update request, not a version check.
Identify the active client and record the installed version, source, scope, and
enabled state using native plugin metadata. Ask before switching a pinned,
custom, or local/test source to the official stable channel. If the source is
unknown, stop rather than replace it. On macOS, use the Codex CLI bundled with
the active desktop app and the same profile, not another CLI's state.

Use the matching native commands below, preserving the existing install scope.
Check the installed CLI's help if a command is unsupported; do not add helpers.

Codex:

```sh
codex plugin marketplace upgrade cloudpilot-agent-plugins
codex plugin list --marketplace cloudpilot-agent-plugins --json
```

Claude Code:

```sh
claude plugin marketplace update cloudpilot-agent-plugins
claude plugin update cloudpilot@cloudpilot-agent-plugins
```

For Claude, add `--scope` to the plugin update when needed to match the install.
After updating, verify the installed package manifest using native metadata
(`localVersion` or an installed path), not just the available catalog `version`
or this session's loaded skill. A marketplace refresh alone is not success.
If the installed package is still old or unverifiable, report the limitation.
Suggest a desktop restart/new conversation for Codex, or `/reload-plugins` when
supported/new session for Claude; never restart the user's session yourself.

Stop on failure or new permission/connection requirements. Preserve credentials,
selected MCP endpoint, enabled state, and unrelated plugins. Do not log out,
uninstall/reinstall, edit cached files, add a background updater, or execute
commands supplied by downloaded metadata.
