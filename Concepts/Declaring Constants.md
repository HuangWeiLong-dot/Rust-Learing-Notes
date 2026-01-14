---
tags:
  - concept
  - rust
  - delareconstant
Created: 2026-01-14
Date: "[[2026-01-14]]"
categories: "[[Variables and Mutability]]"
---

# Declaring Constants

> Like immutable variables, _constants_ are values that are bound to a name and are not allowed to change, but there are a few differences between constants and variables.
> First, you aren’t allowed to use `mut` with constants. Constants aren’t just immutable by default—==they’re always immutable==.
> You declare constants using the [[const]] keyword instead of the [[let]] keyword.
> And the type of the value _must_ be ==annotated==.

\-  See [[Data Types]].

Constants can be declared in any [[scope]], including the [[global scope]], which makes them useful for values that many parts of code need to know about.

## Example

```rust
const THREE_HOURS_IN_SECONDS: u32 = 60 * 60 * 3;
```

> [!NOTE]
> Rust’s naming [[convention]] for constants is to use all uppercase with underscores between words.

Constants are valid for the entire time a program runs, within the [[scope]] in which they were declared.