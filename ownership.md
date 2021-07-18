# Ownership

One of the biggest things to get one's head around in Rust is the memory model.
I'll probably get some terminology wrong in this note, but here we go.

Memory is owned by a single variable. When that variable goes out of scope, the
memory is dropped. Ownership can be moved from one variable to another. This is
the default except for primitive types that are copied.

Variables can "refer" to memory owned by someone else subject to the rule that
there can be either exactly ONE mutable reference OR any number of immutable
references. Also, references must always be valid.

Some questions in my head:

1. Consider a method that mutates `self`. There are (at least) two ways of
   accomplishing this:

```rust
impl T {
    fn f(&mut self) {}
}

impl T {
    fn f(self) -> Self {}
}
```

The first seems more memory efficient, although the second explicitly moves
memory in and out rather than creating unnecessary copies.

The second approach permits chaining.

2. If I have a struct with a field that is a reference to some other memory, it
   would seem that creates a shared reference that lives for as long as the
   struct lives. This seems like a bit of a 'hidden' reference. What is the best
   approach for linking struct instances? A shared reference? `Box`? `Cell`? ...
