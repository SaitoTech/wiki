---
title: Saito CSS and UI Components
description: An introduction to Saito UI Components and CSS Structure
published: true
date: 2022-06-29T03:15:00.087Z
tags: 
editor: markdown
dateCreated: 2022-06-29T02:39:03.187Z
---

# Saito UI Components

Saito comes with UI Components like the Saito Header and the Saito Chatbox which you will see in many applications. You can include these components in any applications that you want to write.

To use a Saito UI component in your application, start by including the component at the top of your module file. A number of UI Components are included by default in the ```/lib/saito/new-ui``` directory. You can build your own module-specific components and include them in the ```/lib``` directory of your module as well.

```
const ModTemplate = require('../../lib/templates/modtemplate');
const SaitoHeader = require('../../lib/saito/new-ui/saito-header/saito-header');
const RedSquareMain = require('./lib/main/redsquare-main');
const RedSquareMenu = require('./lib/menu');
const RedSquareChatBox = require('./lib/chatbox');
const RedSquareSidebar = require('./lib/sidebar');
```

Whenever a module or component is displayed on-screen, it will have its ```render(app, mod);``` function called. To display these components once your application loads, simply modify your module's ```render(app, mod);``` function to load them into view. The standard way of doing this is to call ```addComponent()``` to add the individual components to each other than then your module, and then finally Calling ```super.render(app, this);``` to trigger them all being written to the DOM.

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

If you update a component, you can call ```render(app, mod);``` on the component to update it directly. For updates that happen frequently and affect only minor subcomponents (like chat messages) we recommend using Saito's built-in event system rather than re-writing the DOM to update hte interface with every change.
