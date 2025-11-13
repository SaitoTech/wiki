---
title: Saito Scripts
description: A description of Saito Scripts and how to create them....
published: true
date: 2025-11-13T09:29:03.261Z
tags: 
editor: markdown
dateCreated: 2025-11-12T11:45:21.103Z
---

> # Saito Scripts - Writing Scripts
{.is-info}


Saito Scripts are provided in JSON form, as in the example below. This is intended to provide a HUMAN-READABLE way of encoding scripts. If you are interested you can use our [Script Generator](/scripting/scripts/generate) to create these more complicated script forms as part of the Saito Scriptorium..

```
{
  "op": "AND",
  "args": [
    {
      "op": "CHECKSIG",
      "pubkey": "muJ8J1paK3nvHdFtdpakTejgCsAVkFmG7rGkc2dvCNpm",
      "msg": "hello world"
    },
    {
      "op": "CHECKSIG",
      "pubkey": "muJ8J1paK3nvHdFtdpakTejgCsAVkFmG7rGkc2dvCNpm",
      "msg": "hello again"
    }
  ]
}
```

Once you have written a script, you can sign it and reduce it to a hash using the tools in the Saito Scriptorium, which are provided in the `scripting` module.