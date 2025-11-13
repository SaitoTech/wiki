---
title: Saito Scripting - Script Generator Language
description: 
published: true
date: 2025-11-13T09:29:39.174Z
tags: 
editor: markdown
dateCreated: 2025-11-13T09:29:39.174Z
---

# Saito Script: Generate Field Syntax Guide

This page documents the syntax supported by the **Generate** textfield in the Saito Scripting Module.
It explains **what you can type**, **how the parser interprets it**, and **examples of valid and invalid expressions**.

The Saito Script DSL is designed to be **flexible, predictable, and unambiguous**.
It supports a small set of logical operators and user-defined opcodes.
The current default opcode implemented in the Saito module is:

```
CHECKSIG publickey="..." signature="..."
```

Additional opcodes will follow the same rules.

---

# **1. Core Concepts**

### **1.1 Logical Operators**

The scripting language supports three logical operators:

* `AND`
* `OR`
* `NOT`

These operators are **case-insensitive**:

```
and   AND   And   aNd   → all equivalent
```

### **1.2 Opcodes**

Opcodes represent Saito consensus checks (e.g., signature verification).

Example (the default opcode):

```
CHECKSIG publickey="..." signature="..."
```

Opcodes:

* are **case-insensitive**
* may specify fields using `key=value`
* may rely on default values defined by the module

---

# **2. What the Generate Field Accepts**

Below is a comprehensive list of expressions that are *permitted* and *will work* with the Saito Script parser.

---

# **3. Permitted Expressions**

## **3.1 Single CHECKSIG**

```
CHECKSIG
CHECKSIG publickey="abc"
CHECKSIG publickey="abc" signature="sig123"
(CHECKSIG)
(CHECKSIG publickey="abc" signature="sig123")
```

---

## **3.2 Unary NOT**

Works with or without parentheses:

```
NOT CHECKSIG
NOT (CHECKSIG)
(NOT CHECKSIG)
(NOT (CHECKSIG))
NOT NOT CHECKSIG
```

---

## **3.3 AND Combinations**

```
AND CHECKSIG CHECKSIG
AND (CHECKSIG) (CHECKSIG)
(CHECKSIG) (CHECKSIG)       // implicit AND
CHECKSIG CHECKSIG           // implicit AND
(CHECKSIG) CHECKSIG        // implicit AND
CHECKSIG AND CHECKSIG
```

Multi-argument AND:

```
(AND CHECKSIG CHECKSIG CHECKSIG)
```

---

## **3.4 OR Combinations**

```
OR CHECKSIG CHECKSIG
CHECKSIG OR CHECKSIG
(CHECKSIG) OR (CHECKSIG)
```

Multi-argument OR:

```
(OR CHECKSIG CHECKSIG CHECKSIG)
```

---

## **3.5 Mixed AND + OR (with precedence)**

`AND` binds more tightly than `OR`:

```
CHECKSIG OR CHECKSIG AND CHECKSIG
CHECKSIG AND CHECKSIG OR CHECKSIG
NOT CHECKSIG OR CHECKSIG
```

All valid.

---

## **3.6 Nested Logical Groups**

```
AND (OR CHECKSIG CHECKSIG) CHECKSIG
(AND (OR CHECKSIG CHECKSIG) (CHECKSIG))
OR (AND CHECKSIG CHECKSIG) (NOT CHECKSIG)
AND (CHECKSIG) NOT (CHECKSIG)
```

---

## **3.7 Deep Nested Expressions**

```
AND (CHECKSIG) NOT (CHECKSIG NOT CHECKSIG)
NOT (AND (CHECKSIG) (OR CHECKSIG NOT CHECKSIG))
```

---

## **3.8 Multi-line and Extra Spacing**

Whitespace and newlines are ignored:

```
CHECKSIG
AND
CHECKSIG
```

```
CHECKSIG

CHECKSIG
```

---

## **3.9 Field Assignment Flexibility**

```
CHECKSIG publickey="a"
CHECKSIG signature="s"
CHECKSIG publickey="a" signature="s"
```

Mixed in logic:

```
AND CHECKSIG publickey="a" CHECKSIG publickey="b"
```

---

# **4. Implicit AND (Important)**

When multiple expressions appear at the top level, the parser automatically inserts `AND`:

```
CHECKSIG
NOT CHECKSIG
```

becomes:

```
AND CHECKSIG (NOT CHECKSIG)
```

This makes multi-line scripts natural to write.

---

# **5. Summary of Permitted Features**

✔ Case-insensitive logical operators
✔ Case-insensitive opcodes
✔ Parentheses optional in many cases
✔ Unary NOT without parentheses
✔ Infix AND/OR with correct precedence
✔ Flexible whitespace
✔ Optional quoting for field values
✔ Implicit AND between consecutive expressions
✔ Nested expressions
✔ Opcode fields using `key=value`
✔ Multiple top-level expressions

---

# **6. Non-Permitted / Invalid Input**

While the parser is flexible, several forms are *not allowed*:

---

## ❌ **6.1 Natural-language expressions**

The parser **does not** accept English synonyms like:

```
unless CHECKSIG
either CHECKSIG or CHECKSIG
you need CHECKSIG
must CHECKSIG
```

These are intentionally excluded.

---

## ❌ **6.2 Missing operator between expressions inside parentheses**

Example:

```
(CHECKSIG CHECKSIG)
```

Invalid unless the parser is instructed otherwise. Use:

```
(AND CHECKSIG CHECKSIG)
```

or rely on implicit AND *outside* parentheses only.

---

## ❌ **6.3 Unknown operators**

```
XOR CHECKSIG CHECKSIG
BUT CHECKSIG
NAND CHECKSIG CHECKSIG
```

---

## ❌ **6.4 Unknown opcodes or fields**

```
CHECKSIG foo="bar"
SIGNATURECHECK
CHECKOWN
```

---

## ❌ **6.5 Unterminated parentheses or strings**

```
(CHECKSIG
CHECKSIG publickey="abc
```

---

## ❌ **6.6 Operators without arguments**

```
AND
OR
NOT
```

---

# **7. Guiding Principle**

> The Saito Script syntax is designed to be *simple, logical, and predictable* — not a natural language.
>
> If it reads like a Boolean expression, it will probably work.
> If it reads like English, it probably won’t.

---

# **8. Future Extensions**

The language is designed so new opcodes (e.g. CHECKMULTISIG, CHECKEXPIRY, CHECKOWN) can be added with no change to the syntax rules.

---

If you'd like, I can also produce a companion page:

* **“Saito Script: How It Works Internally”** (parser → AST → schema → script → witness → evaluate).
