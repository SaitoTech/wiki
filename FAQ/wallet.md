---
title: Saito Wallet
description: Information about holding native Saito
published: true
date: 2024-02-29T00:06:48.906Z
tags: 
editor: markdown
dateCreated: 2024-02-29T00:06:48.906Z
---

# Saito Wallet

## Wrapped Tokens and Bridging

The Saito token exists in three forms: a wrapped [ERC20](https://etherscan.io/address/0xFa14Fa6958401314851A17d6C5360cA29f74B57B), a wrapped [BEP20](https://bscscan.com/address/0x3c6dad0475d3a1696b359dc04c99fd401be134da), and the native token. The wrapped tokens can be held on traditional wallets such as Metamask - in order to migrate wrapped tokens to a native Saito wallet, follow closely these [instructions](https://wiki.saito.io/en/tokenomics#migration-to-native-saito-token).

<span style="font-weight:bold; font-size:18px">THERE IS NO NEED TO BRIDGE</span> - there will never be any event which forces users to bridge their wrapped tokens. Wrapped Saito tokens will remain valid indefinitely. Aviod scammers claiming otherwise.

Before bridging, please take care to understand the token [persistence curve](https://wiki.saito.io/en/tokenomics#migration-to-native-saito-token) and what the *minimum* number of tokens is for the balance to stay intact. If less tokens are held than the curve designates for the date, they may be lost. See the [roadmap](https://wiki.saito.io/en/roadmap) for more information.

![token_persistence_curve.png](/token_persistence_curve.png)

## Native Wallet

Upon loading into a [Saito Application](https://wiki.saito.io/en/tech/applications) such as [Red Square](https://saito.io/redsquare/) a native wallet is automatically generated and can be accessed from the hamburger menu in the top right; From here the native Saito balance and ability to send Saito tokens are exposed.

<br>
<div style="display: flex; justify-content: center;">
<img src="/walletgif.gif" alt="screencast showing wallet menu with address, balance, backup and additional apps; accessed from 'Red Square' social media site">
</div>

This wallet is saved in the browser's cache and should be loaded up for future sessions automatically. Users with any attachement to a Saito account are encouraged to find and execute the **backup** functions in this same menu.

### Security

One of the first differences users notice when using Saito for the first time is the lack of certain security practices: creating a wallet and password, storing the seed phrase, and inputting credentials for signatures are not mandatory.

> *I seem to automatically enter my Saito Wallet by clicking on https://saito.io/redsquare.  Is that correct?  Because I don't have to enter any password to access my wallet, it seems very insecure.  Any thoughts about this?*

In the context of Saito's non-financial applications, these are intentional design decisions. Web 3 means users are digitally signing messages and transactions frequently - if users were required to input extra credentials for every digital signature than many apps would become unusable.

### Hot vs. Cold Wallet

The wallet used for day-to-day activities like [video calls](https://saito.io/videocall/)