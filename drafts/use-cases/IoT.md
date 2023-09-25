---
title: Use Cases
description: 
published: true
date: 2023-09-25T06:04:29.281Z
tags: 
editor: markdown
dateCreated: 2023-09-24T01:04:19.828Z
---

# Use Cases

## What Does Saito Do?

A common question for those investigating a new blockchain: what are its use cases? Money, smart contracts, decentralized finance, trustless computation - use cases are evolving constantly. But the creation of new projects to address each use case is unecessary and counter-productive. The common utility beneath all blockchain use cases is the *universal broadcast network*, and the quality of any application of blockchain ultimately relies on this.

Saito's consensus mechanism is fundamentally oriented towards providing an application-agnostic universal broadcast layer, which is optimizes for providing [security](https://wiki.saito.io/consensus/majoritarian-attacks) and affordability for any permisionless application at any scale, including applications for which blockchain was previously too expensive to even consider. By optimizing for universal broadcast rather than any specific use case, the network bears utility for users of all financial and social status.

## Public Key Infrastructure

### Man-in-the-Middle Attacks

Public Key Infrastructures, also referred to as PKI networks, serve a vital role in a ubiquitous cryptographic primitive: key exchange. Assyemtric cryptography makes it possible to set up a secure connection between any parties holding a public key pair, even when attackers can read the messages.

The problem is that such exchanges are vulnerable to *Man in the Middle* (MITM) *Attacks,* where an intercepting party can secretly place themselves between each party and dupe them into encrypting their data in favor of the attacker. Any parties communicating over an open network run the risk of anyone in between who can such messages intercepting and impersonating the authors.

Consult [Wikipedia](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) for a nice visual example.

In order to solve this problem, it is necessary to rely on PKI networks who will vouch for the authenticity of certain parties and thus allow users to spots public keys which do not have their blessing. PKI networks serve as the backbone of secure, remote communication, allowing two parties to establish a secure channel over an insecure network.

### Existing PKI Networks

Everyone who uses the internet today relies on PKI networks for security. All consumer web browsers are compiled, distributed and installed with their trust assumptions resting on the *certificate authorities* within the PKI which bind web domains to public keys and prevent MITM attacks. Without these certificates, it would never be clear to web browsers if a domain it attempted to connect with was truly private or being intercepted.

Typically, when someone on the internet wants to connect to a friend, they do not each register with a PKI network and have their identities certified globally in web browsers, instead they leverage the hiearchy of trust by navigating to a website which is verified by the certificate authority, creating a user account, and finding their friend's user account. The website which connects two parties serves as a miniature PKI network for users to connect.

By the time a casual user of the internet wants to connect with another, they are trusting the PKI network as well as any websites necessary to form a connection. PKI networks themselves have proven lucrative and concentrated targets of attack, both by government and rogue hackers, and websites themselves can be used to attack its users in similar ways.

Today's secure internet ultimately relies on trust in a small collection of authoritative parties who manage a record of identities bound to public keys, preventing MITM attacks. The trust is necessary because the authorities managing such infrastructure ultimtely decide its contents, who is allowed to be certified, and work against malicious parties who may abuse it to commit mass fraud.

### Web 3

Saito is well suited to trustleslly perform the fundamental duties of a PKI without any authorities or any permission. Consider the key exchange again: two parties may share with each other their public keys over an insecure network and establish a secure connection between each other. Yet when they do so without the help of an authoritative web server or PKI network, they cannot be sure that no other parties exist between their secure connection.

If instead each party publishes their initial messages to the blockchain, the MITM attackers lose the ability to freely censor before passing it on.

## Permisionless Internet of Things

Internet of things refers to the market of smart devices which consumers and businesses own and control remotely.


### Privacy Concerns


### Saito use-case

## Timestamping

## Money