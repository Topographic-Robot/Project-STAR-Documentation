Type Definitions
================

Using `typedef` allows for more readable and maintainable code by creating meaningful aliases for types. Follow these guidelines when creating type definitions in this project.

Guidelines
----------

- **Use `_t` Suffix for `typedef` Types**: All user-defined types created with `typedef` must end with `_t`. This is a common convention in C to distinguish type names from variables and functions.

Example 1:
----------

Bad Example:

.. code-block:: c

    typedef struct {
      int x;
      int y;
    } Point;  /* INCORRECT: Missing '_t' suffix */

Good Example:

.. code-block:: c

    typedef struct {
      int x;
      int y;
    } point_t;  /* CORRECT: '_t' suffix added */

- **Use Meaningful Type Names**: Always use descriptive and meaningful names for `typedef` types to make the code more readable and easier to understand.

Example 2:
----------

Bad Example:

.. code-block:: c

    typedef struct {
      int width;
      int height;
    } W_H;  /* INCORRECT: Non-descriptive type name */

Good Example:

.. code-block:: c

    typedef struct {
      int width;
      int height;
    } dimensions_t;  /* CORRECT: Descriptive type name */

- **Use `typedef` to Simplify Complex Types**: Use `typedef` to simplify the declaration of complex types, such as function pointers, or to make the code more consistent and readable.

Example 3:
----------

Bad Example:

.. code-block:: c

    int (*compare)(const void *, const void *);  /* INCORRECT: Hard to read */

Good Example:

.. code-block:: c

    typedef int (*compare_fn_t)(const void *, const void *);  /* CORRECT: Simplified with typedef */

- **Do Not Overuse `typedef`**: Avoid using `typedef` for basic types like `int`, `char`, or `float`, as this can make the code harder to follow and debug. Use `typedef` only when it improves the clarity of the code.

Example 4:
----------

Bad Example:

.. code-block:: c

    typedef int my_int;  /* INCORRECT: Overuse of typedef */

Good Example:

.. code-block:: c

    /* No typedef needed for basic types like int */

- **Struct and Enum Typedefs**: When defining structs or enums, always use `typedef` and the `_t` suffix to create a new type for ease of use. This ensures consistency across the codebase and simplifies the declaration of variables.

Example 5:
----------

Bad Example:

.. code-block:: c

    struct person {
      char *name;
      int age;
    };

    struct person john;  /* INCORRECT: Repeated 'struct' keyword */

Good Example:

.. code-block:: c

    typedef struct {
      char *name;
      int age;
    } person_t;

    person_t john;  /* CORRECT: Typedef used to avoid repeated 'struct' keyword */

- **Enum Type Definitions**: Always use `typedef` with enums, and follow the same convention of appending `_t` to the type name. Enum values should be in `snake_case` and end with `_e`.

Example 6:
----------

Bad Example:

.. code-block:: c

    enum color {
      RED,
      BLUE,
      GREEN
    };

Good Example:

.. code-block:: c

    typedef enum {
      red_e,
      blue_e,
      green_e
    } color_t;

General Guidelines
------------------

- Always use the `_t` suffix for all `typedef` types to distinguish them from variables and functions.

- Use `typedef` to simplify complex types, such as structs, enums, and function pointers.

- Avoid using `typedef` for basic types like `int`, `float`, or `char`.

- Always create meaningful and descriptive names for `typedef` types.

- Follow consistent naming conventions for `struct`, `enum`, and function pointer type definitions.

