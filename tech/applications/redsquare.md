---
title: Red Square
description: 
published: true
date: 2024-12-10T20:15:20.901Z
tags: 
editor: markdown
dateCreated: 2023-01-23T00:47:55.328Z
---

# Saito Red Square
  
[Red Square](https://saito.io/redsquare/) is a P2P clone of Twitter that runs atop the Saito Network. Users can create posts, track and follow their peers, and leave comments or otherwise engage with other people's content.

<!--In addition to Twitter-like functionality, [Red Square](/tech/applications/redsquare) includes a real-time chat functions (powered by Saito Chat), gaming portal (powered by Saito Arcade) and other gaming features like leaderboards. These demonstrate the power of Saito Modules to not only provide features, but add UI Components to other elements.-->

Red Square is also our most powerful demonstration of the Saito Module system. Features like a [crypto wallet](tech/applications/wallet), gaming portal (powered by [Saito Arcade](/tech/applications/arcade)), P2P encrypted, and public [chat](tech/applications/chat) and more are easily integrated thanks to the way lego-brick nature of modules and UI Components.


- Red Square's updated [source code](https://github.com/SaitoTech/saito-lite-rust/tree/master/mods/redsquare) can be found on our Github.


### Why Build a Decentralized Twitter?

Unlike Twitter and other "Web3" social media platforms like Mastadon and Nostr, RedSquare is genuinely decentralized. What this means is that instead of fetching "tweets" and other content from a single server which controls which accounts exist and restricts their access to data, RedSquare users run the application in their browser and request tweets from whichever peer nodes they are connected to across the swarm.

Moderation functions are similarly decentralized, meaning that your experience using the site will depend heavily on the friends you make online. This allows RedSquare to achieve what mainstreain sites like Mastadon or Nostr fail to provide: a truly uncensorable public square in which all users are treated on equal terms, with curation and moderation policies fully in the hands of users and their friends.

![rs-mobile-dark.png](/rs-mobile-dark.png)

 
 <!--
<br><img src="/redsquare.png" alt="Screenshot of Red Square app: typing a reply with an emote to an image gallery post. Notification and home menus, chats, game invites, leaderboards, calender and more can be seen in the background.">
<br>
-->

Like many Saito applications, Red Square is agnostic to whether the content it processes arrives through on-chain or off-chain protocols. By default all content is broadcast onto the underlying Saito blockchain, but content can also be fetched from off-chain transaction archives. The architecture is designed to scale with the amount of traffic on the underlying blockchain, allowing users to shift more activity to off-chain peer-to-peer channels if public broadcast is too expensive.
    
If you are getting started with RedSquare, browse through the content you can see and start *following* users whose content you like. You'll not only get amplified access to their media streams, but you'll allow them to help sculpt the nature of the content you see by default: all fully transparently, and all without adding centralized parties to limit your freedom of action on the web.

![red-square-feed.jpg](/red-square-feed.jpg)

## [DeMod](https://saito.tech/saito-modtools-decentralized-moderation/) - Decentralized Moderation

One of the most important problems addressed by RedSquare is content moderation in a truly decentralized network, with no a trusted third-party to limit access. Red Square handled this by empowering the user.
  
![self-moderate.jpg](/self-moderate.jpg) 

If you wish to hide or block a certain user, click on the tweet and select the appropriate response. In the event of illegal or highly-unethical content, we encourage users to *report* the tweets so the Saito Team can ensure we are not amplifying harmful materials by default.

Spam and fraud prevention, curation and moderation consequently flow from the aggregate preferences of the users to whom you are connected. Instead of relying on centralized parties like Elon Musk to limit access by controlling accounts, RedSquare shifts to a permissionless model where spam is controlled by a decentralized swarm of users flagging and blocking it in real-time.

As site traffic grows and trivial fees become necessary to post tweets, the economic requirements are expected to provide an additional sanity-check against the willful spamming of malicious or harmful materials. Just like a verified Twitter account has less incentive to spam, users may elect to only view Red Square posts that have paid a small network fee, of have some crypto staked to their account.

**Distributed Whitelists and Blacklists**

Most users of the internet don't want a highly proactive relationship with content - they simply want good curation. Open-source, distributed whitelists and blacklists for content solve for this: users can subscribe to sensible policies determined by those they trust, but are also freely able to edit, opt-out or otherwise customize their experience.

The benefits and conveniences of platforms performing moderation functions can still be enjoyed, but not without the ability for each individual user to perform personal oversight and take matters into their own hands as they see fit. Rather than a company buyout or state pressure being necessary to change moderation policy, users can create and select for what they personally see fit.
