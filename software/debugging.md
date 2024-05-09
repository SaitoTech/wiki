---
title: Debugging and Bug Reporting
description: 
published: true
date: 2024-05-09T05:14:25.753Z
tags: 
editor: markdown
dateCreated: 2024-05-09T05:14:25.753Z
---

# Debugging and Bug Reporting


## Reporting Issues to the Team

The best place to let folks know of an issue is saito.io/redsquare the team and community are always around.

## Debugging 

### Snippets

** Delete games array **
This is useful for deleting just the games from your local options. If you are having trouble initialising games start here.

```
let op = JSON.parse(window.localStorage.options);
op.games.length = 0;
window.localStorage.options = JSON.stringify(op); 
```