---
title: Upgrade Saito nodejs stack
description: 
published: true
date: 2026-09-08T04:16:38.792Z
tags: 
editor: markdown
dateCreated: 2026-09-08T04:16:38.792Z
---

# Upgrade Saito nodejs stack
Updated: 2026-09-08

## Instructions

These instructions cover upgrading a running Saito node to the newest version.

| Step | Notes |
|------|-------|
| `cd <path to saito node folder>` | likely `opt/saito/node` |
| `git switch prod` | Make sure you are on the `prod` branch |
| `git pull` | Get the latest code and scripts |
| `npm run upgrade-modules-config` | This script:<br>- removes any deprecated modules<br>- ensures the node is running at least `admin` and `explorer`<br>- sanity checks that referenced modules are available<br>- validates formatting and correctness<br><br>This can be run after manually updating `modules.config.js` without issue.<br><br>`npm run upgrade-modules-config -- --dry-run` will show what will be done without making any changes |
| `npm run upgrade-module-databases` | This script:<br>- backs up databases<br>- checks all database definitions in installed modules exist<br>- adds any missing tables<br>- adds any missing columns or indexes to tables<br><br>`npm run upgrade-module-databases -- --dry-run` will show changes to be made without making changes |
| `npm install` | Install the new Rust core WASM |
| `npm run compile` | Upgrade 'userland' |
| Restart node | Likely `pm2 restart` or your custom process manager command to run `npm start` |