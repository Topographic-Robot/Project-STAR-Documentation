Macros
======

In this project, **macros** should be used sparingly and only when absolutely necessary. While macros can provide some flexibility, they can also make code harder to read, debug, and maintain due to their lack of type safety and visibility. Prefer `const` variables, `inline` functions, or enums wherever possible to avoid the downsides of macros.

Guidelines
----------

- **Avoid Unnecessary Macros**: Always consider using `const`, `inline` functions, or enums before defining a macro. These alternatives offer type safety, debugging support, and better readability.

Example of Using `const` Instead of a Macro
-------------------------------------------

.. code-block:: c

    /* Macro for a constant */
    #define MAX_BUFFER_SIZE 1024

    /* Preferred: Using const instead of macro */
    const int max_buffer_size = 1024;

- **Use All Uppercase for Macro Names**: Macro names should be written in **all uppercase** to distinguish them from variables and functions. Use underscores (`_`) to separate words.

  Correct Example:

  .. code-block:: c

    #define MAX_BUFFER_SIZE 1024

  Incorrect Example:

  .. code-block:: c

    #define maxBufferSize 1024

- **Always Use Parentheses Around Macro Arguments**: When defining macros that take arguments, always use parentheses around both the arguments and the macro body to avoid unexpected behavior due to operator precedence.

  Correct Example:

  .. code-block:: c

    #define SQUARE(x) ((x) * (x))

  Incorrect Example:

  .. code-block:: c

    #define SQUARE(x) x * x

Example of Using `inline` Instead of a Macro
--------------------------------------------

While **inline** functions can be useful in replacing macros and improving type safety, excessive use of `inline` can lead to performance issues. As described in the Linux Kernel guidelines, an overuse of inlining increases the memory footprint and cache usage, which can result in slowdowns due to cache misses and increased memory usage. It's important to inline only small functions that are called frequently.

Guidelines for Using `inline`:

- **Inline small functions**: Only functions with fewer than three lines should generally be inlined.

- **Avoid inlining large functions**: Functions with complex logic should not be inlined as they increase the instruction cache footprint and cause performance degradation.

- **Let the compiler decide**: The compiler is usually smart enough to automatically inline functions where it makes sense, especially for static and frequently used functions. Avoid explicitly forcing `inline` for functions unless absolutely necessary.

Correct Example:

.. code-block:: c

    /* Good inline example: Small and simple function */
    inline int square(int x)
    {
      return x * x;
    }

Incorrect Example:

.. code-block:: c

    /* Bad inline example: Larger function, should not be inlined */
    inline int process_data(int data[], int length)
    {
      int result = 0;
      for (int i = 0; i < length; ++i) {
        result += data[i];
      }
      return result;
    }

- **Enclose Macro Definitions in Blocks**: If the macro body contains more than one statement, enclose the macro body in a `do { ... } while(0)` block to ensure it behaves like a single statement and can be used safely in conditional logic.

  Correct Example:

  .. code-block:: c

    #define SWAP(a, b) do {                \
                         int temp = (a);   \
                         (a)       = (b);  \
                         (b)       = temp; \
                       } while (0)

  Incorrect Example:

  .. code-block:: c

    #define SWAP(a, b) int temp = a; a = b; b = temp;

- **Minimize Macro Scope**: Macros can easily introduce global visibility, making them difficult to track and debug. To avoid issues, keep the scope of macros as limited as possible and prefer function-like macros only where necessary.

- **Document Macros Clearly**: Always provide a clear comment describing the purpose of the macro. Since macros can be harder to trace during debugging, ensure that their usage and intention are well documented.

Correct Example:

.. code-block:: c

    /* Macro to swap two integers */
    #define SWAP(a, b) do {                 \
                          int temp = (a);   \
                          (a)       = (b);  \
                          (b)       = temp; \
                        } while (0)

    /* Macro to calculate the square of a number */
    #define SQUARE(x) ((x) * (x))

Incorrect Example:

.. code-block:: c

    #define SWAP(a, b) int temp = a; a = b; b = temp;
    #define SQUARE(x) x * x

When to Use Macros
------------------

Use macros when other options such as `const` or `inline` functions are not viable, such as:

- **Conditional Compilation**: Macros can be useful for including or excluding code based on certain conditions, especially in cross-platform projects or for debugging.

  Example:

  .. code-block:: c

    #ifdef DEBUG
    #define LOG(msg) printf("DEBUG: %s\n", msg)
    #else
    #define LOG(msg) ((void)0)
    #endif

- **Header Guards**: Macros are essential for preventing multiple inclusions of header files.

  Example:

  .. code-block:: c

    #ifndef MY_HEADER_H
    #define MY_HEADER_H

    /* Header content */

    #endif /* MY_HEADER_H */

General Guidelines
------------------

- Prefer `const`, `inline` functions, and enums over macros when possible.

- Use all uppercase for macro names with underscores to separate words.

- Always enclose macro arguments in parentheses and use blocks for multi-statement macros.

- Keep macros’ scope limited and document their purpose clearly.

- Use macros for conditional compilation and header guards where necessary.

Style Note
----------

When writing multi-line macros, always **align the backslashes (`\\`) vertically** for consistency and readability, similar to how variables and comments are aligned. This improves readability and maintains a uniform coding style across the project.

