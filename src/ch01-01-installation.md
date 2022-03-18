# Installation

There are multiple ways to install dialect.
Choose any one of the methods below that best suit your needs.

## Pre-compiled binaries

Executable binaries are available for download on the [GitHub Releases page][releases].
Download the binary for your platform (Windows, macOS, or Linux) and extract the archive.
The archive contains an executable which you can run to build your books.

To make it easier to run, put the path to the binary into your `PATH`.

[releases]: https://github.com/dialect-rs/

## Build from source using Rust

To build the `dialect` executable from source, you will first need to install Rust and Cargo.
Follow the instructions on the [Rust installation page].
dialect currently requires at least Rust version 1.59.

Once you have installed Rust, the following command can be used to build and install dialect:

```sh
cargo install dialect-rs
```

This will automatically download dialect from [crates.io], build it, and install it in Cargo's global binary directory (`~/.cargo/bin/` by default).

[Rust installation page]: https://www.rust-lang.org/tools/install
[crates.io]: https://crates.io/

### Installing the latest master version

The version published to crates.io will ever so slightly be behind the version hosted on GitHub.
If you need the latest version you can build the git version of dialect yourself.
Cargo makes this ***super easy***!

```sh
cargo install --git https://github.com/dialect-rs/dialect dialect-rs
```

Again, make sure to add the Cargo bin directory to your `PATH`.

If you are interested in making modifications to the software, check out the [Contributing Guide] for more information.

[Contributing Guide]: https://github.com/dialect-rs/
