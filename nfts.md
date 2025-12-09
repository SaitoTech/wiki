---
title: Saito NFTs
description: Non-Fungible Saito Tokens and Apps
published: true
date: 2025-12-09T19:36:17.410Z
tags: 
editor: markdown
dateCreated: 2025-11-06T10:50:40.234Z
---

# Saito NFTs

Saito lets you build NFTs that come with css, javascript, images, embedded-programs and much more, and lets you build them directly from your browser wallet.

This page has a list of simple examples you can copy-and-paste into your own browser to get started. If you want to test out NFTs without the need for mainnet tokens, we recommend grabbing some tokens from the [testnet faucet](https://staging.saito.io/faucet) and then copying and pasting these examples directly into your browser on staging to see how they work!



## Javascript NFTs

<details>
  <summary>Replace Images with External Images </summary>
  
  This recipe replaces any images named "red_back.png" with another file. If you provide your own image you can use it in any of the card games on the Saito Arcade (which use red_back.png as the default card background). You can use this approach to swap out logos too!

```
(() => {
  const replacement = "https://saito.io/saito/img/arcade/cards/purple_back.png";
  const targetName = "red_back.png";

  // Helper: does the URL reference the target file?
  const isTargetUrl = (url) => {
    if (!url || typeof url !== "string") return false;
    if (url.includes(replacement)) return false; // already replaced
    try {
      // handle urls like 'url("...")' or quoted values
      const clean = url.replace(/^url\((['"]?)(.*)\1\)$/i, "$2");
      return clean.split("/").pop() === targetName;
    } catch {
      return false;
    }
  };

  // Safe function to set an img element's src without re-triggering loops
  const setImgSrcIfTarget = (img) => {
    try {
      // some images may have .src resolved to absolute. Check filename.
      if (isTargetUrl(img.getAttribute && img.getAttribute("src"))) {
        img.setAttribute("src", replacement);
      } else if (isTargetUrl(img.src)) {
        // if .src is absolute and ends with targetName
        img.src = replacement;
      }
    } catch (e) {
      // ignore weird elements / cross-origin
    }
  };

  // 1) Override Image constructor (safe)
  try {
    const NativeImage = window.Image;
    window.Image = function(...args) {
      const img = new NativeImage(...args);
      // when someone sets img.src programmatically we can't intercept the setter,
      // but we can watch attribute changes globally (below) — still try to be helpful:
      const origSetAttr = img.setAttribute.bind(img);
      img.setAttribute = function(name, value) {
        if (name === "src" && isTargetUrl(value)) value = replacement;
        return origSetAttr(name, value);
      };
      return img;
    };
    // keep prototype chain so instanceof still works
    window.Image.prototype = NativeImage.prototype;
  } catch (e) {
    // if override fails, ignore — observation below will still catch most cases
  }

  // 2) Patch existing <img> elements now
  document.querySelectorAll("img").forEach(setImgSrcIfTarget);

  // 3) Fix inline styles on existing elements
  const fixInlineBackground = (el) => {
    try {
      const bg = el.style && el.style.backgroundImage;
      if (bg && isTargetUrl(bg)) {
        el.style.backgroundImage = bg.replace(targetName, replacement.split("/").pop())
                                     .replace(/([^"]https?:\/\/[^"]+)/, (m) => m.includes(replacement) ? m : replacement);
        // fallback: set explicit url(...) if above replacement didn't produce absolute URL
        if (!el.style.backgroundImage.includes(replacement)) {
          el.style.backgroundImage = `url("${replacement}")`;
        }
      }
    } catch (e) {}
  };
  document.querySelectorAll("[style]").forEach(fixInlineBackground);

  // 4) Replace stylesheet rules (best-effort; skip CORS-restricted sheets)
  for (const sheet of Array.from(document.styleSheets)) {
    try {
      for (const rule of Array.from(sheet.cssRules || [])) {
        try {
          const bg = rule.style && rule.style.backgroundImage;
          if (bg && isTargetUrl(bg)) {
            // avoid double-wrapping
            if (!bg.includes(replacement)) {
              rule.style.backgroundImage = `url("${replacement}")`;
            }
          }
        } catch (er) {
          // some rule types may throw when accessed; skip
        }
      }
    } catch (e) {
      // stylesheet inaccessible due to CORS — ignore
    }
  }

  // 5) Observe DOM for new images and attribute/style changes
  const observer = new MutationObserver((mutations) => {
    for (const m of mutations) {
      // handle newly added nodes
      if (m.addedNodes && m.addedNodes.length) {
        m.addedNodes.forEach((node) => {
          if (node.nodeType !== 1) return;
          if (node.tagName === "IMG") setImgSrcIfTarget(node);
          // any img descendants
          node.querySelectorAll && node.querySelectorAll("img").forEach(setImgSrcIfTarget);
          // inline styles on added node or descendants
          if (node.hasAttribute && node.hasAttribute("style")) fixInlineBackground(node);
          node.querySelectorAll && node.querySelectorAll("[style]").forEach(fixInlineBackground);
        });
      }
      // handle attribute changes (src or style)
      if (m.type === "attributes") {
        const target = m.target;
        if (!target) continue;
        if (target.tagName === "IMG" && (m.attributeName === "src")) {
          setImgSrcIfTarget(target);
        }
        if (m.attributeName === "style") {
          fixInlineBackground(target);
        }
      }
    }
  });

  observer.observe(document.documentElement || document.body, {
    childList: true,
    subtree: true,
    attributes: true,
    attributeFilter: ["src", "style"]
  });

  // 6) Extra safety: periodically re-scan for stubborn cases (optional, light)
  const rescans = setInterval(() => {
    try {
      document.querySelectorAll("img").forEach(setImgSrcIfTarget);
      document.querySelectorAll("[style]").forEach(fixInlineBackground);
    } catch (e) {}
  }, 1500);

  // Provide a small API to stop if needed
  window.__replaceRedBackStop = () => {
    try { observer.disconnect(); } catch {}
    try { clearInterval(rescans); } catch {}
    // restore Image? we can't reliably restore the original if overridden earlier; skip.
    delete window.__replaceRedBackStop;
    console.log("replacement observer stopped");
  };

  console.log("red_back.png -> purple_back replacement active");
})();
```
  </details>
  


  <details>
  <summary>Replace Images with Embedded Images<</summary>
    
      This recipe is similar to the one above (swap out any image for one you prefer) but shows how to do this using an image that is embedded in the NFT. This makes the NFT larger, but eliminates the need to fetch content from another server.
  
```
const replacement_image = `data:image/png;base64,iVBORw0KGgoAAAANSUhEUg....`;

(() => {
  const replacement = replacement_image;
  const targetName = "red_back.png";

  const isTarget = (url) => {
    if (!url) return false;
    if (url.includes(replacement)) return false;
    const clean = url.replace(/^url\((['"]?)(.*?)\1\)$/i, "$2");
    return clean.split("/").pop() === targetName;
  };

  const fixImg = (img) => {
    try {
      if (isTarget(img.getAttribute("src"))) img.src = replacement;
      else if (isTarget(img.src)) img.src = replacement;
    } catch {}
  };

  const fixBg = (el) => {
    try {
      const bg = el.style?.backgroundImage;
      if (bg && isTarget(bg)) el.style.backgroundImage = `url("${replacement}")`;
    } catch {}
  };

  document.querySelectorAll("img").forEach(fixImg);
  document.querySelectorAll("[style]").forEach(fixBg);

  new MutationObserver((muts) => {
    for (const m of muts) {
      if (m.addedNodes?.length) {
        m.addedNodes.forEach((n) => {
          if (n.nodeType !== 1) return;
          if (n.tagName === "IMG") fixImg(n);
          n.querySelectorAll?.("img").forEach(fixImg);
          if (n.hasAttribute?.("style")) fixBg(n);
          n.querySelectorAll?.("[style]").forEach(fixBg);
        });
      }
      if (m.type === "attributes") {
        if (m.attributeName === "src" && m.target.tagName === "IMG") fixImg(m.target);
        if (m.attributeName === "style") fixBg(m.target);
      }
    }
  }).observe(document.body, {
    childList: true,
    subtree: true,
    attributes: true,
    attributeFilter: ["src", "style"],
  });
})();

```
  </details>

  
<details><summary>Add Keyboard Shortcuts to Saito Applications</summary>

This recipe shows how to add new keyboard shortcuts to Saito. While this NFT is designed for RedSquare, you can use this code to add new functionality to ANY APPLICATION you want! Or even ALL OF THEM!
  
```
// Keyboard shortcut handler:
// - Press "/" then a key for navigation shortcuts
// - Press "?" alone (when not typing) to open help
// All actions log to the console.

(function () {
  let slashMode = false;

  const log = (...args) => console.log("[KS]", ...args);

  const isTextEntryElement = (el) => {
    if (!el) return false;
    const tag = el.tagName;
    if (!tag) return false;
    if (tag === 'INPUT' || tag === 'TEXTAREA') return true;
    if (el.isContentEditable) return true;
    return false;
  };

  const safeClickById = (id) => {
    const el = document.getElementById(id);
    if (el && typeof el.click === 'function') {
      log(`clicking #${id}`);
      el.click();
    } else {
      log(`element #${id} not found`);
    }
  };

  const safeClickSelector = (selector) => {
    const el = document.querySelector(selector);
    if (el && typeof el.click === 'function') {
      log(`clicking ${selector}`);
      el.click();
    } else {
      log(`element ${selector} not found`);
    }
  };

  const showBalanceMessage = () => {
    const amountEl = document.querySelector('.balance-amount');
    const selectEl = document.querySelector('.wallet-select-crypto');

    if (!amountEl || !selectEl || !selectEl.selectedOptions?.[0]) {
      log("balance elements missing — cannot show balance");
      return;
    }

    const cryptoSymbol = selectEl.selectedOptions[0].value;

    const html = `
      <div class="site-message-balance">
        ${amountEl.outerHTML}
        <div>${cryptoSymbol}</div>
      </div>
    `;

    log("showing balance");
    if (typeof siteMessage === 'function') siteMessage(html);
  };

  const keyboardShortcutsHelpHtml = `
    <div class="keyboard-shortcuts-help">
      <h2>Keyboard Shortcuts</h2>
      <p>Press keys (when no text field has focus):</p>
      <ul>
        <li><strong>?</strong> – Show this help</li>
        <li><strong>/ w</strong> – Show wallet</li>
        <li><strong>/ p</strong> – New post</li>
        <li><strong>/ h</strong> – Go to home</li>
        <li><strong>/ n</strong> – Open notifications</li>
        <li><strong>/ s</strong> – Send / withdraw</li>
        <li><strong>/ b</strong> – Show wallet balance</li>
      </ul>
    </div>
  `.trim();

  const showHelp = () => {
    log("showing help");
    if (typeof salert === 'function') salert(keyboardShortcutsHelpHtml);
  };

  document.addEventListener('keydown', function (e) {
    // Modifier keys cancel slash mode
    if (e.ctrlKey || e.metaKey || e.altKey) {
      log("modifier key pressed — cancelling slash mode");
      slashMode = false;
      return;
    }

    const typing = isTextEntryElement(document.activeElement);

    // === HELP KEY (press ? alone) ===
    if (!typing && e.key === '?') {
      log("help key '?' pressed");
      showHelp();
      slashMode = false;
      e.preventDefault();
      return;
    }

    // === SLASH ACTIVATION ===
    if (!slashMode) {
      if (!typing && e.key === '/') {
        slashMode = true;
        log("slash mode activated");
        e.preventDefault();
      } else if (typing) {
        log("typing detected — ignoring key", e.key);
      }
      return;
    }

    // === PROCESS KEY AFTER "/" ===
    slashMode = false;
    const key = e.key.toLowerCase();
    log(`slash+${key} triggered`);

    switch (key) {
      case 'w':
        log("shortcut: wallet");
        safeClickById('saito-header-menu-toggle');
        e.preventDefault();
        break;

      case 'p':
        log("shortcut: post");
        safeClickSelector('.tweet-button');
        e.preventDefault();
        break;

      case 'h':
        log("shortcut: home");
        safeClickSelector('.redsquare-menu-home');
        e.preventDefault();
        break;

      case 'n':
        log("shortcut: notifications");
        safeClickSelector('.redsquare-menu-notifications');
        e.preventDefault();
        break;

      case 's':
        log("shortcut: send");
        safeClickById('wallet-btn-withdraw');
        e.preventDefault();
        break;

      case 'b':
        log("shortcut: balance");
        showBalanceMessage();
        e.preventDefault();
        break;

      default:
        log(`unused shortcut: /${key}`);
        break;
    }
  });
})();

