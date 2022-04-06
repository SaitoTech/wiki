---
title: How to edit and contribute in wiki pages
description: Process in updating and contributing in Saito Wiki
published: true
date: 2022-04-06T09:01:43.909Z
tags: 
editor: markdown
dateCreated: 2022-04-06T08:28:26.977Z
---

# Wiki Page Edit and Suggestions

## Via Email/Comment on the Page

For non-developers, you may leave a comment on any page or email us at community@saito.io.

## Via Github

This is the standard git workflow. To know more, here's the process.

### Forking and Cloning the Wiki Repository
1. Visit https://github.com/SaitoTech/wiki
1. Fork the Saito repository. This creates a copy of the repository under your github user account. ([How to Fork a Repository in Github](https://docs.github.com/en/get-started/quickstart/fork-a-repo))
1. After succesfully forking to your github account, clone the forked repository on your local device by running the following code in the IDE (Integrated development environment) of your choice (e.g. [Visual Studio](https://visualstudio.microsoft.com/downloads/))
```git clone https://github.com/<YourUserName>/demo```
4. Create a new branch on your forked repository
```git checkout -b branch_name```
5. Create a new remote for the upstream repository with the command
```git remote add upstream https://github.com/SaitoTech/wiki.git```
***Note***: this line of code ensures that the original repository is in sync with the forked repository 

### Requesting for Pull Request on changes and approval
1. Execute the following line of codes
``` git add name_of_file or git add ``` 
```git commit -m "add commit message here```
```git push -u origin branch_name```
2. Go to [Saito Pull Requests Queue](https://github.com/SaitoTech/wiki/pulls) to view your pull request
1. Wait for the internal team to review and approve the changes
1. If it has been approved, changes will automatically reflect on the wiki pages.
1. You will receive an email notification from community@saito.tech on the result of the review




