---
title: Saito Wallet
description: Information about holding native Saito
published: true
date: 2024-02-29T06:10:03.591Z
tags: 
editor: markdown
dateCreated: 2024-02-29T00:06:48.906Z
---

# Saito Wallet

## Wrapped Tokens and Bridging

The Saito token exists in three forms: a wrapped [ERC20](https://etherscan.io/address/0xFa14Fa6958401314851A17d6C5360cA29f74B57B), a wrapped [BEP20](https://bscscan.com/address/0x3c6dad0475d3a1696b359dc04c99fd401be134da), and the native token. The wrapped tokens can be held on traditional wallets such as Metamask - in order to migrate wrapped tokens to a native Saito wallet, follow closely these [instructions](https://wiki.saito.io/en/tokenomics#migration-to-native-saito-token).

<span style="font-weight:bold; font-size:18px">THERE IS NO NEED TO BRIDGE</span> - there will never be any event which forces users to bridge their wrapped tokens. Wrapped Saito tokens will remain valid indefinitely. Avoid scammers claiming otherwise.

Before bridging, please take care to understand the token [persistence curve](https://wiki.saito.io/en/tokenomics#migration-to-native-saito-token) and what the *minimum* number of tokens is for the balance to stay intact. If less tokens are held than the curve designates for the date, they may be lost. See the [roadmap](https://wiki.saito.io/en/roadmap) for more information.

![token_persistence_curve.png](/token_persistence_curve.png)

## Native Wallet

Upon loading into a [Saito Application](https://wiki.saito.io/en/tech/applications) such as [Red Square](https://saito.io/redsquare/) a native wallet is automatically generated and can be accessed from the hamburger menu in the top right; From here the native Saito balance and ability to send Saito tokens are exposed.

<br>
<div style="display: flex; justify-content: center;">
<img src="/walletgif.gif" alt="screencast showing wallet menu with address, balance, backup and additional apps; accessed from 'Red Square' social media site">
</div>

This wallet is saved in the browser's cache and should be loaded up for future sessions automatically. Users with any attachment to a Saito account are encouraged to find and execute the **backup** functions in this same menu.


### Hot Wallet

One of the first differences users notice when using Saito for the first time is the lack of certain security rituals: creating a wallet and password, storing the seed phrase, and inputting credentials for signatures are not mandatory.

> *I seem to automatically enter my Saito Wallet by clicking on https://saito.io/redsquare.  Is that correct?  Because I don't have to enter any password to access my wallet, it seems very insecure.  Any thoughts about this?*

In the context of Saito's non-financial applications, these are intentional design decisions. Web 3 means users are digitally signing messages and transactions frequently - if users were required to input extra credentials for every digital signature, the user experience of many apps would degrade significantly.

The wallet used for day-to-day activities like [video calls](https://saito.io/videocall/) or [chat](https://saito.io/chat/) should not require significant amounts of Saito token to operate normally, and in fact, for the majority of the persistence curve timeline, most applications will remain free to use, requiring zero Saito tokens in a hot wallet.

One of the visions for Saito is that anyone can use the open internet, Web 3, with so few tokens required that risk in losing that amount and the incentive to hack it becomes negligible. The wallet everyone uses for the day-to-day internet, need not be a source of anxiety or risk to those users.

Hot wallets are inherently easier to use but less secure. Responsible Saito users are expected to keep a reasonable amount of tokens in their hot wallets at one time. Users who wish to use Saito as a secure token vault are encouraged to manage a cold wallet:

### Cold Wallets

**Note:** Users creating and storing wallets are responsible for their own keys. The Saito team nor the author of these instructions can take any responsibility for loss or theft of wallet credentials or funds.

Those who are insistent on the utmost security should keep their wrapped Saito on a hardware wallet until hardware wallet support arrives for native Saito.

For users who want more security for their native Saito Wallet, they are encouraged to generate a Saito Wallet which is to some degree isolated from frequent use and insecure computing. Starting with the easiest, ending with the most secure; some options for generating wallets with extra security:

Using a browser (easiest):
<ol>
  <li>Create a Saito Wallet and backup its private and public key.</li>
  <li>Save the key somewhere safe.</li>
  <li>Clear the browser cache and use the newly generated key for everyday use.</li>
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