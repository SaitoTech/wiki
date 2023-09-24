---
title: Connecting Saito Repositories locally for M1 | An installation Guide
description: 
published: true
date: 2023-09-24T12:28:02.013Z
tags: 
editor: markdown
dateCreated: 2023-09-20T20:31:08.392Z
---


# Mac (M1) Specific Installations

This page assumes you are using a Mac with the M1 chip and want to compile a custom version of the Saito WASM library and have it used by a locally-compiled version of Saito Javascript. If you are trying to compile Saito on another OS please see our [standard installation guide](/tech/installation).

NOTE: saito-lite-rust relies on two npm modules, saito-js and it's dependency saito-wasm that provide core saito functions to the nodejs and javascript nodes.

These modules are published to npm and included in saito-lite-rust's package.json file.

Developers who want to work on the code in these libraries will need to "link" them using the instructions in this pace. This allows for developers to incorporate their code into saito-lite-rust for testing without having to publish the modules to public npm repositories.

## Prerequisites

Before starting, ensure:

- nodeJS and npm are installed.

- homebrew is installed - [install](https://brew.sh/)

- you have the [saito-lite-rust](https://github.com/SaitoTech/saito-lite-rust), and [saito-rust-workspace](https://github.com/SaitoTech/saito-rust-workspace) repositories cloned on your local machine and are capable of compiling them.


## Step 1. Compiling Saito WASM

#### 1. install LLVM for necessary tools (clang, etc.).
```
brew install llvm
```

#### 2. set environment variables
```bash
export CC=/opt/homebrew/opt/llvm/bin/clang
```

#### 3. navigate into saito-wasm directory
```
cd saito-rust-workspace/saito-wasm
```

#### 4. install wasm-pack: crucial tool for compiling Rust to WebAssembly
```
npm i -g wasm-pack
```

#### 5. compile with wasm-pack
```
CC=/opt/homebrew/opt/llvm/bin/clang AR=/opt/homebrew/opt/llvm/bin/llvm-ar wasm-pack build --target web --out-dir wasm_build/deps/pkg/
```

#### 6. install
```
npm install
```

#### 7. build
```
npm run build
```

#### 8. create symbolic link for saito-wasm
```
npm link 
```

## Step 2: Bundle Saito WASM into NodeJS Package

#### 1. navigate into saito-js directory
```
cd saito-rust-workspace/saito-js
```

#### 2. install  
```
npm install
```

#### 3. link with saito-wasm
```
npm link saito-wasm
```

#### 4. build
```
npm run build
```

#### 5. navigate into dist directory
```
cd dist
```

#### 6. create symbolic link for saito-js
```
npm link
```


## Step 3: Use Custom Saito-JS with Saito Lite (Rust)

#### 1. navigate into Saito Lite (Rust) directory
``` 
cd saito-lite-rust
```

#### 2. install
``` 
npm install
```
#### 3. iink with saito-js
```
npm link saito-js
```

#### 4. build and run SLR
```
npm run go
```


