---
title: Saito-Rust Bootstrap Script
description: 
published: true
date: 2025-05-19T15:42:03.696Z
tags: 
editor: markdown
dateCreated: 2024-03-06T10:09:36.384Z
---

# Saito Rust Bootstrap/Setup Script

This page documents the setup script for configuring a Saito Rust node. The script automates the otherwise process of configuring the environment, managing configuration files, installing dependencies, and starting the node. It is provided here as a reference.

## Usage
To execute the script, navigate to ```/saito/rust/saito-rust/scripts``` and launch ```initial_setup.sh```

## Overview
The script performs the following main tasks:

- configures the node
- creates necessary directories and files
- installs dependencies
- starts the node


###  Configuring the Node
Automatically configures the node. For manual node configuration instructions, please see [saito-rust](/install/saito-rust) installation page.

### Issuance File Setup

Creates an issuance file from a template if one is missing. The issuance file specifies which addresses receive tokens in the first block. After this block, no additional tokens may be added to the network.

Key Operations:
- issuance file setup.


### Installing Dependencies

Detects the operating system (macOS or Linux) and runs the corresponding bootstrap script (bootstrap_mac.sh or bootstrap_linux.sh). These scripts are responsible for installing necessary software packages, ensuring Rust is installed, and setting up the environment for the Saito Rust project.

Key Operations:
- operating system detection.
- execution of OS-specific bootstrap scripts.
- rust installation and environment setup.

### Starting the Node
Prompts the user to start the node immediately after setup. If the user agrees, it starts the node

## Auxiliary Scripts

- ``` bootstrap_linux.sh```
- ``` bootstrap_mac.sh ```

These scripts check for and installs missing dependencies required for the Saito Rust project on Linux or Mac systems. They include checks for Rust installation, updates package lists, and installs various development tools and libraries.










