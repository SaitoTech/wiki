---
title: SaitoArcade
description: 
published: true
date: 2026-09-25T04:40:45.172Z
tags: 
editor: markdown
dateCreated: 2023-02-19T20:49:30.032Z
---

<div style="display:flex;align-items:center;gap:0.5rem;flex-wrap:wrap;margin-bottom:1rem"> <a href="https://mods.saito.io/arcade.saito" class="is-asset-link" style="display:inline-flex;align-items:center;gap:0.35rem;padding:0.55rem 0.9rem;border:1px solid #ccc;border-radius:6px;background:#fff;color:#333 !important;text-decoration:none;line-height:1;white-space:nowrap;"> <span>⬇</span> <span>Download Module</span> </a> <a href="https://github.com/SaitoTech/saito/tree/master/node/mods/arcade" style="display:inline-flex;align-items:center;gap:0.35rem;padding:0.55rem 0.9rem;border:1px solid #ccc;border-radius:6px;background:#fff;color:#333 !important;text-decoration:none;line-height:1;white-space:nowrap;"> <span>Source Code</span> <span style="font-size:0.85em;">↗</span> </a> <a href="https://wiki.saito.io/applications/install" style="display:inline-flex;align-items:center;gap:0.35rem;padding:0.55rem 0.9rem;border:1px solid #ccc;border-radius:6px;background:#fff;color:#333 !important;text-decoration:none;line-height:1;white-space:nowrap;"> <span>Installation Guide</span> <span style="font-size:0.85em;">↗</span> </a> </div> 

# Saito Arcade

[Saito Arcade](https://saito.io/arcade/) is a core part of the Saito Game Engine. It is installed by default in most versions of Saito as it is needed for creating and joining games. Once you have installed the Saito Arcade, any games that are also installed in your wallet will appear in your list of playable games.

<br />

<img src="/arcade-summer-2025.png" style="maxwidth: 600px;">

The games supported by the Saito Arcade all use the Saito Game Engine, allowing for sophisticated cryptographic [techniques](#mentalPoker) that allow players to cooperatively shuffle and deal cards, make simultaneous moves, and communicate securely without the need for a central server. The Saito Arcade is designed to support games that have up to six players.

For these reasons the [Web3 Foundation](https://web3.foundation/) has recognized the Saito Game Engine as an [open standard](https://github.com/w3f/Grants-Program/blob/master/applications/saito-game-protocol-and-engine.md) for open games.

> I like this idea and think it provides something REALLY valuable to the ecosystem, and takes blockchain gaming in a very different (and good!) direction
> - *[Bill Laboon](https://github.com/w3f/Grants-Program/pull/73#issuecomment-713638248), Head of Education and Grants at Web3 Foundation*

### <div id="mentalPoker"> Saito Game Engine </div>

The Saito Arcade offers the most practical implementation of the techniques devised by Rivest, Shamir and Adleman (RSA). These can be used directly in the Saito Poker module -- bundled by default on most installations of the [Saito Arcade](https://saito.io/arcade). For those curious how the Saito Game Engine allows multiple parties to fairly agree on the state of truly random elements necessary for many games on the arcade, the answer begins with [Mental Poker](https://people.csail.mit.edu/rivest/pubs/SRA81.pdf):

<br />

<div style="display: flex; justify-content: center;">
    <img src="/mentalpoker.png" alt="Mental Poker; Adi Shamir, Ronald L. Rivest and Leanard M. Adleman; MASSACHUSETTS INSTITUTE OF TECHNOLOGY; ABSTRACT Can two potentially dishonest players play a fair game of poker without using any cards-for example, over the phone? This paper provides the following answers: 1. No. (Rigorous mathemmatical proof supplied.) 2. Yes. (Correct and complete protocol given.); Once there were two 'mental chess' experts who had become tired of their passtime. 'Let's play 'Mental Mpoker,' for variety' suggested one. 'Sure' said the other,' Just let me deal!'">
</div>

Mental Poker exploits the commutative properties of public key encryption schemes to encrypt deck of cards using the keys of each player, and shuffle it while nobody is able to decrypt it. Cards can then be progressively decrypted by all players as determined by the game rules. A more complete explanation can be sought via [Wikipedia](https://en.wikipedia.org/wiki/Mental_poker).

The Saito Arcade has taken the principles of Mental Poker and generalized the techniques to support several adversarial players and to encode and integrate arbitrary states extending far past a simple game of Poker. Titles like [*Twilight Struggle*](/tech/applications/twilight) and [*Settlers of Saitoa*](/tech/applications/settlers) are two flagship examples of such extensions

## Games

For a full list of the games available in the Saito Arcade please see the [mods directory](https://github.com/SaitoTech/saito/tree/master/node/mods). Links to downloadable versions of some of the more playable games can also be found on the [applications](/applications) page in our wiki.
