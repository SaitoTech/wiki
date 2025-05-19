---
title: Chat
description: 
published: true
date: 2025-05-19T13:54:02.672Z
tags: 
editor: markdown
dateCreated: 2023-03-09T04:44:07.894Z
---

# Saito Chat

[Saito Chat](https://saito.io/chat/) lets you send chat messages, images and more P2P to your friends on the Saito network. Once you have added a contact, your browser will perform a cryptographic handshake that will let you encrypt your messages to them with a private key that only the two of you know.

- Saito Chat [source code.](https://github.com/SaitoTech/saito-lite-rust/tree/master/mods/chat)

![chat-aug-2024.png](/chat-aug-2024.png)

Saito Chat is designed as both an on-chain and off-chain applications, while your browser will likely receive the majority of chat messages directly from other peers, it is also possible to send messages to other users fully on-chain. Communications are quick and secure and involve only the encrypted blockchain messages or messages directly to your recipients - no middlemen to trust for security.

In addition to private chats, the Saito Chat module also supports public channels like the Saito Community Chat - public rooms in which all messages are unencrypted by default. The chat module is also easy to integrate with other applications. You can see it in the sidebar of [Red Square](/tech/applications/redsquare) as well as access it within [games](/tech/applications/arcade) to chat with fellow players.

## How to Add a Contact

To add a friend to Saito Chat click on the "..." menu at the top-right of your Chat menu and select the appropriate option based on the type of account you are trying to add. You can also add contacts by clicking on their username or publickey. This will pull up the User Menu shown in the image below.

![chat-private.png](/chat-private.png)

It normally takes a minute or two for the network to perform a key exchange needed to securely and efficiently communicate off-chain with your new contact. Their address will not be added to your Chat menu until this process is complete. If the person you are adding is not online, you will need to wait until they connect until their wallet can provide the information needed to connect you. Their wallet will receive your request as soon as they re-join the network.

