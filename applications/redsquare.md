---
title: Red Square
description: 
published: true
date: 2025-07-29T21:45:19.911Z
tags: 
editor: markdown
dateCreated: 2023-01-23T00:47:55.328Z
---

# RedSquare
  
[Red Square](https://saito.io/redsquare/) is a decentralized Twitter clone that operates through the Saito Network. Users can create posts, track and follow their peers, leave comments and leverage open source moderation and curation tools.

Red Square is a powerful demonstration of the Saito Module system. Features like a [crypto wallet](tech/applications/wallet), gaming portal (powered by [Saito Arcade](/tech/applications/arcade)), P2P encrypted or public [chat](tech/applications/chat) and more are easily integrated thanks to the lego-brick nature of modules and UI Components.

- Red Square's updated [source code](https://github.com/SaitoTech/saito/tree/master/node/mods/redsquare) can be found on our Github.


### Why Build a Decentralized Twitter?

Unlike Twitter and even self-labelled "Web3" social media platforms like Mastodon and Nostr, the RedSquare network is P2P. Instead of relying on central servers or a few volunteer *instances*, every RedSquare user runs a node in their browser and relays tweets between peer nodes they are connected to across the swarm.

Moderation functions are similarly decentralized, meaning that your experience using the site will depend heavily on the friends you choose and the content you approve. Curation and moderation policies are in the hands of users and their communities rather than just central servers or instances.

![rs-mobile-dark.png](/rs-mobile-dark.png)

 
 <!--
<br><img src="/redsquare.png" alt="Screenshot of Red Square app: typing a reply with an emote to an image gallery post. Notification and home menus, chats, game invites, leaderboards, calander and more can be seen in the background.">
<br>
-->

If you are getting started with RedSquare, browse through the content you can see and start *following* users whose content you like. You'll not only get amplified access to their media streams, but you'll allow them to help sculpt the nature of the content you see by default: all fully transparently, and all without adding centralized parties to limit your freedom of action on the web.

Like many Saito applications, Red Square is agnostic to whether the content it processes arrives through on-chain or off-chain protocols. By default all content is broadcast onto the underlying Saito blockchain, but content can also be fetched from off-chain transaction archives. The architecture is designed to scale with the amount of traffic on the underlying blockchain, allowing users to shift more activity to off-chain peer-to-peer channels if public broadcast is too expensive.

![red-square-feed.jpg](/red-square-feed.jpg)

## Decentralized Moderation

Red Square provides users the tool to control the content on their feed, and to share their configurations with others. See the [modtools page](https://wiki.saito.io/applications/modtools) for more information.
  
![self-moderate.jpg](/self-moderate.jpg)


