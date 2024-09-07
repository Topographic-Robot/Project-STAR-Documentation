Assertions
==========

In this project, **assertions** are used as a tool to catch programming errors and invalid states during development. They help ensure that assumptions made in the code are correct, and they provide valuable debugging information when things go wrong. However, assertions should never be relied on to handle runtime errors or expected conditions in production code.

Guidelines
----------

- **Use Assertions for Debugging**: Assertions are intended to catch conditions that should never occur during normal program execution. Use them to assert assumptions about the state of the program, such as parameter validation or invariants within algorithms.

Example of Using `assert`:

.. code-block:: c

    #include <assert.h>

    void process_data(int *data)
    {
      assert(data != NULL);  /* Assert that data is not NULL */
      /* Continue processing */
    }

- **Avoid Assertions in Production Code**: Assertions should not be used for handling expected runtime errors or conditions that might naturally occur in a program's lifecycle. Instead, use proper error handling techniques like `if` statements or return codes.

Bad Example:

.. code-block:: c

    void read_file(FILE *fp)
    {
      assert(fp != NULL);  /* INCORRECT: This could be a valid runtime error */
      /* Reading file logic */
    }

Good Example:

.. code-block:: c

    void read_file(FILE *fp)
    {
      if (fp == NULL) {
        /* Handle the error, perhaps by returning an error code */
        return;
      }
      /* Reading file logic */
    }

- **Avoid Side Effects in Assertions**: Assertions should not contain side effects, as the code inside the `assert` macro will be removed in non-debug builds (e.g., when `NDEBUG` is defined). Ensure that assertions only check conditions without altering the program state.

Bad Example:

.. code-block:: c

    assert(buffer = malloc(1024));  /* INCORRECT: Side effect inside assert */

Good Example:

.. code-block:: c

    buffer = malloc(1024);
    assert(buffer != NULL);  /* CORRECT: No side effects inside assert */

- **Document Assertions**: When using an assertion, provide a comment to explain what the assertion is checking and why it is necessary. This will help other developers (or future you) understand the assumption being made.

Example:

.. code-block:: c

    assert(index >= 0 && index < MAX_SIZE);  /* Index should always be within bounds */

- **Use `static_assert` When Possible**: For compile-time checks, prefer using `static_assert` (available in C11 and later) to catch errors early in the compilation process.

Example of Using `static_assert`:

.. code-block:: c

    #include <assert.h>

    static_assert(sizeof(int) == 4, "int must be 4 bytes");  /* Compile-time assertion */

ESP32-Specific Assertions
-------------------------

In ESP32 projects, you have two specific macros for error checking: **`ESP_ERROR_CHECK`** and **`ESP_ERROR_CHECK_WITHOUT_ABORT`**. These are commonly used to catch errors during development, especially when working with ESP-IDF functions.

- **`ESP_ERROR_CHECK`**: This macro checks the return value of an ESP-IDF function and aborts the program if the return code is not `ESP_OK`. It is useful for quickly catching errors during development, but it should not be used for handling recoverable errors in production.

Example:

.. code-block:: c

    esp_err_t err = some_esp_function();
    ESP_ERROR_CHECK(err);  /* Abort if an error occurred */

- **`ESP_ERROR_CHECK_WITHOUT_ABORT`**: This macro works similarly to `ESP_ERROR_CHECK`, but it will not abort the program when an error occurs. This can be useful when you want to log errors without stopping the entire program.

Example:

.. code-block:: c

    esp_err_t err = another_esp_function();
    ESP_ERROR_CHECK_WITHOUT_ABORT(err);  /* Log error but continue execution */

**When to Use**:

- Use `ESP_ERROR_CHECK` during development to catch and abort on critical errors that should never occur.

- Use `ESP_ERROR_CHECK_WITHOUT_ABORT` when you want to log errors but allow the program to continue running.

When to Use Assertions
----------------------

- **Parameter Validation**: Use assertions to validate parameters that are assumed to be valid in internal functions. Public API functions should use proper error handling, while internal functions can use assertions to enforce assumptions about input data.

- **Invariants and Assumptions**: Use assertions to enforce invariants (conditions that should always be true) within algorithms or data structures. For example, asserting that a pointer is not `NULL`, or that a buffer index is within valid bounds.

- **Critical Failures in Development**: Use assertions to catch critical failures during development that should never occur in a well-tested, stable system. These might include invalid state transitions or unhandled edge cases.

General Guidelines
------------------

- **Use assertions for catching programming errors** and invalid states during development.

- **Do not rely on assertions for runtime error handling** in production code.

- **Avoid side effects in assertions** since they are removed in non-debug builds.

- **Use `static_assert` for compile-time checks** when available.

- **Provide comments explaining assertions** to clarify their purpose.

- **Use `ESP_ERROR_CHECK` and `ESP_ERROR_CHECK_WITHOUT_ABORT`** in ESP32 projects to catch and log errors effectively.

