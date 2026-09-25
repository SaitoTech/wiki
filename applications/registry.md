---
title: Registry
description: 
published: true
date: 2026-09-25T04:50:16.268Z
tags: 
editor: markdown
dateCreated: 2025-05-20T06:34:04.856Z
---

<div style="display:flex;align-items:center;gap:0.5rem;flex-wrap:wrap;margin-bottom:1rem"> <a href="https://mods.saito.io/registry.saito" class="is-asset-link" style="display:inline-flex;align-items:center;gap:0.35rem;padding:0.55rem 0.9rem;border:1px solid #ccc;border-radius:6px;background:#fff;color:#333 !important;text-decoration:none;line-height:1;white-space:nowrap;"> <span>⬇</span> <span>Download Module</span> </a> <a href="https://github.com/SaitoTech/saito/tree/master/node/mods/registry" style="display:inline-flex;align-items:center;gap:0.35rem;padding:0.55rem 0.9rem;border:1px solid #ccc;border-radius:6px;background:#fff;color:#333 !important;text-decoration:none;line-height:1;white-space:nowrap;"> <span>Source Code</span> <span style="font-size:0.85em;">↗</span> </a> <a href="https://wiki.saito.io/applications/install" style="display:inline-flex;align-items:center;gap:0.35rem;padding:0.55rem 0.9rem;border:1px solid #ccc;border-radius:6px;background:#fff;color:#333 !important;text-decoration:none;line-height:1;white-space:nowrap;"> <span>Installation Guide</span> <span style="font-size:0.85em;">↗</span> </a> </div> 



# Saito Registry (DNS)

The Saito Registry module is a low-level utility module that allows Saito to identify users by usernames instead of just by their cryptographic publickeys. When you see an application display a username instead of a alphanumeric string, you are seeing the results of this module.

The difference between this Saito DNS mechanism and centralized DNS systems is that users have free choice over which registry modules they install. Two users who have different modules installed may show different usernames for the same contacts.

The Saito Registry module is designed to work as painlessly as possible. Applications that use the Saito User UI-Component to display user avatars and usernames will find that their applications will automatically display usernames where possible based on whatever registry module users have installed.