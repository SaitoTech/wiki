---
title: Moderation Tools
description: 
published: true
date: 2026-09-25T04:44:02.626Z
tags: 
editor: markdown
dateCreated: 2025-07-28T11:53:49.645Z
---

<div style="display:flex;align-items:center;gap:0.5rem;flex-wrap:wrap;margin-bottom:1rem"> <a href="https://mods.saito.io/modtools.saito" class="is-asset-link" style="display:inline-flex;align-items:center;gap:0.35rem;padding:0.55rem 0.9rem;border:1px solid #ccc;border-radius:6px;background:#fff;color:#333 !important;text-decoration:none;line-height:1;white-space:nowrap;"> <span>⬇</span> <span>Download Module</span> </a> <a href="https://github.com/SaitoTech/saito/tree/master/node/mods/modtools" style="display:inline-flex;align-items:center;gap:0.35rem;padding:0.55rem 0.9rem;border:1px solid #ccc;border-radius:6px;background:#fff;color:#333 !important;text-decoration:none;line-height:1;white-space:nowrap;"> <span>Source Code</span> <span style="font-size:0.85em;">↗</span> </a> <a href="https://wiki.saito.io/applications/install" style="display:inline-flex;align-items:center;gap:0.35rem;padding:0.55rem 0.9rem;border:1px solid #ccc;border-radius:6px;background:#fff;color:#333 !important;text-decoration:none;line-height:1;white-space:nowrap;"> <span>Installation Guide</span> <span style="font-size:0.85em;">↗</span> </a> </div> 

# Moderation Tools

This module adds support for blacklisting and whitelisting which can be used by all other Saito modules to restrict access to spammers, by providing a secondary and entirely-customizable firewall that users can configure to control which transactions are executed.

In addition to providing support for account blacklisting and whitelisting, the module also provides a way for friends to share their blacklists and whitelists, so that users can implicitly whitelist friends of friends and blacklist spammers collectively. This is essentially a form of decentralized moderation where your friends on the network can help contain spammers by sharing their access lists.

Moderation is used most heavily by RedSquare to try and create a welcoming environment and protect the network and its users from malicious spammers, while nonetheless treating those spammers as first class citizens on the network.

This module is included by default in most Saito wallets. In addition to being a functional module in and of itself, the moderation functions that are extended in this module may be extended by any other module, turning it into a tutorial of sorts in how to write moderation functions that will encourage applications to selectively execute content based on the preferences of the module authors themselves.
