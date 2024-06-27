---
title: Saito Key Exchange Protocol
description: 
published: true
date: 2024-06-27T03:40:18.734Z
tags: 
editor: markdown
dateCreated: 2024-06-02T03:01:34.115Z
---

# Saito Key Exchange Protocol

Saito Applications leverage the Saito blockchain to perform secure key exchange. In order to understand why it is better to perform key exchange on the blockchain over traditional methods, one must first understand <a id="old">Web 2 key exchange</a>, <a id="flaws" href="">the flaws in that model</a>, and <a id="blockchain" href="">how blockchain fixes it</a>.
  
## Web2 Key Exchange

* What follows is a greatly simplified explanation of *public key infrastructure (PKI)* and HTTPS - we encourage readers to search the terms to learn more.

For every website visited or application ran, the user will, ideally, achieve a succesful key exchange with the host which restricts the ability to read messages passed between the host and user to *only* the host and user. In the modern web browser, this is indicated to the user by some sort of lock symbol in the URL bar - if the key exchange fails or uses an outdated scheme, the browser will issue a dire warning.

This isn't the entire story, however. A succesful key exchange by no means ensures a secure connection. There's one crucial step that, without, makes a key exchange hopeleslly insecure. If a [*Man-in-the-Middle* (MITM)](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) is able to intercept the key exchange, they can covertly listen in on and modify the communications of two parties who may believe they are secure.

<figure>
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/e7/Man_in_the_middle_attack.svg/1280px-Man_in_the_middle_attack.svg.png" style="border: 1px gray solid;">
  <figcaption style="opacity: 80%; text-align: center;"> Simplified image of a Man-in-the-Middle Attack; Credit: <a href="https://en.wikipedia.org/wiki/Man-in-the-middle_attack#/media/File:Man_in_the_middle_attack.svg">Wikipedia</a> </figcaption>
  </figure>

The crucial step to prevent a MITM Attack is *authentication -* this step gives some degree of assurance that the cryptographic keys involved in a key exchange belong to the rightful owners.

Authentication is assurance you have performed the key exchange with the real website, application or person rather than an imposter. It comes in many forms, one may even consider a Facebook profile a weaker form of authentication (with strong trust assumptions), but the most relevant for Web2 is that of [certificate authorities](https://en.wikipedia.org/wiki/Certificate_authority) (CAs).

CAs are a type of trusted database which bind public cryptographic keys to website domains or other recognizable titles. When you need to verify that the Facebook page you are loading belongs to the *real* Facebook, and not some arbitrary person who either misled you or is modifying your network traffic, your device will ask a Certificate Authority.

If the digital signature that a supposed Facebook domain provides a browser does not match the associated certificate that your web browser or device knows, then the user will be issued a warning and implored to not continue the interaction.

## Flaws of Web2 Key Exchange

https://cromwell-intl.com/cybersecurity/pki-failures.html#badly

Astute cypherpunks will have already spotted the problem inherent in traditional authentication schemes, that being that a secure key exchange ultimately relies on *trusting* one or a few certificate authorities.

The CAs were put in place to help users protect themselves from imposters and wire-tappers, but there is very little protection a user has from a malicious certificate authority. If a CA has been compromised, it can issue certificates which assure users that any server they visit is indeed authentic and true, when it in fact may not be - it's the same old Man-in-The-Middle Attack, but with extra steps.

Certificate authorities are undoubtedly better than zero authentication - they reduce the attack surface down to a few scrutinized centers of security and are relatively easy to use, but at the end of the day they represent the crux of internet security and users ultimately must *trust* the CAs to both behave honestly and protect themselves from attackers.

Unfortunately, certificate authorities have a history of being compromised:

