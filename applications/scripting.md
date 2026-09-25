---
title: Saito Scriptorium
description: An application to assist with the development and debugging of Saito Scripts, for use by applications and NFTs and transactions.
published: true
date: 2026-09-25T04:50:43.956Z
tags: 
editor: markdown
dateCreated: 2025-11-19T09:24:27.528Z
---

<div style="display:flex;align-items:center;gap:0.5rem;flex-wrap:wrap;margin-bottom:1rem"> <a href="https://mods.saito.io/rustscript.saito" class="is-asset-link" style="display:inline-flex;align-items:center;gap:0.35rem;padding:0.55rem 0.9rem;border:1px solid #ccc;border-radius:6px;background:#fff;color:#333 !important;text-decoration:none;line-height:1;white-space:nowrap;"> <span>⬇</span> <span>Download Module</span> </a> <a href="https://github.com/SaitoTech/saito/tree/master/node/mods/rustscript" style="display:inline-flex;align-items:center;gap:0.35rem;padding:0.55rem 0.9rem;border:1px solid #ccc;border-radius:6px;background:#fff;color:#333 !important;text-decoration:none;line-height:1;white-space:nowrap;"> <span>Source Code</span> <span style="font-size:0.85em;">↗</span> </a> <a href="https://wiki.saito.io/applications/install" style="display:inline-flex;align-items:center;gap:0.35rem;padding:0.55rem 0.9rem;border:1px solid #ccc;border-radius:6px;background:#fff;color:#333 !important;text-decoration:none;line-height:1;white-space:nowrap;"> <span>Installation Guide</span> <span style="font-size:0.85em;">↗</span> </a> </div> 


# Rustscript Scriptorium

The [Saito Scriptorium](https://staging.saito.io/scripting/) is a module used to develop scripts that add higher-level scripting features to Saito modules and NFTs. If you are new to Saito Scripting, you can get an introduction to the underlying concepts and learn how to write scripts on on [dedicated scripting page](/docs/scripting).

<br />

<img src="/img/scripting-ui.png" style="max-width: 600px;">

The image above shows the script being developed on the left, the witness data needed to evaluate it, and a number of tools towards the bottom used when writing apps, like the ability to sign messages (with the privatekey of the browser) and generate hashes, etc.

The Scriptorium is used heavily by many of the more powerful Saito applications and features, such as the [Saito Vault](/applications/vault), which uses scripts to restrict access to privately stored and encrypted transaction data.
