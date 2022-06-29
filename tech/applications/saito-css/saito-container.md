---
title: saito-container
description: saito-container
published: true
date: 2022-06-29T03:24:07.852Z
tags: 
editor: markdown
dateCreated: 2022-06-29T03:20:34.640Z
---

# Saito-Container

The ```saito-container``` is the outermost DIV in the DOM. It is designed 


      ┌───────────────────────────────────────────────────────────────────────────────────────┐
      │saito-container                                                                        │
      │  ┌────────────────────┐ 
<div class=”satio-container”>
  <div></div>
  <div></div>
  <div></div>
</div>




<div class=”satio-container”>
  <div></div>
  <div></div>
  <div></div>
</div>



added *automatically* by Saito's ```/lib/templates/modtemplate.js``` file, and thus will be added automatically to the DOM by any module which inherits from that 



If you want your module NOT to add this element to the screen, override your module's ```render(app, mod)``` function and DO NOT call ```super.render(app, mod)```.

Saito-Container is designed to suppo

