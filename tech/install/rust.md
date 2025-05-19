---
title: Saito Rust - Installation Instructions
description: 
published: true
date: 2025-05-19T13:47:50.350Z
tags: 
editor: markdown
dateCreated: 2023-10-13T08:32:52.212Z
---

# Saito Rust Installation

This guide provides step-by-step instructions for setting up the Saito Rust client. There are two reasons that you might want to install this software instead of the NodeJS client :

 * you wish to run a high-performance client that will merely
   route transactions and do not need to server web3 apps to 
   visitors or provide a server-interface to web3 applications.
   
 * you wish to modify consensus code, and compile a version of
   your custom code so that it can be used by the NodeJS client
   instead of the default version that NodeJS will fetch from 
   the Saito repository.

This guide provides step-by-step instructions for setting up the Saito Rust client on a Linux and Mac environment. If you have not already installed a version of Saito this is not the client to start with. You should begin by installing the standard NodeJS version of Saito that supports browser-based applications.

### Step 1: Download the Softwaret

Make sure you have a local copy of the Saito repository installed on your local machine or server. This is the same repository that contains the Saito NodeJS software. The Rust software is contained within this repository within the ```/rust``` subdirectory.

````bash
git clone https://github.com/saitotech/saito
````

### Step 2: Run the Initial Setup Script

Move into ````/saito/rust```` and run the initial_setup.sh script to automatically configure and prepare your environment. This script is located in the ```./scripts``` subdirectory:

```bash
cd saito/rust/scripts
./initial_setup.sh
````

For a detailed explanation of what this script does, please refer to the [Rust bootstrap script documentation](./rust/rust-bootstrap-script). Our goal with this script is to make initial setup as painless as possible, so please contact our team if you have any problems running this script.

#### Step 3: Run the Application

Upon completion of the aforementioned script, you are ready to start running Saito Rust locally. Go back to your ```/saito/root``` directory and navigate into the ```saito-rust``` subdirectory. Then start the application with Rust's cargo tool:

````bash
cd ../saito-rust
RUST_LOG=debug cargo run
````

You can test if Saito is running on your machine by pointing your browser to http://localhost:12101/. Be aware that the server running on this machine exists mostly to facilitate core network traffic and server monitoring. It is not a full-featured web3-server as similar to the NodeJS code.