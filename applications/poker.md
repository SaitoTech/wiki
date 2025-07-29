---
title: Poker
description: 
published: true
date: 2025-07-29T21:45:24.394Z
tags: 
editor: markdown
dateCreated: 2023-01-23T00:58:05.891Z
---

# Saito Poker

<img src="/poker-wide.png" style="max-width=600px;">

Saito Poker is an implementation of Texas Hold'em Poker that uses advanced cryptographic techniques to allow players to play the game in a provably-fair fashion without the need for a trusted third-party. It was the initial proof of concept for [Saito Web 3 Gaming](https://wiki.saito.io/tech/applications/arcade) and paved the way for a wide variety of games.

Saito Poker supports P2P crypto wagers that settle between hands - no custodian or middleman is required.

- Poker [source code](https://github.com/SaitoTech/saito-lite-rust/tree/master/mods/poker)

## How it Works

Gameplay happens directly peer-to-peer, without the need for a central server to connect players or mediate disputes. This makes Saito Poker fundamentally different from other “web3” poker implementations where players use cryptocurrencies to make wagers, but which still rely on centralized servers or trusted third-parties to shuffle the deck.

The cryptographic techniques used to secure gameplay are provided by the Saito Game Engine and include techniques like \[mental poker\](https://en.wikipedia.org/wiki/Mental\_poker), as described by Adi Shamir, Ronald L. Rivest and Leanard M. Adleman – the inventors of public key cryptography. These techniques leverage the commutative properties of public key encryption schemes to encrypt cards in a way they cannot be dealt from the deck without the consent of all players, i.e. until all players remove their encryption on the card.
  
<img src="/mentalpoker.png" alt="Mental Poker; Adi Shamir, Ronald L. Rivest and Leanard M. Adleman; MASSACHUSETTS INSTITUTE OF TECHNOLOGY;">

Saito Poker is under development but already supports most features needed for a fun game. Players can join or leave tables, and easily stake real-world cryptocurrencies.

<!--
## How to Play

At the start of each turn, two “hole cards” are dealt face down to each player. Five [community cards](https://en.wikipedia.org/wiki/Community_card_poker) are then dealt face-down on the table and revealed in three stages ("the flop", “the turn”, and then “the river”). Once all cards have been revealed, the winner is the player with the best [poker hand](https://en.wikipedia.org/wiki/List_of_poker_hands) created using any combination of their seven cards.

Betting occurs in stages throughout the game. A single round precedes the revelation of any community cards, and then a single round following each one. In all of these stages players can check, call, raise, or fold.
-->