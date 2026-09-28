<p align="center">
  <img src="plugins/betteroff/icon.png" alt="BetterOff logo" width="96">
</p>

# BetterOff for Codex and Claude Code

Ask Codex or Claude Code about the financial records you connect to BetterOff. The connector can read approved household data and prepare corrections for your review. It cannot apply a correction, move money, or place a trade.

## Before you start

You need a BetterOff household owner account and Codex or Claude Code. Connect at least one supported account or wallet in BetterOff to ask questions about your finances.

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

When your client prompts you, sign in to BetterOff. Review the household and requested permissions before selecting **Allow access**. The data returned by a tool is shared with the client you connected.

Try asking: “Show my household overview and flag missing or out-of-date data.” Results can be incomplete when a source is not connected or is out of date. Check available dates and warnings before relying on a result.

## What the connector can do

Version 0.2.0 provides 19 tools:

- **16 financial reads** cover accounts, net worth, cash flow, recurring items, holdings, transactions, spending, debts, observations, and financial activity.
- **Three correction proposals** cover payment categories, recurring items, and debt classifications.

## Approval and disconnection

Preparing a proposal changes no financial record. Open its authenticated BetterOff review page to choose the scope and approve any change. The connector cannot approve or apply it for you.

Only an eligible household owner can grant access. Access lasts up to 30 days. You can disconnect sooner in [BetterOff Agent connections](https://app.betteroff.finance/settings/agents).

For the MCP endpoint, data boundaries, and correction flow, read the [connector guide](plugins/betteroff/README.md). For help, [contact BetterOff](https://betteroff.finance/contact).
