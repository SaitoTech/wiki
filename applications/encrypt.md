---
title: Encrypt
description: 
published: true
date: 2025-07-28T10:06:12.354Z
tags: 
editor: markdown
dateCreated: 2025-05-20T03:09:22.031Z
---

# Saito Encrypt

The encrypt module leverages the Saito blockchain to perform a secure key-exchange between two addresses on the network. This permits users who cannot communicate securely otherwise to create a key to privately exchange information over the blockchain.

The Saito encrypt application is a utility module that most browsers will install by default. It is used whenever you add a user to your contact list in order to create a secure way for you to communicate with your friends without a need for reliance on a central server.

## What Problem Does Saito Solve?

In traditional networks, generating secure secrets exposes users to [*Man-in-the-Middle* Attacks (MITM)](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) where any third party who can intercept the key exchange can listen in on the communications of two parties who believe they are secure.

Saito solves this by adding *authentication* to the process of key exchange. As long as the parties have knowledge of their address on the network (assumed in security model) their creation of a shared secret is still possible as the network itself forces each party to authenticate itself in order to respond.

For more information on interception attacks in distributed PKI networks, see the following page:

https://cromwell-intl.com/cybersecurity/pki-failures.html#badly


