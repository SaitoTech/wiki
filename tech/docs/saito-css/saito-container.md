---
title: saito-container
description: saito-container
published: true
date: 2022-06-30T10:21:29.804Z
tags: 
editor: markdown
dateCreated: 2022-06-29T03:20:34.640Z
---

# Saito-Container

The ```saito-container``` class should be the outermost DIV in the dom heirarchy. It is responsive and contains a main panel and optional left and right sidebars.

If any components are removed, the application will resize appropriately. If there are only two components they will be treated as a left-sidebar and a main-panel. A single component will be treated as a main panel.

````
<div class=”saito-container”>
  <div class="saito-sidebar left"></div>
  <div class="saito-main"></div>
  <div class="saito-sidebar right"></div>
</div>
````

Interior class declarations may be ommitted:
````
<div class=”saito-container”>
  <div></div>
  <div></div>
  <div></div>
</div>
````

The CSS contains definitions for both the element in the hierarchy and the style name:

```
.saito-cointainer div:first-child, .saito-sidebar.left {
  /* css */
}
```

PlEASE NOTE: as the base-layer component in the Saito CSS design, this DIV element will be added *automatically* by any module that inherits from Saito's ```/lib/templates/modtemplate.js``` class when the ```render(app, mod)``` function in the parent class is called. You should call ```super.render(app, mod)``` before you begin manipulating the DOM.

To skip ```saito-container``` being added to the DOM, do not call ```super.render(app, mod)``` within your module.

