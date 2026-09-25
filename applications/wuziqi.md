---
title: Wuziqi
description: 
published: true
date: 2026-09-25T04:55:04.877Z
tags: 
editor: markdown
dateCreated: 2023-01-26T04:19:56.757Z
---

<div style="display:flex;align-items:center;gap:0.5rem;flex-wrap:wrap;margin-bottom:1rem"> <a href="https://mods.saito.io/wuziqi.saito" class="is-asset-link" style="display:inline-flex;align-items:center;gap:0.35rem;padding:0.55rem 0.9rem;border:1px solid #ccc;border-radius:6px;background:#fff;color:#333 !important;text-decoration:none;line-height:1;white-space:nowrap;"> <span>⬇</span> <span>Download Module</span> </a> <a href="https://github.com/SaitoTech/saito/tree/master/node/mods/wuziqi" style="display:inline-flex;align-items:center;gap:0.35rem;padding:0.55rem 0.9rem;border:1px solid #ccc;border-radius:6px;background:#fff;color:#333 !important;text-decoration:none;line-height:1;white-space:nowrap;"> <span>Source Code</span> <span style="font-size:0.85em;">↗</span> </a> <a href="https://wiki.saito.io/applications/install" style="display:inline-flex;align-items:center;gap:0.35rem;padding:0.55rem 0.9rem;border:1px solid #ccc;border-radius:6px;background:#fff;color:#333 !important;text-decoration:none;line-height:1;white-space:nowrap;"> <span>Installation Guide</span> <span style="font-size:0.85em;">↗</span> </a> </div> 


# Wuziqi
<br>
<img src="/wuziqi-timer.png" style="maxwidth: 600px;">
          
Wuziqi, also called *Five in a Row*, is a [strategy game](https://en.wikipedia.org/wiki/Abstract_strategy_game) played with black and white stones on a Go board. The Saito module was developed to show how easy it is to implement games of this sort.

- Wuziqi [source code.](https://github.com/SaitoTech/saito/tree/master/node/mods/wuziqi)  
 

#### Game Rules

Players take turns placing a stone of their color on an empty intersection atop the 12x12 board. Black plays first. The winner is the first player to form an unbroken chain of five stones horizontally, vertically, or diagonally. If placement creates a line of more than five stones that is considered an "overline" and does not result in a win.

