---
title: Saito Wallet
description: Cryptocurrencies in Saito
published: true
date: 2025-05-19T15:14:10.185Z
tags: 
editor: markdown
dateCreated: 2024-08-22T15:17:12.953Z
---

# Saito Wallet

The Saito Wallet is a general application which adds support for multiple non-Saito cryptocurrencies to the Saito Wallet. The wallet is automatically integrated into the Saito ecosystem, allowing staking of crypto on games in the arcade, sending money to friends via chat and various other feature available to native Saito.

<img src="/wallet.png" style="max-width: 600px;">

Saito makes it possible to write applications that use tokens and assets on other blockchains. You can code a game that requires a payment to be made in another cryptocurrency, for instance, or a plugin that reads data on other chains. Saito does this by supporting third-party "cryptocurrency modules" that provide a bridge to other networks.

Once your wallet has these modules installed, you will have the option to enable them, at which point the Saito Wallet will provide you with a network address and allow you to send-and-receive tokens on those networks. Right now Saito includes support for Bitcoin and Ethereum by default, but we expect to expand the list as usage grows. The wallet along with the whole Saito software suite is open source, developers interested in getting their favourite cryptocurrency supported are free to do so.

## Getting Started

Once you have installed a cryptocurrency module into your Saito Wallet, you will be able to see the new crypto as an option in the dropdown crypto-select available in your wallet. Simple change to the cryptocurrency that you wish to you. The QRCode in your wallet will update along with the address provided by that module.

You can now use the standard Saito Wallet tools to send and receive crypto. Information on confirmations required and fees required will be provided by the module directly to you via the standard functionality of the Saito Wallet.

## Trust Assumptions?

It is common for users to ask how exactly Saito is supporting third party transfers. Have we invented a decentralized way of making off-chain payments on other networks? The straightforward answer is "no".

How exactly third party modules work depend on the modules themselves. Saito is simply a data network that passes requests between users. This makes it suitable as an application layer for any other network design, whether that is an L1 network or an L2 rollup or a BTC lightning client.

The modules developed by our own team span the range from completely trustless to relying on third-party APIs and offering fee-free transfers. For a completely trustless solution, you would want your module to actually serve as a full client on the remove network. Most users prefer modules with simplified trust assumptions, such as keeping the private keys necessary to spend tokens secured in their Saito Wallet but using an API access point on the remote network to receive and process their transactions once they are made.

At the end of the day, every crypto module on Saito can make its own security/usability tradeoffs at the behest of users and developers. Saito does not force developers to use any particular method when defining how their modules work.