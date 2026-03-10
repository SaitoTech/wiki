---
title: Moderation Tools
description: 
published: true
date: 2026-03-10T22:00:16.694Z
tags: 
editor: markdown
dateCreated: 2025-07-28T11:53:49.645Z
---

<div style="display: block;border: 2px solid rgb(204, 204, 204);border-radius: 8px;padding: 0.5rem;background-color: rgb(249, 249, 249);opacity: 1;z-index: 99999;position: relative;margin-bottom: 1rem;max-width: max-content;padding-top: 1rem;padding-bottom: 1rem;padding-left: 1rem;padding-right: 1rem;">
	<div class="header-box">
		<div id="download" class="toc-header" style="margin-top: 0px !important;display: grid;grid-template-columns: min-content 1fr;align-items: start;">
			<div class="header-box-title" style="width: max-content; float: left; display: relative;"> 📦 Download</div>
			<ul class="header-box-links" style="display: flex; gap: 3rem; padding-top: 0rem; margin-left: 1rem;">
				<li style="margin-top: 0px;"><a href="https://mods.saito.io/modtools.saito">Saito Module</a></li>
				<li style="margin-top: 0px;"><a href="https://github.com/SaitoTech/saito/tree/master/node/mods/mahjong" class="">Source Code</a></li>
				<li style="margin-top: 0px;"><a href="https://wiki.saito.io/applications/install" class="">Installation Guide</a></li>
			</ul>
		</div>
	</div>
</div>


# Moderation Tools

This module adds support for blacklisting and whitelisting which can be used by all other Saito modules to restrict access to spammers, by providing a secondary and entirely-customizable firewall that users can configure to control which transactions are executed.

In addition to providing support for account blacklisting and whitelisting, the module also provides a way for friends to share their blacklists and whitelists, so that users can implicitly whitelist friends of friends and blacklist spammers collectively. This is essentially a form of decentralized moderation where your friends on the network can help contain spammers by sharing their access lists.

Moderation is used most heavily by RedSquare to try and create a welcoming environment and protect the network and its users from malicious spammers, while nonetheless treating those spammers as first class citizens on the network.

This module is included by default in most Saito wallets. In addition to being a functional module in and of itself, the moderation functions that are extended in this module may be extended by any other module, turning it into a tutorial of sorts in how to write moderation functions that will encourage applications to selectively execute content based on the preferences of the module authors themselves.
