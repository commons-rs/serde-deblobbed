> [!IMPORTANT]
> Changes that are equivalent to the patch applied in this fork have been
> accepted for serde, and have been released as serde / serde_derive v1.0.185.
> Since this eliminates the need for a fork, this project will be archived and
> will not receive any further changes.

---

# Serde &emsp; [![Build Status]][actions] [![Latest Version]][crates.io] [![serde: rustc 1.31+]][Rust 1.31] [![serde_derive: rustc 1.56+]][Rust 1.56]

[Build Status]: https://img.shields.io/github/actions/workflow/status/serde-rs/serde/ci.yml?branch=master
[actions]: https://github.com/serde-rs/serde/actions?query=branch%3Amaster
[Latest Version]: https://img.shields.io/crates/v/serde.svg
[crates.io]: https://crates.io/crates/serde
[serde: rustc 1.31+]: https://img.shields.io/badge/serde-rustc_1.31+-lightgray.svg
[serde_derive: rustc 1.56+]: https://img.shields.io/badge/serde_derive-rustc_1.56+-lightgray.svg
[Rust 1.31]: https://blog.rust-lang.org/2018/12/06/Rust-1.31-and-rust-2018.html
[Rust 1.56]: https://blog.rust-lang.org/2021/10/21/Rust-1.56.0.html

**Serde is a framework for *ser*ializing and *de*serializing Rust data structures efficiently and generically.**

> [!IMPORTANT]
> This is a fork of [serde-rs/serde](https://github.com/serde-rs/serde) which
> addresses [serde#2538](https://github.com/serde-rs/serde/issues/2538) by
> reverting the addition of the pre-compiled binary blob. It should function as
> a drop-in replacement for serde / serde_derive `>= 1.0.172`.

The changes are based on [two][patch0] [patches][patch1] that have been applied
to the Fedora Linux packages for all versions of serde_derive `>= 1.0.172`.

[patch0]: https://src.fedoraproject.org/rpms/rust-serde_derive/blob/rawhide/f/serde_derive-fix-metadata.diff
[patch1]: https://src.fedoraproject.org/rpms/rust-serde_derive/blob/rawhide/f/0001-Drop-usage-of-precompiled-binary-that-s-not-usable-f.patch

Note that some crates have already pinned serde / serde_derive to `<= 1.0.171`,
in which case using this git repository as an [override] will not work (due to
the higher version numbers).

[override]: https://doc.rust-lang.org/cargo/reference/overriding-dependencies.html#the-patch-section

I will attempt to merge new releases of serde / serde_derive here in a timely
fashion. If there's enough interest in this fork, I will publish the deblobbed
code on crates.io under a different name.

---

You may be looking for:

- [An overview of Serde](https://serde.rs/)
- [Data formats supported by Serde](https://serde.rs/#data-formats)
- [Setting up `#[derive(Serialize, Deserialize)]`](https://serde.rs/derive.html)
- [Examples](https://serde.rs/examples.html)
- [API documentation](https://docs.rs/serde)
- [Release notes](https://github.com/serde-rs/serde/releases)

## Serde in action

<details>
<summary>
Click to show Cargo.toml.
<a href="https://play.rust-lang.org/?edition=2018&gist=72755f28f99afc95e01d63174b28c1f5" target="_blank">Run this code in the playground.</a>
</summary>

```toml
[dependencies]

# The core APIs, including the Serialize and Deserialize traits. Always
# required when using Serde. The "derive" feature is only required when
# using #[derive(Serialize, Deserialize)] to make Serde work with structs
# and enums defined in your crate.
serde = { version = "1.0", features = ["derive"] }

# Each data format lives in its own crate; the sample code below uses JSON
# but you may be using a different one.
serde_json = "1.0"
```

</details>
<p></p>

```rust
use serde::{Deserialize, Serialize};

#[derive(Serialize, Deserialize, Debug)]
struct Point {
    x: i32,
    y: i32,
}

fn main() {
    let point = Point { x: 1, y: 2 };

    // Convert the Point to a JSON string.
    let serialized = serde_json::to_string(&point).unwrap();

    // Prints serialized = {"x":1,"y":2}
    println!("serialized = {}", serialized);

    // Convert the JSON string back to a Point.
    let deserialized: Point = serde_json::from_str(&serialized).unwrap();

    // Prints deserialized = Point { x: 1, y: 2 }
    println!("deserialized = {:?}", deserialized);
}
```

## Getting help

Serde is one of the most widely used Rust libraries so any place that Rustaceans
congregate will be able to help you out. For chat, consider trying the
[#rust-questions] or [#rust-beginners] channels of the unofficial community
Discord (invite: <https://discord.gg/rust-lang-community>), the [#rust-usage] or
[#beginners] channels of the official Rust Project Discord (invite:
<https://discord.gg/rust-lang>), or the [#general][zulip] stream in Zulip. For
asynchronous, consider the [\[rust\] tag on StackOverflow][stackoverflow], the
[/r/rust] subreddit which has a pinned weekly easy questions post, or the Rust
[Discourse forum][discourse]. It's acceptable to file a support issue in this
repo but they tend not to get as many eyes as any of the above and may get
closed without a response after some time.

[#rust-questions]: https://discord.com/channels/273534239310479360/274215136414400513
[#rust-beginners]: https://discord.com/channels/273534239310479360/273541522815713281
[#rust-usage]: https://discord.com/channels/442252698964721669/443150878111694848
[#beginners]: https://discord.com/channels/442252698964721669/448238009733742612
[zulip]: https://rust-lang.zulipchat.com/#narrow/stream/122651-general
[stackoverflow]: https://stackoverflow.com/questions/tagged/rust
[/r/rust]: https://www.reddit.com/r/rust
[discourse]: https://users.rust-lang.org

<br>

#### License

<sup>
Licensed under either of <a href="LICENSE-APACHE">Apache License, Version
2.0</a> or <a href="LICENSE-MIT">MIT license</a> at your option.
</sup>

<br>

<sub>
Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in Serde by you, as defined in the Apache-2.0 license, shall be
dual licensed as above, without any additional terms or conditions.
</sub>
