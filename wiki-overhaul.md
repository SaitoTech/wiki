---
title: dcm install test
description: 
published: true
date: 2024-11-14T02:42:54.185Z
tags: 
editor: markdown
dateCreated: 2024-11-13T20:09:07.715Z
---

# Wiki Overhaul

Table of contents template:
<style>
  .wiki-toc {
    max-width: 800px;
    margin: 20px;
    line-height: 1.6;
  }

  .wiki-toc h1 {
    border-bottom: 2px solid #ddd;
    padding-bottom: 10px;
    margin-bottom: 20px;
  }

  .section {
    margin: 15px 0;
  }

  .section-title {
    font-size: 1.2em;
    font-weight: bold;
    margin: 15px 0 10px 0;
    color: #2c3e50;
  }

  .section-content {
    margin-left: 20px;
  }

  .section-content ul {
    margin: 5px 0;
    padding-left: 20px;
  }

  .section-content li {
    margin: 5px 0;
  }

  .section-content a {
    color: #3498db;
    text-decoration: none;
  }

  .section-content a:hover {
    text-decoration: underline;
  }
</style>

<div class="wiki-toc">
  <h1>📚 Documentation</h1>
  
  <div class="section">
    <div class="section-title">🚀 Getting Started</div>
    <div class="section-content">
      <ul>
        <li><a href="introduction">Introduction</a></li>
        <li><a href="quickstart">Quick Start Guide</a></li>
        <li><a href="installation">Installation</a>
          <ul>
            <li><a href="installation#requirements">System Requirements</a></li>
            <li><a href="installation#setup">Setup Instructions</a></li>
          </ul>
        </li>
      </ul>
    </div>
  </div>

  <div class="section">
    <div class="section-title">📖 Core Concepts</div>
    <div class="section-content">
      <ul>
        <li><a href="concepts/basics">Basic Principles</a></li>
        <li><a href="concepts/architecture">Architecture</a></li>
        <li><a href="concepts/components">Key Components</a>
          <ul>
            <li><a href="concepts/components#component-a">Component A</a></li>
            <li><a href="concepts/components#component-b">Component B</a></li>
          </ul>
        </li>
      </ul>
    </div>
  </div>

  <div class="section">
    <div class="section-title">⚙️ Advanced Topics</div>
    <div class="section-content">
      <ul>
        <li><a href="advanced/config">Advanced Configuration</a></li>
        <li><a href="advanced/security">Security</a>
          <ul>
            <li><a href="advanced/security#auth">Authentication</a></li>
            <li><a href="advanced/security#best-practices">Best Practices</a></li>
          </ul>
        </li>
      </ul>
    </div>
  </div>

  <div class="section">
    <div class="section-title">🔌 API Reference</div>
    <div class="section-content">
      <ul>
        <li><a href="api/overview">API Overview</a></li>
        <li><a href="api/endpoints">Endpoints</a></li>
        <li><a href="api/auth">Authentication</a></li>
      </ul>
    </div>
  </div>

  <div class="section">
    <div class="section-title">🔍 Troubleshooting</div>
    <div class="section-content">
      <ul>
        <li><a href="troubleshooting/common-issues">Common Issues</a></li>
        <li><a href="troubleshooting/faq">FAQs</a></li>
        <li><a href="troubleshooting/support">Support</a></li>
      </ul>
    </div>
  </div>
</div>

## Psuedo App Store - Dynamically Compiled Module Install

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