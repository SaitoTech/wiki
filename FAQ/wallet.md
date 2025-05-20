---
title: Saito Wallet
description: Information about holding native Saito
published: true
date: 2025-05-20T11:06:04.800Z
tags: 
editor: markdown
dateCreated: 2024-02-29T00:06:48.906Z
---

# Saito Wallet Helpo

<ol>
  <li><a href="#native">Where is my Saito wallet?</a></li>
  <li><a href="#backup">How to backup my Saito wallet?</a></li>
  <li><a href="#wallet">How to make a cold wallet?</a></li>
</ol>

## <div id="native"> Where is my Saito Wallet?</div>

The first time you run a [Saito Application](https://wiki.saito.io/applications) in your browser, a Saito wallet will be created inside your browser which can be accessed by clicking on the hamburger menu in the top-right corner. From here you can see your Saito balance and network address.

This wallet used repeatedly until your browser cache is purged or deleted. To avoid loss of funds, users who hold non-trivial balances should **backup** their wallet. This involves extracting your private information from the browser as a file you can use to restore it in the future.

<div style="text-align: center;margin-top:1rem">
<img src="/wallet-backup-p1.png" alt="Image 1" style="width:80%;">
</div>


## <div id="backup"> How to backup my Saito Wallet?</div>

To backup your wallet, access the Saito Wallet menu by clicking the hamburger icon and hitting the 'Account' button. on the slide-in menu. This will pull up an overlay with details on your account as well as the modules you are running.

The easiest way to backup your wallet is simply to copy the private-key somewhere safe. If you wish to keep your friends list and any additional cryptographic keys created by Saito applications (such as access keys for other cryptocurrencies) use the "backup wallet" option at the top of the over. This will export ALL of the data in your wallet to file you can use to restore it.

<br>

<div style="text-align: center;with:100%">
<img src="/wallet-backup-p2.png" alt="Image 1" style="width:49%;">
<img src="/wallet-backup-p3.png" alt="Image 1" style="width:49%;">
</div>

## <div id="native"> How to make a Cold Wallet?</div>

One of the first differences users notice when using Saito for the first time is the lack of certain security rituals: creating a wallet and password, storing the seed phrase, and inputting credentials for signatures are not mandatory. Sometimes this can seem odd:

> *I seem to automatically enter my Saito Wallet by clicking on https://saito.io/redsquare.  Is that correct?  Because I don't have to enter any password to access my wallet, it seems very insecure.  Any thoughts about this?*

Providing total control to users is an intentional design decision -- many PKI applications require the ability for the wallet to quickly sign and send data to peers. If users are required to input extra credentials for every digital signature, the usability of these applications would degrade significantly. For this reason, we recommend those unfamiliar with Saito or unsure of the security of the applications they are installing not to keep large amounts of SAITO in a hot wallet. Cold wallets may be created as follows:

Using a browser (easiest):

<ol>
  <li>Create a Saito Wallet and backup its private and public key.</li>
  <li>Save the key somewhere safe.</li>
  <li>Clear the browser cache. and use a separate, newly generated key for everyday use.</li>
</ol>