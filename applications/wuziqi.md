---
title: Wuziqi
description: 
published: true
date: 2026-03-10T19:18:09.019Z
tags: 
editor: markdown
dateCreated: 2023-01-26T04:19:56.757Z
---

<div style="display: block;border: 2px solid rgb(204, 204, 204);border-radius: 8px;padding: 0.5rem;background-color: rgb(249, 249, 249);opacity: 1;z-index: 99999;position: relative;margin-bottom: 1rem;max-width: max-content;padding-top: 1rem;padding-bottom: 1rem;padding-left: 1rem;padding-right: 1rem;">
	<div class="header-box">
		<div id="download" class="toc-header" style="margin-top: 0px !important;display: grid;grid-template-columns: min-content 1fr;align-items: start;">
			<div class="header-box-title" style="width: max-content; float: left; display: relative;"> 📦 Download</div>
			<ul class="header-box-links" style="display: flex; gap: 3rem; padding-top: 0rem; margin-left: 1rem;">
				<li style="margin-top: 0px;"><a href="https://mods.saito.io/wuziqi.saito" class="is-asset-link">Saito Module</a></li>
				<li style="margin-top: 0px;"><a href="https://github.com/SaitoTech/saito/tree/master/node/mods/wuziqi" class="">Source Code</a></li>
				<li style="margin-top: 0px;"><a href="https://wiki.saito.io/applications/install" class="">Installation Guide</a></li>
			</ul>
		</div>
	</div>
</div>


# Wuziqi
<br>
<img src="/wuziqi-timer.png" style="maxwidth: 600px;">
          
Wuziqi, also called *Five in a Row*, is a [strategy game](https://en.wikipedia.org/wiki/Abstract_strategy_game) played with black and white stones on a Go board. The Saito module was developed to show how easy it is to implement games of this sort.

- Wuziqi [source code.](https://github.com/SaitoTech/saito/tree/master/node/mods/wuziqi)  
 

#### Game Rules

Players take turns placing a stone of their color on an empty intersection atop the 12x12 board. Black plays first. The winner is the first player to form an unbroken chain of five stones horizontally, vertically, or diagonally. If placement creates a line of more than five stones that is considered an "overline" and does not result in a win.

