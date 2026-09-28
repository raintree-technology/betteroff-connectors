# BetterOff connectors

Connect an eligible BetterOff household to Codex or Claude Code. Version 0.2.0 exposes 19 financial tools on BetterOff's production MCP server: 16 reads and three correction proposals. Reads cover accounts, net worth, cash flow, recurring items, holdings, transactions, spending, debts, observations, and financial activity. Each proposal opens an authenticated BetterOff review page; the connector cannot apply a correction, move money, or place a trade.

## Codex

```sh
codex plugin marketplace add raintree-technology/betteroff-connectors
codex plugin add betteroff@betteroff
```

## Claude Code

```sh
claude plugin marketplace add raintree-technology/betteroff-connectors
claude plugin install betteroff@betteroff
```

Authorize the BetterOff connection when prompted. Access requires an eligible household owner and expires after at most 30 days. The consent screen lists the household and requested permissions. Disconnect under **Settings → Agent connections** in BetterOff.

Codex and Claude Code have discovered all 19 tools after production consent. Complete client verification and directory approval remain pending. See [the plugin guide](plugins/betteroff/README.md) for the data and approval boundaries.
