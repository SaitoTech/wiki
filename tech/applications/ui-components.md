---
title: Saito CSS and UI Components
description: An introduction to Saito UI Components and CSS Structure
published: true
date: 2022-06-29T02:53:42.767Z
tags: 
editor: markdown
dateCreated: 2022-06-29T02:39:03.187Z
---

# Saito UI Components

To use Saito UI components in your application, include them at the top of your module file. A number of UI Components are included by default in the ```/lib/saito/new-ui``` directory. Additional module-specific components can be created in the ```/lib``` directory of your module.

```
const ModTemplate = require('../../lib/templates/modtemplate');
const SaitoHeader = require('../../lib/saito/new-ui/saito-header/saito-header');
const SaitoCalendar = require('../../lib/saito/new-ui/saito-calendar/saito-calendar');
const RedSquareMain = require('./lib/main/redsquare-main');
const RedSquareMenu = require('./lib/menu');
const RedSquareChatBox = require('./lib/chatbox');
const RedSquareSidebar = require('./lib/left-sidebar');
const RedSquareSidebar = require('./lib/right-sidebar');
```

Once your module is aware of these components, modify your render(app, mod) function to load them into your module, as in the code below. Calling ```super(app, this);``` will render all of the components that have been created and added to the module in the order they have been added, as below:

```
 render(app, mod) {

    if (!this.ui_initialized) {

      this.main = new RedSquareMain(app);
      this.header = new SaitoHeader(app);
      this.menu = new RedSquareMenu(app);
      this.chatBox = new RedSquareChatBox(app)

      this.lsidebar = new SaitoSidebar(app);
      this.lsidebar.align = "left";

      this.rsidebar = new RedSquareSidebar(app);

      //
      // add components
      //
      this.addComponent(this.lsidebar);
      this.addComponent(this.main);
      this.addComponent(this.rsidebar);
      this.addComponent(this.header);
      this.lsidebar.addComponent(this.chatBox);
      this.lsidebar.addComponent(this.menu);

      this.ui_initialized = true;

    }

    super.render(app, this);

  }
```

Using Saito's default UI Components will avoid the need for you to manage CSS -- default styling will be added to components as they are rendered. If you wish to understand how these components are programmed and styled in  order to modify them , here is a separate list of the critical CSS containers and properties that form the core CSS of our application design. 

- saito-container
- saito-header
- saito-main
- saito-sidebar \[left \| right\]
- saito-list
	- saito-list-user
	- saito-list-game
- saito-identicon
- saito-menu
- saito-overlay
- saito-backdrop
