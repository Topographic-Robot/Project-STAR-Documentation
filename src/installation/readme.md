# Installation

There are many things that need to be installed in order to start developing.
There might be a release on GitHub, but likely not. 
To run this yourself you must go through the install process.

The section below can most likely be skipped unless you plan on making changes to the documentation.

## mdBook setup

### Linux

If you are going to do development for the documentation of this project, this is for you. Otherwise, continue to the next pages.

#### Installation of Rust
First Rust needs to be installed on your system:

```sh
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

#### Installation of gcc
You will need to install gcc for mdBook. The provided command below is for apt systems and will need to be ran with sudo.

```sh
apt-get update
apt-get install gcc
```

#### Installation of mdBook
Once you have installed Rust, the following command can be used to build and install mdBook, this does not need to be ran as root.

```sh
cargo install mdbook
```

#### mdBook documentation

All of the official documentation for mdBook can be found on the [official mdBook docs](https://rust-lang.github.io/mdBook/).
However some good commands are:

- `mdbook build` --- Renders the book.
- `mdbook watch` --- Rebuilds the book any time a source file changes.
- `mdbook serve` --- Runs a web server to view the book, and rebuilds on changes.
- `mdbook test` --- Tests Rust code samples.
- `mdbook clean` --- Deletes the rendered output.
- `mdbook completions` --- Support for shell auto-completion.


### Windows

####  Installation of Visual Studio

#### Installation of Rust

#### Installation of mdBook

#### mdBook documentation


To install RUST for windows follow the following link provided
[https://www.rust-lang.org/tools/install](https://www.rust-lang.org/tools/install)
Download the 64 bit .exe and run the file.
Your command prompt should open once the file is ran.

1. "Rust requires a linker and Windows API libraries but they don't seem to be available."  The following prompt should appear; select the 1st option by typing the number 1. This should be the free version. Selecting this will prompt Windows to install Visual Studio.

2. When prompted, click continue and install both packages displayed.

3. Once completed, the command prompt should update. Reboot your computer to continue.

4. Once your computer has rebooted, reopen your command prompt by reopening the rustup-init file previously downloaded. Three options should appear:
    - Proceed with standard installation (default - just press enter)
    - Customize installation
    - Cancel installation

Select the 1st option.

5. Once install close the command prompt and reopen.This would reload its PATH environment variable to include Cargo's bin directory 
(`%USERPROFILE%\.cargo\bin`).

6. Next reopen the command prompt and rust should be properly installed.


