---
title: Saito Rust - Installation Instructions
description: 
published: true
date: 2024-11-16T21:46:08.371Z
tags: 
editor: markdown
dateCreated: 2023-10-13T08:32:52.212Z
---

# Saito Rust Installation

This guide provides step-by-step instructions for setting up the Saito Rust workspace on a Linux and mac environment. Follow these steps to clone the repository, prepare the environment, and run the application.

#### Requirements

* Operating System: Ubuntu 20.04 or macOS
* Build Tools: git, g++, make (Linux), or equivalent development tools (macOS)
* Stack: Cargo, Rust (version 1.5.7 or higher)
* Repository: https://github.com/saitotech/saito-rust-workspace


## Setup Instructions

### Step 1: Step 1: Clone the Repository

Clone the Saito Rust workspace repository from GitHub:

````bash
git clone https://github.com/saitotech/saito-rust-workspace
````


### Step 2: Run the Initial Setup Script

Once you have downloaded Saito, move into your cloned directory and run the initial_setup.sh script to automatically configure and prepare your environment. This script is located in the ```./scripts``` subdirectory:

```bash
cd saito-rust-workspace/scripts
./initial_setup.sh
````

For a detailed explanation of what the script does, please refer to the [Rust bootstrap script documentation](./rust/rust-bootstrap-script). Our goal is to make initial setup as painless as possible, so please contact our team if you have any problems running this script.


#### Step 3: Run the Application

Upon completion of the setup script, you are ready to start running Saito Rust locally. Go back to the root directory and navigate into the ```saito-rust``` subdirectory. Then start the application with Rust's cargo tool:

````bash
cd ../saito-rust
RUST_LOG=debug cargo run
````

You can now test if Saito is running on your machine by pointing your browser to http://localhost:12101/. 