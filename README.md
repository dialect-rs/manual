# User Guide for dialect

[![LICENSE](https://img.shields.io/github/license/dialect-rs/manual.svg)](LICENSE)

This repository contains the manual/user guide for the dialect software package. 

Check out the **[User Guide]** for a list of features and installation and usage information.

## Contributing 

If you are interested in contributing to the manual you can build it yourself using [mdBook].

### Requirements

Building the manual requires [mdBook]. To get it:

[mdBook]: https://github.com/rust-lang-nursery/mdBook

```bash
cargo install mdbook
```

### Building

To build the manual, type:

```bash
mdbook build
```

The output will be in the `book` subdirectory. To check it out, open `book/index.html` 
in your web browser. Or use 

```bash
mdbook serve --open
```
to preview the manual by serving it via HTTP at `localhost:3000`. 


## License

All the code in this repository is released under the MIT license for more information take a look at the [LICENSE] file.

[User Guide]: https://dialect-rs.github.io/manual/
[LICENSE]: https://github.com/dialect-rs/manual/blob/main/LICENSE


