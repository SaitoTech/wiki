---
title: Registry
description: 
published: true
date: 2025-05-20T06:34:04.856Z
tags: 
editor: markdown
dateCreated: 2025-05-20T06:34:04.856Z
---

# Saito Registry (DNS)

The Saito Registry module is a low-level utility module that allows Saito to identify users by usernames instead of just by their cryptographic publickeys. When you see an application display a username instead of a alphanumeric string, you are seeing the results of this module.

The difference between this Saito DNS mechanism and centralized DNS systems is that users have free choice over which registry modules they install. Two users who have different modules installed may show different usernames for the same contacts.

The Saito Registry module is designed to work as painlessly as possible. Applications that use the Saito User UI-Component to display user avatars and usernames will find that their applications will automatically display usernames where possible based on whatever registry module users have installed.