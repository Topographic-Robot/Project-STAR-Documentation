Project Structure
=================

In this project, each module should reside in its own directory, containing source files and a separate `include/` folder for header files. The build system will be managed using **CMake** with `CMakeLists.txt` files for defining how each module is built. This structure makes the project modular, scalable, and easy to maintain.

General Guidelines for Project Structure
----------------------------------------

- **Module-Based Structure**: Each module should have its own directory with source files and a dedicated `include/` folder for header files.

- **CMake for Build Management**: The project should use **CMake** for the build process, with each module having its own `CMakeLists.txt` file to manage its build instructions.

- **Consistent Naming Conventions**: Use consistent naming conventions across the project for directories, files, and functions.

Recommended Directory Structure
-------------------------------

The following is an example of a modular project structure:

.. code-block::

    project_root/
    ├── module1/
    │   ├── include/          # Header files for module1
    │   │   └── module1.h
    │   ├── module1.c         # Source file for module1
    │   └── CMakeLists.txt    # CMake file for module1
    ├── module2/
    │   ├── include/          # Header files for module2
    │   │   └── module2.h
    │   ├── module2.c         # Source file for module2
    │   └── CMakeLists.txt    # CMake file for module2
    ├── common/               # Shared headers or utility files
    │   ├── include/
    │   │   └── common.h
    │   ├── common.c
    │   └── CMakeLists.txt
    ├── main/
    │   ├── main.c            # Main entry point of the application
    │   └── CMakeLists.txt    # CMake file for main module
    ├── build/                # Generated build files (excluded from version control)
    ├── CMakeLists.txt        # Top-level CMake file for the entire project
    └── tests/                # Unit tests for the project

Directory Breakdown
-------------------

- **Module Directories**: Each module has its own directory, with an `include/` folder for header files and the source files directly in the module directory. This structure keeps the code modular and allows each module to be built independently.
  
  Example:
  
  .. code-block:: c

    /* module1/include/module1.h */
    #ifndef MODULE1_H
    #define MODULE1_H

    void module1_function(void);

    #endif /* MODULE1_H */

    /* module1/module1.c */
    #include "module1.h"

    void module1_function(void)
    {
      /* Implementation */
    }

- **Common Directory**: Shared utilities, functions, or constants that are used across multiple modules can reside in a `common/` directory. This directory should follow the same structure with an `include/` folder for header files and source files directly in the directory.

- **Main Directory**: This directory contains the entry point of the program (e.g., `main.c`), and it may depend on one or more modules.

- **Tests Directory**: This directory holds unit tests for different modules. Tests should be organized based on the modules they are testing.

CMake Build System
------------------

The project uses **CMake** for managing the build process. Each module should have its own `CMakeLists.txt` file that specifies how that module should be built. The top-level `CMakeLists.txt` file in the project root will include all modules and manage the overall build process.

Top-Level `CMakeLists.txt` Example
----------------------------------

.. code-block:: cmake

    cmake_minimum_required(VERSION 3.16)
    project(MyProject)

    # Add each module
    add_subdirectory(module1)
    add_subdirectory(module2)
    add_subdirectory(common)
    add_subdirectory(main)

Module-Level `CMakeLists.txt` Example
-------------------------------------

Each module will have its own `CMakeLists.txt` file that defines the source files and include directories for that module.

.. code-block:: cmake

    # module1/CMakeLists.txt
    set(SOURCES module1.c)
    set(HEADERS include/module1.h)

    add_library(module1 ${SOURCES} ${HEADERS})

    target_include_directories(module1 PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)

Main Module `CMakeLists.txt` Example
------------------------------------

The `main/` module should include the other modules it depends on.

.. code-block:: cmake

    # main/CMakeLists.txt
    set(SOURCES main.c)

    add_executable(MyProgram ${SOURCES})

    target_link_libraries(MyProgram PRIVATE module1 module2)

Naming Conventions
------------------

- **Source and Header Files**: Use `snake_case` for all source (`.c`) and header (`.h`) file names to keep consistent with the project’s naming conventions.

- **Directory Names**: Use `snake_case` for directories and make sure that directory names describe the purpose of the module.

- **Test Files**: Prefix test files with `test_` to indicate their purpose.

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

Documentation
-------------

Ensure that the `docs/` directory contains up-to-date documentation for the project, including:

- **Doxygen Documentation**: Automatically generated API documentation from the codebase.

- **Markdown Files**: General project overviews, setup guides, or developer documentation.

General Guidelines
------------------

- **Modular Structure**: Keep each module self-contained, with source files in the module directory and header files in `include/`.

- **Consistent Naming**: Follow naming conventions for files and directories to maintain a consistent structure.

- **CMake for Build Management**: Use **CMake** for build management, with each module having its own `CMakeLists.txt` file.

- **Version Control**: Use a `.gitignore` file to exclude unnecessary files from version control.

