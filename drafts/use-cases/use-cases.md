---
title: PKI and ATR
description: Public Key Infrastructure and Automatic Transaction Rebroadcasting
published: true
date: 2024-03-11T22:00:37.588Z
tags: 
editor: markdown
dateCreated: 2023-09-24T01:04:19.828Z
---

# Public Key Infrastructure and Automatic Transaction Rebroadcasting - PKI & ATR

This page serves as an abstract discussion of the utility of Saito and scalable, but specifically, transient, blockchain generally. To learn about applications leveraging this technology on Saito right now, visit the [applications](https://wiki.saito.io/en/tech/applications) page of the Wiki or [try them](https://saito.io/redsquare/) yourself.

<ul style="color:">
  <li> 1. <a style="text-decoration:none" href="#1"> Universal Broadcast </a> </li>
  <!--<li> 2. <a style="text-decoration:none" href="#2"> What Does Saito Pay For?</a> </li>-->
  <li> 2. <a style="text-decoration:none" href="#2"> Public Key Infrastructure</a> </li>
  <ul>
    <li> 2a. <a style="text-decoration:none" href="#2a"> Man-in-the-Middle Attacks </a> </li>
    <li> 2b. <a style="text-decoration:none" href="#2b"> Implicit PKI Networks </a> </li>
    <li> 2c. <a style="text-decoration:none" href="#2b"> Blockchain as PKI </a> </li>
    <li> 2d. <a style="text-decoration:none" href="#2b"> Web 3 </a> </li>
  </ul>
  <br>
  <li> 3. <a style="text-decoration:none" href="#3"> Web 3 </a> </li>
  <ul>
    <li> 3a. <a style="text-decoration:none" href="#3a"> What is Web 3? </a> </li>
    <li> 3b. <a style="text-decoration:none" href="#3b"> placeholder </a> </li>
    <li> 3c. <a style="text-decoration:none" href="#3b"> placeholder </a> </li>
    <li> 3d. <a style="text-decoration:none" href="#3b"> placeholder </a> </li>
  </ul>
  <br>
  <!--
  <li> 4. <a style="text-decoration:none" href="#3b"> Permissionless Internet of Things </a> </li>
-->
  <li> 3. <a style="text-decoration:none" href="#3b"> Conclusion </a> </li>
</ul>

## Introduction

Many wonder what possible use cases another new blockchain could possibly serve, and yet others wonder what compelling use case blockchain truly serves at all. This page answers the latter by contextualizing Saito's strengths as solutions to known problems in existing internet infrastructure.

As to the former question: why another blockchain need exist to solve this problem; the complete answer is out of scope. The short answer is that [Saito Consensus](https://wiki.saito.io/en/consensus) solves known market failures which impede traditional and 'modern' blockchain's ability to scale while remaining open.
  
## <div id="1">Universal Broadcast</div>

Saito's primary use case is the most fundamental utility blockchain, implemented with superiority over all previous designs: Universal Broadcast.

A common question for those investigating a new blockchain is "what are its use cases?" Money, smart contracts, decentralized finance, trustless computation - applications of blockchain are evolving constantly. But in a very fundamental sense, the blockchain has a singular source of value from which all applications flow: *Universal Broadcast*.

Universal Broadcast means a network in which anyone paying the market rate may publish and access global data. The uncensorable and open nature of many existing blockchains, notably including Bitcoin, allows this same utility, but Saito consensus is the only protocol design which allows for a universal broadcast blockchain network which can retain this property at arbitrary scale and under arbitrary adverserial network conditions.

Universal Broadcast is also the reason Saito does not consider techniques which fracture the publication of data across different parties, like sharding or layered approaches, to be scaling techniques. While these methods may still have value, they do not scale the fundamental use-case of Universal Broadcast.

*How* Saito scales is as important to this goal as the fact that it does: it scales by incentivizing the provision of the very network resources which scales performance, increases volume, or drives individual fees down. As importantly, it rewards sharing and punishes hoarding transaction data; it is a system which bears no monopoly privilege; this is how it can remain *open* at scale.

Because Saito can scale arbitrarily large without latent economic misalignments waiting to foster [private chokepoints](https://saitoofficial.medium.com/the-infura-problem-fe68866484ec) like [Infura](https://cryptobriefing.com/infura-outage-sparks-debate-over-ethereums-decentralization/), use cases for which many believe are impossibly expensive for an open and secure layer-1 blockchain are possible on Saito at whatever scale hardware can provide.

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
## <div id="2">Public Key Infrastructure</div>

Public Key Infrastructures (PKI) are, among other uses, one of the most important but least discussed components of the modern, secure, internet. Their origins come from the early desire to securely transact electronically over the web; without them, eCommerce as we know it could not exist - nor could the other security assumptions many take for granted while using the internet. 

It is fitting that the next generation of PKI stems too from a general upgrade in the way we transact with one another. In much the same way that this need to securely send money lead to the modern PKIs and their emergent use cases, Saito, an economic system, revolutionizes how we transact while also opening the door for open, trustless security at a global scale.

If no other point is taken away about PKIs, it's that the modern approach to web security, rooted in PKI, fundamentally rests on assumptions of trust, while Saito's PKI is secured by economic security capable of foiling even a state-level [majority attacker](https://wiki.saito.io/en/drafts/fifty-one-percent-attacks), but also scalable enough for everyday use.

### <div id="2a">Man-in-the-Middle Attacks</div>

Safe and secure key exchange is fundamental to the internet as we know it, yet the current paradigm provides the best security only to the largest players and is globally marred by trust assumptions. Public Key Infrastructures (PKI networks), are the current solution to this problem.

Assyemtric cryptography makes it possible to set up a secure connection between any parties who each hold a public key pair, even when attackers can spy on the setup. The problem is that such exchanges are vulnerable to *Man in the Middle* (MITM) *Attacks,* where an intercepting party can secretly place themselves between each party and dupe them into encrypting their data in favor of the attacker's key, who then relays the apparently secret messages between the unsuspecting parties.

Consult [Wikipedia](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) for a visual example.

PKI networks, in the simplest of terms, serve as trusted middlemen which can audit key exchange requests to spot and stop MITM attacks. Some PKIs are small, like for individual businesses, some are large, like for the world wide web, and some are hidden in plainsight, like the user security protocols on social media.

These middleman serve the important role of binding identities to keys, such that when a man-in-the-middle attack is attempted, a mismatch occurs between the expected key and the recieved key.

Since these middlemen are all that stands in the way of a MITM attack, they also have the unique privilege to perform such attacks, making them prime targets for hackers, government corruption, and the prying eyes of data-hungry social media companies. Your connection is only as safe as your middleman.

### <div id="2b">Implicit PKI Networks</div>

All consumer web browsers are compiled, distributed and installed with their trust assumptions resting on the *certificate authorities* of PKI networks, which bind web domains to public keys in hopes of preventing MITM attacks. Without this, it would never be clear to web browsers if a connection to some domain was secure or being intercepted.

Typically, when someone on the internet wants to connect to a friend, they do not each register with a 'global' PKI network and have their identities certified across all web browsers. Instead they navigate to a website verified by a certificate authority, authorize a user account, and connect to their friend's user account reliant on the security within that website.

Much like the website had to identify itself with a certificate authority, a user usually identifies themselves with the website by creating an account. Since the website is determining who owns which keys (or more typically: user accounts), it serves as an implicit PKI (though rarely referred to as such) for users - it prevents MITM attacks by audting connections against their own database of users.

The reliance on middlemen to provide these trust assumptions is a security risk for all involved - companies make themselves targets for hackers, and users must rely on the skill and honesty behind corporate security practices. Often this is only achieved with relative safety by large corporations who then pilfer and monetize user data.

Today's secure internet ultimately relies on trust in a small collection of authoritative parties who catalog and mediate interactions between identities. Faith that these authorities will not perform a MITM attack of their own volition and to protect their operation from bribes and hackers is an unfortunate requirement. Their permission to register and use the system is also required.

While the PKI networks behind the websites themselves are generally considered more secure, the ramifications of those being compromised are also much more severe. Due to incompetence, or malice disguised as such, crucial security infrastructure has been discovered compromised [several times](https://cromwell-intl.com/cybersecurity/pki-failures.html) in the past. One can only speculate on what vulnerabilities or trust assumptions are exploited in secret.

Putting more existential risks aside: everyday users of the internet end up reliant on the weakest and least trustworthy link in this cryptographic chain to secure their communications: corporate Web 2 servers.

### <div id="2c">Blockchain as PKI</div>

Saito is well suited to perform the much of the serious and fundamental responsibilities of a PKI without any authorities, any permission, and no central point of attack or corruption. Consider the key exchange again: two parties may share with each other their public keys over an insecure network and establish a secure connection between each other. Yet when they do so without the help of an authoritative web server or PKI network, they cannot be sure that no other parties exist between their connection.

If Alice wants to communicate with Bob and sends a transaction stating that intent, Mallory intercepts the message and instead publishes her own message to the blockchain. Bob receives the same treatment, and what Mallory has ended up doing is publishing two transactions from herself purporting to be Alice and Bob. She then attempts to set up a connection between the two by convincing them to each individually connect to her.

But thanks to blockchain, and unlike public networks of the past, key exchange participants select their partners from a universal and uncensorable medium - where Mallory previously had the ability to censor for free, she now must resist the economic security of the blockchain in order to fulfill her attack.

Alice and Bob using Saito to perform key exchange remove the ability for a MITM to freely and easily censor their original messages. Mallory can still impersonate Alice and Bob, but unlike in any other network, she has objective and growing cost to censor the original messages. Saito [incentivizes](https://wiki.saito.io/en/consensus) nodes to compete to spread and include data in blocks - naturally routing around MITM attackers.

Nodes wishing to best serve users will route those relevant transactions back to them, and Alice and Bob can then see all key exchange requests directed towards them. When Alice or Bob sees that they each have multiple connection requests claiming to be the other, 

Only when Alice and Bob both see that both of their messages were posted to the universal broadcast network do they then have economic security which protects those messages and allows each counter-party to see them in their original form. By establishing connections only after both messages appear on the blockchain, the attacker loses the crucial ability to censor those messages before replacing them and can thus no longer attempt the attack without being detected and ultimately shunned.

## <div id="3">Web 3</div>

### <div id="3a"> Web 3 is Greater Than Web 2 </div>

Web 3 is well defined: a system of networking in which interested parties may safely connect directly to each other without any authoritative middlemen; without permission.  It may be considered the internet free of trust assumptions of central parties. When assessing the benefits of Web 3, there are several compromising aspects of Web 2 which are frequently taken for granted but highlight its inability to naively extend into Web 3:

* The extent of the reliance on PKI networks for internet security
* The extent to which registering with Web 2 PKIs is permissioned 
* The security vulnerabilities of Web 2 PKIs
* How, in practice, corporations serve as implicit and less secure PKIs for users
* The ability for blockchain to serve as PKI

By now it should be obvious that since the advent of public key cryptography, systems of trusted authority have developed in order to solve the most basic problem of key exchange. Users of the internet rely on the *trust* which trickles down from Web 2 PKIs and is then delegated to social media platforms and businesses in the form of user accounts.

Web 3, using blockchain as PKI, solves the MITM attack and does not require any participant to request certification from an authority, nor does it require users to rely on any hierarchies of trust which place them at the bottom rung. All participants in Web 3 will have access to a universal broadcast network which grants measurable and objective economic security to perform key direct exchange permissionlessly.

Not only do users enjoy open and affordable access to raw security of the root-level PKI (the blockchain), a tool for which most have never had direct access too, but this most foundational layer as instantiated on Saito, free from majoritarian attacks, is an order of magnitude more secure than the largely-gated, private, Web 2 PKIs, as censorship has measurable costs.

The way in which this reshapes the internet and a user's relationship to internet services is absolutely fundamental. For starters, the services which connect people need not be bound by any corporate interests, as users no longer rely on the trickle-down-trust that corporations receive from Web 2 PKIs and sometimes pass faithfully down to users. Every individual instead has secure and direct access to one another via open source software.

### <div id="3b"> Practical Benefits </div>

**Native interoperability** is a natural consequence of a more open internet. Though many choices may exist, they can each interoperate via the Web 3 PKI and peer-to-peer connections rather than the walled-gardens of private companies. Those designing user-facing software are no longer burdened with being shepherds of *trust* - they instead allow user security to be handled by the most scalable and secure universal broadcast network: Saito blockchain.

## Conclusion

When the internet is flipped on its head such that individuals are no longer dependent on the  authoritative and trusted coalitions of the internet today, Web 2 PKIs, there is no predicting from the ground floor all the developments which will generate. The Saito philosophy rests on one assumption: the internet is better when individuals have more freedom, sovereignty and power - and the only way to provide that through an universal broadcast network which is secure against majority power and will not economically collapse or exclude users at scale.

<!--
## <div id="4">Permisionless Internet of Things</div>

Internet of things refers to the market of smart devices which consumers and businesses own and control remotely.

Consider a security camera which connects to the internet - the manufacturer already respects user privacy, so it is end-to-end encrypted by default, and open source. When you set it up, you connect your phone and they swap public keys - now no matter what medium they connect through, they will only establish connections if the public keys match what was supplied during setup.

This is convenient and practical for a single device, and can use an untrusted medium without fear of a MITM attack.


### Privacy Concerns


### Saito use-case

## Timestamping

## Money
-->