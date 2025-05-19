---
title: Linux Installation
description: Linux SLR Installation Instructions
published: true
date: 2025-05-19T13:02:34.884Z
tags: 
editor: markdown
dateCreated: 2022-01-18T09:49:16.786Z
---

# Linux Installation

The instructions below cover how to install the pre-requisite software needed to compile and install Saito for developers building on Linux. We have separate installation instructions for [Mac users](./mac) and [Windows users](./windows).


### 1) Install Dependencies (Ubuntu 22.04 (LTS) x64)
```
sudo apt-get update
sudo apt-get install g++ make git python-is-python3 npm
curl -sL https://deb.nodesource.com/setup_16.x | sudo -E bash
sudo apt-get install -y nodejs
```

<br />

### 2) Download Saito

At this point, you should be ready to [install Saito](https://wiki.saito.io/install) using our standard instructions for Linux and Mac nodes. If you run into any problems that are not documented that require explanation, please contact the team so we can update hte documentation here.