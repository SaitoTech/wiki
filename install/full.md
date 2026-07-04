---
title: Saito Installation - Full
description: 
published: true
date: 2026-07-04T13:37:46.208Z
tags: 
editor: markdown
dateCreated: 2026-07-04T13:37:46.208Z
---

# Installing Saito - Full

The ```/rust``` directory contains the full backend code that is compiled into the ```saito-js``` npm bundle. If you want to modify this Rust-level consensus code locally, you will need to follow the instructions on this page. These allow your machine to compile the full software stack locally, and use your locally-compiled code instead of the pre-compiled wasm bundle published by the project.

Once you have installed and compiled the software successfully for the first time, you can skip this step and "re-compile" at any time by running ```npm run linklocal```. This is useful if you want to make changes to the backend code and then immediately recompile and see them in action.


### Step 1: Clone the Repository

Navigate to the cloned directory and run the bootstrap script to prepare your environment. The script will work for Mac or Linux, auto-detecting the appropriate bootstrap script based on your environment. Select YES when asked if you want to "Build Project":

````bash
cd rust/scripts
bash bootstrap.sh
````
If you want to run the Saito Rust client, you can now do so using the following, which enables debug logging:

````bash
RUST_LOG=debug cargo run
````

### Step 2: Compile WASM Package

If you are using a Mac, please see our instructions on [installing WASM compiler for Mac](https://wiki.saito.io/install/saito-wasm/mac). Otherwise:

````bash
cd saito-wasm
cargo install wasm-pack
npm install
npm run build
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