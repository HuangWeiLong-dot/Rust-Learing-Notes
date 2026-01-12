---
tags:
  - function
  - first
  - rust
  - project
Created: 2026-01-11
categories: "[[Rust]]"
---

# Hello World

```rust
fn main() {
    println!("Hello, world!");
}
```


> [!info] A program that prints `Hello, world!`
>

```terminal
> rustc main.rs 
> .\main 
Hello, world!
```

`println!` calls a [[Rust macro]]
If it had called a function instead, it would be entered as `println` (without the `!`)