---
title: Using Wasm in Saito
description: How to using wasm inside Saito applications
published: true
date: 2025-01-21T16:07:42.431Z
tags: 
editor: markdown
dateCreated: 2025-01-21T16:07:42.431Z
---

# Using WebAssembly (Wasm) in JavaScript

1. **Add a `.wasm` File**  
   Place your compiled WebAssembly file (e.g., `module.wasm`) in the same directory as your JavaScript code.

2. **Import the Wasm Module**
   In your JavaScript or TypeScript file, import the `.wasm` module:
   ```js
   import wasmModule from "./module.wasm";
   ```
 
3. **Instantiate the Wasm Module** 
Define the JavaScript functions or objects that the Wasm module will use as imports. Then, instantiate the Wasm module:
```js
  const importObject = {
  env: {
    // any functions or global values for the module should go here
    imported_func: (arg) => {
      console.log("Called from Wasm with arg:", arg);
    },
  },
};

// Instantiate the module with the import object
const { instance } = await WebAssembly.instantiate(wasmModule, importObject);
```

4. **Call Exported Functions from Wasm**

Access and invoke functions that the Wasm module exports:

```js
const result = instance.exports.exported_func(42);
console.log("Returned from Wasm:", result);
```

5. **Example usage inside a Saito Module**

```js

import wasmModule from "./path-to/module.wasm";

class Blog extends ModTemplate {
  constructor(app) {
    super(app);
    this.app = app;
  }

  async initialize() {
    const importObject = {
      env: {
        imported_func: (arg) => {
          console.log("Wasm called JS:", arg);
        },
      },
    };

    // Instantiate the Wasm module
    const { instance } = await WebAssembly.instantiate(wasmModule, importObject);
    
    this.wasm_instance = instance

    // Use an exported function
    const value = this.instance.exports.exported_func(42);
    console.log("Wasm returned:", value);
  }
}

module.exports = Blog;

```


