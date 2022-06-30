---
title: Saito Overlay
description: 
published: true
date: 2022-06-30T07:08:14.348Z
tags: 
editor: markdown
dateCreated: 2022-06-30T06:52:51.770Z
---

# Saito Overlay

The ```saito-overlay``` class can be used to display a fixed overlay with greater z-index over any page. It can be used in concert with ```saito-backdrop``` to display necessary information temporarily or act as a prompt to a user of a Saito application


``` saito-overlay ```:

````
   <div class="saito-overlay">
       <div class="saito-backdrop">
            <i class="fas fa-power-off"> </i>
          <div>
  						/// content here
          </div>
       </div>
   </div>
````