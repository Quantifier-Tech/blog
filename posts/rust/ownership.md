<!--
@name: Ownership
@title: Rust Ownership
@description:
  Explain the ownership model in Rust
@tags:
 - rust
 - ownership
 - concurrency
-->

# Ownership in Rust

According to [the book](https://doc.rust-lang.org/stable/book/ch04-01-what-is-ownership.html)

> *Ownership* is a set of rules that governs how a Rust program manages memory.

All programs, in any language, need a way to manage their use of the computer's memory. Some languages (e.g. Java, Scala, OCaml) use a garbage collector which is just a program running in tandem that regularly scans for memory which is no longer in use by your program. In other languages, memory most be explicitly managed (e.g. C). Rust takes a third approach, managing the memory through a set of rules which the compiler checks. This is nice because it exists in the space between garbage collection and manual memory management, giving us the performance we expect from manual memory management without having to `alloc` or `free` anything!

How can this be? All pros? Not quite! As with everything though, it has its cons. It is common for beginners to struggle to understand Rust's concept of *ownership*. Here, we attempt to demystify *ownership*!

## Stack and Heap

TODO

## Ownership Rules

Without further ado, the ownership rules:

- Each value in Rust has an *owner*
- There can be at most *one* owner at a time
- When the owner goes out of scope, the value is dropped

Simple enough, right!? While the rules may be simple, their consequences are quite profound!

At this point, you would be justified in wondering about variable scopes.

## Variable Scopes

An example

```rust
{
                     // s is not in scope yet because it hasn't been declared yet
    let s = "hello"; // s is valid, i.e. in scope, from this point on

    // s is in scope here so we can use it in computations

}                    // s is no longer in scope
```

Here, `s` is a *string literal*, denoted by `str`. String literals are a simple, immutable, stack-allocated type.

## The `String` type

`String` is a rather complicated type because it has a variable size. As a consequence, `String`s cannot be stored on the stack and are thus, stored on the heap.

- mutable (`push_str`)

## Memory and Allocation

String literals are hardcoded into the final executable because they are immutable and have a known size at compile time. On the other hand, `String` values can't be hardcoded into the executable since they are mutable and their size is not known at compile time. As a result

1. the memory must be requested from the *memory allocator* at runtime, and
2. we need a way to return this memory to the allocator once we're done with it

The programmer does 1. and the compiler handles 2. via the ownership rules.
