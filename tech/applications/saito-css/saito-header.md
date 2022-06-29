---
title: saito-header
description: saito-header
published: true
date: 2022-06-29T04:25:21.074Z
tags: 
editor: markdown
dateCreated: 2022-06-29T03:55:14.489Z
---

# Saito-Header

The ```saito-header``` is the classname of the red-orange banner that stretches across the top of most Saito applications. It also handles the right-hand slide-in menu that is triggered by clicking on the hamburger icon. 

The SaitoHeader element is a standard UIComponent, and can be included in any application by adding the component to the module before rendering it, as below:

```
  const SaitoHeader = require('../../lib/saito/new-ui/saito-header/saito-header');
 
  render(app, mod) {
    
    if (!this.ui_initialized) {
      this.header = new SaitoHeader(app);
      this.addComponent(this.header);
      this.ui_initialized = true;
    }
    
    super.render(app, mod);
  }
```

The default HTML for ```saito-header``` looks like this:

````
<header id="saito-header">
    <img class="logo" alt="Logo" src="/saito/img/logo.svg"> 
    <nav>
    <ul>
    <li class="header-link-container">
    <div id="header-link-toggle" href="#">Tabs</div>
    <div id="saito-tab-buttons" class="header-link-list">
    <a active="" class="active" data-target="#general"> General </a>
    <a data-target="#forms"> Forms </a>
    <a data-target="#grids"> Grids </a>
    <a data-target="#boxes"> Boxes </a>
    <a data-target="#menus"> Menus </a>
    <a data-target="#user_lists"> User Lists </a>
    <a data-target="#example1"> Example 1 </a>
    <a data-target="#example2"> Example 2 </a>
    <a data-target="#example3"> Example 3 </a>
    <a data-target="#example4"> Example 4 </a>
    <a data-target="#components"> Components </a>
    </div>
  </li>
  </ul>
      <div class="relative" style="">
        <div id="header-menu-toggle">
          <span></span>
          <span></span>
          <span></span>
        </div>
        <div class="header-hamburger-contents">
          <div class="header-profile">
                <img src="/saito/img/background.png">
                <div>
                    <p>t4gEMWsDjZ4xeYGn2gCGxFg8ty53rs7UQKUpwfvsBq33 </p>
                    <i class="fas fa-copy"></i>
                </div>
          </div>
          <select class="saito-new-select saito-select-border" style="display: none;">
          <option value="0">0.0000 SAITO</option>
          <option value="1">0.0000 TRX</option>
      </select><div class="saito-select-wrapper"> <div class="saito-select-btn">
           <span>0.0000 SAITO</span>
           <div>
           <i class="fas fa-caret-down"></i>
           </div>
           
       </div>
       <div class="saito-select-content saito-select-border">
         
           <ul class="options">
            <li>0.0000 SAITO </li><li>0.0000 TRX </li>
       </ul>
       </div>
  </div>

          <div class="header-menu-section">
            <div class="saito-menu-list  saito-white-background">
            <ul>
              <li class="no-icon">
                <i class="far fa-address-card saito-primary-color"> </i>
                <span> Create Game </span>
            </li>
              <li>
                <i class="far fa-address-card saito-primary-color"> </i>
                <span> Send Tokens</span>
              </li>
          
            </ul>
            </div>
          </div>
          <div class="header-menu-section">
          <div class="saito-menu-list  saito-white-background">
          <ul>
            <li class="no-icon">
              <i class="far fa-address-card saito-primary-color"> </i>
              <span> Reset/Nuke Wallet </span>
            </li>
            <li>
              <i class="far fa-address-card saito-primary-color"> </i>
              <span> Backup Access Keys</span>
            </li>
            <li>
              <i class="far fa-address-card saito-primary-color"> </i>
              <span> Restore Access Keys</span>
            </li>
            <li>
              <i class="far fa-address-card saito-primary-color"> </i>
              <span> Settings</span>
            </li>
            <li>
              <i class="far fa-address-card saito-primary-color"> </i>
              <span>Scan</span>
            </li>
        
          </ul>
          </div>
          </div>
          <div class="header-menu-section">
          <div class="saito-menu-list  saito-white-background">
          <ul>
          <li class="no-icon">
            <i class="far fa-address-card saito-primary-color"> </i>
            <span> Arcade </span>
          </li>
          <li>
            <i class="far fa-address-card saito-primary-color"> </i>
            <span> Chat</span>
          </li>
          <li>
            <i class="far fa-address-card saito-primary-color"> </i>
            <span> Dev Center</span>
          </li>
          <li>
            <i class="far fa-address-card saito-primary-color"> </i>
            <span> Post</span>
          </li>
         
      
        </ul>
        </div>
          </div>
            
          </div>
        </div>
      
    </nav>
  </header>````
Developers may also omit the interior class declarations entirely:
````
<div class=”saito-header”>
</div>
````
