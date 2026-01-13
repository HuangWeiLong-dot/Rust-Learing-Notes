---
tags:
  - cargo
  - concept
  - rust
Created: 2026-01-11
Date: "[[2026-01-11]]"
categories: "[[Concepts]]"
---

Cargo is [[Rust]]’s build system and package manager

# Check Cargo

```terminal
$ cargo --version
```

# Creating a Project with Cargo

```terminal
$ cargo new hello_cargo
$ cd hello_cargo
```


> [!info] `Cargo.toml`
> This file is in the [_TOML_](https://toml.io/) (_Tom’s Obvious, Minimal Language_) format, which is Cargo’s configuration format.

# Building and Running a Cargo Project

```terminal
$ cargo build
.\target\debug\hello_cargo.exe
```
or
```
$ cargo run
```

## Cargo Check

```
$ cargo check
```


> [!info] 
> This command quickly checks your code to make sure it compiles but doesn’t produce an executable

# Summation

- We can create a project using `cargo new`.
- We can build a project using `cargo build`.
- We can build and run a project in one step using `cargo run`.
- We can build a project without producing a binary to check for errors using `cargo check`.
- Instead of saving the result of the build in the same directory as our code, Cargo stores it in the _target/debug_ directory.