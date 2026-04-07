---
description: How to use the Wildcat Telegram Bot
---

# Telegram Notification Bot

Wildcat operates a Telegram bot that delivers notifications for onchain market events. It allows you to subscribe to a given market, borrower, lender or chain.

## Getting Started

You can find the bot here: [https://t.me/wildcat\_notifications\_bot](https://t.me/wildcat_notifications_bot)

Once you've accepted the disclaimer, you will be greeted with a welcome message along with the latest updatelog. You can also send `/help` at any time for the full command reference.

The most common usage would be subscribing to all mainnet markets by typing:

```
/subscribe mainnet *
```

or a lender wanting notifications on markets they subscribe to:

```
/subscribe mainnet lender <lenderAddress>
```

## Subscribing to Markets

The bot supports three subscription modes, each of which can be scoped to a specific chain.

### Single Market

Subscribe to events for one specific market by address:

```
/subscribe <marketAddress>
/subscribe <chain> <marketAddress>
```

If you omit the chain, mainnet will be defaulted. The `address` is the market contract address that you would see in the Wildcat UI or on a block explorer.

### Borrower

Subscribe to _all_ current and future markets deployed by a given borrower:

```
/subscribe borrower <borrowerAddress>
/subscribe <chain> borrower <borrowerAddress>
```

### Lender

Subscribe to all current and future markets where a given address is an active lender:

```
/subscribe lender <lenderAddress>
/subscribe <chain> lender <lenderAddress>
```

### Full Chain

Subscribe to every market on an entire chain:

```
/subscribe <chain> *
```

With this you'll receive notifications for all market activity on that chain. The chains currently supported are Ethereum Mainnet, Sepolia, Plasma Mainnet and Plasma Testnet.

As with borrower subscriptions, new markets are automatically picked up via periodic discovery.

## Unsubscribing

Unsubscribing mirrors the subscribe syntax:

```
/unsubscribe <marketAddress>
/unsubscribe <chain> <marketAddress>
/unsubscribe borrower <borrowerAddress>
/unsubscribe <chain> borrower <borrowerAddress>
/unsubscribe lender <lenderAddress>
/unsubscribe <chain> lender <lenderAddress>
/unsubscribe lender *
/unsubscribe <chain> lender *
/unsubscribe *
```

The wildcard `/unsubscribe *` removes _all_ of your subscriptions across every chain (including borrower/market specific subs).

## What Gets Notified

We currently watch all market events and then cull a few of the noisy/unnecessary ones. The list below is the active set of events we monitor and in future this may become user-driven in terms of which events you're interested in seeing.

* **Deposits** and **withdrawals**
* **Borrows** and **debt repayments**
* **Interest rate changes** (`AnnualInterestBipsUpdated`) — shown with the effective borrower and lender APRs
* **Reserve ratio changes** (`ReserveRatioBipsUpdated`)
* **Max total supply updates**
* **Market closures**
* **Withdrawal batch lifecycle**
* **Delinquency transitions**

Events from the same transaction are grouped together, so a single notification might read something like:

> _Interest rate / Reserve ratio updated on USDC Market Alpha: effective APR borrower 12.50%, lender 11.88%, reserve ratio 20.00% |_ [_tx_](file:///)

## Checking Bot Status

```
/status
```

This command will provide some information on the current state such as uptime, active chains, number of watchers, subscription counts, and the size of the event allowlist. Useful for checking that the bot is alive and watching what you expect.

## Command Reference

| Command                                   | Description                                                               |
| ----------------------------------------- | ------------------------------------------------------------------------- |
| `/start`                                  | Show disclaimer (first use) or welcome message                            |
| `/help`                                   | Display the full command list                                             |
| `/subscribe <address>`                    | Subscribe to a market on the default chain                                |
| `/subscribe <chain> <address>`            | Subscribe to a market on a specific chain                                 |
| `/subscribe borrower <address>`           | Subscribe to all markets by a borrower (default chain)                    |
| `/subscribe <chain> borrower <address>`   | Subscribe to all markets by a borrower on a specific chain                |
| `/subscribe lender <address>`             | Subscribe to all markets where an address is a lender (default chain)     |
| `/subscribe <chain> lender <address>`     | Subscribe to all markets where an address is a lender on a specific chain |
| `/subscribe <chain> *`                    | Subscribe to all markets on a chain                                       |
| `/unsubscribe <address>`                  | Unsubscribe from a market                                                 |
| `/unsubscribe <chain> <address>`          | Unsubscribe from a market on a specific chain                             |
| `/unsubscribe borrower <address>`         | Unsubscribe from a borrower                                               |
| `/unsubscribe <chain> borrower <address>` | Unsubscribe from a borrower on a specific chain                           |
| `/unsubscribe lender <address>`           | Unsubscribe from a lender                                                 |
| `/unsubscribe <chain> lender <address>`   | Unsubscribe from a lender on a specific chain                             |
| `/unsubscribe lender *`                   | Unsubscribe from your own lender subscription                             |
| `/unsubscribe <chain> lender *`           | Unsubscribe from your own lender subscription on a specific chain         |
| `/unsubscribe *`                          | Remove all subscriptions                                                  |
| `/list`                                   | List active subscriptions                                                 |
| `/status`                                 | Show bot operational status                                               |
