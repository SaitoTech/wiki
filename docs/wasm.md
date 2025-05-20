---
title: Using Wasm in Saito
description: How to using wasm inside Saito applications
published: true
date: 2025-05-20T03:11:29.956Z
tags: 
editor: markdown
dateCreated: 2025-01-21T16:07:42.431Z
---

- # WasmLoader Documentation

## Overview
The WasmLoader is a utility module for loading and managing WebAssembly modules in your Saito application. It provides:
- Cross-platform WebAssembly loading (browser & Node.js)
- Instance caching and management
- Automatic path resolution

## Basic Usage in a Saito mod

####  Before Usage, make sure all wasm files are located in the /web directory of the saito module 
*

### 1. Import the WasmLoader
```js
const WasmLoader = require("../../lib/helpers/wasmLoader");
```

### 2. Create Import Object

Generate or provide the import object required by your WASM module:

```js
const importObject = {
    env: {
        memory: new WebAssembly.Memory({ initial: 256 })
        // ... other imports
    }
};
```

### 3. Load and Use the WASM Module

```js
// Load module
onPeerHandshakeComplete(){
const loader = new WasmLoader(app, mod);
const instance = await loader.loadWasm('file_name.wasm', importObject);

// Execute functions
const result = instance.exports.yourFunction();
}
```



### 4. Instance Management

```js
// Clear specific instance
loader.clearInstance('file_name.wasm');

// Clear all instances
loader.clearAllInstances();
```








