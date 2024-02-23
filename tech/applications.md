---
title: Saito Apps
description: 
published: true
date: 2024-02-23T00:55:51.912Z
tags: 
editor: markdown
dateCreated: 2022-12-21T01:40:41.364Z
---

# Saito Applications

<!-- INTRO - (mention importance of p2p and true web3) -->

<ul style="color:">
  <li> 1. <a style="text-decoration:none" href="#1"> Gaming </a> </li>
  <ul>
    <li> <a style='text-decoration:none' href='#1a'> Better Business Models </a> </li>
    <li> <a style='text-decoration:none' href='#1a'> Mental Poker </a> </li>
  </ul>
  <br>
  <li> 2. <a style="text-decoration:none" href="#2"> P2P Social Media </a> </li>
  <li> 3. <a style="text-decoration:none" href="#3"> Build Your Own </a> </li>
  <ul>
    <li> 3a. <a style="text-decoration:none" href="#3a"> 3a </a> </li>
    <li> 3b. <a style="text-decoration:none" href="#3b"> 3b </a> </li>
    <li> 3c. <a style="text-decoration:none" href="#3b"> 3c </a> </li>
    <li> 3d. <a style="text-decoration:none" href="#3b"> 3d </a> </li>
  </ul>
  <br>
  <li> 4. <a style="text-decoration:none" href="#3b"> d</a> </li>
</ul>

## Gaming

