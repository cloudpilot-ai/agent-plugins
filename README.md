# CloudPilot Agent Plugins

Preview plugins for explaining CloudPilot product fields and behavior with
official documentation and relevant read-only MCP data. Codex and Claude Code
share one lightweight skill; each client has its own plugin manifest.

The current milestone covers documentation retrieval, field explanations, and
read-only observations. Validated configuration-recommendation strategies are
planned for a later milestone. This package does not apply settings or perform
cluster operations.

## Prerequisites

- A client version that supports plugin marketplaces and remote HTTP MCP.
- Your own CloudPilot account and permission to access the selected organization.
- A CloudPilot MCP deployment exposing the `search` and `fetch` knowledge tools.
  Backend releases are independent of this plugin. Installing the plugin or
  completing OAuth does not prove those tools are available.

The bundled production endpoint is `https://mcp.cloudpilot.ai/mcp`. Sign in
through your client's OAuth flow and verify the account and organizations before
granting access. Do not copy tokens into the plugin or repository.

## Install

The repository commands below use the default branch after the package is merged.
For an unmerged preview or local backend, use the checkout workflow in the
[package guide](plugins/cloudpilot/README.md#local-testing).

### Codex

Register the repository marketplace:

```sh
codex plugin marketplace add cloudpilot-ai/agent-plugins
```

Restart the desktop app, open Plugins, choose **CloudPilot Plugins (Preview)**,
and install **CloudPilot**. Complete the connection's authorization flow when
requested. See the [official packaging documentation](https://developers.openai.com/plugins/build/plugins)
for client-specific marketplace support.

Start a fresh conversation and explicitly select the installed CloudPilot
knowledge skill for an initial test. Natural questions can also select the skill,
but selection depends on the client and prompt; it is not guaranteed.

### Claude Code

Run these commands in a shell:

```sh
claude plugin marketplace add cloudpilot-ai/agent-plugins
claude plugin install cloudpilot@cloudpilot-agent-plugins
```

Start a new session, use `/mcp` to inspect and authorize the CloudPilot connection,
then invoke `/cloudpilot:cloudpilot-knowledge`. See the
[official marketplace documentation](https://code.claude.com/docs/en/plugin-marketplaces).

Avoid loading a standalone copy of the same skill or enabling a duplicate MCP
connection during testing. Preserve existing credentials and unrelated services;
do not clear global authentication to troubleshoot this plugin.

## Try it

- What does `minNonSpotReplicas` mean in CloudPilot?
- How do CPU used, requested, allocatable, and provisioned differ?
- Does enabling Image Accelerator prove images are pulled from peers?
- For my selected cluster, explain its NodePool consolidation settings.

Documentation-only questions should not read cluster inventory. Cluster-specific
questions need a selected connection and relevant read permissions. If knowledge
tools or required evidence are missing, the expected response is an explicit
limitation, not an invented answer or a switch to another environment.

Connecting MCP alone does not install this skill. The plugin bundles the skill
and connection configuration, while authorization remains an interactive user
step. This repository marketplace is not a listing in a client's public directory.

## Maintenance

Keep procedural guidance in the shared skill, and product facts in the official
documentation served by MCP. Update plugin manifests together when releasing a
package change. Use the [package guide](plugins/cloudpilot/README.md) for packaging
and local testing and the [evaluation cases](plugins/cloudpilot/evaluation.md)
for behavioral checks. Do not commit credentials, customer data, or transcripts.
