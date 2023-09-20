---
title: Connecting Saito Repositories locally for M1 | An installation Guide
description: 
published: true
date: 2023-09-20T20:41:41.924Z
tags: 
editor: markdown
dateCreated: 2023-09-20T20:31:08.392Z
---


# Mac (M1) Specific Installations
This guide provides a detailed walkthrough on how to link the saito-lite-rust repository to the saito-wasm locally via the saito-js wrapper. This process leverages the npm link command.

Note: The saito-lite-rust (SLR) repository by default comes bundled with the saito-js library in its package.json. If, however, you wish to manually establish this linkage, the instructions below will guide you.

## Prerequisites

Before starting, ensure:

- Node.js and npm are installed.

- [saito-lite-rust](https://github.com/SaitoTech/saito-lite-rust), [saito-js](https://github.com/SaitoTech/saito-rust-workspace), and [saito-wasm](https://github.com/SaitoTech/saito-rust-workspace) repositories are cloned on your local machine.




## Installation Guide

## Step 1: Prepare `saito-wasm` for Linking

#### Navigate to the saito-wasm directory

#### Create a symbolic link for saito-wasm in the global node_modules after installation and building

If you're using a Mac with the M1 chip, follow these additional steps:

#### 2. Set Environment Variables

```bash
export CC=/opt/homebrew/opt/llvm/bin/clang
```
#### 3. Install LLVM: This provides the necessary tools, including clang.

```
brew install llvm
```

#### 4 Install wasm-pack: This is a crucial tool for compiling Rust to WebAssembly.

```
npm i -g wasm-pack
```

#### 5 Build with wasm pack
```
CC=/opt/homebrew/opt/llvm/bin/clang AR=/opt/homebrew/opt/llvm/bin/llvm-ar wasm-pack build --target web --out-dir wasm_build/deps/pkg/
```
```
npm install
npm run build
npm link 
```

## Step 2: Link saito-js to saito-wasm

#### 1. Navigate to the saito-js directory


#### 6 Proceed with Installation building and creating a symbolic link
```
npm install
```
```
npm link saito-wasm
```
```
npm run build
```
```
npm link
```

## Step 3: Link SLR to saito-js

#### Navigate to the SLR directory

#### Link to saito-js
``` 
npm install
npm link saito-js
npm run go
```

