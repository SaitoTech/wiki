---
title: SaitoArcade
description: 
published: true
date: 2024-08-17T01:54:01.156Z
tags: 
editor: markdown
dateCreated: 2023-02-19T20:49:30.032Z
---

# Arcade

![arcade-updated.png](/arcade-updated.png)[](/arcade.png)

[Saito Arcade](https://saito.io/arcade/) is an open source game engine that runs as a fully-distributed peer-to-peer blockchain application in the browser. The arcade and its numerous games not only laid the groundwork for a more diverse suite of peer-to-peer applications but represents what we believe to be some of the richest and most developed Web 3 experiences available to date by any project.

Many of the games leverage sophisticated cryptographic [techniques](#mentalPoker) to ensure fair elements of chance can exist without the need for any third-party oversight. Games on Saito require some of the most advanced use of Saito's cryptographic suite in order to ensure fair play in **genuine, peer-to-peer Web 3** (rather than a centrally hosted [Gacha-style](https://en.wikipedia.org/wiki/Gacha_game) game with token integrations). 

All games, whether they rely on complex cryptographic interactivity or are simple single-player experiences, benefit from the Saito Consensus's natural ability to fund open source applications by allowing service providers to earn their share of payment for network bandwidth or service provided.

For these reasons the [Web3 Foundation](https://web3.foundation/) has recognized the Saito Game Engine as a standard for open, cryptographic gaming, where it successfully [applied](https://github.com/w3f/Grants-Program/blob/master/applications/saito-game-protocol-and-engine.md) and fulfilled requirements for its grants program.

> I like this idea and think it provides something REALLY valuable to the ecosystem, and takes blockchain gaming in a very different (and good!) direction
> - *[Bill Laboon](https://github.com/w3f/Grants-Program/pull/73#issuecomment-713638248), Head of Education and Grants at Web3 Foundation*

### <div id="betterBusiness"> Better Business Models </div>

High  quality games with significant followings often struggle to make money from digital sales. Companies like Apple and Google force developers to list games at extremely low prices to compete for visibility in their distribution channels, and then restrict how publishers can collect money from users.

Web 2 forces publishers to revert to selling physical editions, merchandise, access to lightly-veiled gambling boxes or tokens of questionable utility and origin. Saito blurs the line between developer and publisher through new and better business models which rid developers of the need to pay rent to centralized, digital storefronts.

Saito Arcade, and Saito generally, is an open index of applications which any node, full or lite, can earn fees for serving to users. Open source developers can thus route their application's transactions into the network and earn the larger part of that fee. Developers can simply and permissionlessly become their own publishers. Saito [revolutionizes](https://medium.com/@0xluminous/the-future-of-open-source-software-7c77592f8f24) open source monetization.

The best games may still gravitate towards free-to-play models, but alternative services and their monetization are not to be restricted: leader-boards, rankings, match-making services, and the like. Game designers on Saito have the freedom to experiment with different choices. Some games may be better off integrating decentralized advertising networks, or collecting micro-payments on a game-by-game or even a turn-by-turn basis.

### <div id="mentalPoker"> Mental Poker Techniques </div>

For question of how the Saito Game Engine allows multiple parties to fairly agree on the state of truly random elements necessary for many games on the arcade, the answer begins with [Mental Poker](https://people.csail.mit.edu/rivest/pubs/SRA81.pdf):

  <br>
<div style="display: flex; justify-content: center;">
    <img src="/mentalpoker.png" alt="Mental Poker; Adi Shamir, Ronald L. Rivest and Leanard M. Adleman; MASSACHUSETTS INSTITUTE OF TECHNOLOGY; ABSTRACT Can two potentially dishonest players play a fair game of poker without using any cards-for example, over the phone? This paper provides the following answers: 1. No. (Rigorous mathemmatical proof supplied.) 2. Yes. (Correct and complete protocol given.); Once there were two 'mental chess' experts who had become tired of their passtime. 'Let's play 'Mental Mpoker,' for variety' suggested one. 'Sure' said the other,' Just let me deal!'">
</div>

Indeed, the most direct use of the techniques which authors Rivest, Shamir and Adleman (RSA) devised are most directly employed and enhanced in Saito's very own, peer-to-peer, Web 3 Poker - available to [play](https://saito.io/arcade) on the arcade or to [audit](https://github.com/SaitoTech/saito-lite-rust/tree/master/mods/poker) on Github.

Mental Poker exploits the commutative properties of public key encryption schemes to encrypt and shuffle a deck of cards using the keys of each player, and then progressively decrypt card when they must be revealed. A more complete explanation can be sought via [Wikipedia](https://en.wikipedia.org/wiki/Mental_poker).

The Saito Arcade has taken the principles of Mental Poker and generalized and extended the technique to support several adversarial players and to encode and integrate arbitrary values which extend far past a simple game of Poker. Titles like *Twilight Struggle* and *Settlers of Saitoa* are two flagship examples.







<!--

The [Saito Arcade](https://saito.io/arcade/) is an open-source game engine that runs as a fully-distributed peer-to-peer (p2p) blockchain application. All the games you can play run directly in the browser using p2p communications to send and receive game moves. Players interact only with each other - there is no central trusted server for deals or storing game data.

This is one of the first open-source software developed by the Saito team. It has been recognized by the Web3 Foundation as a standard for open cryptographic gaming.  Also, the arcade works as a showcase for the games/app/chat/forum/AppStore /etc. These are all applications that run in the browser and send-and-receive on-chain data.

-->


<!-- OLD VERSION
![](/arcade.png)

# Saito Arcade

The [Saito Arcade](https://saito.io/arcade/) is an open-source game engine that runs as a fully-distributed peer-to-peer (p2p) blockchain application. All the games you can play run directly in the browser using p2p communications to send and receive game moves. Players interact only with each other - there is no central trusted server for deals or storing game data.

This is one of the first open-source software developed by the Saito team. It has been recognized by the Web3 Foundation as a standard for open cryptographic gaming.  Also, the arcade works as a showcase for the games/app/chat/forum/AppStore /etc. These are all applications that run in the browser and send-and-receive on-chain data.
-->