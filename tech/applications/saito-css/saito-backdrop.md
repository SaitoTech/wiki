---
title: Saito Backdrop
description: 
published: true
date: 2022-06-30T07:24:41.086Z
tags: 
editor: markdown
dateCreated: 2022-06-30T07:24:41.086Z
---

# Saito Backdrop


The ```saito-backdrop``` class is used in concert with the ``` saito-overlay``` class to display necessary information or act as a prompt to a user of a Saito application.

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


Developers can choose to omit the close icon, in cases like this, the backdrop should be closed by clicking outside the ```saito-backdrop``` element.

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