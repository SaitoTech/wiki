---
title: CSS Guidelines
description: 
published: true
date: 2022-12-20T01:51:33.839Z
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
The Saito overlay is a container for arbitray content. It:
* placed the content centered in the page
* surronds the contend with a dark backdrop (that closes on click)
* a close "x" at the top right corner of the content.

#### Saito Modal
The Saito Modal provides a standard backdrop (dreamscape) for a variety of modal forms.

Example - Saito Modal Menu


#### Saito Module


