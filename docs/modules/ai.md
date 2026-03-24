---
title: Module Development for AI
description: 
published: true
date: 2026-03-24T06:13:55.463Z
tags: 
editor: markdown
dateCreated: 2026-03-24T06:13:55.463Z
---

# Building a Saito Module

A Saito module is a self-contained feature that plugs into the Saito network. It typically includes core logic, UI components, templates, and optionally server-side functionality.

The design philosophy is simple: **separate logic, rendering, and layout cleanly**.

---

## 1. Directory Structure

A standard module should follow this structure:

    /mods/yourmodule/
    │
    ├── yourmodule.js                   # main module file (required)
    ├── web/
    │   ├── index.html								  # html file
    │   ├── style.css                   # will auto-compile
    │   ├── img/                        # images go here
    │   └── css/                        # css files
    │       ├── yourmodule-base.css     
    │       └── yourmodule-main.css     
    ├── lib/
    │   └── ui/                    # ALL UI components
    │       ├── main.js            # main ui component 
    │       ├── main.template.js   # main template file
    │       └── overlays/          # modals, popups
    │
    └── sql/                       # sqlite3 files (optional)

---

## 2. Core Module File (yourmodule.js)

This is the brain of your module. It coordinates everything but should not directly construct UI.

### Responsibilities

- Register the module
- Handle blockchain and application events
- Manage state
- Trigger rendering

### Example

    class YourModule extends ModTemplate {

      constructor(app) {
        super(app);
        this.name = "YourModule";
        this.slug = "yourmodule";
      }

      async initialize() {
        if (!this.browser_active) { return; }      
        this.main = new MainUI(this.app, this);
      }

      render() {
      
        if (!this.browser_active) { return; }

        this.main.render();
      }

      onConfirmation(blk, tx, conf) {
        // handle blockchain events here
      }

    }

    module.exports = YourModule;

**Important:** The module orchestrates UI — it does not build it.

---

## 3. UI Organization (/lib/ui/)

All UI code must live in `/lib/ui/`.

    /lib/ui/
    │
    ├── main/              # top-level layout
    │   ├── main.js
    │   └── main.template.js
    │
    └── overlays/          # modals and popups
        └── compose/
            ├── compose.js
            └── compose.template.js

---

## 4. UI Component Pattern

Each UI component consists of two files:

- component.js → logic and behavior  
- component.template.js → HTML rendering  

### Component Logic Example

    const ComponentTemplate = require('./component.template');

    class Component {

      constructor(app, mod, container=".saito-container", data = {}) {
        this.app = app;
        this.mod = mod;
        this.data = data;
      }

      render() {

        if (!document.querySelector(this.container)) {
          this.app.browser.addElementToSelector(
            ComponentTemplate(this),
            container
          );
        } else {
          this.app.browser.replaceElementBySelector(
            ComponentTemplate(this),
            '.component-wrapper-class-from-template-file'
          );
        }

        this.attachEvents();
      }

      attachEvents() {
        // bind DOM events here
      }

    }

    module.exports = Component;

---

### Template File Example

    module.exports = (component) => {
      return `
        <div class="component-wrapper-class-from-template-file">
          <div class="title">${component.data.title}</div>
        </div>
      `;
    };

---

## 5. Key Design Rules

### Templates are pure

- No logic  
- No DOM manipulation  
- Only return HTML  

### Components control rendering

- Decide when to add vs replace elements  
- Attach DOM events  

### Module handles orchestration

- Creates components  
- Passes data  
- Manages state  

---

## 6. Rendering Flow

Rendering should always be handled by the render() function in components, and re-rendering a component should simply call that component and run render() again. The logic dictating how content is updated can be specific to that item.

### Example

    this.main = new MainUI(this.app, this);
    this.main.render();

Inside MainUI:

    this.header.render();
    this.feed.render();
    this.sidebar.render();

---

## 7. DOM Strategy

Use consistent rendering methods provided in the /lib/saito/browser.js file:

- addElementToSelector → initial render  
- replaceElementBySelector → updates  

Avoid:

- Direct innerHTML manipulation  
- Global DOM queries across unrelated components  

---

## 8. CSS Organization

Your CSS should mirror your UI structure:

    .yourmodule-container

    .main
    .header
    .feed
    .tweet
    .sidebar

Keep layout and component styling logically separated.

---

## 9. Web Server (Optional)

If your module uses /web/index.html there is no need to provide a custom webServer() function as below -- the server will automatically notice the existence of the file and serve it in response to any requests. If you wish to customize the landing page with routing, you can override that webServer() function and specify what it serves:

### /web/webServer.js

    webServer(app, expressapp, express) {

      expressapp.get('/yourmodule', (req, res) => {
        res.sendFile(__dirname + '/index.html');
      });

    }

---

## 10. Mental Model

A Saito module consists of:

- A stateful controller (yourmodule.js)  
- A tree of UI components (/lib/ui)  
- A set of pure templates  

Think in layers:

    State → Components → Templates → DOM

---

## 11. Common Mistakes

Avoid:

- Mixing logic into templates  
- Rendering UI directly in the module  
- Putting everything in a single file  
- Using global DOM selectors across components  
- Failing to properly re-render components  

---

## 12. Minimal Example Checklist

To build a new module:

1. Create yourmodule.js  
2. Create /lib/ui/main/main.js  
3. Create /lib/ui/main/main.template.js  
4. Call main.render() from the module  
5. Add subcomponents as needed  

---

This structure keeps modules modular, predictable, and easy to extend.