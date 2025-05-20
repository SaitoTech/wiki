---
title: How to edit and contribute in wiki pages
description: Process in updating and contributing in Saito Wiki
published: true
date: 2025-05-20T07:55:03.053Z
tags: 
editor: markdown
dateCreated: 2022-04-06T08:28:26.977Z
---

# Saito Wiki - How to Contribute

This wiki is a collaborative effort to help others understand what Saito Consensus is, why we need a non-excludable PKI network, and how people can run nodes and contribute to the network. If you see problems or have suggestions on how to improve it, here is how you can help us make updates.

## Via Email/Comment

Leave a comment on any page or email us at community@saito.io.

## Via Github

Clone the Saito Wiki

```git clone https://github.com/<YourUserName>/demo```

Create a new branch for your edits

```git checkout -b [branch_name]```

Ensures our repository gets notified of your updates

```git remote add upstream https://github.com/SaitoTech/wiki.git```

You can find any file by examining its path and just looking for the properly-named markdown (.md) file at that location. You can create new files by following the same convention. After you make any edits to existing files or add new ones, make a **pull request** to submit your changes:

```
  git add [modified_file]
  git commit -m "add commit message here"
  git push -u origin [branch_name]
```

You will be able to see your request in the [Saito Pull Requests Queue](https://github.com/SaitoTech/wiki/pulls). Feel welcome to hit up a member of the community for us to fast-track the changes. You will receive an email notification from community@saito.tech with the result of the review.

Don't be offput by the need for this review process. While it's unfortunate to need a complicated process for an open source project, these controls are needed to avoid scammers targetting our community and defrauding members of the general public.