Globals
=======

In this project, **global variables should be avoided as much as possible**. Global variables can introduce unintended side effects, increase complexity, and make the code harder to debug and maintain. Instead, prefer using local variables, passing arguments to functions, or encapsulating data within structures or objects.

Guidelines
----------

- **Avoid Global Variables**: Global variables can create dependencies between different parts of the code, leading to bugs that are hard to trace. Instead, use function arguments or encapsulation methods like structs to pass data.

- **Use `static` for File Scope**: If a variable needs to persist across function calls but is only used within a single source file, declare it `static` to limit its scope to that file. This helps prevent accidental changes from other parts of the project.

  Example:

  .. code-block:: c

    static int s_counter = 0; /* File-scope variable, limited to this file */

- **Minimize Use of Global Constants**: If you need a constant across multiple files, prefer using `const` or `enum` values in a header file rather than using global variables.

  Example of Using `const` in a Header File:

  .. code-block:: c

    /* In a header file, declare the constant */
    extern const int max_connections;

  .. code-block:: c

    /* In the source file, define the constant */
    const int max_connections = 100;

- **Document Global Variables Clearly**: If a global variable is absolutely necessary, document its purpose clearly and describe how it interacts with other parts of the code. This includes comments explaining why the global is used and any important constraints.

When to Use Global Variables
----------------------------

Global variables should be used **only in the rarest cases** where there is a legitimate reason to have a single shared state across the entire program or module. Even in such cases, you should ensure:

- The variable is `const` to prevent unintended modifications, wherever possible.

- The variable is used across multiple files and cannot be scoped to a single file or function.

- The variable’s behavior is well-documented, with clear usage patterns to prevent side effects.

Correct Example (Avoiding Globals)
----------------------------------

.. code-block:: c

    /* Prefer passing arguments or using static variables instead of global variables */

    void process_data(int input) {
      static int s_data_count = 0; /* Limited to this file */
      s_data_count           += input;
      /* ... */
    }

Incorrect Example (Using Globals)
----------------------------------

.. code-block:: c

    int g_data_count = 0; /* Global variable, avoid this */

    void process_data(int input) {
      g_data_count += input; /* Global access, can cause side effects */
    }

General Guidelines
------------------

- **Minimize global variable usage**: Avoid using global variables unless absolutely necessary.

- **Use `static` for file-scoped variables**: To prevent other files from accessing variables that don’t need global visibility.

- **Use `const` globals** when constants need to be shared across files, as they are safer and provide better control than mutable globals.

- **Document global variables**: Clearly comment on any global variables, explaining their purpose and the reason they are needed in the context of the project.

