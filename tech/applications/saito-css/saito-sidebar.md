---
title: saito-sidebar
description: saito-sidebar
published: true
date: 2022-06-29T04:42:49.992Z
tags: 
editor: markdown
dateCreated: 2022-06-29T04:42:49.992Z
---

# Saito-Sidebar

The ```saito-sidebar``` classname is assigned to either the left-hand or right-hand sidebars that can be added to ```saito-container``` as one of the up-to-three main components of a Saito application. The expected structure for these elements within the ```saito-container``` class is as follows:

```
<div class=”saito-container”>
  <div class="saito-sidebar left"></div>
  <div class="saito-main"></div>
  <div class="saito-sidebar right"></div>
</div>
```
A sidebar can be written manually using the above CSS declarations (please note the addition of "left" or "right" to indicate the appropriate position on the page), or invoked automatically by creating the associated UI Component, as below:

```
const SaitoSidebar = require('../../lib/saito/new-ui/saito-sidebar/saito-sidebar');
const ModuleMainPage = require('./lib/main/main');
   
render(app, mod) {
    
    if (!this.ui_initialized) {

      this.left_sidebar = new SaitoSidebar(app, this);
      this.left_sidebar.align = "left";

      this.right_sidebar = new SaitoSidebar(app, this);
      this.left_sidebar.align = "right";

      this.main = new ModuleMainPage(app, this);

      this.addComponent(this.left_sidebar);
      this.addComponent(this.main);
      this.addComponent(this.right_sidebar);

      this.ui_initialized = true;
    }
    
    super.render(app, mod);
  }
```

If the UI Component is used to create a left-hand sidebar, it will automatically insert the subclasses necessary to create a mobile-responsive menu on smaller screen. Once the class is defined, all interior components will be treated as standalone boxes. If UI Components are added to the sidebar component via ```addComponent()``` they will be rendered in the order which they were added to the component.

````
   <div class="saito-sidebar left">
      <div class="">Component 1</div>
      <div class="">Component 2</div>
      <div class="">Component 3</div>
   </div>
````
