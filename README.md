# BetterOff connectors

Connect an eligible BetterOff household to Codex or Claude Code. The connector reads accounts, net worth, cash flow, recurring bills, holdings, transactions, and debts. It cannot move money or change financial data.

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

Authorize the BetterOff connection when prompted. Access requires a BetterOff household owner with an eligible account. Disconnect in BetterOff settings.
