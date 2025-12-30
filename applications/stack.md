---
title: Saito Stack
description: Self-Publishing on Saito
published: true
date: 2025-12-30T04:28:10.032Z
tags: 
editor: markdown
dateCreated: 2025-12-30T04:28:10.032Z
---

# Saito Stack

![](/img/stack.png)


**Saito Stack** is a permissioned, peer-to-peer publishing platform built directly atop the Saito network. It allows creators to publish blog posts and other kinds of content directly as signed transactions, retain cryptographic ownership of their work, and distribute their work without relying on centralized hosting platforms or opaque recommendation systems.

Stack is designed as an open-source alternative to platforms such as Substack, Medium, or Ghost, but implemented as a first-class Saito module rather than a traditional web service. In addition, users can control access to their posts using Saito Scripting to control access restrictions, such as requiring holders to control an author-issued NFT as an access for content. 

---

## Design Goals

Saito Stack is built around a small number of strict design principles:

### Content Ownership  
All posts are authored and published as cryptographically signed transactions. Creators retain direct authorship and control over their content without platform-level ownership or censorship.

### Deterministic Publishing  
What the author sees in the editor is exactly what gets published. There is no server-side rewriting, hidden mutation, or post-processing of content.

### Permissioned Access  
Stack supports both free and paid content using cryptographic access control, rather than centralized accounts or platform-enforced paywalls.

### Peer-to-Peer Availability  
Content is cached and served by peers on the Saito network. There is no single hosting provider and no single point of failure.

---

## Architecture Overview

Each post is published as a Saito transaction containing:

- `content` — Markdown representation of the post body  
- `image` — A single teaser or header image used for previews  
- `images[]` — Embedded content images referenced by the Markdown  
- additional metadata (title, timestamp, tags, etc.)

This design permits posts to be verified, cached, and served by any peer on the network. Users can publish their posts directly into the peer-to-peer network or indirect via inclusion in the blockchain.

---

## Drafts and Editor Sessions

Stack distinguishes carefully between drafts and published posts.

- Drafts exist only as local recovery artifacts.
- Editor sessions are explicit and intent-based (resume, select, or create new).
- Publishing consumes the active draft and ends the session.
- Drafts are never silently overwritten or implicitly reused.

This design prevents accidental data loss and makes editor behavior fully explainable.

---

## Image Handling

Stack separates image structure from image storage:

- Markdown content contains **references** to images.
- The actual image payloads are stored in the transaction’s `images[]` array.
- When rendering a post, image references are resolved against `images[]`.

This keeps content clean, deterministic, and extensible to future storage backends.

---

## URL-Based Navigation

Stack supports canonical, shareable URLs that map directly to content:

- `/stack/<publicKey>`  
  Displays the list of published posts for a creator.

- `/stack/<publicKey>/<transactionSignature>`  
  Loads and displays a specific blog post.

When content is loaded via URL, Stack shows a loading state while fetching data from local archives or network peers and fails gracefully if content cannot be retrieved.

---

## Monetization and Access Control

Stack supports both free and paid content tiers:

- Free posts are accessible to all readers.
- Paid posts require cryptographic proof of subscription.
- Access enforcement happens at the content level, not via centralized accounts.

This allows creators to monetize directly without intermediaries.

---

## Relationship to the Saito Network

Saito Stack is not a standalone application layered on top of a blockchain. It is a native Saito module and benefits directly from:

- Saito’s routing-based incentive design
- Peer-to-peer content caching
- Sybil-resistant transaction propagation
- Built-in cryptographic identity

Stack demonstrates how application-layer publishing can be implemented without centralized servers while remaining usable and familiar to end users.

---

## Status

Saito Stack is under active development and evolving alongside the Saito ecosystem. It serves both as a production publishing tool and as a reference implementation for building rich, peer-to-peer applications on Saito.

---
