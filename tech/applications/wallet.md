---
title: Saito Wallet
description: Cryptocurrencies in Saito
published: true
date: 2024-09-17T10:57:37.309Z
tags: 
editor: markdown
dateCreated: 2024-08-22T15:17:12.953Z
---

# Saito Wallet

<img src="/wallet.png" style="max-width: 600px;">

Saito makes it possible to write applications that use tokens and assets on other blockchains. You can code a game that requires a payment to be made in another cryptocurrency, for instance, or a plugin that reads data on other chains. Saito does this by supporting third-party "cryptocurrency modules" that provide a bridge to other networks.

Once your wallet has these modules installed, you will have the option to enable them, at which point the Saito Wallet will provide you with a network address and allow you to send-and-receive tokens on those networks. Right now Saito includes support for Bitcoin and Ethereum by default, but we expect to expand the list as usage grows -- if you are a developer interested in getting your favourite cryptocurrency supported get in touch.

- Wallet [source code.](https://github.com/SaitoTech/saito-lite-rust/tree/master/mods/wallet)


## Getting Started

Once you have installed a cryptocurrency module into your Saito Wallet, you will be able to see the new crypto as an option in the dropdown crypto-select available in your wallet. Simple change to the cryptocurrency that you wish to you. The QRCode in your wallet will update along with the address provided by that module.

You can now use the standard Saito Wallet tools to send and receive crypto. Information on confirmations required and fees required will be provided by the module directly to you via the standard functionality of the Saito Wallet.

Once you have a third-party crypto module enabled, you 


## Trust Assumptions?

It is common for users to ask how exactly Saito is supporting third party transfers. Have we invented a decentralized way of making off-chain payments on other networks? The straightforward answer is "no".

How exactly third party modules work depend on the modules themselves. Saito is simply a data network that passes requests between users. This makes it suitable as an application layer for any other network design, whether that is an L1 network or an L2 rollup or a BTC lightning client.

The modules developed by our own team span the range from completely trustless to relying on third-party APIs and offering fee-free transfers. For a completely trustless solution, you would want your module to actually serve as a full client on the remove network. Most users prefer modules with simplified trust assumptions, such as keeping the private keys necessary to spend tokens secured in their Saito Wallet but using an API access point on the remote network to receive and process their transactions once they are made.

