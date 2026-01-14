---
tags:
  - concept
  - rust
  - shadow
Created: 2026-01-14
Date: "[[2026-01-14]]"
categories: "[[Variables and Mutability]]"
---
# In [Chapter 2](https://doc.rust-lang.org/book/ch02-00-guessing-game-tutorial.html#comparing-the-guess-to-the-secret-number)

you can declare a new variable with the same name as a previous variable.
In effect, the second variable overshadows the first, taking any uses of the variable name to itself until either it itself is shadowed or the [[scope]] ends. 
We can shadow a variable by using the same variable’s name and repeating the use of the [[let]] keyword as follows

```rust
fn main() {
    let x = 5;

    let x = x + 1;

    {
        let x = x * 2;
        println!("The value of x in the inner scope is: {x}");
    }

    println!("The value of x is: {x}");
}
```

> [!NOTE] Expected output
> The value of x in the inner scope is: 12  
> The value of x is: 6

Shadowing is different from marking a variable as `mut`.

Because using `mut` make the value keep the mutability.

By using [[let]], we can perform a few transformations on a value but have the variable be immutable after those transformations have completed.

The other difference between `mut` and shadowing is that because we’re effectively creating a new variable when we use the [[let]] keyword.

we can change the type of the value but reuse the same name.

```rust
    let spaces = "   ";
    let spaces = spaces.len();
```

but `mut`can not.

```rust
    let mut spaces = "   ";
    spaces = spaces.len();
```


> [!warning]
> $ cargo run
>    Compiling variables v0.1.0 (file:///projects/variables)
> error[E0308]: mismatched types
>  --> src/main.rs:3:14
>   |
> 2 |     let mut spaces = "   ";
>   |                      ----- expected due to this value
> 3 |     spaces = spaces.len();
>   |              ^^^^^^^^^^^^ expected `&str`, found `usize`
> 
> For more information about this error, try `rustc --explain E0308`.
> error: could not compile `variables` (bin "variables") due to 1 previous error
