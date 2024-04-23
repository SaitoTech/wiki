---
title: HIS Tutorial
description: 
published: true
date: 2024-04-23T04:36:58.373Z
tags: 
editor: markdown
dateCreated: 2024-04-20T08:11:24.441Z
---

# *Here I Stand* Game Tutorial

## Saito Version

The goal for this tutorial is to serve as an in-game aid and get new players started without first studying a longer rulebook. It gets right to the point.

This tutorial is built ground-up for the <a href="saito.io/arcade">Saito Arcade</a> version of *Here I Stand.* It is breifer than the official rulebook because the Saito version simplifies some game elements and automates many of the complex mechanisms for the player (such as score-keeping).


* This open-source tutorial uses excerpts from the [official rulebook](https://www.gmtgames.com/living_rules/HIS-Rules-2010.pdf). Please refer to the license agreements <a href="#license">below</a>.

## The Goal

Though special conditions can trigger <a href="#early">early victory</a>, the game is most commonly won by simply having more victory points than your opponents. 

You win a game of *Here I Stand*, most simply, by ammassing *Victory Points.*

In the victory track pictured below, you can see six <a href=#factions onclick="flashDiv()">factions'</a> *VP* tiles as they lie at the start of a game:

![his-victory-track-gamestart.png](/his-victory-track-gamestart.png)

You play as one or more of the six factions - many game scenarios take place in the following order:
<br>
<div class="factionBox" style="background-color: #019d4c;"></div> Ottomans

<div class="factionBox" style="background-color: #fce75a;"></div> Hapsburgs

<div  class="factionBox" style="background-color: #e54640;"></div> England

<div  class="factionBox" style="background-color: #0090cf;"></div> France

<div  class="factionBox" style="background-color: #7b4d96;"></div> Papacy

<div  class="factionBox" style="background-color: #a2583d;"></div> Protestants


## Earning Victory Points

The 'base' VP is calculated at the end of each turn as follows:

<div class="box">
<div class="factionBox" style="background-color: #019d4c;"></div> Ottomans

<div class="factionBox" style="background-color: #fce75a;"></div> Hapsburgs

<div class="factionBox" style="background-color: #e54640;"></div> England

<div class="factionBox" style="background-color: #0090cf;"></div> France

<div class="factionBox" style="background-color: #7b4d96;"></div> Papacy
<br>

Each earn VP equal to the number of <a href="keys">keys</a> they control. 
</div>

<div class="box">
<div  class="factionBox" style="background-color: #a2583d;"></div> Protestants
<br>

Earns 2 VP for each <a href="#electorates">electorate</a> that is under Protestant religious influence and political control.
</div>

**Neither <a href="keys">keys</a> nor <a href="#electorates">electorates</a>** provide VPs to a faction when those spaces are under <a href="#unrest">unrest</a>.
  


## Types of Victory

### <div id="determination"> Victory Determination Phase </div>

Victory Determination Phases happen at the end of each turn - this is the phase of the game where winners may be determined. Having the most VPs on the final phase equals a win. But there are also a few special conditions to strategize around in order to win the game before the last turn.

### <div id="early" class="targetDiv"> Early Victories </div>

<details> <summary>Types of Early Victory</summary>
  
  <details><summary> Automatic Victory </summary>
    Standard Victory - 
 
		Domination Victory - 
  
		Time Limit Victory - 
	</details>

</details>
</details>
  




<br>

## <div id="license" class="targetDiv"> License </div>

This open-source tutorial uses some excerpts from the [official rulebook](https://www.gmtgames.com/living_rules/HIS-Rules-2010.pdf). Please support the creators and obtain a license for *Here I Stand* before enjoying any open source, non-commercial content (like this guide and the game hosted Saito Arcade) from the game.

All game module code released under the MIT license. All GMT-developed materials (board design, cards, gameplay text) remain owned by GMT Games and are distributed under their license which provides for gameplay and distribution under the following conditions:

1. The game files may only be used by open source, non-commercial game engines

2. At least ONE player in every game should have purchased a commercial copy of the game.

If you are a player or developer who enjoys playing around with this implementation, please respect the goodwill shown by GMT Games and purchase a copy of the game. Likewise, if you make this demo available for play on a public server, please make sure that any players you support can fulfill these conditions by making it easy for them to purchase commercial copies of the game.

GMT GAMES: https://www.gmtgames.com/p-917-here-i-stand-500th-anniversary-reprint-edition-2nd-printing.aspx

AMAZON: https://www.amazon.com/Here-I-Stand-Board-Game/dp/B077QTQGYQ


<style>
  
  .box {
    padding: 10px 10px;
    margin: 10px;
    border: 4px solid #00000090;
    border-radius: 15px;
  }
  .factionBox {
    display: inline-block;
    width: 16px; height: 16px;
    border: solid 0.5px black;
    border-radius: 2px;
  }

 @keyframes flash {
    0% { background-color: transparent; }
    33% { background-color: #f71f3d; }
    100% { background-color: transparent; }
 }
 .targetDiv {
    animation-name: flash;
    animation-duration: 1.5s;
    animation-iteration-count: 1;
 }
 .targetDiv:target {
    animation-iteration-count: 1;
 }
</style>

