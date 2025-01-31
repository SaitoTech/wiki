---
title: How to create ZK-enabled apps on Saito
description: This documentation describes how to create and integrate ZK proofs on Saito application using ZK-Snarks
published: true
date: 2025-01-31T19:42:28.481Z
tags: 
editor: markdown
dateCreated: 2025-01-31T18:45:46.925Z
---

# Saito and Zero-Knowledge Proof Integration Guide

## Overview

This documentation describes how Saito integrates with zero-knowledge proofs (ZK proofs) to enable privacy-preserving applications while maintaining blockchain verifiability.

## Architecture

### Components

#### 1. Saito Module Layer
* Handles application logic and state management
* Loads ZK-related components (verification keys, circuits) 
* Manages transaction flow and blockchain storage

#### 2. ZK Proof System
* Uses snarkjs for proof operations
* WebAssembly-compiled circuits for browser execution
* Client-side proof generation and verification

### Core Files
/zk/
  ├── build/circuit_name_js/
  │   └── circuit_name.wasm    # WebAssembly-compiled circuit
  └── output/
      ├── verification_key.json # For proof verification
      └── circuit_final.zkey    # Proving parameters
      
   
## Creating and Packaging Zero-Knowledge Proofs for Saito

## Prerequisites

* [circom](https://docs.circom.io/) - For writing ZK circuits 
* [snarkjs](https://github.com/iden3/snarkjs) - For proof generation and verification
* Node.js environment

## Steps

### 1. Write the Circuit

For a detailed guide on creating circuits, refer to the [SnarkJS tutorial](https://github.com/iden3/snarkjs#create-the-circuit).

### 2. Compile Circuit 

Use our compilation script:

```bash
# Make script executable
chmod +x compile_circuit.sh

## Running the Script
# Navigate to mod directory
cd mods/your_mod

# Run compilation script for your circuit
../../scripts/compile_circuit.sh circuit_name 
```
**The script will:**
1. Create necessary directories if they don't exist
2. Compile circuit to WASM and generate supporting JavaScript files 
3. Generate proving/verification keys
4. Place all outputs in appropriate locations:
  * WASM and JS files → `build/your_circuit_js/`
  * Keys and other outputs → `output/`

## Script Requirements

Make sure you have:
* `input.json` file in your working directory
* Circuit file named `your_circuit.circom` in the circuits folder

## Generated Files

The compilation produces several important files:
* `your_circuit.wasm`: WebAssembly binary of your circuit
* `generate_witness.js`: Script for generating witnesses
* `witness_calculator.js`: Core witness calculation logic
* Supporting proof and verification files

## Notes
* The script requires execute permissions: `chmod +x scripts/compile-circuit.sh`
* Make sure circom and snarkjs are installed globally
* Keep `input.json` in the directory where you run the script






      
      
      