The [Saito Arcade](https://saito.io/arcade/) is an open source game engine that runs as a fully-distributed peer-to-peer blockchain application in the browser. Many of the games leverage sophisticated cryptographic [techniques](#mental-poker) to ensure fair elements of chance can exist without any third-party oversight.



Games on Saito require some of the most advanced use of Saito's cryptographic suite in order to ensure fair play in **genuine, peer-to-peer Web 3** (rather than a centrally hosted [Gacha-style](https://en.wikipedia.org/wiki/Gacha_game) game with token integrations). 
The Arcade not only laid the groundwork for a more diverse suite of peer-to-peer applications but represents what we believe to be some of the richest Web 3 experiences online.

All games, whether they rely on complex cryptographic interactivity or are simple single-player experiences, benefit from the Saito Consensus's natural ability to fund open source applications by allowing service providers to earn their share of payment for network bandwidth or service provided.

For these reasons the [Web3 Foundation](https://web3.foundation/) has recognized the Saito Game Engine as a standard for open, cryptographic gaming, where it successfully [applied](https://github.com/w3f/Grants-Program/blob/master/applications/saito-game-protocol-and-engine.md) and fulfilled requirements for its grants program.

> I like this idea and think it provides something REALLY valuable to the ecosystem, and takes blockchain gaming in a very different (and good!) direction
> - *[Bill Laboon](https://github.com/w3f/Grants-Program/pull/73#issuecomment-713638248), Head of Education and Grants at Web3 Foundation*

### Better Business Models

High  quality games with significant followings often struggle to make money from digital sales. Companies like Apple and Google force developers to list games at extremely low prices to compete for visibility in their distribution channels, and then restrict how publishers can collect money from users.

Instead of forcing publishers to revert to selling physical editions, merchandise, access to lightly-vieled gambling boxes or tokens of questionable utility and origin, Saito blurs the line between developer and publisher through new and better business models which rid themselves of the need to pay rent to centralized, digital storefronts.

Saito Arcade, and Saito generally, is an open index of applications which any node, full or lite, can earn fees for serving to users. Open source developers can thus route their application's transactions into the network and earn part of that fee, all while keeping an open and direct line between them and their users. Saito [revolutionizes](https://medium.com/@0xluminous/the-future-of-open-source-software-7c77592f8f24) open source monetization.

The best games may still gravitate towards free-to-play models, but alternative services and their monitization are not to be restricted: leaderboards, rankings, match-making services, and the like. Game designers on Saito have the freedom to experiment with different choices. Some games may be better off integrating decentralized advertising networks, or collecting micro-payments on a game-by-game or even a turn-by-turn basis.

### Mental Poker Technique

For question of how the Saito Game Engine allows multiple parties to fairly agree on the state of truly random elements necessary for many games on the arcade, the answer begins with [Mental Poker](https://people.csail.mit.edu/rivest/pubs/SRA81.pdf):

![mentalpoker.png](/mentalpoker.png)

Indeed, the most direct use of the techniques which authors Rivest, Shamir and Adleman (RSA) devised are most directly employed and enchanced in Saito's very own, peer-to-peer, Web 3 Poker - available to [play](https://saito.io/arcade) on the arcade or to [audit](https://github.com/SaitoTech/saito-lite-rust/tree/master/mods/poker) on Github.

Mental Poker exploits the commutative nature properties of most public key encryption schemes to encrypt a deck of cards multiple times using the keys of the players who then shuffle the cards, ignorant of their unencrypted values and obscuring the order in which they were sent. A more complete explanation can be sought via [Wikipedia](https://en.wikipedia.org/wiki/Mental_poker).

The Saito Arcade has taken the principles of Mental Poker and generalized and extended the technique to support several adversarial players and to encode and integrate arbitrary values which extend far past a simple game of Poker. Titles like Twilight Struggle and Settlers of Saitoa are two flagship examples. Because Saito solves the *man-in-the-middle attack* (MITM) without the need for a trusted party, it is in the unique position to apply the techniques without sweeping related trust assumptions under the rug.

The entire process, from peer discovery to setup to gameplay benefits uniquely from taking place on a universal broadcast layer like Saito blockchain. Whereas many of these steps require a trusted party like Facebook to prevent MITM attacks, Saito does it trustlessly and in the open. While Mental Poker removes trust assumptions from the game, Saito removes trust assumptions from the network infrastructure, and thus can serve a secure and affordable Web 3 experience through every layer of interaction.

For a more technical dive into how the current suite of games on Saito Arcade work, pay a visit to our [Github Repository](https://github.com/SaitoTech/saito-lite-rust/blob/dbd9d622c8cb69c682045b780c63207eed8d7bf1/docs/gaming/saito-game-engine/readme.md) or ask a question on Saito's social media platform [Red Square](https://saito.io/redsquare/).


## Social Media

## Build Your Own

Those interested in building on Saito should start [here](/tech/building_apps). The SDK used to make the all apps on this page is fully available for anyone to begin using. It has built-in functions to interact with the blockchain, perform basic cryptography, establish peer-to-peer connections and more. Applications are built using Javascript and run in the browser.

Many of the beloved Saito apps like [Beleaguered Castle](/tech/applications/BeleagueredCastle) and even [Red Square](/tech/applications/RedSquare) were built or spurred to life by community members. Any developers seeking assistance or who want to offer feedback can reach the lead developers on [Red Square](https://saito.io/redsquare/), [Saito Community Chat](https://saito.io/chat/), [Saito Community Telegram](https://t.me/SaitoIO) or make an [issue](https://github.com/SaitoTech/saito-lite-rust/issues) on the Github. The team is thrilled to see what the community builds and values developer feedback.

<!--
![](/apps.png)

## Core Apps

Saito Applications are programs that run directly in your browser. These applications have a built-in wallet and use the Saito network to communicate with peers. See our full list of [available programs](https://github.com/SaitoTech/saito-lite-rust/tree/master/mods) or our [tutorials](/tech/tutorials) on how to develop a module from scratch, or check out our flagship applications below.


|     |     |     |
| --- | --- | --- |
|     | [Saito Arcade](/tech/applications/arcade) | [Red Square](/tech/applications/RedSquare) |
|     | [Chat](/tech/applications/chat) | [Encrypt](/tech/applications/encrypt) |
|     | [Video Call](/tech/applications/VideoCall)| [Registry (DNS)](/tech/applications/Registry (DNS)) |

## Games

There is a good amount of games running on the Saito platform now, and more to come that are currently in development, some of them have been made for members of the community. With Saito being an open-source project that is delighted to receive apps from other developers to run them in the network, this is just the tip of the iceberg for what is to come.

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
|     | [Chess](/tech/applications/chess) | [Blackjack](/tech/applications/Blackjack) |     | [Beleaguered Castle](/tech/applications/BeleagueredCastle) |     |
|     | [Epidemic](/tech/applications/epidemic) | [Mahjong](/tech/applications/Mahjong) |     | [Nintendo 64 (Emulator)](/tech/applications/n64) |     |
|     | [Poker](/tech/applications/poker) | [Quake 3](/tech/applications/quake3) |     | [Red Imperium](/tech/applications/redImperium) |     |
|     | [Solitrio](/tech/applications/solitrio) | [Saito Realm](/tech/applications/realm) |     | [Settlers of Saitoa](/tech/applications/settlers) |     |
|     | [Shogun](/tech/applications/Shogun) | [Wordblocks](/tech/applications/wordblocks) |     | [Saito Mania](/tech/applications/SaitoMania) |     |
|     | [Spider](/tech/applications/spider) | [Wuziqi](/tech/applications/wuziqi) |     | [Twilight Struggle](/tech/applications/twilightStruggle) |     |
-->