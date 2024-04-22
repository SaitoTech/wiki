---
title: HIS Tutorial
description: 
published: true
date: 2024-04-22T01:06:42.346Z
tags: 
editor: markdown
dateCreated: 2024-04-20T08:11:24.441Z
---

# *Here I Stand* Game Tutorial

This open-source tutorial uses excerpts from the [official rulebook](https://www.gmtgames.com/living_rules/HIS-Rules-2010.pdf). Please refer to the license agreements <a href="#license">below</a>.

## The Goal

You win a game of *Here I Stand*, most simply, by ammassing *Victory Points.*

In the victory track pictured below, you can see six colored *VP* tiles as they lie at the start of a game; each color represents a <a href=#factions onclick="flashDiv()">faction</a>. 

![his-victory-track-gamestart.png](/his-victory-track-gamestart.png)

## How to Gain Victory Points

Though special conditions can trigger <a href="#early">early victory</a>, the game is most commonly won by simply having more victory points than your opponents.

## Types of Victory

### Victory Determination Phase

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
  

## <div id="factions" class="targetDiv"> Factions </div>

These are the six factions of the game - many game scenarios take place in the following order:

<div style="display: inline-block; width: 16px; height: 16px; background-color: #019d4c; border: solid 0.5px black; border-radius: 2px;"></div> Ottomans
<br>

<div style="display: inline-block; width: 16px; height: 16px; background-color: #fce75a; border: solid 0.5px black; border-radius: 2px;"></div> Hapsburgs
<br>

<div style="display: inline-block; width: 16px; height: 16px; background-color: #e54640; border: solid 0.5px black; border-radius: 2px;"></div> England
<br>

<div style="display: inline-block; width: 16px; height: 16px; background-color: #0090cf; border: solid 0.5px black; border-radius: 2px;"></div> France
<br>

<div style="display: inline-block; width: 16px; height: 16px; background-color: #7b4d96; border: solid 0.5px black; border-radius: 2px;"></div> Papacy
<br>

<div style="display: inline-block; width: 16px; height: 16px; background-color: #a2583d; border: solid 0.5px black; border-radius: 2px;"></div> Protestants
<br>


<br>

## <div id="license" class="targetDiv"> License </div>

This open-source tutorial uses some excerpts from the [official rulebook](https://www.gmtgames.com/living_rules/HIS-Rules-2010.pdf).

All game module code released under the MIT license. All GMT-developed materials (board design, cards, gameplay text) remain owned by GMT Games and are distributed under their license which provides for gameplay and distribution under the following conditions:

1. The game files may only be used by open source, non-commercial game engines

2. At least ONE player in every game should have purchased a commercial copy of the game.

If you are a player or developer who enjoys playing around with this implementation, please respect the goodwill shown by GMT Games and purchase a copy of the game. Likewise, if you make this demo available for play on a public server, please make sure that any players you support can fulfill these conditions by making it easy for them to purchase commercial copies of the game.

GMT GAMES: https://www.gmtgames.com/p-917-here-i-stand-500th-anniversary-reprint-edition-2nd-printing.aspx

AMAZON: https://www.amazon.com/Here-I-Stand-Board-Game/dp/B077QTQGYQ


<style>
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

