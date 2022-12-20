---
title: CSS Guidelines
description: 
published: true
date: 2022-12-20T03:36:08.008Z
tags: 
editor: markdown
dateCreated: 2022-12-07T07:41:32.600Z
---

# CSS Guidelines

## General Format

Follow X standard

* Use double quotes for font names, url() and @import definitions.

* Preference shortand definitions where more than one parameter is set:
  ```margin: 0 1rem;``` 
  rather than 
  ```margin-left: 1rem;```
  ```margin-right: 1rem;```
  
* Use leading zeros on definitions. ```0.5rem``` not ```.5rem``` 
* Put spaces after ```:``` in property declarations.
* Put spaces before ```{``` in rule declarations.
* Use hex color codes ```#000``` avoid ```rgba()``` and never use color names - i.e. ```whitesmoke```.
* Use one line per property declaration.
* Always follow a rule with one line of whitespace.

## Saito Specifices

* Colors should be defined in variables kept in ```saito-variables.css``` 
  *This is to comply with requirements for theme switching*
  
* Files in ```/web/saito/css-imports``` should only contain generic css for the element or structure they define.

* Naming should be consistent throughout ui structures:
```
      saito-hat
        saito-hat-top
          saito-hat-top-band
        saito-hat-brim
```

## Reusable Components

#### Saito Overlay
Saito overlay is a container for arbitray content. It:

```
<div class="saito-overlay">
    Content
<div class="saito-overlay-backdrop"></div>
```

* placed the content centered in the page
* surronds the contend with a dark backdrop (that closes on click)
* a close "x" at the top right corner of the content.

#### Saito Modal
Saito Modal provides a standard backdrop (dreamscape) for a variety of modal forms.

Example - Saito Modal Menu
```
<div class="saito-modal">
    <h6>Saito Menu</h6>
    <div class="saito-modal-content">
        <div id="user_menu_item_0" class="saito-modal-menu-option">
            <i class="far fa-id-card"></i> (icon)
            <div>Add Contact</div>         (text)
        </div>
        ... (further menu entries)
    </div>
</div>
```

**"saito-modal"** provides the centered div with padding and the dreamscape background.
**"saito-modal-menu-option"** spaces an icon-text pair and handles cursor look and feel

*TODO: Add further modal types.

#### Saito Table
Satio Table provides a standard formated table.

Example - Rankings





#### Saito Module
Saito Module provides a dynamic (auto responsive) card for showing modules in lists or grids. Examples are game invites or Appstore cards

Example - Saito Game Invite

```
<div class="saito-module saito-game">
    <div class="saito-module-titlebar">
        <span class="saito-module-titlebar-title">Twilight Struggle</span>
        <div class="saito-module-titlebar-details game-type">CUSTOM GAME</div>
    </div>
    <div class="saito-module-details saito-game-identicons">
        <div class="tip">
            <img class="saito-module-identicon saito-identicon">
            <div class="tiptext">
                <div class="saito-address">kris088Chess@saito</div>
            </div>
        </div>
    </div>
</div>
```

**"saito-module"** provides the flexible card
**"saito-module-titlebar"** provides theming for a stanard Title/Subtitle
**"saito-module-details"** is flexible space that can house arbitrary HTML. This could be identicons in the invite as per the example but could also be buttons or controls (as in an "intsall" button in appstore).
