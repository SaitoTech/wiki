---
title: Connecting Saito Repositories locally for M1 | An installation Guide
description: 
published: true
date: 2023-09-21T10:19:18.806Z
tags: 
editor: markdown
dateCreated: 2023-09-20T20:31:08.392Z
---


# Mac (M1) Specific Installations

This page assumes you are using a Mac with the M1 chip and want to compile the Saito WASM library and link it to a locally-compiled version of Saito Javascript. If you are trying to compile Saito on another OS please see our [standard installation guide](/tech/installation).

 It provides a detailed walkthrough on how to compile the Saito WASM library under MacOS so that Saito Javascript will use your locally-compiled version of the Saito WASM library instead of the default one hosted on NPM.

Note: The saito-lite-rust (SLR) repository by default comes bundled with the saito-js library in its package.json. So it should work without the need to do anything on this page. These steps are only necessary if you want to modify the Rust/Javascript code or debug core parts of the software from within javascript.

## Prerequisites

Before starting, ensure:

- nodeJS and npm are installed.

- homebrew is installed - [install](https://brew.sh/)

- you have the [saito-lite-rust](https://github.com/SaitoTech/saito-lite-rust), and [saito-rust-workspace](https://github.com/SaitoTech/saito-rust-workspace) repositories cloned on your local machine and are capable of compiling them.


## Step 1. Compiling Saito WASM

#### 1. Install LLVM: This provides the necessary tools, including clang.

```
brew install llvm
```

#### 2. Set Environment Variables

```bash
export CC=/opt/homebrew/opt/llvm/bin/clang
```


#### 3. Navigate to the saito-wasm directory

```
cd saito-rust-workspace/saito-wasm
```


#### 4. Install wasm-pack: This is a crucial tool for compiling Rust to WebAssembly.

```
npm i -g wasm-pack
```

#### 5. build with wasm pack
```
CC=/opt/homebrew/opt/llvm/bin/clang AR=/opt/homebrew/opt/llvm/bin/llvm-ar wasm-pack build --target web --out-dir wasm_build/deps/pkg/
```

#### 6. Install
```
npm install
```
#### 7. build
```
npm run build
```
#### 8. create a symbolic link for saito-wasm
```
npm link 
```

## Step 2: Linking to Your Compiled WASM Library

#### 1. Navigate to the saito-js directory


#### 2. Installation  
```
npm install
```
#### 3. linking with saito-wasm
```
npm link saito-wasm
```
#### 4. build
```
npm run build
```
#### 5. create a symbolic link for saito-js
- Navigate into the dist folder in the saito-js directory
- Run link command 
```
npm link
```


## Step 3: Linking Saito-JS SLR to saito-js

#### 1. Navigate to the Saito Javascript directory
``` 
cd saito-lite-rust
```

#### 2. Install
``` 
npm install
```
#### 3. Link with saito-js
```
npm link saito-js
```

#### 4. Build and run SLR
```
npm run go
```


