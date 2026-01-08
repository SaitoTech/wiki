---
title: Saito Wallet
description: Cryptocurrencies in Saito
published: true
date: 2025-09-30T17:54:47.148Z
tags: 
editor: markdown
dateCreated: 2024-08-22T15:17:12.953Z
---

# Saito Wallet

The Saito Wallet adds support for multiple non-Saito cryptocurrencies to the Saito Wallet and automatically integrates them into the broader Saito ecosystem.

Tips for [backing up a Saito wallet](/tutorials/user/wallet).

<br />
<img src="/wallet.png" style="max-width: 600px;">

Saito makes it possible to write applications that use tokens and assets on other blockchains. You can code a game that requires a payment to be made in another cryptocurrency, for instance, or a plugin that reads data on other chains. Saito does this by supporting third-party "cryptocurrency modules" that provide a bridge to other networks.

Once your wallet has these modules installed, you will have the option to enable them, at which point the Saito Wallet will provide you with a network address and allow you to send-and-receive tokens on those networks. At the time of writing our node supports Bitcoin, Ethereum and MultiverseX, and we expect that list to grow. 

The wallet is open source, and developers wishing to expand the list of available currencies beyond our version of the wallet are encouraged to do so.

## Getting Started

Once you have installed a cryptocurrency module into your Saito Wallet, you will be able to see the new crypto as an option in the dropdown crypto-select available in your wallet. Simply change to the cryptocurrency that you wish to create a key-pair for. The QRCode in your wallet will update along with the address provided by that module.

You can now use the standard Saito Wallet tools to send and receive crypto. Information on confirmations required and fees required will be provided by the module directly to you via the standard functionality of the Saito Wallet.

Be sure to back up your wallet after adding a new currency! You will see a reminder to do so after adding a currency.