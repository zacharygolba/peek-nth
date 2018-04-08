# peek-nth

[![CircleCI branch](https://img.shields.io/circleci/project/github/zacharygolba/peek-nth/master.svg?style=flat-square)](https://circleci.com/gh/zacharygolba/peek-nth/tree/master) [![AppVeyor branch](https://img.shields.io/appveyor/ci/zacharygolba/peek-nth/master.svg?logo=appveyor&style=flat-square)](https://ci.appveyor.com/project/zacharygolba/peek-nth/branch/master) [![Crates.io](https://img.shields.io/crates/v/peek-nth.svg?style=flat-square)](https://crates.io/crates/peek-nth)

An iterator adapter that allows you to efficiently peek the nth item of an iterator.

Itermediate values are memoized and heap allocations are avoided when possible.

## Installation

First, add `peek-nth` to the dependencies section of your `Cargo.toml`:

```toml
[dependencies]
peek-nth = "0.1"
```

Next, add the following snippet to the entry point of your crate (`lib.rs` or `main.rs`):

```rust
extern crate peek_nth;
```

## Usage

```rust
extern crate peek_nth;

use peek_nth::IteratorExt;

fn main() {
    let mut iter = "Hello, world!".chars().peekable_nth();

    assert_eq!(iter.peek_nth(4), Some(&'o')); // Cache Miss
    assert_eq!(iter.peek_nth(3), Some(&'l')); // Cache Hit
    assert_eq!(iter.peek_nth(2), Some(&'l')); // Cache Hit
    assert_eq!(iter.peek_nth(1), Some(&'e')); // Cache Hit
    assert_eq!(iter.peek_nth(0), Some(&'H')); // Cache Hit
    assert_eq!(iter.peek_nth(7), Some(&'w')); // Cache Miss

    assert_eq!(iter.collect::<String>(), "Hello, world!");
}
```

## License

Licensed under either of

* Apache License, Version 2.0
  ([LICENSE-APACHE](LICENSE-APACHE) or http://www.apache.org/licenses/LICENSE-2.0)
* MIT license
  ([LICENSE-MIT](LICENSE-MIT) or http://opensource.org/licenses/MIT)

at your option.

## Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in the work by you, as defined in the Apache-2.0 license, shall be
dual licensed as above, without any additional terms or conditions.
