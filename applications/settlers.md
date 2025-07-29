---
title: Settlers of Saitoa
description: 
published: true
date: 2025-07-29T21:45:13.083Z
tags: 
editor: markdown
dateCreated: 2023-01-29T19:34:11.091Z
---

![](/settlers-wide.png)
<!-- <img src="/settlers-wide.png" style="width: 600px;"/> -->

# Settlers of Saitoa

[Settlers of Saitoa](https://saito.io/arcade) is an open source implementation of an island-settling game with similar mechanics to the well-known Settlers of Catan. Players build settlements, cities, and roads to expand their control over island resources and earn Victory Points. The game board, which represents the island, is composed of hexagonal tiles ([hexes](https://en.wikipedia.org/wiki/Hex_map)) which are laid out randomly at the beginning of each game.   
  
The goal of the game is to reach ten victory points, but this can be customized. The two-player game also has some unique customizations designed to make victory harder. Once a player has an entrenched lead, the local bandit ("Robin Hood") will typically favour them over their opponent out of sense of natural justice.

Settlers of Saitoa [source code.](https://github.com/SaitoTech/saito/tree/master/node/mods/settlers)
  
## How to Play  
  
Players build by spending [resources](https://en.wikipedia.org/wiki/Game_mechanics#Resource_management) (wool, grain, lumber, brick, and ore) that are depicted by these resource cards; each land type, with the exception of the unproductive desert, produces a specific resource: hills produce brick, forests produce lumber, mountains produce ore, fields produce grain, and pastures produce wool. 

On the player's turn, the player may spend resource cards to build roads or settlements, upgrade settlements to cities (which replace existing settlements), or buy development cards. Players can trade resource cards with each other; players may also trade off-island (in effect, with the non-player bank) at a ratio of four-to-one resources for one of any other. By building settlements adjacent to ports, players may trade with the bank at three-to-one (three of any single resource type) or two-to-one (two of a specific resource) ratios, depending on the port's location.

Players score one point for each settlement they own and two for each city. Various other achievements, such as establishing the longest road and the largest army (by playing the most [knight](https://en.wikipedia.org/wiki/Knight) cards), grant a player additional victory points.  
  
There is also a bandit token; if a player rolls 7, the bandit must be moved to another hex, which will no longer produce resources until the bandit is moved again. That player may also steal a resource card from another player with a settlement or city adjacent to the bandit's new placement. In addition, when a 7 is rolled, all players with 8 or more resource cards must discard their choice of half of their cards, rounded down. For example, If a player has 9 resource cards, and a 7 is rolled, the player must get rid of 4 cards.