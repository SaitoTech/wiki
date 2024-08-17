---
title: Swarmcast
description: 
published: true
date: 2024-08-17T03:29:13.103Z
tags: 
editor: markdown
dateCreated: 2024-08-17T03:29:13.103Z
---

# Swarmcast

[Swarmcast](https://saito.io/swarmcast) is a revolutionary peer-to-peer (P2P) livestreaming protocol that empowers users to create live audio and video broadcasts with just consumer hardware, at minimal cost, and without any logins or subscriptions.

![swarmcast-chat.png](/swarmcast-chat.png)

Swarmcast creates a branching network from a source broadcast:

1. The host streams content to a few initial peers.
2. These peers pass the content to more peers.
3. The process repeats, forming a “swarm” of connected users.

This recursive network structure allows for decent scale without relying on centralized servers or expensive infrastructure.

## Simulcast on YouTube

You can amplify a Swarmcast onto YouTube by providing a [YouTube Stream Key](https://support.google.com/youtube/answer/9854503?hl=en#zippy=%2Cstream-key). This feature currently requires you start a Swarmcast from within the [Video Call](https://saito.io/videocall/) app.

1. Start a Saito [Video Call](https://saito.io/videocall/)
2. Click the *Cast* button on the bottom row.
3. Click the YouTube icon in the top bar - enter your stream key
4. Hit the play button

