# <picture><source media="(prefers-color-scheme: dark)" srcset="assets/betteroff-mark-white.svg"><img src="assets/betteroff-mark-graphite.svg" alt="" width="48" height="48" align="absmiddle"></picture> BetterOff connectors

Ask Codex, Claude Code, Hermes Agent, Muse Code, OpenClaw, or Pi about the financial records you connect to BetterOff. The connector can read approved household data and prepare corrections for your review. It cannot apply a correction, move money, or place a trade.

## Before you start

You need a BetterOff household owner account and one of those clients. Connect at least one supported account or wallet in BetterOff to ask questions about your finances.

## Install the connector

Run the commands for your client in a terminal.

### Codex

```sh
codex plugin marketplace add raintree-technology/betteroff-connectors
codex plugin add betteroff@betteroff
```

### Claude Code

```sh
claude plugin marketplace add raintree-technology/betteroff-connectors
claude plugin install betteroff@betteroff
```

### Hermes Agent

Add the server to `~/.hermes/config.yaml`. With `trust: untrusted`, Hermes asks you before any tool that is not marked read-only, including the three proposal tools, runs:

```yaml
mcp_servers:
  betteroff:
    url: "https://api.betteroff.finance/mcp"
    auth: oauth
    trust: untrusted
    sampling:
      enabled: false
```

Then sign in and install the skill:

```sh
hermes mcp login betteroff
hermes skills install raintree-technology/betteroff-connectors/plugins/betteroff/skills/household-review
```

### Muse Code

Add the server to `~/.config/muse/settings.json`. Keep `"schema_version": 1` and merge the `mcp_servers` block into any existing settings:

```json
{
  "schema_version": 1,
  "mcp_servers": {
    "betteroff": {
      "transport": "streamable_http",
      "url": "https://api.betteroff.finance/mcp",
      "mode": "optional"
    }
  }
}
```

Then sign in and install the skill from a clone of this repository:

```sh
muse mcp login betteroff
muse skills install ./plugins/betteroff/skills/household-review --scope user
```

Do not choose **Always allow** for the proposal tools. Each proposal should get its own approval.

### OpenClaw

Use OpenClaw only in a direct chat with the household owner. By default, OpenClaw shares one BetterOff sign-in with everyone who can message the agent, so anyone in a group chat could read your household finances.

```sh
openclaw mcp add betteroff --url https://api.betteroff.finance/mcp --transport streamable-http --auth oauth
openclaw mcp configure betteroff --approval prompt
openclaw mcp login betteroff
openclaw mcp doctor betteroff --probe
```

Then install the skill from a clone of this repository:

```sh
openclaw skills install ./plugins/betteroff/skills/household-review --global
```

Sign-in returns to `http://127.0.0.1:8989/oauth/callback`. If the Gateway runs on another machine, finish with `openclaw mcp login betteroff --code <code>`. OpenClaw's built-in agent can run the proposal tools without asking, but nothing changes until you approve the proposal in BetterOff.

### Pi

Requires Pi 0.99.0 or later.

```sh
pi mcp add betteroff --url https://api.betteroff.finance/mcp --exposure direct
pi mcp login betteroff
pi mcp list
```

Then copy the skill from a clone of this repository:

```sh
cp -R plugins/betteroff/skills/household-review ~/.agents/skills/
```

Run `/reload` in an open Pi session to pick up the server. Pi runs tools without asking. The proposal tools only prepare a correction, and nothing changes until you approve it in BetterOff.

When your client prompts you, sign in to BetterOff. Review the household and requested permissions before selecting **Allow access**. The data returned by a tool is shared with the client you connected.

Try asking:

- “Show my household overview and flag missing or out-of-date data.”
- “Compare my spending by category this month with the same days last month.”
- “List my debts and tell me which terms are missing.”

Results can be incomplete when a source is not connected or is out of date. Check available dates and warnings before relying on a result.

## What the connector can do

Version 0.3.0 provides 19 tools:

- **16 financial reads** cover accounts, net worth, cash flow, recurring items, holdings, transactions, spending, debts, observations, and financial activity.
- **Three correction proposals** cover payment categories, recurring items, and debt classifications.

## Approval and disconnection

Preparing a proposal changes no financial record. Open its authenticated BetterOff review page to choose the scope and approve any change. The connector cannot approve or apply it for you.

Only an eligible household owner can grant access. Access lasts up to 30 days. You can disconnect sooner in [BetterOff Agent connections](https://app.betteroff.finance/settings/agents).

For the MCP endpoint, data boundaries, and correction flow, read the [connector guide](plugins/betteroff/README.md). For help, [contact BetterOff](https://betteroff.finance/contact).
