---
title: QR Scanner
description: 
published: true
date: 2026-09-25T04:48:51.001Z
tags: 
editor: markdown
dateCreated: 2025-07-28T12:52:14.799Z
---

<div style="display:flex;align-items:center;gap:0.5rem;flex-wrap:wrap;margin-bottom:1rem"> <a href="https://mods.saito.io/qrscanner.saito" class="is-asset-link" style="display:inline-flex;align-items:center;gap:0.35rem;padding:0.55rem 0.9rem;border:1px solid #ccc;border-radius:6px;background:#fff;color:#333 !important;text-decoration:none;line-height:1;white-space:nowrap;"> <span>⬇</span> <span>Download Module</span> </a> <a href="https://github.com/SaitoTech/saito/tree/master/node/mods/qrscanner" style="display:inline-flex;align-items:center;gap:0.35rem;padding:0.55rem 0.9rem;border:1px solid #ccc;border-radius:6px;background:#fff;color:#333 !important;text-decoration:none;line-height:1;white-space:nowrap;"> <span>Source Code</span> <span style="font-size:0.85em;">↗</span> </a> <a href="https://wiki.saito.io/applications/install" style="display:inline-flex;align-items:center;gap:0.35rem;padding:0.55rem 0.9rem;border:1px solid #ccc;border-radius:6px;background:#fff;color:#333 !important;text-decoration:none;line-height:1;white-space:nowrap;"> <span>Installation Guide</span> <span style="font-size:0.85em;">↗</span> </a> </div> 


# QR Scanner

The Saito QRScanner module adds the ability for Saito wallets to generate QR codes and integrate with any hardware camera to scan them. This is reasonably basic functionality included in most wallets.

The QRScanner is provided as an installable module as it can be customized to provide extra features, such as programmatically executing features in other modules when QRCodes are scanned by users. This makes it desirable to have the QR scanner code running as a separate module instead of as a hardcoded part of the underlying wallet.

