---
title: Saito Apps
description: 
published: true
date: 2024-02-23T03:57:52.492Z
tags: 
editor: markdown
dateCreated: 2022-12-21T01:40:41.364Z
---

# Saito Applications

<!-- INTRO - (mention importance of p2p and true web3) -->
<ul style="color:">
  <li>  <a style="text-decoration:none" href="#gaming"> Gaming </a> </li>
  <ul>
    <li> <a style='text-decoration:none' href='#betterBusiness'> Better Business Models </a> </li>
    <li> <a style='text-decoration:none' href='#mentalPoker'> Mental Poker </a> </li>
  </ul>
  <br>
  <li>  <a style="text-decoration:none" href="#2"> P2P Social Media </a> </li>
  <ul>
  	<li>  <a style="text-decoration:none" href="#redSquare"> Red Square </a> </li>
    <li>  <a style="text-decoration:none" href="#saitoTalk"> Saito Talk </a> </li>
    <li>  <a style="text-decoration:none" href="#saitoChat"> Saito Chat </a> </li>
  </ul>
  <br>
  <li> <a style="text-decoration:none" href="#build"> Build Your Own </a> </li>
<!--
  <ul>
    <li> 3a. <a style="text-decoration:none" href="#3a"> 3a </a> </li>
    <li> 3b. <a style="text-decoration:none" href="#3b"> 3b </a> </li>
    <li> 3c. <a style="text-decoration:none" href="#3b"> 3c </a> </li>
    <li> 3d. <a style="text-decoration:none" href="#3b"> 3d </a> </li>
  </ul>
  <br>
  <li> 4. <a style="text-decoration:none" href="#3b"> d</a> </li>
</ul>
-->
  
## <div id="gaming"> Gaming </div>

