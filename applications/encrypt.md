---
title: Encrypt
description: 
published: true
date: 2026-09-25T04:42:13.550Z
tags: 
editor: markdown
dateCreated: 2025-05-20T03:09:22.031Z
---

<div style="display:flex;align-items:center;gap:0.5rem;flex-wrap:wrap;margin-bottom:1rem"> <a href="https://mods.saito.io/encrypt.saito" class="is-asset-link" style="display:inline-flex;align-items:center;gap:0.35rem;padding:0.55rem 0.9rem;border:1px solid #ccc;border-radius:6px;background:#fff;color:#333 !important;text-decoration:none;line-height:1;white-space:nowrap;"> <span>⬇</span> <span>Download Module</span> </a> <a href="https://github.com/SaitoTech/saito/tree/master/node/mods/encrypt" style="display:inline-flex;align-items:center;gap:0.35rem;padding:0.55rem 0.9rem;border:1px solid #ccc;border-radius:6px;background:#fff;color:#333 !important;text-decoration:none;line-height:1;white-space:nowrap;"> <span>Source Code</span> <span style="font-size:0.85em;">↗</span> </a> <a href="https://wiki.saito.io/applications/install" style="display:inline-flex;align-items:center;gap:0.35rem;padding:0.55rem 0.9rem;border:1px solid #ccc;border-radius:6px;background:#fff;color:#333 !important;text-decoration:none;line-height:1;white-space:nowrap;"> <span>Installation Guide</span> <span style="font-size:0.85em;">↗</span> </a> </div> 

# Saito Encrypt

The encrypt module leverages the Saito blockchain to perform a secure key-exchange between two addresses on the network. This permits users who cannot communicate securely otherwise to create a key to privately exchange information over the blockchain.

The Saito encrypt application is a utility module that most browsers will install by default. It is used whenever you add a user to your contact list in order to create a secure way for you to communicate with your friends without a need for reliance on a central server.

## What Problem Does Saito Solve?

In traditional networks, generating secure secrets exposes users to [*Man-in-the-Middle* Attacks (MITM)](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) where any third party who can intercept the key exchange can listen in on the communications of two parties who believe they are secure.

Saito solves this by adding *authentication* to the process of key exchange. As long as the parties have knowledge of their address on the network (assumed in security model) their creation of a shared secret is still possible as the network itself forces each party to authenticate itself in order to respond.

For more information on interception attacks in distributed PKI networks, see the following page:

https://cromwell-intl.com/cybersecurity/pki-failures.html#badly


