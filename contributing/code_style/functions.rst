Functions
=========

In this project, functions should be designed with clear and consistent return values and names to improve readability and prevent bugs. Return values should clearly indicate whether a function succeeded or failed, and function names should reflect the type of return value expected. Braces for function definitions must be placed on the next line, while control structures like `if`, `for`, `while`, etc., should have braces on the same line.

Use `const` and Pass-by-Reference
_________________________________
Whenever possible, parameters should be declared as `const` to indicate that they are read-only. Additionally, prefer passing large structures or data by reference (using pointers) to improve performance. However, prioritize readability if passing by reference makes the function unclear.

Example of `const` and Pass-by-Reference:

.. code-block:: c

    void process_data(const int *data)
    {
      /* Function logic */
    }

Return Value Conventions
------------------------

Functions can return values of many different kinds, but the two most common types are:

- **Error-code integer**: (-Exxx = failure, 0 = success)

- **Succeeded boolean**: (0 = failure, non-zero = success)

Mixing these two types of return values is a common source of bugs. Always follow this convention to avoid confusion:

**Action vs. Predicate Functions**

- If the name of a function is an action (or an imperative command), it should return an **error-code integer**.

- If the name is a predicate (a function that returns true/false), it should return a **succeeded boolean**.

**Example**:

If the function name is an action, return an error-code integer:

.. code-block:: c

    int add_work(void)
    {
      return 0;      /* Success */
      return -EBUSY; /* Failure */
    }

If the function name is a predicate, return a succeeded boolean:

.. code-block:: c

    int pci_dev_present(void)
    {
      return 1; /* Success */
      return 0; /* Failure */
    }

All exported functions must respect this convention, and all public functions should as well. Private (static) functions are not required to follow this convention, but it is recommended.

Private and Exposed Private Functions
--------------------------------------

- **Private Functions**: When possible, private functions should be declared `static` to restrict their scope to the source file.

Example:

.. code-block:: c

    static int calculate_internal_value(int input)
    {
      return input * 2;
    }

- **Exposed Private Functions**: If a function cannot be `static` and must be exposed, prefix its name with `priv_` to clearly indicate that it is meant for internal use and should not be accessed by users of the API.

Example:

.. code-block:: c

    int priv_process_data(int data)
    {
      return data + 10;
    }

General Function Guidelines
----------------------------

- **Use `const` for Parameters**: If a parameter is not going to be modified, always declare it as `const` to ensure clarity and prevent accidental changes.
  
- **Pass by Reference for Large Data**: When dealing with large data structures, prefer passing by reference to avoid unnecessary copying. However, prioritize readability if passing by reference makes the function less clear.

Example of `const` and Passing by Reference:

.. code-block:: c

    void update_values(const int *values)
    {
      /* Function logic */
    }

- **Clear Names**: Function names should describe what the function does, and the return type should match the behavior of the function name (e.g., use a boolean return type for predicate functions).
  
- **Static Functions**: Use `static` for private functions that are only used within a single source file. Public functions should be declared in header files and follow the naming conventions.

- **Exposed Private Functions**: Use the `priv_` prefix for functions that cannot be static but are intended for internal use only.

- **Return NULL for Failed Pointer Functions**: For functions that return pointers, use `NULL` to indicate failure.

Example:

.. code-block:: c

    void *get_buffer(void)
    {
      void *buffer = malloc(1024);
      if (!buffer) {
        return NULL; /* Return NULL on failure */
      }
      return buffer;
    }

- **Prefer Early Exits**: Use early `return` statements to handle errors and avoid deeply nested control structures.

Example:

.. code-block:: c

    int process_input(int input_value)
    {
      if (input_value < 0) {
        return -EINVAL; /* Early exit on invalid input */
      }
      /* Continue processing */
      return 0;
    }

- **Always Use Braces for Functions on New Line**: For all function definitions, the opening brace must be on the next line.

Bad Example:

.. code-block:: c

    static void my_function(void) {
      /* INCORRECT: Function braces on the same line */
    }

Good Example:

.. code-block:: c

    static void my_function(void)
    {
      /* CORRECT: Function braces on the next line */
    }

- **Always Use Braces for Control Structures on Same Line**: For control structures like `if`, `for`, and `while`, the opening brace should be on the same line as the statement.

Bad Example:

.. code-block:: c

    if (foo)
    {
      bar(); /* INCORRECT: Braces on the next line */
    }

Good Example:

.. code-block:: c

    if (foo) {
      bar(); /* CORRECT: Braces on the same line */
    }

**Exported Functions**
----------------------

Functions that are exposed publicly in headers should follow the return value conventions described above. They should also be clearly documented using Doxygen, and should avoid returning raw error codes directly to the user when possible.

General Guidelines
------------------

- Use clear and descriptive function names.

- **Always declare parameters as `const` when possible**.

- **Pass by reference for large data**, unless it makes the function unreadable.

- Follow return conventions: action functions return error codes, predicate functions return boolean values.

- Always use `static` for functions not exposed in the header files.

- Use the `priv_` prefix for private functions that cannot be made `static`.

- Use `NULL` for failed pointer returns.

- Avoid deeply nested control structures by using early exits.

- Always include braces around conditional blocks, even for single lines.

- **Function braces must always be placed on the next line**, but control structure braces should stay on the same line.

