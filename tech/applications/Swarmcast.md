---
title: Swarmcast
description: 
published: true
date: 2024-08-18T18:10:01.042Z
tags: 
editor: markdown
dateCreated: 2024-08-17T03:29:13.103Z
---

[Swarmcast](https://saito.io/swarmcast) is a revolutionary peer-to-peer (P2P) livestreaming protocol that empowers users to create live audio and video broadcasts with just consumer hardware, at minimal cost, and without any logins or subscriptions.

![swarmcast-chat.png](/swarmcast-chat.png)

Swarmcast creates a branching network from a source broadcast:

1. The host streams content to a few initial peers.
2. These peers pass the content to more peers.
3. The process repeats, forming a “swarm” of connected users.

This recursive network structure allows for decent scale without relying on centralized servers or expensive infrastructure.

## How to Simulcast on YouTube

You can amplify (restream) a Swarmcast onto YouTube by providing a [YouTube Stream Key](https://support.google.com/youtube/answer/9854503?hl=en#zippy=%2Cstream-key). This feature currently requires you start a Swarmcast from within the [Video Call](https://saito.io/videocall/) app.


## Steps:

**1. Start a Saito [Video Call](https://saito.io/videocall/)**
**2. Click the *Cast* button on the bottom row - enter a title and description.**
![step1-cast-circle.png](/step1-cast-circle.png)
![step2-namecast.png](/step2-namecast.png)
**3. Click the YouTube icon in the top bar - enter your stream key.**
![step3-youtube-button-circled.png](/step3-youtube-button-circled.png)
![step4-enterkey.png](/step4-enterkey.png)
**4. Hit the play button.**
![step3-youtube-button-circle-start.png](/step3-youtube-button-circle-start.png)

Congratulations! You are now streaming P2P with YouTube amplification! Viewers have the option of finding your stream and connecting directly via [Swarmcast](https://saito.io/swarmcast) or your YouTube Stream. 