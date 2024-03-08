---
title: Saito Rust - Installation Instructions
description: 
published: true
date: 2024-03-08T08:13:41.838Z
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
The setup process has been simplified to just running the initial_setup.sh script. This script automates the environment setup, application configuration, and prepares your system for the Saito Rust workspace. For a detailed explanation of what the script does, please refer to the Rust Bootstrap Script Documentation. https://wiki.saito.io/e/en/tech/installation/rust-bootstrap-script Rust Bootstrap Script Documentation.

### Step 1: Step 1: Clone the Repository

Clone the Saito Rust workspace repository from GitHub:

````bash
git clone https://github.com/saitotech/saito-rust-workspace
````


### Step 2: Run the Initial Setup Script

Navigate to the cloned directory, then run the initial_setup.sh script to automatically configure and prepare your environment.

```bash
cd saito-rust-workspace/scripts
./initial_setup.sh
````

This script handles the environment setup, dependencies installation, configuration files preparation, and data directories setup across both Linux and macOS platforms.


#### Step 3: Run the Application

Upon completion of the setup script, your Saito Rust workspace is ready to use. Start the application with Rust's cargo tool:

````bash
cd ../saito-rust
RUST_LOG=debug cargo run
````

After executing these steps, your Saito Rust workspace should be fully operational. The initial_setup.sh script simplifies the process, making it straightforward to get up and running. For customization or further information, refer to the detailed documentation or contact the Saito community for support.
