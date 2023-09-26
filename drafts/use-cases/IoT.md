---
title: Use Cases
description: 
published: true
date: 2023-09-26T02:35:12.832Z
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

Public Key Infrastructures, also referred to as PKI networks, serve a vital role in a ubiquitous cryptographic primitive: key exchange. Safe and secure key exchange is so fundamental that it would be imspossible to fully describe every possible use case of scaalable and secure blockchain without first examining it.

Assyemtric cryptography makes it possible to set up a secure connection between any parties holding a public key pair, even when attackers can read the messages.  The problem is that such exchanges are vulnerable to *Man in the Middle* (MITM) *Attacks,* where an intercepting party can secretly place themselves between each party and dupe them into encrypting their data in favor of the attacker. Any parties communicating over an open network run the risk of anyone in between who can such messages intercepting and impersonating the authors.

Consult [Wikipedia](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) for a nice visual example.

In order to solve this problem, it is necessary to rely on PKI networks who will vouch for the authenticity of certain parties and thus allow users to spots public keys which do not have their blessing. PKI networks serve as the backbone of secure, remote communication, allowing two parties to establish a secure channel over an insecure network.

### Existing PKI Networks

Everyone who uses the internet today relies on PKI networks for security. All consumer web browsers are compiled, distributed and installed with their trust assumptions resting on the *certificate authorities* within the PKI which bind web domains to public keys and prevent MITM attacks. Without these certificates, it would never be clear to web browsers if a domain it attempted to connect with was truly private or being intercepted.

Typically, when someone on the internet wants to connect to a friend, they do not each register with a PKI network and have their identities certified globally in web browsers, instead they leverage the hiearchy of trust by navigating to a website which is verified by the certificate authority, creating a user account, and finding their friend's user account. The website which connects two parties serves as a miniature PKI network for users to connect.

By the time a casual user of the internet wants to connect with another, they are trusting the PKI network as well as any websites necessary to form a connection. PKI networks themselves have proven lucrative and concentrated targets of attack, both by government and rogue hackers, and websites themselves can be used to attack its users in similar ways.

Today's secure internet ultimately relies on trust in a small collection of authoritative parties who manage a record of identities bound to public keys, preventing MITM attacks. The trust is necessary because the authorities managing such infrastructure ultimtely decide its contents, who is allowed to be certified, and work against malicious parties who may abuse it to commit mass fraud.

### Blockchain as PKI

Saito is well suited to trustleslly perform the fundamental duties of a PKI without any authorities or any permission. Consider the key exchange again: two parties may share with each other their public keys over an insecure network and establish a secure connection between each other. Yet when they do so without the help of an authoritative web server or PKI network, they cannot be sure that no other parties exist between their secure connection.

If Alice wants to communicate with Bob and sends a transaction stating that intent, Mallory intercepts the message and instead publishes her own message to the blockchain. Bob recieves the same treatment, and what Mallory has ended up doing is publishing two transactions from herself purporting to be Alice and Bob. She then attempts to set up a connection between the two by convincing them to each individually connect to her.

But thanks to blockchain, and unlike public networks of the past, key exchange participants select their partners from a universal and uncensorable medium - where Mallory previously had the ability to censor for free, she now must resist the economic security of the blockchain in order to fulfill her attack.

Only when Alice and Bob both see that both of their messages were posted to the universal broadcast network do they then have economic security which protects those messages and allows each counterparty to see them in their original form. By establishing connections only after both messages appear on the blockchain, the attacker loses the crucial ability to censor those messages before replacing them and can thus no longer attempt the attack without being detected and ultimately shunned.

### Web 3

There are several considerations at play here which are very often taken for granted:

* The extent of the reliance on PKI networks for internet security
* The extent to which registering with Web 2 PKIs is permissioned 
* The security vulnerabilities of Web 2 PKIs
* The ability for blockchain to serve as PKI

Web 3 is well defined: a system of networking in which interested parties may safely connect directly to each other without any authoritative middlemen; without permission. By now it should be obvious that since the advent of public key cryptography, systems of authority have developed in order to solve the most basic problem of key exchange, and that all consumers rely on the security which  trickles down to social media platforms, and businesses on the blessings of authority to grant certificates.

Web 3, using blockchain as PKI, solves the MITM attack and does not require any participant to request certification from an authority, nor does it require users to rely on any heiarchies of trust which place them at the bottom rung. All participants in Web 3 will have access to a universal broadcast network which grants measurable and objective economic security to perform key direct exchange permissionlessly.

The way in which this reshapes the internet and a user's relationship to internet services is absolutely fundamental. For starters, the services which connect people need not be bound by any corporate interests, as users no longer rely on the trickle-down-trust that corporations recieve from Web 2 PKIs and sometimes pass faithfully down to users. Every individual instead has secure and direct access to one another via open source software.

While users may still have their preference of software based on user experience and user interface, their secure use of Web 3 relies on that software being open source, auditable to the public (else it may as well be Web 2 software considering the trust assumptions users must make). Though many choices may exist, they can each interoperate via the Web 3 PKI and peer-to-peer connections. Those designing user-facing software are no longer burdened with being shepards of *trust* - they instead allow user security to be handled by the most scalable and secure universal broadcast network: Saito blockchain.

When the internet is flipped on its head such that individuals are no longer dependent on the  authoritative and trusted coalitions of the internet today, Web 2 PKIs, there is no predicting from the ground floor all the developments which will generate. The Saito philosophy rests on one assumption: the internet is better when individuals have more freedom, soveriegnty and power - and the only way to provide that through an universal broadcast network which is secure against majority power and will not economically collapse or exclude users at scale.

## Permisionless Internet of Things

Internet of things refers to the market of smart devices which consumers and businesses own and control remotely.


### Privacy Concerns


### Saito use-case

## Timestamping

## Money