Compiling, Linking, Flashing
=============================

ESP32's ``idf.py``
------------------

1. **Set up the ESP32 environment**

   First, make sure the ESP32 environment is set up by running the following command (after installation):

   .. code-block:: bash

       get_idf

2. **Build the project**

   To compile your ESP32 project, run:

   .. code-block:: bash

       idf.py build

3. **Flash the project**

   Once the project is built, you can flash it to the ESP32 by running:

   .. code-block:: bash

       idf.py flash

4. **Monitor the serial output**

   To monitor the serial output from the ESP32 after flashing, use the following command:

   .. code-block:: bash

       idf.py monitor

5. **Clean the build directory**

   If you need to clean up the build directory before building again, use:

   .. code-block:: bash

       idf.py clean

6. **Full clean of the build directory**

   If you want to completely remove the entire build directory (for a more thorough clean), run:

   .. code-block:: bash

       idf.py fullclean

7. **Check ROM usage (flash memory)**

   After building your project, you can check how much of the ESP32's flash memory is used by running:

   .. code-block:: bash

       idf.py size

Sphinx
------

`Sphinx GitHub <https://github.com/sphinx-doc/sphinx>`_

1. **Build the Documentation**

   To build the documentation using Sphinx, run:

   .. code-block:: bash

       make html

2. **View Locally**

   You can view the generated documentation locally by running a simple HTTP server:

   .. code-block:: bash

       python -m http.server 8080 --directory docs/html

