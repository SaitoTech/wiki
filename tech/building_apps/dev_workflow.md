---
title: Dev Workflow
description: 
published: true
date: 2023-08-15T05:41:42.746Z
tags: 
editor: markdown
dateCreated: 2023-08-15T05:28:38.425Z
---

# Development Workflow

## General Dev Pattern


```mermaid
flowchart LR;
   A(dev branch) -- pull/rebase --> B(feature branch);
   B -- PR --> C{tests};
   C -- Fail --> B;
   C -- Pass --> A;
   A -- PR --> D{tests};
   D -- Pass --> E(main branch);
   D -- Fail --> A;
   E --> F[Deploy]
```


### Notes

* New development should start with a pull and rebase:
```
   git checkout dev
   git pull
   git checkout -b new-branch-name
```
* Branches can only be merged to the dev branch via Pull Requests
* The dev branch can only be merged into main via a Pull Request
* Tests include linting and style checks