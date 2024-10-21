MacOS Installation
==================

The installation process for other operating systems like Linux and Windows is similar to the steps provided for macOS below.

ESP32's ``idf.py``
------------------

MacOS Environment
~~~~~~~~~~~~~~~~~
Tested on MacBook Air M1 2020 with macOS Sonoma v14.5.

You can install the ESP32 development environment using the terminal or Visual Studio Code. The terminal installation method is recommended and detailed below.

1. Install ESP-IDF
~~~~~~~~~~~~~~~~~~

To set up the ESP-IDF environment on macOS, follow these steps:

For detailed instructions, see the official documentation: `ESP-IDF MacOS Setup <https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/linux-macos-setup.html>`__.

   a. Install required packages:
   
      .. code-block:: bash

         brew install cmake ninja dfu-util

   b. Clone the ESP-IDF repository:
   
      .. code-block:: bash

         git clone --recursive https://github.com/espressif/esp-idf.git

   c. Navigate to the ESP-IDF directory:
   
      .. code-block:: bash

         cd esp-idf

   d. Run the installation script for ESP32:
   
      .. code-block:: bash

         ./install.sh esp32

   e. Add an alias to your ``.zshrc`` file for easy access to ``idf.py``:
   
      .. code-block:: bash

         echo "alias get_idf='. $(pwd)/export.sh'" >> ~/.zshrc

   f. Source the updated profile:
   
      .. code-block:: bash

         source ~/.zshrc

**Note:**  
After the setup, run the following command in each project to activate ``idf.py``:
   
   .. code-block:: bash

      get_idf

2. Install Additional Packages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You may also need the following packages to work with ESP-IDF:
   
   .. code-block:: bash

      brew install gcc make pkg-config arm-none-eabi-gcc openocd bear screen qemu

**Important:**  
``gdb`` cannot be installed on macOS, so you'll need to use ``lldb`` as an alternative.

- **GNU Make Utility:**  
  GNU ``make`` is installed as ``gmake``. If you need to use it as ``make``, add the following line to your ``.zshrc`` to update your PATH:
   
   .. code-block:: bash

      export PATH="/opt/homebrew/opt/make/libexec/gnubin:$PATH"

Sphinx
------

Sphinx is used to generate HTML documentation (not Doxygen). You don't need to install Sphinx unless you're contributing to the documentation.

1. Install Sphinx
~~~~~~~~~~~~~~~~~

To install Sphinx and the required theme:

   .. code-block:: bash

      pip install sphinx sphinx-book-theme

