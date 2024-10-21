Comments
========

Comments are an essential part of writing readable code, but they should be used effectively. Follow these guidelines to ensure that comments add clarity without being excessive. Since we use Doxygen for generating documentation, **all functions must include Doxygen comments**, and they should follow specific conventions regarding where to place them.

General Commenting Guidelines
-----------------------------

- **Use Block Comments (`/* */`)**: Always prefer `/* */` comments over `//`. Block comments are more versatile and consistent for C projects. Avoid starting block comments with an empty first line.

  - For single-line comments, keep them on one line:

    Correct:

    .. code-block:: c

      /* This is a single-line comment */

    Incorrect:

    .. code-block:: c

      /* This is a single-line comment
       */

  - For comments following variables or statements, align them for consistency:

    Correct:

    .. code-block:: c

      int x;   /* This is x */
      int foo; /* This is foo */

    Incorrect:

    .. code-block:: c

      int x; /* This is x */
      int foo; /* This is foo */

Doxygen Documentation
----------------------

Since we use Doxygen to generate documentation, **every function** must include a Doxygen-style comment block. These comments provide valuable information about what each function does, its parameters, return values, and any important details about usage.

**Where to place Doxygen comments:**

- **Header files (`.h` files)**: Doxygen comments should be placed in header files for public functions and any functions that are shared across multiple source files. This allows the comments to be used for API documentation and ensures that users of your code understand the function's purpose and usage.
  
- **Source files (`.c` files)**: You may include Doxygen comments in source files for private or static functions that are not exposed through header files. If the function is defined in both a header and source file, place the Doxygen comment in the header file only.

**Doxygen Comment Structure:**

- **@brief**: A short summary of what the function does.

- **@param**: A description of each parameter, including type and usage.

- **@return**: What the function returns, or `void` if nothing is returned.

- **@note**: (Optional) Any additional notes about the function, such as important edge cases or limitations.

Doxygen Example
---------------

For public functions (in header file):

.. code-block:: c

  /**
   * @brief  Adds two numbers.
   * @param  a First number to be added.
   * @param  b Second number to be added.
   * @return The sum of a and b.
   */
  int add(int a, int b);

For private/static functions (in source file):

.. code-block:: c

  /**
   * @brief Initializes the internal counter.
   * @param value Initial value for the counter.
   * @note  This function is only used internally and is static.
   */
  static void init_counter(int value);

Key Doxygen Tags
----------------

- **@brief**: Provides a concise summary of the function.

- **@param**: Describes the function parameters. List each parameter separately.

- **@return**: Describes the return value. If the function does not return a value, you can omit this tag or specify `void`.

- **@note**: Use this for any important additional information, such as side effects, limitations, or edge cases.

- **@warning**: Used for warning the user about potential risks in the function's use.

- **@deprecated**: Marks a function as deprecated, with a note on what to use instead.

Example with Additional Tags:

.. code-block:: c

  /**
   * @brief      Opens a connection to the server.
   * @param      server_address The address of the server.
   * @param      port Port number to use for the connection.
   * @return     0 on success, -1 on error.
   * @warning    Ensure that the server address is valid before calling this function.
   * @deprecated Use `open_server_connection_v2()` instead.
   */
  int open_connection(const char *server_address, int port);

Block Diagrams at the Start of Files
------------------------------------

At the start of each file, when relevant, include a block diagram to represent the current part of the project or module. This provides context for what the file or module does at a glance.

Example:

.. code-block:: c

  /* Block Diagram: This module handles user input
   *  +---------+      +---------+
   *  | Input   | ---> | Handler |
   *  +---------+      +---------+
   */

Purpose of Comments
-------------------

Comments should describe **what** the code does, not **how** it works. Avoid over-commenting or explaining how code works, especially if it's complex. Instead, focus on writing clear and self-explanatory code.

- **Avoid Explaining How Code Works**: Well-written code should be clear enough to convey how it works. Comments should not be used to explain poorly written code.

- **Explain What the Code Does**: Use comments to describe the intent or purpose of code, particularly for more complex functions or logic.

Bad Example
-----------

.. code-block:: c

    int x = 5; /* Set x to 5
                */
    /* This loop increments x by 1 ten times
     */
    for (int i = 0; i < 10; i++) {
      x++;
    }

Good Example
------------

.. code-block:: c

    /* Increments x ten times */
    for (int i = 0; i < 10; i++) {
      x++;
    }

Placing Comments Outside Functions
----------------------------------

- **Head of the Function**: Place comments at the start of functions to describe **what** the function does and, if necessary, **why** it does it. Avoid putting comments inside the function body unless there's something specific that needs a note or a warning.

Example:

.. code-block:: c

  /* Processes user input and updates state
   * Handles edge cases for invalid input
   */
  static void process_input(int input_value)
  {
    /* ... */
  }

General Guidelines
------------------

- Use `/* */` for comments.

- Do not start block comments with an empty first line.

- Use Doxygen formatting for documentation generation (e.g., `@param`, `@return`, `@brief`).

- Use keywords like `TODO:`, `FIXME:`, `BUG:`, and `XXX:` to mark important areas.

- For single-line comments, keep them on one line (e.g., `/* This is a comment */`).

- Align comments after variable declarations or statements.

- Include block diagrams at the start of files when relevant.

- Focus on explaining **what** the code does, not **how** it works.

- Place comments at the head of functions, not inside function bodies.

