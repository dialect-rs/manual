# Installation

There are multiple ways to install __DIALECT__.
Choose any one of the methods below that best suit your needs.

## Pre-compiled binaries

An executable binary for linux x86 operating systems is available for download on the [GitHub Releases page][releases].
Download the binary for your platform and add the directory of the executable to your `PATH`.

[releases]: https://github.com/dialect-rs/DIALECT-rs/releases

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
