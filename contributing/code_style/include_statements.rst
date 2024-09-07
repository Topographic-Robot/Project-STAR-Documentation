Include Statements
==================

In C projects, **include statements** are used to bring in the necessary header files for a module to function correctly. Proper management of include statements helps reduce compilation time, avoid dependency issues, and maintain clear project structure. This section outlines the best practices for managing include statements in header and source files.

General Guidelines for Include Statements
-----------------------------------------

- **Use Angle Brackets for System/Library Headers**: When including standard library headers or external library headers, always use angle brackets (`< >`). This ensures that the compiler searches the system directories first.

  Example:

  .. code-block:: c

    #include <stdio.h>
    #include <stdint.h>

- **Use Quotation Marks for Project Headers**: When including project-specific headers, use double quotation marks (`" "`). This tells the compiler to first search the project's directories for the file.

  Example:

  .. code-block:: c

    #include "my_project.h"
    #include "device_manager.h"

- **Minimal Includes in Header Files**: Include only the necessary headers in your header files to reduce unnecessary dependencies. Use forward declarations instead of including entire header files whenever possible.

  Example of Forward Declaration:

  .. code-block:: c

    /* Forward declare struct device_t instead of including its full header */
    struct device_t;

    void init_device(struct device_t *device);  /* Declaration without including "device.h" */

  By using forward declarations, you reduce the number of headers included in header files, improving compilation times and avoiding circular dependencies.

Forward Declaration Explained
-----------------------------

Forward declarations allow you to declare a type or function without providing its full definition. This is particularly useful when only a pointer to a type is required, or when you need to avoid circular dependencies between header files.

When to Use Forward Declarations
--------------------------------

- **For Structs**: Use forward declarations when you only need a pointer to a struct, and you do not need to access its members.

- **For Functions**: Use forward declarations in header files to declare the existence of a function without defining its logic. The full implementation can be placed in the corresponding `.c` file.

Example:

.. code-block:: c

    /* Forward declaration of struct device_t */
    struct device_t;

    /* Function that only needs a pointer to device_t */
    void init_device(struct device_t *device);

Full Definition of Forward Declared Struct
------------------------------------------

In the source file (or another header file), the full definition of the struct can be provided:

.. code-block:: c

    struct device_t {
        int id;
        int status;
    };

Benefits of Forward Declarations
--------------------------------

- **Reduced Dependencies**: By using forward declarations, you can minimize the number of headers that need to be included in a file. This reduces dependency chains and improves compilation time.

- **Avoid Circular Dependencies**: Forward declarations help break circular dependencies, which can occur when two headers include each other.

- **Simpler and Cleaner Code**: By declaring only what is necessary, your headers remain simpler and easier to maintain.

When Not to Use Forward Declarations
------------------------------------

- **When accessing struct members**: If you need to access or modify the members of a struct, you must include the full definition of the struct.

- **For complex types**: If the type is used heavily throughout a file, it may be clearer to include the full definition to avoid confusion.

Include Complete Headers in Source Files
----------------------------------------

While header files should include minimal dependencies, source files should include the full set of headers they require. This ensures that all dependencies are fully met during compilation.

Example:

.. code-block:: c

    #include <stdio.h>
    #include "device.h"

    void print_device_info(device_t *device)
    {
        printf("Device ID: %d\n", device->id);
    }

Order of Includes
-----------------

Include statements should be organized in a specific order to improve readability and minimize conflicts:
  
1. First include the corresponding header file for the source file.

2. Then include any external or system headers.

3. Lastly, include any project-specific headers.
  
Example:

.. code-block:: c

    #include "my_source.h"   /* Corresponding header file */
    #include <stdio.h>       /* Standard library headers */
    #include "device.h"      /* Project-specific headers */

Guard Against Redundant Includes
--------------------------------

Avoid including the same header multiple times in a file, especially within a single source file. Header guards ensure that headers are only included once during the compilation process, but it's still important to include only what's necessary.

Use `#include` in the Correct Location
--------------------------------------

Avoid placing `#include` statements in the middle of functions or blocks. Include all necessary headers at the top of the file for clarity.

When to Include Headers
-----------------------

- **Always Include What You Use**: Each source file should include the necessary headers for the functions and types it uses. Do not rely on indirect includes (headers included by other headers). This makes dependencies explicit and easier to track.

- **Forward Declarations Instead of Full Includes**: In header files, use forward declarations whenever possible to avoid pulling in unnecessary dependencies.

- **Place Includes at the Top**: Always place `#include` statements at the top of the file, before any other code.

