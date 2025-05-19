---
title: Saito Rust - Installation Instructions
description: 
published: true
date: 2025-05-19T15:43:33.254Z
tags: 
editor: markdown
dateCreated: 2023-10-13T08:32:52.212Z
---

# Saito Rust Installation

This guide provides step-by-step instructions for setting up the Saito Rust client. There are two main reasons you might want to install this software instead of the NodeJS client: (1) you wish to run a high-performance client without support for web3 apps, or (2) you wish to modify consensus-level code, and compile a version of your code to work with a custom NodeJS client.

In short, if you do not know what you are doing here, you probably want to install our [regular client](/install) instead. The following instructions assume you are installing this client remotely on a Unix-style OS.

### Step 1: Download the Software

Make sure you have a local copy of the Saito repository installed on your local machine or server. The Rust software packages that we will be compiling and running are contained in this repository within the ```/rust``` subdirectory.

````bash
git clone https://github.com/saitotech/saito
````

### Step 2: Run the Initial Setup Script

Move into ````/saito/rust```` and run the initial_setup.sh script to automatically configure and prepare your environment. This script is located in the ```./scripts``` subdirectory:

```bash
cd saito/rust/scripts
./initial_setup.sh
````

For a detailed explanation of what this script does, please refer to the [Rust bootstrap script documentation](./saito-rust/setup-script). Our goal with this script is to make initial setup as painless as possible, so please contact our team if you have any problems running this script.

#### Step 3: Run the Application

Upon completion of the aforementioned script, you are ready to start running Saito Rust locally. Go back to your ```/saito/root``` directory and navigate into the ```saito-rust``` subdirectory. Then start the application with Rust's cargo tool:

````bash
cd ../saito-rust
RUST_LOG=debug cargo run
````

You can test if Saito is running on your machine by pointing your browser to http://localhost:12101/. Be aware that the server running on this machine exists mostly to facilitate core network traffic and server monitoring. It is not a full-featured web3-server as similar to the NodeJS code.