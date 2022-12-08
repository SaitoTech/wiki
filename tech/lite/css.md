---
title: CSS Guidelines
description: 
published: true
date: 2022-12-08T05:56:30.213Z
tags: 
editor: markdown
dateCreated: 2022-12-07T07:41:32.600Z
---

# CSS Guidelines

## General Format

Follow X standard

* Preference shortand definitions where more than one parameter is set:
  ```margin: 0 1rem;``` 
  rather than 
  ```margin-left: 1rem;```
  ```margin-right: 1rem;```
  
* Use leading zeros on definitions. ```0.5rem``` not ```.5rem``` 

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







