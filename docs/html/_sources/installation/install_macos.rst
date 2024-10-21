MacOS Installation
==================

For other operating systems such as Linux and Windows the process should be very similar.

ESP32's idf.py
==============

MacOS Environment (tested on MacBook Air M1 2020 with Sonoma v14.5)

You can install this through the terminal or Visual Studio Code, both ways are shown below. I recommend using the terminal way.

1. Install esp-idf follow and run: `esp-idf MacOS Setup <https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/linux-macos-setup.html>`__

    1. ``brew install cmake ninja dfu-util``
    2. ``git clone --recursive https://github.com/espressif/esp-idf.git``
    3. ``cd esp-idf``
    4. ``./install.sh esp32``
    5. ``echo "alias get_idf=\". $(pwd)/export.sh\"" >> ~/.zshrc``
    6. ``source ~/.zshrc``

Run this every time in a project to get idf.py: `get_idf`

2. Install more packages

    ``brew install gcc make pkg-config arm-none-eabi-gcc openocd bear screen qemu``

    NOTE: `gdb` cant be installed so `lldb` must be used instead

    *Keep in mind*

    GNU "make" has been installed as "gmake". If you need to use it as "make", you can add a "gnubin" directory to your PATH from your zshrc like:

    ``export PATH="/opt/homebrew/opt/make/libexec/gnubin:$PATH"``

Sphinx
======

Sphinx is used to generate HTML for the docs you are currently viewing, this is not doxygen, but rather rst to html.
You don't need to install this unless you want to work on documentation.

1. **Install Sphinx**

    .. code-block:: bash

        pip install sphinx sphinx-book-theme
