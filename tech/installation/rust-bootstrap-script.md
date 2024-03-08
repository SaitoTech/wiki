---
title: Saito-Rust Bootstrap Script
description: 
published: true
date: 2024-03-08T08:25:14.858Z
tags: 
editor: markdown
dateCreated: 2024-03-06T10:09:36.384Z
---

# Documentation for Saito Rust Setup Script

This documentation covers the setup script for configuring a Saito Rust node. The script automates the process of configuring the environment, managing configuration files, installing dependencies, and starting the node.

## Usage
For executing the script, navigate to the script directory and launch ```initial_setup.sh```

## Overview
The script performs the following main tasks:

- Configures the Node
- Creates Necessary Directories and Files
- Installs Dependencies
- Starts the node


###  Configuring the Node
This section checks if a config.json file exists. If not, it copies a template configuration file and modifies it to ensure the node is set correctly.
How to configure the node for explaination of the configuration file, click [saito-rust-config](/tech/installation/saito-rust-config)

### Creating Necessary Directories and Files

Ensures the data/blocks directory exists for blockchain data storage and creates an issuance file from a template if it's missing.

Key Operations:
- Directory creation for blocks.
- Issuance file setup.


### Installing Dependencies

Detects the operating system (macOS or Linux) and runs the corresponding bootstrap script (bootstrap_mac.sh or bootstrap_linux.sh). These scripts are responsible for installing necessary software packages, ensuring Rust is installed, and setting up the environment for the Saito Rust project.

Key Operations:
- Operating system detection.
- Execution of OS-specific bootstrap scripts.
- Rust installation and environment setup.

### Starting the Node
Prompts the user to start the node immediately after setup. If the user agrees, it starts the node

## Auxiliary Scripts

- ``` bootstrap_linux.sh```
- ``` bootstrap_mac.sh ```

These scripts checks for and installs missing dependencies required for the Saito Rust project on Linux or mac systems. It includes checks for Rust installation, updates package lists, and installs various development tools and libraries.










