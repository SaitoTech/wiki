---
title: dcm install test
description: 
published: true
date: 2024-11-14T02:48:46.208Z
tags: 
editor: markdown
dateCreated: 2024-11-13T20:09:07.715Z
---

# Wiki Overhaul



## <div id="app">Psuedo App Store - Dynamically Compiled Module Install</div>

DCM applications should be installable form the wiki.

1. Is it possible to host the files on the Wiki? [yes](/tutorial01.saito)
2. Can any install steps be automated?

**Problem:** Updating these app files is a pain.

It would be nice if they were just hosted on Github and updated there - Wiki would provide a link to that folder in the repo.

**Idea**:
Move all mods into a seperate Github Repo.

* This is how third-praty mods will be hosted already
* Serves as a page for the app which is better suited than a Wiki page
* That page is updated with the app
* Wiki can link to those repos

<!--An app can be hosted which fethes and installs from such a link, or installs a user uploaded file for more advanced users wishing to install trustlessly i.e. have access to source code.-->

## <div id="mods">"Mod" vs "App" Language</div>

![apps-vs-mods.png](/apps-vs-mods.png)

Saito Applications are Saito Modules that have a user interface.

## SLR Developer Structure

"App Development" page that has links to everything an SLR dev needs in the order they will need them:

1. Running an SLR Node
2. Configuring
3. Tutorials
4. Docs

Then there can be just two pages under Development
1. App Development
2. Core Development