[Saito Arcade](https://saito.io/arcade/) is an open source game engine that runs as a fully-distributed peer-to-peer blockchain application in the browser. The arcade and its numerous games not only laid the groundwork for a more diverse suite of peer-to-peer applications but represents what we believe to be some of the richest and most genuine Web 3 experiences available to date.

Many of the games leverage sophisticated cryptographic [techniques](#mental-poker) to ensure fair elements of chance can exist without the need for any third-party oversight. Games on Saito require some of the most advanced use of Saito's cryptographic suite in order to ensure fair play in **genuine, peer-to-peer Web 3** (rather than a centrally hosted [Gacha-style](https://en.wikipedia.org/wiki/Gacha_game) game with token integrations). 

All games, whether they rely on complex cryptographic interactivity or are simple single-player experiences, benefit from the Saito Consensus's natural ability to fund open source applications by allowing service providers to earn their share of payment for network bandwidth or service provided.

For these reasons the [Web3 Foundation](https://web3.foundation/) has recognized the Saito Game Engine as a standard for open, cryptographic gaming, where it successfully [applied](https://github.com/w3f/Grants-Program/blob/master/applications/saito-game-protocol-and-engine.md) and fulfilled requirements for its grants program.

> I like this idea and think it provides something REALLY valuable to the ecosystem, and takes blockchain gaming in a very different (and good!) direction
> - *[Bill Laboon](https://github.com/w3f/Grants-Program/pull/73#issuecomment-713638248), Head of Education and Grants at Web3 Foundation*

### <div id="betterBusiness"> Better Business Models </div>

High  quality games with significant followings often struggle to make money from digital sales. Companies like Apple and Google force developers to list games at extremely low prices to compete for visibility in their distribution channels, and then restrict how publishers can collect money from users.

Instead of forcing publishers to revert to selling physical editions, merchandise, access to lightly-vieled gambling boxes or tokens of questionable utility and origin, Saito blurs the line between developer and publisher through new and better business models which rid themselves of the need to pay rent to centralized, digital storefronts.

Saito Arcade, and Saito generally, is an open index of applications which any node, full or lite, can earn fees for serving to users. Open source developers can thus route their application's transactions into the network and earn part of that fee, all while keeping an open and direct line between them and their users. Saito [revolutionizes](https://medium.com/@0xluminous/the-future-of-open-source-software-7c77592f8f24) open source monetization.

The best games may still gravitate towards free-to-play models, but alternative services and their monitization are not to be restricted: leaderboards, rankings, match-making services, and the like. Game designers on Saito have the freedom to experiment with different choices. Some games may be better off integrating decentralized advertising networks, or collecting micro-payments on a game-by-game or even a turn-by-turn basis.

### <div id="mentalPoker"> Mental Poker Techniques </div>

For question of how the Saito Game Engine allows multiple parties to fairly agree on the state of truly random elements necessary for many games on the arcade, the answer begins with [Mental Poker](https://people.csail.mit.edu/rivest/pubs/SRA81.pdf):

<!-- ![mentalpoker.png](/mentalpoker.png) -->
  <br>
<div style="display: flex; justify-content: center;">
    <img src="/mentalpoker.png" alt="Mental Poker; Adi Shamir, Ronald L. Rivest and Leanard M. Adleman; MASSACHUSETTS INSTITUTE OF TECHNOLOGY; ABSTRACT Can two potentially dishonest players play a fair game of poker without using any cards-for example, over the phone? This paper provides the following answers: 1. No. (Rigorous mathemmatical proof supplied.) 2. Yes. (Correct and complete protocol given.); Once there were two 'mental chess' experts who had become tired of their passtime. 'Let's play 'Mental Mpoker,' for variety' suggested one. 'Sure' said the other,' Just let me deal!'">
</div>

Indeed, the most direct use of the techniques which authors Rivest, Shamir and Adleman (RSA) devised are most directly employed and enchanced in Saito's very own, peer-to-peer, Web 3 Poker - available to [play](https://saito.io/arcade) on the arcade or to [audit](https://github.com/SaitoTech/saito-lite-rust/tree/master/mods/poker) on Github.

Mental Poker exploits the commutative nature properties of most public key encryption schemes to encrypt a deck of cards multiple times using the keys of the players who then shuffle the cards, ignorant of their unencrypted values and obscuring the order in which they were sent. A more complete explanation can be sought via [Wikipedia](https://en.wikipedia.org/wiki/Mental_poker).

The Saito Arcade has taken the principles of Mental Poker and generalized and extended the technique to support several adversarial players and to encode and integrate arbitrary values which extend far past a simple game of Poker. Titles like Twilight Struggle and Settlers of Saitoa are two flagship examples. Because Saito solves the *man-in-the-middle attack* (MITM) without the need for a trusted party, it is in the unique position to apply the techniques without sweeping related trust assumptions under the rug.

The entire process, from peer discovery to setup to gameplay benefits uniquely from taking place on a universal broadcast layer like Saito blockchain. Whereas many of these steps require a trusted party like Facebook to prevent MITM attacks, Saito does it trustlessly and in the open. While Mental Poker removes trust assumptions from the game, Saito removes trust assumptions from the network infrastructure, and thus can serve a secure and affordable Web 3 experience through every layer of interaction.

For a more technical dive into how the current suite of games on Saito Arcade work, pay a visit to our [Github Repository](https://github.com/SaitoTech/saito-lite-rust/blob/dbd9d622c8cb69c682045b780c63207eed8d7bf1/docs/gaming/saito-game-engine/readme.md) or ask a question on Saito's social media platform [Red Square](https://saito.io/redsquare/).


## <div id="socialMedia"> Social Media </div>
  
### <div id="redSquare"> Red Square </div>
  
[Red Square](https://saito.io/redsquare/) is the Web 3 public square leveraging the Saito Blockchain and its peer-to-peer capabilities. While it may appear to function like a standard Web 2 Twitter-clone, Red Square's infrastructure has been heavily abstracted down into pure peer-to-peer interactions. Users of Red Square keep eachother up to date and can remain online despite the whims of any central authorities.
<br>
### <div id="saitoTalk"> Saito Talk </div>
  
Saito Talk pure peer-to-peer video conferencing software, currently with support for up to four callers. [Transient Saito Transactions](https://wiki.saito.io/en/consensus#h-4-automatic-transaction-rebroadcasting-atr) securely bootstrap a STUN connection for the participants using their public keys, and those participants then enjoy a fully private, fully encrypted video call independent of the node originally providing STUN services.
  
We encourage users of centralized conferencing or video call software concerned with privacy and open source values to head over to [Red Square](https://saito.io/redsquare/) and find Saito Call under the hamburger menu in the top left. Saito proves that premium and everyday use cases can be stable and enjoyable under an open and privacy respecting model.
<br>
<div style="display: flex; justify-content: center;">
    <img src="/howtosaitocall.gif" width="400" alt="Use hamburger menu then Saito Call button to use the app">
</div>
<br>

### <div id="saitoChat"> Saito Chat </div>
  
[Saito Chat](https://saito.io/chat/) is an end-to-end encrypted (with the exception of public chats) peer-to-peer chat client which leverages the Saito blockchain to securely find and initiate key exchanges with peers. While the premise is simple and familiar, the privacy implications are profound:
  
Unlike other chat applications which require a user account and sometimes even a phone number, Saito Chat offers sovereign account creation and access by merely opening the web page (as do all Saito apps); a public key is automatically and locally generated. Not only is account creation more private, open and secure, but so is key exchange:
  
While the key exchange for a Web 2 encrypted messaging application relies on a central authority to assert that the true owners of the encryption keys are who they claim to be, Saito, defends against the man-in-the-middle attack by making it prohibitively costly to censor users, thus making the public-key identity theft as expensive, and moreso over time.
  
Users with the greatest need for security would be encouraged to delay sensitive messaging until the cost-to-attack the blockchain grows sufficiently large for the situation. Saito Chat demonstrates that the basic function as a leaderless yet secure public key infrastructure has application to all of our standard needs online.

## <div id="build"> Build Your Own </div>
  
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