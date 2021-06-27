# Regular Expressions

Regular expressions are provided in the
[`regex` crate](https://github.com/rust-lang/regex).

- [Homepage](https://github.com/rust-lang/regex)
- [`docs.rs`](https://docs.rs/regex/1.5.4/regex/)
- [`crates.io`](https://crates.io/crates/regex)

## Advent of Code Use Cases

My current use of the regex crate has been in the context of Advent of Code
puzzles. For example, see:

- [Advent of Code 2015 Day 02](https://github.com/anthonycramp/aoc2015-rust/blob/main/day02/src/main.rs)
- [Advent of Code 2015 Day 09](https://github.com/anthonycramp/aoc2015-rust/blob/main/day09/src/main.rs)

Use in these cases follows a common pattern

```rust
use regex::Regex;

#[macro_use]
extern crate lazy_static;

fn parse(input: &str) -> T {
    lazy_static!{
        static ref RE: Regex = Regex::new(r"...").unwrap();
    }

    let fields = RE.captures(input).unwrap();

    let first_capture = fields.get(1).unwrap().as_str();
    let second_capture: i32 = fields.get(2).unwrap().as_str().parse().unwrap();
}
```

The `lazy_static` macro prevents the regular expression from being compiled on
each call to `parse`. Compiling the regular expression can be computationally
expensive and it will add up when I'm calling `parse` for each line of a many
line file.

I don't know what `#[macro_use]` does. Nor `extern crate ...`.
