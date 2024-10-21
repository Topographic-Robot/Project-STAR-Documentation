Project Structure
=================

In this project, each module should reside in its own directory, containing source files and a separate `include/` folder for header files. The build system will be managed using **CMake** with `CMakeLists.txt` files for defining how each module is built. This structure makes the project modular, scalable, and easy to maintain.

General Guidelines for Project Structure
----------------------------------------

- **Module-Based Structure**: Each module should have its own directory with source files and a dedicated `include/` folder for header files.

- **CMake for Build Management**: The project should use **ESP-IDF CMake** for the build process, with each module having its own `CMakeLists.txt` file to manage its build instructions.

- **Consistent Naming Conventions**: Use consistent naming conventions across the project for directories, files, and functions.

Recommended Directory Structure
-------------------------------

The following is an example of a modular ESP32 project structure:

.. code-block::

    project_root/
    ├── components/
    │   └── toporobo_hal/
    │       ├── bh1750/
    │       │   ├── include/          # Header files for bh1750 module
    │       │   │   └── bh1750.h
    │       │   ├── bh1750.c          # Source file for bh1750
    │       │   └── CMakeLists.txt    # CMake file for bh1750 module
    │       └── CMakeLists.txt        # CMake file for toporobo_hal module
    ├── main/
    │   ├── main.c                    # Main entry point of the application
    │   └── CMakeLists.txt            # CMake file for main module
    ├── CMakeLists.txt                # Top-level CMake file for the entire project
    └── sdkconfig                     # ESP-IDF SDK configuration file

CMake Build System (ESP-IDF)
----------------------------

The project uses **ESP-IDF CMake** for managing the build process. Each module should have its own `CMakeLists.txt` file that specifies how that module should be built. The top-level `CMakeLists.txt` file in the project root includes all modules and manages the overall build process.

Top-Level `CMakeLists.txt` Example
----------------------------------

In your project, the top-level `CMakeLists.txt` includes the ESP-IDF's project definitions.

.. code-block:: cmake

    cmake_minimum_required(VERSION 3.16)

    include($ENV{IDF_PATH}/tools/cmake/project.cmake)
    project(Topographic-Robot)

`toporobo_hal` Module `CMakeLists.txt`
--------------------------------------

The `toporobo_hal` module's `CMakeLists.txt` file registers the `bh1750` component within the `components/toporobo_hal/` directory. It includes the necessary source files and header directories for the build.

.. code-block:: cmake

    idf_component_register(SRCS "bh1750/bh1750.c"
                           INCLUDE_DIRS "bh1750/include")

`bh1750` Module `CMakeLists.txt`
--------------------------------

The `bh1750` module's `CMakeLists.txt` file directly registers the component using the `idf_component_register()` function.

.. code-block:: cmake

    idf_component_register(SRCS "bh1750.c"
                           INCLUDE_DIRS "include")

Main Module `CMakeLists.txt` Example
------------------------------------

The `main/` module should include the `toporobo_hal` module using the `REQUIRES` keyword to declare its dependency on it.

.. code-block:: cmake

    idf_component_register(SRCS "main.c"
                           INCLUDE_DIRS ""
                           REQUIRES toporobo_hal)

Naming Conventions
------------------

- **Source and Header Files**: Use `snake_case` for all source (`.c`) and header (`.h`) file names to keep consistent with the project’s naming conventions.

- **Directory Names**: Use `snake_case` for directories and make sure that directory names describe the purpose of the module.

Version Control
---------------

- **Use `.gitignore` (or equivalent)**: Ensure that unnecessary files like object files (`.o`), binaries, and the `build/` directory are excluded from version control.

  Example:

  .. code-block::

    # Ignore build files
    build/

    # Ignore object files
    *.o

    # Ignore binaries
    *.exe
    *.out

