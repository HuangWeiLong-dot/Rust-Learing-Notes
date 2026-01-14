---
tags:
  - concept
  - rust
  - variablesandmutability
Created: 2026-01-13
Date: "[[2026-01-13]]"
categories: "[[Concepts]]"
---
```rust
fn main() {
    let x = 5;
    println!("The value of x is: {x}");
    x = 6;
    println!("The value of x is: {x}");
}
```

save and run

> [!warning]
> $ cargo run
>    Compiling variables v0.1.0 (file:///projects/variables)
> error[E0384]: cannot assign twice to immutable variable `x`
>  --> src/main.rs:4:5
>   |
> 2 |     let x = 5;
>   |         - first assignment to `x`
> 3 |     println!("The value of x is: {x}");
> 4 |     x = 6;
>   |     ^^^^^ cannot assign twice to immutable variable
>   |
> help: consider making this binding mutable
>   |
> 2 |     let mut x = 5;
>   |         +++
> 
> For more information about this error, try `rustc --explain E0384`.
> error: could not compile `variables` (bin "variables") due to 1 previous error


> [!NOTE] This example shows how the compiler helps you find errors in your programs.

![[Declaring Constants]]

![[Shadowing]]