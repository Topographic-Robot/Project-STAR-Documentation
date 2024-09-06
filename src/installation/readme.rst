Installation
============

There are many things that need to be installed in order to start
developing. There might be a release on GitHub, but likely not. To run
this yourself you must go through the install process.

If you are going to do development for the documentation of this
project, this is for you. Otherwise, continue to the next pages.

mdBook setup
------------

Linux
~~~~~

1. Install Rust

   1. ``curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh``

2. Install gcc

   1. ``apt-get install gcc``

3. Install mdBook

   1. ``cargo install mdbook``

MacOS
~~~~~

1. Install Rust

   1. ``curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh``

2. Install gcc

   1. ``brew install gcc``

3. Install mdBook

   1. ``cargo install mdbook``

Windows
~~~~~~~

To install Rust for windows follow the following link provided
https://www.rust-lang.org/tools/install Download the 64 bit .exe and run
the file. Your command prompt should open once the file is ran.

1. “Rust requires a linker and Windows API libraries but they don’t seem
   to be available.” The following prompt should appear; select the 1st
   option by typing the number 1. This should be the free version.
   Selecting this will prompt Windows to install Visual Studio.

2. When prompted, click continue and install both packages displayed.

3. Once completed, the command prompt should update. Reboot your
   computer to continue.

4. Once your computer has rebooted, reopen your command prompt by
   reopening the rustup-init file previously downloaded. Three options
   should appear:

   -  Proceed with standard installation (default - just press enter)
   -  Customize installation
   -  Cancel installation

Select the 1st option.

5. Once install close the command prompt and reopen.This would reload
   its PATH environment variable to include Cargo’s bin directory
   (``%USERPROFILE%\.cargo\bin``).

6. Next reopen the command prompt and rust should be properly installed.

7. Install mdBook

   1. ``cargo install mdbook``

mdBook documentation
~~~~~~~~~~~~~~~~~~~~

All of the official documentation for mdBook can be found on the
`official mdBook docs <https://rust-lang.github.io/mdBook/>`__. However
some good commands are:

-  ``mdbook build`` — Renders the book.
-  ``mdbook watch`` — Rebuilds the book any time a source file changes.
-  ``mdbook serve`` — Runs a web server to view the book, and rebuilds
   on changes.
-  ``mdbook test`` — Tests Rust code samples.
-  ``mdbook clean`` — Deletes the rendered output.
-  ``mdbook completions`` — Support for shell auto-completion.
