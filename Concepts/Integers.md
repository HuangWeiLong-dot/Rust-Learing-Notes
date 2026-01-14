---
tags:
  - concept
  - rust
  - integer
Created: 2026-01-14
Date: "[[2026-01-14]]"
categories: "[[Scalar]]"
---

| Length                 | Signed  | Unsigned |
| ---------------------- | ------- | -------- |
| 8-bit                  | `i8`    | `u8`     |
| 16-bit                 | `i16`   | `u16`    |
| 32-bit                 | `i32`   | `u32`    |
| 64-bit                 | `i64`   | `u64`    |
| 128-bit                | `i128`  | `u128`   |
| Architecture-dependent | `isize` | `usize`  |
_[[Signed]]_ and _[[Unsigned]]_ refer to whether it’s possible for the number to be 

When the sign matters, a number is shown with a plus sign or a minus sign; however, when it’s safe to assume the number is positive, it’s shown with no sign. Signed numbers are stored using [two’s complement](https://en.wikipedia.org/wiki/Two%27s_complement) representation.

![[Signed]]

---
![[Unsigned]]

> [!important]
> Additionally, the [[isize]]and [[usize]] types depend on the architecture of the computer your program is running on: 64 bits if you’re on a 64-bit architecture and 32 bits if you’re on a 32-bit architecture.

![[Integer Literals]]

Rust’s defaults are generally good places to start: Integer types default to `i32`.

The primary situation in which you’d use [[isize]] or [[usize]] is when indexing some sort of collection.

![[Integer Overflow]]