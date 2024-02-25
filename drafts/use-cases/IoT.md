---
title: Use Cases
description: 
published: true
date: 2024-02-25T03:43:57.917Z
tags: 
editor: markdown
dateCreated: 2023-09-24T01:04:19.828Z
---

# Use Cases

This page serves as an abstract discussion of the utility of Saito and scalable blockchain generally. To learn more about the applications running on Saito currently, visit the [applications](https://wiki.saito.io/en/tech/applications) page of the Wiki.

<ul style="color:">
  <li> 1. <a style="text-decoration:none" href="#1"> What Does Saito Do?</a> </li>
  <li> 2. <a style="text-decoration:none" href="#2"> What Does Saito Pay For?</a> </li>
  <li> 3. <a style="text-decoration:none" href="#3"> Public Key Infrastructure</a> </li>
  <ul>
    <li> 3a. <a style="text-decoration:none" href="#3a"> Man-in-the-Middle Attacks </a> </li>
    <li> 3b. <a style="text-decoration:none" href="#3b"> Implicit PKI Networks </a> </li>
    <li> 3c. <a style="text-decoration:none" href="#3b"> Blockchain as PKI </a> </li>
    <li> 3d. <a style="text-decoration:none" href="#3b"> Web 3 </a> </li>
  </ul>
  <br>
  <li> 4. <a style="text-decoration:none" href="#3b"> Permissionless Internet of Things </a> </li>
</ul>
  
## <div id="1">What Does Saito Do?</div>

Saito's primary use case is the most fundamental utility blockchain, implemented with superiority over all previous designs: Universal Broadcast.

A common question for those investigating a new blockchain is "what are its use cases?" Money, smart contracts, decentralized finance, trustless computation - applications of blockchain are evolving constantly. But in a very fundamental sense, the blockchain has a singular source of value from which all applications flow: *Universal Broadcast*.

Universal Broadcast means a network in which anyone paying the market rate may publish and access data. The uncensorable and open nature of many existing blockchains, notably including Bitcoin, allows this same utility, but Saito consensus is the only protocol design which allows for a universal broadcast blockchain network which optimizes for the lowest possible fee-rate.

Saito achieves this by incentivizing the provision of the very network resources which scales performance, increases volume, or drives individual fees down. Because Saito can scale arbitrarily large without latent economic misalignments waiting to enforce bottlenecks, use cases for which many believe are impossibly expensive for blockchain are possible on Saito at a global scale.

<!--
pays for data distribution and broadcasts the data 'universally' i.e. to every node in the network. This feature is crucial to censorship resistance and to ensuring all participants share and agree on the network state.

For this reason, the creation of new projects to address each use case is largely unnecessary and counter-productive. The common need for a *universal broadcast network* which these applications share implies that the blockchain for which the majority of application development and economic security should accumulate is the one which best serves that need.

## <div id="2"> What Does Saito Pay For?</div>

One of the most common arguments for new chains created to serve new use cases is that the new chain is built to fund that specific utility - thus it is a "utility chain." Saito invalidates this argument in two ways:

1. It recognizes that diverting funding explicitly towards some overly specified 'utility' degrades necessary funding towards Universal Broadcast

2. Saito pays nodes generating fee volume; therefore it naturally funds *any* utility which users demand.

Thanks to Saito, it is no longer necessary to redesign consensus to pay for every new use case; a dangerous practice which both fractures security across chains and constraints the market's ability to generally fund infrastructure. Because Saito rewards the service of users as its form of security rather than any arbitrary form of work, the best performing nodes are incentivized to efficiently provide scale without sacrificing (and actually [enhancing](https://wiki.saito.io/consensus/attack-vectors)) security.

Saito consensus rewards nodes for collecting transaction fees, so any node which provides Universal Broadcast via its Saito application is paid. This makes the many utilities of blockchain far more flexible and secure as they do not need to 'bring their own (economic) security,' and the incentives of nodes is to compete to provide the lowest fee.

Applications for which blockchain was previously too expensive to even consider are now possible thanks to Saito's ability to universally broadcast data at a market rate, paying not much more than typical bandwidth and storage costs. The most fundamental use case, which all secure internet communication relies on, is the Public Key Infrastructure.
-->
## <div id="3">Public Key Infrastructure</div>

Public Key Infrastructures (PKI) are one of the most important but least discussed components of the modern, secure, internet. Their origins come from the early desire to securely transact electronically over the web; without them, ecommerce as we know it could not exist - nor could the other security assumptions many take for granted while using the internet. 

It is fitting that the next generation of PKI stems too from a general upgrade in the way we transact with one another. In much the same way that this need to securely send money lead to the modern PKIs and their emergent use cases, Saito, an economic system, revolutionizes how we transact while also opening the door for open, trustless security at a global scale.

If no other point is taken away about PKIs, it's that the modern approach to web security, rooted in PKI, fundamentally rests on an assumption of trust, while Saito's PKI is secured by economic security capable of foiling even a [majority attacker](https://wiki.saito.io/en/drafts/fifty-one-percent-attacks), but also scalable enough for everyday use.

### <div id="3a">Man-in-the-Middle Attacks</div>

Safe and secure key exchange is fundamental to the internet as we know it, yet the current paradigm provides the best security only to the largest players and is globally marred by trust assumptions. Public Key Infrastructures, also referred to as PKI networks, are the current solution to this problem.

Assyemtric cryptography makes it possible to set up a secure connection between any parties holding a public key pair, even when attackers can read the messages. The problem is that such exchanges are vulnerable to *Man in the Middle* (MITM) *Attacks,* where an intercepting party can secretly place themselves between each party and dupe them into encrypting their data in favor of the attacker, who then relays the not-so-secret messages between the unsuspecting parties.

Consult [Wikipedia](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) for a step-by-step example.

PKI networks, in the simplest of terms, serve as trusted middlemen which can audit key exchange requests to spot and stop MITM attacks. Some PKIs are small, like for individual businesses, some are large, like for the world wide web, and some are hidden in plainsight, like the user security protocols on social media.

Since these middlemen are all that stands in the way of a MITM attack, they also have the unique privilege to perform such attacks, making them prime targets for hackers, government corruption, and the prying eyes of data-hungry social media companies. Your connection is only as safe as your middleman.

### <div id="3b">Implicit PKI Networks</div>

All consumer web browsers are compiled, distributed and installed with their trust assumptions resting on the *certificate authorities* of PKI networks, which bind web domains to public keys in hopes of preventing MITM attacks. Without this, it would never be clear to web browsers if a connection to some domain was secure or being intercepted.

Typically, when someone on the internet wants to connect to a friend, they do not each register with a 'global' PKI network and have their identities certified across all web browsers. Instead they navigate to a website verified by a certificate authority, authorize a user account, and connect to their friend's user account reliant on the security within that website.

Much like the website had to identify itself with a certificate authority, a user usually identifies themselves with the website by creating an account. Since the website is determining who owns which keys (or more typically: user accounts), it serves as an implicit PKI (though rarely referred to as such) for users - it prevents MITM attacks by audting connections against their own database of users.

The reliance on middlemen to provide these trust assumptions is a security risk for all involved - companies make themselves targets for hackers, and users must rely on the skill and honesty behind corporate security practices. Often this is only acheived with relative safety by large corporations who then pilfer and monetize user data.

Today's secure internet ultimately relies on trust in a small collection of authoritative parties who catalog and mediate interactions between identities. Faith that these authorities will not perform a MITM attack of their own volition and to protect their operation from bribes and hackers is a requirement. Their permission to register and use the system is also required.

While the PKI networks behind the websites themselves are generally considered more secure, the ramifications of those being compromised are also much worse. Despite this, everyday users of the internet end up reliant on the weakest link in this cryptographic chain to secure their communications: corporate Web 2 servers.

### <div id="3c">Blockchain as PKI</div>

Saito is well suited to perform the much of the serious and fundamental responsibilities of a PKI without any authorities, any permission, and no central point of attack or corruption. Consider the key exchange again: two parties may share with each other their public keys over an insecure network and establish a secure connection between each other. Yet when they do so without the help of an authoritative web server or PKI network, they cannot be sure that no other parties exist between their connection.

If Alice wants to communicate with Bob and sends a transaction stating that intent, Mallory intercepts the message and instead publishes her own message to the blockchain. Bob recieves the same treatment, and what Mallory has ended up doing is publishing two transactions from herself purporting to be Alice and Bob. She then attempts to set up a connection between the two by convincing them to each individually connect to her.

But thanks to blockchain, and unlike public networks of the past, key exchange participants select their partners from a universal and uncensorable medium - where Mallory previously had the ability to censor for free, she now must resist the economic security of the blockchain in order to fulfill her attack.

Alice and Bob using Saito to perform key exchange remove the ability for a MITM to censor their original messages. Mallory can still impersonate Alice and Bob, but unlike in any other network, she has objective and growing cost to censor the original messages. Saito incentivizes nodes to compete to spread and include data in blocks - naturally routing around MITM attackers.

Nodes wishing to best serve users will route those relevant transactions back to them, and Alice and Bob can then see all key exchange requests directed towards them. When Alice or Bob sees that they each have multiple connection requests claiming to be the other, 

Only when Alice and Bob both see that both of their messages were posted to the universal broadcast network do they then have economic security which protects those messages and allows each counterparty to see them in their original form. By establishing connections only after both messages appear on the blockchain, the attacker loses the crucial ability to censor those messages before replacing them and can thus no longer attempt the attack without being detected and ultimately shunned.

### <div id="3d">Web 3</div>

There are several considerations at play here which are very often taken for granted:

* The extent of the reliance on PKI networks for internet security
* The extent to which registering with Web 2 PKIs is permissioned 
* The security vulnerabilities of Web 2 PKIs
* How, in practice, corporations serve as implicit and less secure PKIs for users
* The ability for blockchain to serve as PKI

Web 3 is well defined: a system of networking in which interested parties may safely connect directly to each other without any authoritative middlemen; without permission. By now it should be obvious that since the advent of public key cryptography, systems of authority have developed in order to solve the most basic problem of key exchange, and that all consumers rely on the security which  trickles down to social media platforms, and businesses on the blessings of authority to grant certificates.

Web 3, using blockchain as PKI, solves the MITM attack and does not require any participant to request certification from an authority, nor does it require users to rely on any heiarchies of trust which place them at the bottom rung. All participants in Web 3 will have access to a universal broadcast network which grants measurable and objective economic security to perform key direct exchange permissionlessly.

The way in which this reshapes the internet and a user's relationship to internet services is absolutely fundamental. For starters, the services which connect people need not be bound by any corporate interests, as users no longer rely on the trickle-down-trust that corporations recieve from Web 2 PKIs and sometimes pass faithfully down to users. Every individual instead has secure and direct access to one another via open source software.

While users may still have their preference of software based on user experience and user interface, their secure use of Web 3 relies on that software being open source, auditable to the public (else it may as well be Web 2 software considering the trust assumptions users must make). Though many choices may exist, they can each interoperate via the Web 3 PKI and peer-to-peer connections. Those designing user-facing software are no longer burdened with being shepards of *trust* - they instead allow user security to be handled by the most scalable and secure universal broadcast network: Saito blockchain.

When the internet is flipped on its head such that individuals are no longer dependent on the  authoritative and trusted coalitions of the internet today, Web 2 PKIs, there is no predicting from the ground floor all the developments which will generate. The Saito philosophy rests on one assumption: the internet is better when individuals have more freedom, soveriegnty and power - and the only way to provide that through an universal broadcast network which is secure against majority power and will not economically collapse or exclude users at scale.

## <div id="4">Permisionless Internet of Things</div>

Internet of things refers to the market of smart devices which consumers and businesses own and control remotely.

Consider a security camera which connects to the internet - the manufacturer already respects user privacy, so it is end-to-end encrypted by default, and open source. When you set it up, you connect your phone and they swap public keys - now no matter what medium they connect through, they will only establish connections if the public keys match what was supplied during setup.

This is convenient and practical for a single device, and can use an untrusted medium without fear of a MITM attack.


### Privacy Concerns


### Saito use-case

## Timestamping

## Money