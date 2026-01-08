---
title: Saito Stack
description: Self-Publishing on Saito
published: true
date: 2026-01-08T08:33:02.716Z
tags: 
editor: markdown
dateCreated: 2025-12-30T04:28:10.032Z
---

# Saito Stack

![](/img/stack.png)


**Saito Stack** is a permissioned, peer-to-peer publishing platform built directly atop the Saito network. It allows creators to publish blog posts and other kinds of content directly as signed transactions, retain cryptographic ownership of their work, and distribute their work without relying on centralized hosting platforms or opaque recommendation systems.

Stack is designed as an open-source alternative to platforms such as Substack, Medium, or Ghost, but implemented as a first-class Saito module rather than a traditional web service. In addition, users can control access to their posts using Saito Scripting to control access restrictions, such as requiring holders to control an author-issued NFT as an access for content. 

---

## Writing Help

To create a header, start a new paragraph with Markdown heading markers and press Enter:

\# Header 1
\#\# Header 2
\#\#\# Header 3

When you press Enter, the leading # markers are removed automatically and the line is converted into the appropriate header. You can use similar keyboard shortcuts to provide bullet points:

\* bullet points
\- bullet points

Once you enter a single bullet point, the system will permit you to continue simply by pressing Enter. Pressing Enter on an empty bullet point will terminate the bullet point object and return you to a fresh paragraph.

Quotes work similarly:

\> your quote here

Code blocks also work 

\`\`\`
the content of the code block here
\`\`\`

Images may be dragged directly into the blog post. You will observe a "placement line" appear where the image will be displayed if "dropped" into the text at that point. Adjust your 

The code needed to update is complicated as it has different kinds of edge-cases. If you run into problems that affect your ability to write or edit posts, please flag them for us. Most issues that surface these days come from complicated edits that break the expectations of the software. A quick workaround if you run into trouble is to move to a new paragraph or reload the page to reset the javascript.

## Publishing Help

All posts are published as cryptographically-signed transactions. Creators retain direct authorship and control over their content without platform-level ownership or censorship. Any images or other content required to view the post is included in the transaction.

When publishing a blog post, set its access restrictions as "Public" if you wish members of the general public to be able to read it. If you set your access restrictions as "Private" or "Subscription" access will be limited

Publishers should note that unless they are encrypting your underlying content or publishing onto private archive nodes, it will always be possible for users and network owners to retrieve their content by syncing the full blockchain. While Saito servers generally respect access controls, if users wish perfect control over their content it is recommended to use a private archive server.


## Relationship to the Saito Network

Saito Stack is not a standalone application layered on top of a blockchain. It is a native Saito module and benefits directly from:

- Saito’s routing-based incentive design
- Peer-to-peer content caching
- Sybil-resistant transaction propagation
- Built-in cryptographic identity

Stack demonstrates how application-layer publishing can be implemented without centralized servers while remaining usable and familiar to end users.
