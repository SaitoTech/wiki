---
title: Web3 Cryptocurrencies
description: Adding non-Saito Cryptocurrency support to Saito Applications
published: true
date: 2022-03-25T02:17:49.915Z
tags: 
editor: markdown
dateCreated: 2022-01-08T05:05:16.041Z
---

# Web3 Crypto Support

## Introduction

Saito makes it possible to write applications that use tokens and assets on other blockchains. You can code a game that requires a payment to be made in another cryptocurrency, for instance, or a wallet-plugin that lets you send and receive transactions stored on another chain. Saito does this by allowing wallets to install third-party "cryptocurrency modules" that provides a bridge to other networks.

In order to use another cryptocurrency with Saito applications, users need to have the appropriate module installed in their Saito wallet. Saito comes by default with bundles that provide support for a number of other cryptocurrencies like Polkadot and Elrond. Modules can easily be built that add support for other tokens as well -- if you are a developer interested in getting your favourite cryptocurrency supported get in touch!

## Using Cryptocurrencies within Saito Applications

Applications should not be coded which call web3 crypto modules directly. This creates brittle applications that stop working as soon as the user installs a different set of modules or switches to a different cryptocurrency. Code applications instead that work regardless of which cryptocurrency users prefer.

The Saito Wallet enables this by providing a standard interface for dealing with all non-Saito cryptocurrency modules. It simplifies the functions that cryptocurrency modules need to support to a minimal set that check account balances and send payments. The specific functions all cryptocurrency modules should support is:

```
cryptoMod.returnBalance(address);
cryptoMod.returnPrivateKey();
cryptoMod.returnAddress();
cryptoMod.sendPayment(amount, recipient);
cryptoMod.hasPayment(amount, recipient);
```

Application should not interact with these functions directly. Rather, interactions with external blockchains should be triggered by sending requests to the Saito Wallet, which provides several functions that simplify interactions with external blockchains and perform sanity-checks to attempt to prevent double-spends and other errors:

```
app.wallet.returnBalance();
app.wallet.returnPublicKey();
async app.wallet.sendPayment(senders=[], receivers=[], amounts=[], timestamp, mycallback, ticker);
async app.wallet.receivePayment(senders=[], receivers=[], amounts=[], timestamp, mycallback, ticker, tries=36, pollWaitTime=5000);
async app.wallet.returnPreferredCryptoBalances(addresses=[], mycallback=null, ticker="") {
```

The Saito Wallet class has all of these functions listed in its WEB# crypto section. At present the best documentation is the code itself, as these function names and their arguments are evolving. The current standard is now implemented by the Saito Game Engine and other applications and thus should be reasonably stable.
