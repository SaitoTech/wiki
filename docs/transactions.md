---
title: Transaction Message Field
description: 
published: true
date: 2025-11-11T17:21:40.813Z
tags: 
editor: markdown
dateCreated: 2025-11-11T17:21:40.813Z
---

# Transaction Reference Fields

| Field                     | Role / Meaning                                                                                               | When It’s Used                                |
| ------------------------- | ------------------------------------------------------------------------------------------------------------ | --------------------------------------------- |
| **`msg.module`**          | Target module that should interpret the message.                                                             | Always present.                               |
| **`msg.request`**         | Operation or command for that module (e.g. `"save"`, `"load"`, `"mint"`, `"transfer"`).                      | Always present.                               |
| **`msg.data`**            | Deterministic payload or content data. Included in transaction hash and signature.                           | Always present.                               |
| **`msg.opt`**             | Optional / mutable metadata (UI hints, routing notes, previews). Ignored for hashing and signing.            | Optional.                                     |
| **`msg.sig`**             | Creator’s digital signature over canonical hashed message fields. Proves authorship.                         | Always present.                               |
| **`msg.access_hash`**     | Hash of the **access (locking) script** — defines who may read, write, or delete related content.            | Stored when transaction is created.           |
| **`msg.access_script`**   | Full **access script** defining the rule whose hash equals `access_hash`. Supplied when proving access.      | Provided by requester when accessing content. |
| **`msg.access_witness`**  | Runtime variables and proofs (signatures, NFT ownership proofs, timestamps) used to satisfy `access_script`. | Provided by requester when accessing content. |
| **`msg.payment_hash`**    | Hash of the **payment (locking) script** — defines who may spend a UTXO created by this transaction.         | Stored when UTXO is created.                  |
| **`msg.payment_script`**  | Full **payment (redeem) script** whose hash equals `payment_hash`. Revealed when spending a UTXO.            | Included only in spending transactions.       |
| **`msg.payment_witness`** | Runtime proofs and signatures that satisfy the `payment_script`.                                             | Included only in spending transactions.       |
