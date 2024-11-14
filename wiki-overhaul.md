---
title: dcm install test
description: 
published: true
date: 2024-11-14T02:46:16.461Z
tags: 
editor: markdown
dateCreated: 2024-11-13T20:09:07.715Z
---

# Wiki Overhaul

Table of contents template:
<style>
  .toc {
    display: table;
    border: 1px solid #a2a9b1;
    background-color: #f8f9fa;
    padding: 5px;
    margin: 1em 0;
    font-size: 95%;
  }

  .toc-title {
    text-align: center;
    font-weight: bold;
    margin: 0.5em 1;
  }

  .toc ul {
    list-style: none;
    margin: 0.3em 0 0 1em;
    padding: 0;
    line-height: 1.4;
  }

  .toc li {
    margin: 0.1em 0;
  }

  .toc a {
    color: #0645ad;
    text-decoration: none;
  }

  .toc a:hover {
    text-decoration: underline;
  }
</style>

<div class="toc">
  <div class="toc-title">Contents</div>
  <ul>
    <li>1. <a href="app">App Store</a>
      <ul>
        <li>1.1 <a href="quickstart">Quick Start Guide</a></li>
        <li>1.2 <a href="installation">Installation</a></li>
        <li>1.3 <a href="requirements">System Requirements</a></li>
      </ul>
    </li>
    <li>2. <a href="concepts">Core Concepts</a>
      <ul>
        <li>2.1 <a href="concepts/basics">Basic Principles</a></li>
        <li>2.2 <a href="concepts/architecture">Architecture</a></li>
        <li>2.3 <a href="concepts/components">Key Components</a></li>
      </ul>
    </li>
  </ul>
</div>

## <div id="app">Psuedo App Store - Dynamically Compiled Module Install</div>

DCM applications should be installable form the wiki.

1. Is it possible to host the files on the Wiki? Yes.
2. Can any install steps be automated?

Here is a DCM file hosted on the wiki: [tutorial01.saito](/tutorial01.saito)

**Problem:** Updating these app files is a pain.

It would be nice if they were just hosted on Github and updated there - Wiki would provide a link to that folder in the repo.

**Idea**:
Move all mods into a seperate Github Repo.

* This is how third-praty mods will be hosted already
* Serves as a page for the app which is better suited than a Wiki page
* That page is updated with the app
* Wiki can link to those repos

<!--An app can be hosted which fethes and installs from such a link, or installs a user uploaded file for more advanced users wishing to install trustlessly i.e. have access to source code.-->

## "Mod" vs "App" Language

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