```
</details>

  
  
  <details>
    <summary>Add Menu Item to Slide-In Header Menu</summary>
    
    This creates and adds a module that does nothing except respond to the respondTo() that fetches items to list in the Saito Header. It then provides a menu item and allows us to specify how the module should react to getting clicked
    
```

//
// add new module to stack...
//
let demo_mod = this.app.modules.createAndAddTemplateModule("DemoMod", {

  //
  // have it respond to Saito Header requests for menu items
  //
  respondTo: function (type = '', obj) {
    if (type == "saito-header") {
      return [{
        text: "Demo",
        icon: this.icon || "fas fa-bullhorn",
        rank: 10,
        callback: function (app, id) {
          alert("Clicked!");
        },
      }];
    }
    return null;
  }

});

//
// re-render header
//
this.app.connection.emit("saito-header-render"); 
```
  
  
## CSS NFTS

  <details>
    <summary>Custom CSS Theme -- The Matrix Recipe </summary>

CSS NFTs let you re-skin ALL SAITO APPS by injecting the CSS you provide in the NFT into the application. You can use this to re-theme existing applications, or even add new features. This example switches the NFT holder to a follow-the-rabbit dark-mode Matrix theme:

```
:root {
  --saito-bg: #000 !important;
  --saito-text: #00ff9c !important;
  --saito-muted: #003b2f !important;
  --saito-border: #005533 !important;
  --saito-hover: #00cc88 !important;
  --saito-accent: #00ffcc !important;
  --saito-primary: #00ff88 !important;
  --saito-secondary: #007755 !important;
}

