# Installation

There are multiple ways to install dialect.
Choose any one of the methods below that best suit your needs.

## Pre-compiled binaries

Executable binaries are available for download on the [GitHub Releases page][releases].
Download the binary for your platform (macOS, or Linux) and extract the archive.
The archive contains an executable which you can run to build your books.

To make it easier to run, put the path to the binary into your `PATH`.

[releases]: https://github.com/dialect-rs/

## Build from source using Rust
Once you have installed Rust, you need to download the source code of the latest release of `DIALECT` from the [GitHub Releases page][releases]. After extracting the source code, change into the new directory
```bash
cd DIALECT-rs
```
and build the executable with the package manager Cargo
```bash
cargo build --release
```
The option `--release` enables all optimization during the build and ensures fast runtimes, but can
result in very long compile times. If you want to compile often e.g. in the case of debugging, then 
it makes sense to just execute
```bash
cargo build
``` 
To be able to execute the `DIALECT` programm you should set `DIALECT_SRC_DIR` to the installation directory and you 
can add the binary path to your `PATH` environment variable.
