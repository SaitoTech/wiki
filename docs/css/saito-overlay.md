---
title: Saito Overlay
description: 
published: true
date: 2025-05-20T04:03:30.349Z
tags: 
editor: markdown
dateCreated: 2022-06-30T06:52:51.770Z
---

# Saito Overlay

The ```saito-overlay``` class can be used to display a fixed overlay with greater z-index over any page. It can be used in concert with ```saito-backdrop``` to temporarily display necessary information or act as a prompt to a user of a Saito application.


**DEFAULT** :

````
   <div class="saito-overlay">
       <div class="saito-backdrop">
            <i class="fas fa-times"> </i>
          <div>
  						/// content here
          </div>
       </div>
   </div>
````


Developers can choose to omit the close icon, in cases like this, the overlay should be closeD by clicking outside the ```saito-backdrop``` element.

**NO CLOSE ICON** :

````
   <div class="saito-overlay">
       <div class="saito-backdrop">
          <div>
  						/// content here
          </div>
       </div>
   </div>
````