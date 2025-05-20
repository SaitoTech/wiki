---
title: Saito Wallet
description: Information about holding native Saito
published: true
date: 2025-05-20T09:36:31.874Z
tags: 
editor: markdown
dateCreated: 2024-02-29T00:06:48.906Z
---

# Saito Wallet

<ol>
  <li><a href="#tokens">Can I Stake Saito?</a></li>
  <li><a href="#native">Where is my native Saito wallet?</a></li>
  <li><a href="#wallet">Cold wallet for native tokens?</a></li>
</ol>

## <div id="tokens"> Staking Saito?</div>

A portion of the transaction fees collected by the network (25%) are pushed into a network treasury that is issued to users who leave their SAITO unspent each loop. While this is not a traditional form of staking, it means that you can earn revenue by purchasing tokens, leaving them unspent, and encouraging others to use the network in ways that generate transaction fees.


## <div id="native"> Wallet Backups </div>

The first time you load any [Saito Application](https://wiki.saito.io/applications) in your browser, a native wallet is created which can be accessed by clicking on the hamburger menu in the top-right corner of most applications. From here you can see your native Saito balance and your balance and send Saito to other addresses.

This wallet is saved in the browser's cache and will be used repeatedly until it is purged or deleted. Because sometimes browsers like to purge cached content, users who hold non-trivial balances should **backup** their wallet. This involves extracting your private information from the browser so you can restore your wallet in the future.

To backup your wallet, access the Saito Wallet menu (as seen below) by clicking the hamburger icon in the top right of the screen and hitting the 'Account' button.

The buttons that allow you to backup your wallet are listed at the top of the overlay that will appear. Note that while you can save your private-key directly, if you wish to keep your friends list and any additional cryptographic keys your wallet has added (such as for other cryptocurrencies) you will need to use the "backup wallet" option, which will export that data in addition to your native Saito public and private-key.
<br>

<div style="text-align: center;">
<img src="/wallet-backup-p1.png" alt="Image 1" style="width:45%;">
<img src="/wallet-backup-p2.png" alt="Image 1" style="width:45%;">
<img src="/wallet-backup-p3.png" alt="Image 1" style="width:75%;">
</div>

### Hot Wallet

One of the first differences users notice when using Saito for the first time is the lack of certain security rituals: creating a wallet and password, storing the seed phrase, and inputting credentials for signatures are not mandatory. Sometimes this can seem odd:

> *I seem to automatically enter my Saito Wallet by clicking on https://saito.io/redsquare.  Is that correct?  Because I don't have to enter any password to access my wallet, it seems very insecure.  Any thoughts about this?*

In the context of Saito's non-financial applications, these are intentional design decisions. Web3 users sign messages and transactions frequently - if users were required to input extra credentials for every digital signature, the usability of many apps would degrade significantly.

The wallet used for day-to-day activities like [video calls](https://saito.io/videocall/) or [chat](https://saito.io/chat/) should not require significant amounts of Saito token to operate normally, and in fact, for most applications will effectively remain free to use, requiring zero Saito tokens in a hot wallet. Users who wish to use Saito as a secure token vault are encouraged to manage a cold wallet.

### <div id="wallet"> Cold Wallets </div>

**Note:** Users creating and storing wallets are responsible for their own keys. The Saito team nor the author of these instructions can take any responsibility for loss or theft of wallet credentials or funds.

Those who are insistent on the utmost security should keep their wrapped Saito on a hardware wallet until hardware wallet support arrives for native Saito.

For users who want more security for their native Saito Wallet, they are encouraged to generate a Saito Wallet which is to some degree isolated from frequent use and insecure computing. Starting with the easiest, ending with the most secure; some options for generating wallets with extra security:

Using a browser (easiest):
<ol>
  <li>Create a Saito Wallet and backup its private and public key.</li>
  <li>Save the key somewhere safe.</li>
  <li>Clear the browser cache and use a separate, newly generated key for everyday use.</li>
</ol>

Using a one-time browser:
<ol>
  <li>Fresh install a trusted, open source Web Browser to create and backup a key.</li>
  <li>Save the key somewhere safe.</li>
  <li>Uninstall the browser.</li>
</ol>

Using an offline device (most secure):
<ol>
  <li>Disable the networking capabilities of a device.</li>
  <li> <a href="https://wiki.saito.io/en/tech/installation">Install</a> Saito Node Software on that device.</li>
  <li>Save and optionally encrypt the backup on that device.</li>
  <li>Keep the device disconnected from all networking.</li>
</ol>

There are many tradeoffs involved in securing *any* sensitive data. These options should not be considered comprehensive - users are encouraged to do their own research when it comes to securely backing up data.

#### Storing Private Keys

Do not consider an everyday device as a secure store for backed up private keys. No device with networking should be considered full-proof and many, including smart phones, should be considered unsafe by default.

The most hack-proof place to store a private key is written or engraved on a physical object, or saved with encryption on a device which has never been and will never be connected to the internet. Consider too the tradeoff between security and recoverability - many users optimizing for security end up locking *themselves* out of their own keys.