---
title: dcm install test
description: 
published: true
date: 2024-11-14T02:41:28.847Z
tags: 
editor: markdown
dateCreated: 2024-11-13T20:09:07.715Z
---

# Wiki Overhaul

Table of contents template:
<style>
  .wiki-toc {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
  }

  .wiki-toc h1 {
    color: #2d3748;
    border-bottom: 2px solid #e2e8f0;
    padding-bottom: 10px;
    margin-bottom: 20px;
  }

  .section {
    margin-bottom: 20px;
  }

  .section input[type="checkbox"] {
    display: none;
  }

  .section-header {
    background-color: #f7fafc;
    border-left: 4px solid #4299e1;
    padding: 10px 15px;
    margin: 10px 0;
    cursor: pointer;
    display: flex;
    justify-content: space-between;
    align-items: center;
    transition: background-color 0.2s;
  }

  .section-header:hover {
    background-color: #edf2f7;
  }

  .section-header::after {
    content: '+';
    font-size: 1.2em;
    font-weight: bold;
  }

  .section input[type="checkbox"]:checked ~ .section-header::after {
    content: '−';
  }

  .section-content {
    padding-left: 20px;
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.3s ease-out;
  }

  .section input[type="checkbox"]:checked ~ .section-content {
    max-height: 500px; /* Adjust based on content */
  }

  .section-content ul {
    list-style: none;
    padding-left: 20px;
    margin: 10px 0;
  }

  .section-content li {
    margin: 8px 0;
  }

  .section-content a {
    color: #4a5568;
    text-decoration: none;
    transition: color 0.2s;
  }

  .section-content a:hover {
    color: #2b6cb0;
  }

  .emoji {
    margin-right: 8px;
  }
</style>

<div class="wiki-toc">
  <h1>📚 Table of Contents</h1>
  
  <div class="section">
    <input type="checkbox" id="getting-started">
    <label class="section-header" for="getting-started">
      <span><span class="emoji">🚀</span> Getting Started</span>
    </label>
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
    <input type="checkbox" id="core-concepts">
    <label class="section-header" for="core-concepts">
      <span><span class="emoji">📖</span> Core Concepts</span>
    </label>
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
    <input type="checkbox" id="advanced">
    <label class="section-header" for="advanced">
      <span><span class="emoji">⚙️</span> Advanced Topics</span>
    </label>
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
    <input type="checkbox" id="api">
    <label class="section-header" for="api">
      <span><span class="emoji">🔌</span> API Reference</span>
    </label>
    <div class="section-content">
      <ul>
        <li><a href="api/overview">API Overview</a></li>
        <li><a href="api/endpoints">Endpoints</a></li>
        <li><a href="api/auth">Authentication</a></li>
      </ul>
    </div>
  </div>

  <div class="section">
    <input type="checkbox" id="troubleshooting">
    <label class="section-header" for="troubleshooting">
      <span><span class="emoji">🔍</span> Troubleshooting</span>
    </label>
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