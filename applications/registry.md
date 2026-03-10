---
title: Registry
description: 
published: true
date: 2026-03-10T22:15:14.993Z
tags: 
editor: markdown
dateCreated: 2025-05-20T06:34:04.856Z
---

<div style="display: block;border: 2px solid rgb(204, 204, 204);border-radius: 8px;padding: 0.5rem;background-color: rgb(249, 249, 249);opacity: 1;z-index: 99999;position: relative;margin-bottom: 1rem;max-width: max-content;padding-top: 1rem;padding-bottom: 1rem;padding-left: 1rem;padding-right: 1rem;">
	<div class="header-box">
		<div id="download" class="toc-header" style="margin-top: 0px !important;display: grid;grid-template-columns: min-content 1fr;align-items: start;">
			<div class="header-box-title" style="width: max-content; float: left; display: relative;"> 📦 Download</div>
			<ul class="header-box-links" style="display: flex; gap: 3rem; padding-top: 0rem; margin-left: 1rem;">
				<li style="margin-top: 0px;"><a href="https://mods.saito.io/registry.saito" class="is-asset-link">Saito Module</a></li>
				<li style="margin-top: 0px;"><a href="https://github.com/SaitoTech/saito/tree/master/node/mods/registry" class="">Source Code</a></li>
				<li style="margin-top: 0px;"><a href="https://wiki.saito.io/applications/install" class="">Installation Guide</a></li>
			</ul>
		</div>
	</div>
</div>


# Saito Registry (DNS)

The Saito Registry module is a low-level utility module that allows Saito to identify users by usernames instead of just by their cryptographic publickeys. When you see an application display a username instead of a alphanumeric string, you are seeing the results of this module.

The difference between this Saito DNS mechanism and centralized DNS systems is that users have free choice over which registry modules they install. Two users who have different modules installed may show different usernames for the same contacts.

The Saito Registry module is designed to work as painlessly as possible. Applications that use the Saito User UI-Component to display user avatars and usernames will find that their applications will automatically display usernames where possible based on whatever registry module users have installed.