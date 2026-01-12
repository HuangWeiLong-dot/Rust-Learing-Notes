---
tags:
  - project
  - rust
Created: 2026-01-11
---
# First Part

```rust
use std::io;

fn main() {
    println!("Guess the number!");

    println!("Please input your guess.");

    let mut guess = String::new();

    io::stdin()
        .read_line(&mut guess)
        .expect("Failed to read line");

    println!("You guessed: {guess}");
}
```


> [!info] 
> Code that gets a guess from the user and prints it

---

## Bring The IO

```rust
use std::io;
```


> [!info] 
> bring the `io` [[input/output library]] into [[scope]]. The `io` library comes from the standard library, known as `std`

---
## Initialize The Variables

```rust
let apples = 5; // immutable
let mut bananas = 5; // mutable
```


> [!info] 
> In Rust, variables are immutable by default, meaning once we give the variable a value, the value won’t change
> See [[Variables and Mutability]]

`let mut guess` will introduce a [[mutable variable]] named `guess`.

On the right of the equal sign is the value that `guess` is bound to, which is the result of calling `String::new`, a function that returns a new instance of a [[String]].

The `::` syntax in the `::new` line indicates that `new` is an associated function of the `String` type.

---

## Receiving User Input

```rust
    io::stdin()
        .read_line(&mut guess)
```

the line `.read_line(&mut guess)` calls the [`read_line`](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.read_line) method on the standard input handle to get input from the user.

The `&` indicates that this argument is a _[[reference]]_, which gives you a way to let multiple parts of your code access one piece of data without needing to copy that data into memory multiple times.

references are [[immutable]] by default.

---

## Handling Errors (Failure)

```rust
        .expect("Failed to read line");
```

`read_line` puts whatever the user enters into the string we pass to it, but it also returns a [[Result]] value.

[`Result`](https://doc.rust-lang.org/std/result/enum.Result.html) is an [_enumeration_](https://doc.rust-lang.org/book/ch06-00-enums.html), often called an _[[enum]]_, which is a type that can be in one of multiple possible states.

`Result`’s variants are `Ok` and `Err`. The `Ok` variant indicates the operation was successful, and it contains the successfully generated value. The `Err` variant means the operation failed, and it contains information about how or why the operation failed.

---

```rust
    println!("You guessed: {guess}");
```


> [!info] 
> The `{}` set of curly brackets is a placeholder

---

## Generating A Random Number

## Implement With A [[Crate]]

a crate is a collection of Rust source code files

---

Filename: Cargo.toml

```rust
[dependencies]
rand = "0.8.5"
```

```rust
use rand::Rng;
    let secret_number= rand::thread_rng().gen_range(1..=100);
```

`rand::thread_rng` function that gives us the particular random number generator we’re going to use: one that is local to the current thread of execution and is seeded by the operating system.

## Comparing

```rust
use std::cmp::Ordering;

match guess.cmp(&secret_number) { 
	Ordering::Less => println!("Too small!"), 
	Ordering::Greater => println!("Too big!"), 
	Ordering::Equal => println!("You win!"), 
	}
```

The `Ordering` type is another [[enum]] and has the variants `Less`, `Greater`, and `Equal`.

We use a [`match`](https://doc.rust-lang.org/book/ch06-02-match.html) expression to decide what to do next based on which variant of `Ordering` was returned from the call to `cmp` with the values in `guess` and `secret_number`.


> [!warning]
A few of Rust’s number types can have a value between 1 and 100: `i32`, a 32-bit number; `u32`, an unsigned 32-bit number; `i64`, a 64-bit number; as well as others. Unless otherwise specified, Rust defaults to an `i32`, which is the type of `secret_number`

The reason for the error is that Rust cannot compare a string and a number type.

```rust
let guess: u32 = guess.trim().parse().expect("Please type a number!");
```

> [!tip]
> Rust allows us to shadow the previous value of `guess` with a new one.
> _[[Shadowing]]_ lets us reuse the `guess` variable name rather than forcing us to create two unique variables

We bind this new variable to the expression `guess.trim().parse()`.
The `trim` method on a `String` instance will eliminate any whitespace at the beginning and end.
The [`parse` method on strings](https://doc.rust-lang.org/std/primitive.str.html#method.parse) converts a string to another type.

## Allowing Multiple Input

```rust
    // --snip--

    println!("The secret number is: {secret_number}");

    loop {
        println!("Please input your guess.");

        // --snip--

        match guess.cmp(&secret_number) {
            Ordering::Less => println!("Too small!"),
            Ordering::Greater => println!("Too big!"),
            Ordering::Equal => println!("You win!"),
        }
    }
}
```

## Quit After Win

```rust
        // --snip--

        match guess.cmp(&secret_number) {
            Ordering::Less => println!("Too small!"),
            Ordering::Greater => println!("Too big!"),
            Ordering::Equal => {
                println!("You win!");
                break;
            }
        }
    }
}
```

## Handling Invalid Input

```rust
        // --snip--

        io::stdin()
            .read_line(&mut guess)
            .expect("Failed to read line");

        let guess: u32 = match guess.trim().parse() {
            Ok(num) => num,
            Err(_) => continue,
        };

        println!("You guessed: {guess}");

        // --snip--
```


> [!important] 
> We switch from an `expect` call to a `match` expression to move from crashing on an error to handling the error. Remember that `parse` returns a `Result` type and `Result` is an enum that has the variants `Ok` and `Err`. We’re using a `match` expression here, as we did with the `Ordering` result of the `cmp` method.

If `parse` is able to successfully turn the string into a number, it will return an `Ok` value that contains the resultant number. That `Ok` value will match the first arm’s pattern, and the `match` expression will just return the `num` value that `parse` produced and put inside the `Ok` value. That number will end up right where we want it in the new `guess` variable we’re creating.

If `parse` is _not_ able to turn the string into a number, it will return an `Err` value that contains more information about the error. The `Err` value does not match the `Ok(num)` pattern in the first `match` arm, but it does match the `Err(_)` pattern in the second arm. The underscore, `_`, is a catch-all value; in this example, we’re saying we want to match all `Err` values, no matter what information they have inside them. So, the program will execute the second arm’s code, `continue`, which tells the program to go to the next iteration of the `loop` and ask for another guess. So, effectively, the program ignores all errors that `parse` might encounter!
