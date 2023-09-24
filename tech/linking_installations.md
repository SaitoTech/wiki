---
title: Connecting Saito Repositories Locally: An Installation Guide
description: This guide details how to manually link the saito-lite-rust repository to saito-wasm using the saito-js wrapper, leveraging the npm link command for local integration.
published: true
date: 2023-09-24T12:29:00.318Z
tags: 
editor: markdown
dateCreated: 2023-09-20T20:23:18.461Z
---


# Overview


#### If you're using a Mac with the M1 chip, you can find specific instructions [here](https://wiki.saito.io/e/en/tech/linking_installations_mac)

This guide provides a detailed walkthrough on how to link the saito-lite-rust repository to the saito-wasm locally via the saito-js wrapper. This process leverages the npm link command.

NOTE: unless you know why you are doing this you probably don't need to do it at all! Our Saito Javascript repository (saito-lite-rust) comes bundled with a pre-compiled version of the WASM saito-js library included its package.json and will work without the need to compile or link anything locally. These steps are only necessary if you want to modify the Rust/Javascript code or debug core parts of the software from within javascript.



## Prerequisites

Before starting, ensure:

- Node.js and npm are installed.

- [saito-lite-rust](https://github.com/SaitoTech/saito-lite-rust), [saito-js](https://github.com/SaitoTech/saito-rust-workspace), and [saito-wasm](https://github.com/SaitoTech/saito-rust-workspace) repositories are cloned on your local machine.




## Installation Guide

## Step 1: Prepare `saito-wasm` for Linking

#### 1. Navigate to `saito-wasm` directory
#### 2. Install
```
npm install
```
#### 3. build
```
npm run build
```
#### 4. create a symbolic link for saito-wasm
```
npm link 
```

## Step 2: Link saito-js to saito-wasm

#### 1. Navigate to the saito-js directory


#### 2. Install 
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

## Step 3: Link SLR to saito-js

#### 1. Navigate to the SLR directory

#### 2. Install
``` 
npm install
```
#### 3. Link with saito js
```
npm link saito-js
```
#### 4. Build and run SLR
```
npm run go
```


