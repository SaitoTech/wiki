---
title: Saito Scripting
description: 
published: true
date: 2025-11-11T17:47:07.858Z
tags: 
editor: markdown
dateCreated: 2025-11-11T17:47:07.858Z
---

# Saito Scripting

Saito is developing a lightweight, deterministic scripting language that can be used within Saito both to handle **access control** (off-chain authorization) for requests to private transactino archives and then eventually **payment control** (programmatically spending UTXO using the same scripting language).

Access control works through these standardized fields, which may be included in the transaction message (`tx.msg`) space:

| Field                     | Purpose                  | Description                                                                                                          |
| ------------------------- | ------------------------ | -------------------------------------------------------------------------------------------------------------------- |
| **`msg.access_hash`**     | Locking rule – Access    | Blake3 hash of the *access script* that defines who may read, write, or delete associated content.                   |
| **`msg.access_script`**   | Unlocking rule – Access  | The full script evaluated by Archive nodes when a user requests access. Its canonical hash must equal `access_hash`. |
| **`msg.access_witness`**  | Runtime inputs – Access  | Per-request variables and proofs (signatures, NFT proofs, timestamps) supplied by the requester.                     |

---

### How Scripting Works

Access scripts are structured as **expression trees** encoded in JSON:

```json
{
  "op": "<OPCODE>",
  "args": [ <sub-expressions> ]
}
```

Every node specifies an operation (`op`) and zero or more arguments (`args`). In order to be valid the finished script must hash down to the `tx.msg.access_hash` value. And when provided to a remote server along with the `tx.msg.access_witness` data, it must evaluate to a positive boolean result.

We are starting with support for the following primitive OPCODES:

| Opcode          | Description                                                       |
| --------------- | ----------------------------------------------------------------- |
| `AND`           | Returns true if all child expressions evaluate true.              |
| `OR`            | Returns true if any child expression evaluates true.              |
| `NOT`           | Logical negation of its single child.                             |
| `CHECKSIG`      | Verifies a signature in the witness matches the given public key. |
| `CHECKMULTISIG` | Requires *m* of *n* valid signatures supplied in the witness.     |
| `CHECKOWN`      | Confirms requester owns the UTXO specified.  |
| `CHECKEXPIRY`   | Valid only if the current time ≤ `t`.                             |

Future releases will add additional OPCODES to provide expanded support for more complicated scripting requirements.

---

The scripting engine is called by providing all three critical values:

```js
access_hash
access_script
access_witness
```

The `access_script` is first hashed to check that it reduces to the `access_hash`. If this is successful the `access_witness` data is inserted into the `access_script` and the program is executed to see if a positive result is returned.

Our goal is to provide a basic but flexible scripting language that can be upgraded in the future as usage demands. For practical reasons, we impose the following constraints on scripts at present and will exit rather than run programs that exceed these safety limits:

* Maximum recursion depth: 8
* Maximum total nodes per script: 16
* No loops or side effects.
* Reject or ignore unknown opcodes

