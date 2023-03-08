---
title: Saito CSS
description: Saito CSS Design
published: true
date: 2023-03-08T02:11:47.190Z
tags: 
editor: markdown
dateCreated: 2022-06-29T02:53:29.274Z
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
* Use hex color codes ```#000``` avoid ```rgba()``` and never use color names - i.e. ```whitesmoke```. \
Note use of color varliables below.
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
```
<div class="saito-table">
    <div class="saito-table-head"></div> (unused in this case)
    <div class="saito-table-body">
	      <div class="saito-table-row league-leaderboard-ranking">
            <div>Blackjack</div>
            <div>…</div>
        </div>
        ...
    </div>
</div>
```
**"saito-table"** vertically spaces the rows in a grid with spacing.
**"saito-table-head"** allows for a header row with titles differently styled.
**"saito-table-row"** handles basic row theming 
*NOTE* the grid columns of "saito-table-row" can be over-ridden to create specific layouts (defult is two column).


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


The Saito Module Development environment proivdes optional pre-build UI commponents and styling.

This page provides information on the core classes and explains their internal / expected structures.

### Important Classes

- [saito-container](/tech/applications/saito-css/saito-container)
- [saito-header](/tech/applications/saito-css/saito-header)
- [saito-sidebar  \[ left \| right \]](/tech/applications/saito-css/saito-sidebar)
- [saito-list](/tech/applications/saito-css/saito-list)
- [saito-identicon](/tech/applications/saito-css/saito-identicon)
- [saito-username](/tech/applications/saito-css/saito-username)
- [saito-user]
- [saito-group]
- [saito-table]
- [saito-calendar]
- [saito-datepicker]
- [saito-menu](/tech/applications/saito-css/saito-menu)
- [saito-overlay](/tech/applications/saito-css/saito-overlay)
- [saito-backdrop](/tech/applications/saito-css/saito-backdrop)