body, .saito-container, .saito-main, .saito-sidebar {
  background-color: var(--saito-bg) !important;
  color: var(--saito-text) !important;
  font-family: 'Courier New', monospace !important;
  letter-spacing: 0.5px;
  text-shadow: 0 0 2px #009966;
}

a, .saito-link {
  color: var(--saito-accent) !important;
  text-decoration: none !important;
}
a:hover, .saito-link:hover {
  color: var(--saito-hover) !important;
  text-shadow: 0 0 8px var(--saito-hover);
}

.saito-header, .saito-footer, .saito-toolbar {
  background-color: #001a12 !important;
  border-bottom: 1px solid var(--saito-border) !important;
  box-shadow: 0 0 10px #002a1a inset;
}

.saito-card, .saito-modal, .saito-overlay {
  background-color: #000 !important;
  border: 1px solid var(--saito-border) !important;
  box-shadow: 0 0 20px #002a1a, inset 0 0 10px #001a0f;
  color: var(--saito-text) !important;
}

input, textarea, select {
  background-color: #000 !important;
  color: var(--saito-text) !important;
  border: 1px solid var(--saito-border) !important;
  outline: none !important;
  padding: 6px 10px;
}
input:focus, textarea:focus, select:focus {
  border-color: var(--saito-primary) !important;
  box-shadow: 0 0 10px var(--saito-primary);
}

