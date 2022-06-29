---
title: saito-container
description: saito-container
published: true
date: 2022-06-29T03:47:24.475Z
tags: 
editor: markdown
dateCreated: 2022-06-29T03:20:34.640Z
---

# Saito-Container

Our ```saito-container``` class should be the outermost DIV in our application heirarchy. It is responsive to various display sized and designed to contain up to three elements: a left sidebar, a main panel, and a right sidebar.

If any components are removed, the application will resize appropriately. If there are only two components they will be treated as a left-sidebar and a main-panel. A single component will be treated as a main panel.

````
<div class=”saito-container”>
  <div class="saito-sidebar left"></div>
  <div class="saito-main"></div>
  <div class="saito-sidebar right"></div>
</div>
````
Developers may also omit the interior class declarations entirely:
````
<div class=”saito-container”>
  <div></div>
  <div></div>
  <div></div>
</div>
````

PlEASE NOTE: as the base-layer component in the Saito CSS design, this DIV element will be added *automatically* by any module that inherits from Saito's ```/lib/templates/modtemplate.js``` class when the ```render(app, mod)``` function in the parent class is called. You should call ```super.render(app, mod)``` before you begin manipulating the DOM.

If you wish to skip ```saito-container``` being added to the DOM, you should avoid calling ```super.render(app, mod)``` within your module.

