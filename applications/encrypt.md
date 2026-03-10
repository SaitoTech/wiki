---
title: Encrypt
description: 
published: true
date: 2026-03-10T19:47:38.278Z
tags: 
editor: markdown
dateCreated: 2025-05-20T03:09:22.031Z
---

<div style="display: block;border: 2px solid rgb(204, 204, 204);border-radius: 8px;padding: 0.5rem;background-color: rgb(249, 249, 249);opacity: 1;z-index: 99999;position: relative;margin-bottom: 1rem;max-width: max-content;padding-top: 1rem;padding-bottom: 1rem;padding-left: 1rem;padding-right: 1rem;">
	<div class="header-box">
		<div id="download" class="toc-header" style="margin-top: 0px !important;display: grid;grid-template-columns: min-content 1fr;align-items: start;">
			<div class="header-box-title" style="width: max-content; float: left; display: relative;"> 📦 Download</div>
			<ul class="header-box-links" style="display: flex; gap: 3rem; padding-top: 0rem; margin-left: 1rem;">
				<li style="margin-top: 0px;"><a href="https://mods.saito.io/encrypt.saito">Saito Module</a></li>
				<li style="margin-top: 0px;"><a href="https://github.com/SaitoTech/saito/tree/master/node/mods/encrypt" class="">Source Code</a></li>
				<li style="margin-top: 0px;"><a href="https://wiki.saito.io/applications/install" class="">Installation Guide</a></li>
			</ul>
		</div>
	</div>
</div>


# Saito Encrypt

The encrypt module leverages the Saito blockchain to perform a secure key-exchange between two addresses on the network. This permits users who cannot communicate securely otherwise to create a key to privately exchange information over the blockchain.

The Saito encrypt application is a utility module that most browsers will install by default. It is used whenever you add a user to your contact list in order to create a secure way for you to communicate with your friends without a need for reliance on a central server.

## What Problem Does Saito Solve?

In traditional networks, generating secure secrets exposes users to [*Man-in-the-Middle* Attacks (MITM)](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) where any third party who can intercept the key exchange can listen in on the communications of two parties who believe they are secure.

Saito solves this by adding *authentication* to the process of key exchange. As long as the parties have knowledge of their address on the network (assumed in security model) their creation of a shared secret is still possible as the network itself forces each party to authenticate itself in order to respond.

For more information on interception attacks in distributed PKI networks, see the following page:

https://cromwell-intl.com/cybersecurity/pki-failures.html#badly


