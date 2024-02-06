---
title: Saito Rust - Installation Instructions
description: 
published: true
date: 2024-02-06T05:06:03.405Z
tags: 
editor: markdown
dateCreated: 2023-10-13T08:32:52.212Z
---

# Saito Rust Workspace Setup Guide

This guide provides step-by-step instructions for setting up the Saito Rust workspace on a Linux and mac environment. Follow these steps to clone the repository, prepare the environment, and run the application.

#### Requirements

* OS: Ubuntu 20.04 (MacOS instructions)
* Build tools: git, g++, make
* Stack: cargo rust (v.1.5.7+)
* https://github.com/saitotech/saito-rust-workspace


## Setup Instructions

### Step 1: Clone the Repository

First, clone the Saito Rust workspace repository from GitHub using the following command:

```bash
git clone https://github.com/saitotech/saito-rust-workspace 
````

### Step 2: Initialize the Environment

Navigate to the cloned directory and run the bootstrap script to prepare your environment:

**For Linux**
Run the bootstrap_linux.sh script to prepare your Linux environment:

````bash
cd saito-rust-workspace
bash scripts/bootstrap_linux.sh
````

**For macOS**
If you are on a macOS device, use the bootstrap_mac.sh script instead:

````bash
cd saito-rust-workspace
bash scripts/bootstrap_mac.sh
````

**Build workspace**
````bash
cargo build
````


### Step 3: Configure the Application

Change to the saito-rust directory:

```bash
cd saito-rust
```

Copy the configuration template to create your own configuration file:

````bash
cp configs/config.template.json configs/config.json
````
for explaination of the configuration file, click [saito-rust-config](/tech/installation/saito-rust-config)




#### Step 4: Prepare Data Directories

Copy the issuance template to the appropriate directory:


````bash
cp data/issuance/issuance.template data/issuance/issuance
````

Create a directory for blockchain blocks:

````bash
mkdir data/blocks
````

#### Step 5: Run the Application

Finally, start the Saito application with Rust's cargo tool, enabling debug logging:


````bash
RUST_LOG=debug cargo run

````


After completing these steps, the Saito Rust workspace should be up and running on your system. You can modify the configs/config.json file as needed to customize your setup. For further assistance, consult the official Saito documentation or reach out to the Saito community.
