# mdBook setup

If you are going to do development for the documentation of this project, this is for you. Otherwise, continue to the next pages.

## Installation of Rust
First Rust needs to be installed on your system:

```sh
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

## Installation of gcc
You will need to install gcc for mdBook. The provided command below is for apt systems and will need to be ran with sudo.

```sh
apt-get update
apt-get install gcc
```

## Installation of mdBook
Once you have installed Rust, the following command can be used to build and install mdBook, this does not need to be ran as root.

```sh
cargo install mdbook
```

## mdBook documentation

All of the offical documentation for mdBook can be found on the [official mdBook docs](https://rust-lang.github.io/mdBook/).
However some good commands are:

- `mdbook build` --- Renders the book.
- `mdbook watch` --- Rebuilds the book any time a source file changes.
- `mdbook serve` --- Runs a web server to view the book, and rebuilds on changes.
- `mdbook test` --- Tests Rust code samples.
- `mdbook clean` --- Deletes the rendered output.
- `mdbook completions` --- Support for shell auto-completion.
