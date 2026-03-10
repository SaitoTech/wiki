---
title: QR Scanner
description: 
published: true
date: 2026-03-10T22:07:51.389Z
tags: 
editor: markdown
dateCreated: 2025-07-28T12:52:14.799Z
---

<div style="display: block;border: 2px solid rgb(204, 204, 204);border-radius: 8px;padding: 0.5rem;background-color: rgb(249, 249, 249);opacity: 1;z-index: 99999;position: relative;margin-bottom: 1rem;max-width: max-content;padding-top: 1rem;padding-bottom: 1rem;padding-left: 1rem;padding-right: 1rem;">
	<div class="header-box">
		<div id="download" class="toc-header" style="margin-top: 0px !important;display: grid;grid-template-columns: min-content 1fr;align-items: start;">
			<div class="header-box-title" style="width: max-content; float: left; display: relative;"> 📦 Download</div>
			<ul class="header-box-links" style="display: flex; gap: 3rem; padding-top: 0rem; margin-left: 1rem;">
				<li style="margin-top: 0px;"><a href="https://mods.saito.io/qrscanner.saito">Saito Module</a></li>
				<li style="margin-top: 0px;"><a href="https://github.com/SaitoTech/saito/tree/master/node/mods/qrscanner" class="">Source Code</a></li>
				<li style="margin-top: 0px;"><a href="https://wiki.saito.io/applications/install" class="">Installation Guide</a></li>
			</ul>
		</div>
	</div>
</div>


# QR Scanner

The Saito QRScanner module adds the ability for Saito wallets to generate QR codes and integrate with any hardware camera to scan them. This is reasonably basic functionality included in most wallets.

The QRScanner is provided as an installable module as it can be customized to provide extra features, such as programmatically executing features in other modules when QRCodes are scanned by users. This makes it desirable to have the QR scanner code running as a separate module instead of as a hardcoded part of the underlying wallet.

