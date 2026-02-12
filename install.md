---
title: Install
description: 
published: true
date: 2026-02-12T13:11:10.423Z
tags: 
editor: markdown
dateCreated: 2024-10-15T23:32:31.744Z
---

# Installing Saito

This page assumes you want to run a Saito server locally to run or develop applications like the Saito Arcade, Videocall, or RedSquare. If you want to run Saito on a remote machine, we have a [remote deployment guide](/install/deploy) that includes a script which automates entire setup process. The rest of this page assumes you are installing on a local machine.

### Installation Requirements:

- Machine with at least 4GB RAM.
- Build tools: git, g++, make, python, tsc
- Stack: node.js (v.16+), npm (v6+)
- TypeScript

If you are missing any of these tools we have dedicated pages to help you install them for [Linux](/install/linux), [Mac](/install/mac) and [Windows](/install/windows). The remainder of these instructions assumes you have these packages installed and are comfortable using the command-line.


### 1. Download Saito

Clone the official Saito repository and move into the ```node``` sub-directory. Run ```npm install``` to download all of the packages you will need to run Saito, including a pre-compiled version of the Rust codebase.

```
git clone https://github.com/saitotech/saito
cd saito/node
npm install
```

**Note:** if ```npm install``` fails to install a module, you may need to install `python-is-python3` to work around the problem. On Ubuntu this can be done with ```sudo apt-get install python-is-python3```.



### 2) Compile Saito

These instructions run a script that compiles Saito into a compressed javascript file that can be served to browsers and contains all of the modules your browsers will use. The second starts the server:

```
npm run nuke
npm start
```

After a few moments, you should see a large Saito ASCII logo appear on your screen. This indicates that Saito is running normally and you can start using it!

### 3) Visit Saito in your Browser

Congratulations! You can now open a browser and visit:

> http://localhost:12101

Ready to change the default set of modules on your machine? For detailed instructions on compiling the node.js stack refer to the [Compilation Guide](/install/compile). If you run into problems installing Saito on a remote machine, check the configuration changes needed for remote deployment in our [remote deployment guide](/install/deployment).

## Running a Saito Rust Node

Saito Rust node is a rust application using the saito-core library to run a standalone saito node.

Following are the steps to run a saito rust node.

### Step 1: Clone the Repository

First, make sure you have a copy of the Saito repository. If you have not already done this:

```bash
git clone https://github.com/saitotech/saito 
````

### Step 2: Initialize the Environment

Navigate to the cloned directory and run the bootstrap script to prepare your environment. The script will work for Mac or Linux, auto-detecting the appropriate bootstrap script based on your environment. Select YES when asked if you want to "Build Project":

````bash
cd scripts
bash scripts/bootstrap.sh
````


#### Step 3: Run the Application

Finally, start the Saito application with Rust's cargo tool, enabling debug logging:

````bash
RUST_LOG=debug cargo run

````


## Development Setup

### 1. Git clone repo
```
git clone https://github.com/saitotech/saito
```

### 2. Run dev setup script
```
cd <repo>/rust/scripts
./dev_setup.sh
```

Provide any expected inputs and wait till the script completes. Script will install all the required software, compile the code and locally link the npm packages.

### 3. Link local saito-js package

```
cd <repo>/node/
npm install
npm link saito-js
npm run compile
```

Now the node js server can be started with the locally linked saito-js package.

### A. Locally linking wasm projects manually

#### building and linking saito-wasm project
```
cd <repo>/rust/saito-wasm
npm install
npm run build
npm link # this will setup saito-wasm to be locally linked by other projects
```

#### building and linking saito-js project
```
cd <repo>/rust/saito-js
npm install
npm link saito-wasm # this is linking previously built saito-wasm into saito-js project
npm run build 
cd dist 
npm link # this will setup saito-js to be locally linked by other projects
```

Now link the local saito-js as in aboe step 3.

Local links will stay there until npm install is called. So you don't need to run `npm link saito-js` everytime you compile but only when you run npm install.

### B. Compiling new wasm code
Once you do any rust changes, below is the procedure to compile wasm code. (Assuming saito-wasm and saito-js are locally linked)

```
cd <repo>/rust/saito-wasm
npm run build
cd <repo>/rust/saito-js
npm run build
```

## C. Using the new wasm code in nodejs

```
cd <repo>/node/
npm link saito-js
npm run compile #or equivalent
npm start
```

## Releasing new npms

Once you test everything in the local environment. If you need to publish new npms with the changes, all you have to do is below steps.

1. Increment the number in [repo]/rust/VERSION file. Make sure the incremented version number is not already used to publish an npm. (Check https://www.npmjs.com/~saitotech for latest npm versions)
2. Push / merge changes to develop branch
3. Create a PR from develop to master branch
4. Wait till the PR is completed / green.
5. Merge the PR.
6. Now the Github actions will automatically run the CI process to publish the new npms. You can check the status in the https://github.com/SaitoTech/saito/actions page.