---
title: Saito NFTs
description: Non-Fungible Saito Tokens and Apps
published: true
date: 2025-11-12T04:37:59.878Z
tags: 
editor: markdown
dateCreated: 2025-11-06T10:50:40.234Z
---

# Saito NFTs

Saito supports programmatic NFTs that contain images, javascript, css and a lot more. This page offers a quick code-reference for developers and users who want to copy-and-paste their own custom NFTs.


### Dynamic Image Replacement

Thiis code replaces any files named "red_back.png" with the file linked in the replacement variable. If you provide your own image you can now use it to play cards in any of the Saito card games (which use red_back.png as the card background filename)

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

### Dynamic Image Replacement (embedded)

Almost exactly the same as above, except the image is embedded in the NFT itself as a data:image binary file. The contents need to be updated with whatever image is desired as a replacement...

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

### CSS Insertion

You can insert arbitrary CSS into NFTs by creating a CSS NFT or putting the stylesheet into txmsg.data.css. Here is an example of a simple Matrix enter-the-rabbithole theme:

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


### Mixin Module Crypto

This NFT adds an additional Mixin-supported web3 crypto to the browser wallet. There are 500 of them! Which one do you want running your browser? reference: https://api.mixin.one/network/assets/top?kind=NORMAL
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

