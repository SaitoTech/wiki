---
title: Saito NFTs
description: Non-Fungible Saito Tokens and Apps
published: true
date: 2025-11-06T11:23:34.832Z
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