button, .saito-button {
  background: linear-gradient(180deg, #002b1b, #000) !important;
  color: var(--saito-primary) !important;
  border: 1px solid var(--saito-border) !important;
  border-radius: 4px !important;
  padding: 6px 14px !important;
  text-transform: uppercase;
  letter-spacing: 1px;
  transition: all 0.2s ease-in-out;
  box-shadow: 0 0 10px #003b24;
}
button:hover, .saito-button:hover {
  background: linear-gradient(180deg, #004b2b, #000) !important;
  border-color: var(--saito-primary) !important;
  box-shadow: 0 0 15px var(--saito-primary);
  color: #00ffaa !important;
}
button:active, .saito-button:active {
  transform: scale(0.98);
  box-shadow: 0 0 5px var(--saito-secondary) inset;
}

hr {
  border: none;
  border-top: 1px solid var(--saito-border);
}
.saito-highlight, mark {
  background-color: #002a1a !important;
  color: var(--saito-primary) !important;
  border-radius: 2px;
  padding: 0 3px;
}

@keyframes matrix-glow {
  0%, 100% { text-shadow: 0 0 2px #009966, 0 0 4px #00ffcc; }
  50% { text-shadow: 0 0 8px #00ffcc, 0 0 16px #00ff88; }
}
.matrix-glow { animation: matrix-glow 2s infinite alternate; }

@keyframes matrix-cursor {
  0%, 100% { opacity: 1; }
  50% { opacity: 0; }
}
.matrix-cursor::after {
  content: "_";
  animation: matrix-cursor 1s infinite;
  color: var(--saito-accent);
}

::-webkit-scrollbar {
  width: 8px;
  background-color: #000;
}
::-webkit-scrollbar-thumb {
  background-color: var(--saito-secondary);
  border-radius: 4px;
}

::selection {
  background-color: var(--saito-accent);
  color: #000;
}
```
  </details>

  <details>
    <summary>BONUS - add Javascript to any CSS Theme </summary>

This isn't a full recipe, but it shows how to combine JS and CSS into a single NFT. To create this DEMO RECIPE go to the CREATE NFT overlay and select "JSON" from the NFT-TYPE dropdown. Couldn't be easier!

```
{
  js : `alert("Hello World!")` ,
  css : `#saito-header { background : #000; }`
}
```
  </details>
    
  
## Web3 Cryptocurrencies
  
  <details><summary>Add Support for Mixin Crypto </summary>

This recipie shows how to add any Mixin-supported web3 crypto to the browser wallet, where it can then be used with any of the Arcade Games or other apps running on Saito, There are [more than 500 cryptos to choose from](https://api.mixin.one/network/assets/top?kind=NORMA) -- install this NFT to make any of them a first class citizen on Saito!

```
let mixin_mod = this.app.modules.returnModule("Mixin");
if (!mixin_mod) { return; }

let MixinModule = mixin_mod.MixinModule;
if (!MixinModule) {
  console.error("MixinModule not available on Mixin");
  return;
}

//
// crypto definition
//
const cryptoConfig = {
  appname:     "NEAR",
  name:        "NEAR",
  slug:        "near",
  ticker:      "NEAR",
  description: "Adds support for Mixin-powered NEAR transfers on the Saito Network",
  categories:  "Utility Cryptocurrency Finance",
  asset_id:    "97e3c2c1-9967-3a59-9b25-b30bc2045bbb",
  chain_id:    "43d61dcd-e413-450d-80b8-101d5e903357",
};

//
// instantiate crypto module
//
let crypto_module = new MixinModule(
  this.app,
  mixin_mod,
  cryptoConfig.ticker,
  cryptoConfig.asset_id,
  cryptoConfig.chain_id
);

//
// fetch metadata + install
//
let info = await crypto_module.returnNetworkInfo();
crypto_module.price_usd = info?.price_usd ?? 0;

await crypto_module.installModule(mixin_mod.app);

//
// attach to mixin runtime state
//
if (!Array.isArray(mixin_mod.crypto_mods)) {
  mixin_mod.crypto_mods = [];
}

mixin_mod.crypto_mods.push(crypto_module);
this.app.modules.mods.push(crypto_module);

//
// auto-activate if possible
//
if (mixin_mod.account_created) {
  if (crypto_module.isActivated()) {
    await mixin_mod.fetchSafeUtxoBalance();
  } else if (crypto_module.address) {
    crypto_module.activate();
  }
}

//
// notify UI / app
//
this.app.connection.emit("saito-header-update-crypto");
```
</details>
  
  
  
