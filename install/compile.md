---
title: Compiling the node.js stack
description: 
published: true
date: 2025-09-22T14:18:57.302Z
tags: 
editor: markdown
dateCreated: 2025-09-22T14:18:57.302Z
---

# Saito Compile Script

A comprehensive build and compilation script for the Saito blockchain platform that handles CSS consolidation, JavaScript bundling, and system configuration.

## Overview

The `compile` script is a Bash utility that manages the build process for Saito's lite client. It handles CSS compilation, module configuration, build numbering, and various reset operations for development and production environments.

## Usage

```bash
npm run [mode] [options] #(./scripts/compile [MODE] [OPTIONS])
```

### Modes

#### `dev` - Development Mode
```bash
npm run compile dev #./scripts/compile dev
```
- Links CSS files instead of concatenating them
- Skips build number updates
- Optimized for rapid development cycles
- Preserves source file structure for debugging
- Uses Cacheing for much faster compilation

#### `reset` - Reset Non-Persistent Data
```bash
npm run reset #./scripts/compile reset
```
- Resets blockchain data and temporary files
- Preserves user databases and core configuration
- Compiles TypeScript and JavaScript
- Ideal for testing with fresh blockchain state

#### `nuke` - Complete Reset
```bash
npm run nuke #./scripts/compile nuke
```
- ** WARNING: Destructive operation**
- Resets ALL data including persistent databases
- Completely rebuilds the bundler directory
- Use only when starting completely fresh

#### `recompile` - JavaScript Only
```bash
npm run compile #./scripts/compile recompile
```
- Rebuilds only JavaScript bundles
- Skips data reset operations
- Fastest option for code-only changes

## What It Does

### 1. Build Number Management
- Generates timestamp-based build numbers
- Creates `config/build.json` if missing
- Skips build number updates in dev mode

### 2. Configuration Setup
- Ensures essential config files exist:
  - `config/options.conf` (from template if missing)
  - `config/modules.config.js` (from template if missing)

### 3. CSS Processing

#### Development Mode (`dev`)
- **Links** CSS files using `@import` statements
- Enables hot-reloading and easier debugging
- Creates import-based `style.css` files for each module

#### Production Mode
- **Concatenates** all CSS files into single files
- Processes module-specific CSS: `mods/*/web/css/*.css` → `mods/*/web/style.css`
- Consolidates core CSS:
  - `game-*.css` files → `web/saito/game.css`
  - `saito-*.css` files → `web/saito/saito.css`

### 4. Module Management
- Copies modules to bundler directory based on `config/modules.config.js`
- Removes development files (docs, source, etc.) from production bundles
- Handles lite client module configuration

### 5. Data Management

#### Non-Persistent Reset (`reset`)
- Backs up databases to `data/backup/`
- Removes temporary files:
  - Block files (`*.sai`, `*.zip`)
  - Log files
  - Journal files
  - Development databases
- Preserves user data and registry

#### Persistent Reset (`nuke`)
- Removes core databases:
  - `memento.sq3`
  - `assetstore.sq3` 
  - `registry.sq3`
  - `league.sq3`
- Complete fresh start

## File Structure

### Input Files
```
config/
├── build.json                 # Build number storage
├── options.conf              # Runtime configuration
├── modules.config.js         # Module definitions
├── .template.options.conf    # Template configuration
└── .template.modules.config.js

mods/*/web/css/              # Module CSS files
web/saito/
├── game-*.css               # Game-specific styles
├── saito-*.css             # Core platform styles
└── css-imports/xclose.css  # Shared components
```

### Output Files
```
web/saito/
├── saito.js                 # Compiled JavaScript bundle
├── game.css                # Compiled game styles
└── saito.css               # Compiled platform styles

mods/*/web/style.css        # Per-module compiled styles
bundler/default/            # Production bundle directory
```

## Development Workflow

### Daily Development
```bash
npm run compile dev #./scripts/compile dev
```
Use this for regular development work. Fast compilation with linked CSS for easy debugging.

### Testing New Features
```bash
npm run reset [dev] #./scripts/compile reset
```
Clean blockchain state but preserve user data. Good for testing features that need fresh chain state.

### Clean Environment
```bash
npm run nuke [dev] #./scripts/compile nuke
```
**Use sparingly** - completely wipes all data. Only for major testing or when you need to start completely fresh.

### Code-Only Changes
```bash
npm run compile #./scripts/compile recompile
```
Fastest option when you've only changed JavaScript/TypeScript code.

## Dependencies

- **Node.js** - For webpack compilation
- **TypeScript Compiler** (`tsc`) - For TypeScript compilation  
- **Webpack** - For JavaScript bundling
- **Standard Unix tools** - `find`, `sed`, `cat`, `cp`, `rm`

## Configuration

### Module Configuration
Edit `config/modules.config.js` to control which modules are included in lite client builds.

### Build Options  
The script reads configuration from:
- `config/options.conf` - Runtime options
- `config/build.json` - Build number tracking

## Troubleshooting

### Missing Configuration Files
The script automatically creates missing config files from templates. If you see template-related errors, ensure the template files exist in the `config/` directory.

### Build Failures
Check that all dependencies are installed:
```bash
npm install
```

### Selective Module Building
Modify `config/modules.config.js` to control which modules are included in the lite client bundle.

---

**Note**: This script modifies files and databases. Always backup important data before running destructive operations like `nuke`.
