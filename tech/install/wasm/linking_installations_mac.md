---
title: Connecting Saito Repositories locally for M1 | An installation Guide
description: 
published: true
date: 2024-11-21T05:52:08.330Z
tags: 
editor: markdown
dateCreated: 2023-09-20T20:31:08.392Z
---


# Mac (M1) Specific Installations

This page assumes you are using a Mac with the M1 chip and want to compile a custom version of the Saito WASM library and have it used by a locally-compiled version of Saito Javascript. If you are trying to compile Saito on another OS please see our [standard installation guide](/tech/install/wasm).

NOTE: unless you know why you are doing this you probably don't need to do it at all! Our Saito Javascript repository (saito-lite-rust) comes bundled with a pre-compiled version of the WASM saito-js library included its package.json and will work without the need to compile or link anything locally. These steps are only necessary if you want to modify the Rust/Javascript code or debug core parts of the software from within javascript.

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

## Troubleshooting:

If you run into a problem compiling or linking after installing software, please restart your machine. The following may also assist (restart after):
```
rustup target add wasm32-unknown-unknown
cargo install wasm-pack
cargo install wasm-opt
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


## Step 4: Finalization Registry Bug

If you get a problem when compiling Saito-Lite-Rust, you may need to comment-out the following lines from the file ```/saito-js/lib/wasm_wrapper.ts```. You will then need to recompile saito-js by running ```npm run build``` in your saito-js directory as shown in Step 2 above:

```
export default class WasmWrapper<T> {
  public instance: T;

  private static createdCounter = 0;
  private static deletedCounter = 0;
  // private static registry = new FinalizationRegistry((value: any) => {
  //   // WasmWrapper.deletedCounter++;
  //   // console.log(deleted : ${WasmWrapper.deletedCounter} created : ${WasmWrapper.createdCounter} ptr : ${value.__wbg_ptr});
  //   // @ts-ignore
  //   if (value && !!value.__wbg_ptr) {
  //     value.free();
  //   }
  // });
  constructor(instance: T) {
    this.instance = instance;
    WasmWrapper.createdCounter++;
  }


  // free() {
  //   // @ts-ignore
  //   this.instance.free();
  // }
}
```

## Step 5: Confirm Install Successful

This step is completely optional, but if you're not sure that your machine is using your local copy of saito-js, you can check by looking for the initialize() function in the file ```/saito-rust-workspace/saito-wasm/src/saitowasm.rs``` and editing the call to info() somewhere around line 338 to print a custom message such as ```info!("initializing local copy of saito-wasm!");```. 

Repeat Steps 1-3 above and when you run Saito-Lite-Rust you should see your log message printed instead of the default.



## Troubleshooting:

wasm-unknown-unknown issues - seee https://github.com/briansmith/ring/issues/1824