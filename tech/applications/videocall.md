---
title: Video Call
description: 
published: true
date: 2024-09-15T21:01:42.749Z
tags: 
editor: markdown
dateCreated: 2023-03-27T03:22:36.662Z
---

# Video Call

[Saito Video Call](https://saito.io/videocall/) is a peer-to-peer, end-to-end encrypted video conferencing tool for everyday use. And because it is decentralized you don't need to download software, create an account, or provide your phone or credit card number to use it - just create the call and share the link with a friend.

- Video Call [source code.](https://github.com/SaitoTech/saito-lite-rust/tree/master/mods/videocall)

<br>
  
<img src="/saito-talk.jpg" style="maxwidth: 600px;">

In addition to direct calls, video calls also come with chat channels, and support standard use cases like sharing presentations. You can also now [swarmcast](/tech/applications/swarmcast) your video calls to turn private calls into realtime public broadcasts.

Video Call can be accessed directly via the above link or through the slide-in menu that is visible in [Red Square](https://saito.io/redsquare/) and other applications.

## How it Works

Saito Video Call uses WebRTC to negotiate direct P2P connections between clients. The Saito Blockchain and routing network serve as the coordation layer both to authenticate users and to perform peer discovery, as well as provide incentives to any nodes hosting STUN/TURN services.

Because the coordation layer and application are completely open protocols, users, developers and security researchers can all enjoy, leverage and audit the same robust infrastructure without the hassle of a privatized middleman service like Zoom extorting money, privacy and sanity.

<!--
<br>
<div style="display: flex; justify-content: center;">
    <img src="/howtosaitocall.gif" width="400" alt="Use hamburger menu then Saito Call button to use the app">
</div>
-->