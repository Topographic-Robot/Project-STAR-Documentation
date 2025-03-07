Header Files
============

Header files play a crucial role in organizing and structuring a C project. They contain declarations of functions, constants, macros, and types that can be shared across multiple source files. This section provides guidelines for creating clear, maintainable, and reusable header files, along with the proper use of header guards.

General Guidelines for Header Files
-----------------------------------

- **Header Files Should Only Contain Declarations**: Header files should declare, but not define, functions, variables, and types. Function implementations, global variable definitions, and other logic should remain in the corresponding source files (`.c`).

  Example:

  .. code-block:: c

    /* header file: math_utils.h */
    #ifndef MATH_UTILS_H
    #define MATH_UTILS_H

    int add(int a, int b); /* Declaration only */

    #endif /* MATH_UTILS_H */

  The implementation will go in the source file:

  .. code-block:: c

    /* source file: math_utils.c */
    #include "math_utils.h"

    int add(int a, int b) {
      return a + b; }

- **Minimal Includes in Headers**: Header files should include only the headers that are strictly necessary for their declarations. Avoid excessive includes to reduce dependency chains and compilation time. Use forward declarations where possible.

  Example:

  .. code-block:: c

    /* Avoid including unnecessary headers */
    struct device_t; /* Forward declaration instead of including device.h */

    void init_device(struct device_t* device);

- **Self-Contained Headers**: Ensure that each header file is self-contained, meaning it can be included independently without relying on the inclusion of other headers beforehand. Always include the necessary headers for types and constants used within the file.

  Example:

  .. code-block:: c

    #ifndef MY_HEADER_H
    #define MY_HEADER_H

    #include <stdint.h> /* Ensure the necessary headers are included */

    typedef struct {
      uint32_t id;
      uint8_t  status;
    } device_t;

    #endif /* MY_HEADER_H */

- **Use `extern` for Global Variables**: If global variables need to be declared in a header file, they should be declared using `extern` to avoid multiple definition errors.

  Example:

  .. code-block:: c

    /* Declaration in header file: */
    extern int global_counter;

    /* Definition in source file: */
    int global_counter = 0;

- **Documentation in Headers**: Use Doxygen-style comments for documenting functions, constants, and types in header files. This allows the automatic generation of documentation and makes the code more understandable to other developers.

  Example:

  .. code-block:: c

    /**
     * @brief  Adds two integers.
     * @param  a First integer.
     * @param  b Second integer.
     * @return The sum of a and b.
     */
    int add(int a, int b);

- **Consistency in Naming Conventions**: Use consistent naming conventions for types, functions, and constants in headers. Follow the naming conventions specified in this project's guidelines (e.g., `snake_case` for variables, `PascalCase` for structs, and `_t` for typedefs).

  Example:

  .. code-block:: c

    typedef struct {
      int x;
      int y;
    } point_t;

Header Guards
-------------

Header guards prevent multiple inclusions of the same header file and avoid issues like redefinition of types, constants, or functions. Proper use of header guards ensures that each header file is only included once during compilation.

- **Use Include Guards in Every Header File**: All header files must use include guards to prevent multiple inclusions.

Example of a Header Guard:

.. code-block:: c

    #ifndef MY_HEADER_H
    #define MY_HEADER_H

    /* Declarations and definitions */

    #endif /* MY_HEADER_H */

- **Naming Convention for Header Guards**: The macro used for header guards should follow a consistent naming convention to avoid conflicts with other projects or libraries. It should be based on the file name, converted to uppercase, with words separated by underscores (`_`), and ending with `_H`.

Example:

For a file named `device_manager.h`:

.. code-block:: c

    #ifndef DEVICE_MANAGER_H
    #define DEVICE_MANAGER_H

    /* Declarations for device manager module */

    #endif /* DEVICE_MANAGER_H */

- **Avoid Underscore Prefixes**: Do not use leading underscores in the header guard macro name, as these are reserved for use by the C standard library.

Bad Example:

.. code-block:: c

    #ifndef _DEVICE_MANAGER_H
    #define _DEVICE_MANAGER_H
    /* INCORRECT: Leading underscores are reserved by the standard */

    #endif /* _DEVICE_MANAGER_H */

- **Use Unique Names**: Ensure that header guard names are unique to the project. In larger projects with many files, it is a good practice to prefix the header guard with the project or module name to avoid potential conflicts with other projects or libraries.

Example:

.. code-block:: c

    #ifndef PROJECT_NAME_DEVICE_MANAGER_H
    #define PROJECT_NAME_DEVICE_MANAGER_H

    /* Declarations for device manager module */

    #endif /* PROJECT_NAME_DEVICE_MANAGER_H */

- **Place Header Guards at the Very Beginning**: The `#ifndef`, `#define`, and `#endif` should be the very first and last lines in the header file, ensuring that the entire file is protected from multiple inclusions.

Bad Example:

.. code-block:: c

    /* Some comment or code */

    #ifndef DEVICE_MANAGER_H
    #define DEVICE_MANAGER_H

    /* Declarations for device manager module */

    #endif /* DEVICE_MANAGER_H */
    /* INCORRECT: Code placed before the include guard */

Good Example:

.. code-block:: c

    #ifndef DEVICE_MANAGER_H
    #define DEVICE_MANAGER_H

    /* Declarations for device manager module */

    #endif /* DEVICE_MANAGER_H */
    /* CORRECT: Include guard is the very first and last thing in the file */

ESP32-Specific Header Guards
----------------------------

When working with the ESP32 platform, follow the same conventions for header guards. However, to avoid conflicts with the ESP-IDF or other external libraries, it is recommended to include the project's name or a module-specific prefix in the guard names.

Example:

For a file named `wifi_manager.h` in a project called `my_project`:

.. code-block:: c

    #ifndef MY_PROJECT_WIFI_MANAGER_H
    #define MY_PROJECT_WIFI_MANAGER_H

    /* Declarations for Wi-Fi manager */

    #endif /* MY_PROJECT_WIFI_MANAGER_H */

When to Use Header Guards
-------------------------

- **Every Header File**: All header files must use header guards to prevent multiple inclusion issues.
  
- **Use Project/Module Prefixes**: In larger projects, always use a unique prefix to avoid conflicts with third-party libraries.

General Guidelines
------------------

- Always use `#ifndef`, `#define`, and `#endif` for header guards.

- The header guard should be based on the file name, converted to uppercase with underscores separating words, and end with `_H`.

- Avoid leading underscores in header guard names.

- Use project or module-specific prefixes for large projects to avoid name conflicts.

- Place header guards at the very top and bottom of the file.

- Keep header files focused on declarations, not definitions.

- Include only necessary headers to avoid dependency chains and reduce compilation time.

- Use forward declarations where possible to minimize includes.

- Document all functions, constants, and types in header files using Doxygen-style comments.

