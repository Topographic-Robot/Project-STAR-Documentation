Structures
==========

Structures (structs) in this project should be used to group related data together in a clean and organized manner. Proper use of structures enhances code readability, maintainability, and provides an efficient way to represent complex data. Follow these guidelines for struct usage and naming conventions.

General Guidelines for Structures
----------------------------------

- **Use Structs to Group Related Data**: Structs should be used to encapsulate related variables into a single entity, rather than passing around or managing multiple separate variables.

  Example:

  .. code-block:: c

    typedef struct {
        int x;
        int y;
    } point_t;

- **Struct Names Should End in `_t`**: All struct types should end with `_t` to indicate that they are typedefs, ensuring consistency across the project.

  Example:

  .. code-block:: c

    typedef struct {
        int width;
        int height;
    } rectangle_t;

- **Use Snake Case for Struct Members**: All member variables inside a struct should follow snake_case naming conventions. This ensures uniformity across the project and improves readability.

  Example:

  .. code-block:: c

    typedef struct {
        int x_position;
        int y_position;
    } position_t;

- **Always Document Each Member of the Struct**: Every struct member should be clearly documented with a comment, providing a short description of its purpose or role within the structure.

  Example:

  .. code-block:: c

    /**
     * @brief Struct representing a 2D point.
     */
    typedef struct {
        int x_position;  /**< X-coordinate of the point */
        int y_position;  /**< Y-coordinate of the point */
    } point_t;

- **Use Pointers for Large Structs**: When passing large structs around, use pointers instead of passing by value. This avoids the overhead of copying the entire struct and improves performance.

  Example:

  .. code-block:: c

    void move_point(point_t *p) {
        p->x_position += 1;
        p->y_position += 1;
    }

- **Initialize Structs to Zero or Default Values**: Always ensure that structs are initialized properly, either with zero or appropriate default values. This avoids potential bugs caused by uninitialized data.

  Example:

  .. code-block:: c

    point_t p = {0};  /* Initialize struct to zero */

  Or:

  .. code-block:: c

    point_t p = { .x_position = 0, .y_position = 0 };  /* Initialize with default values */

- **Use `const` with Struct Pointers When Data Shouldn't Change**: If a function should not modify the data inside a struct, mark the pointer as `const` to enforce this behavior.

  Example:

  .. code-block:: c

    void print_point(const point_t *p) {
        printf("X: %d, Y: %d\n", p->x_position, p->y_position);
    }

Struct Alignment and Padding
----------------------------

- **Minimize Padding and Align Struct Members**: Struct members should be ordered to minimize padding and ensure proper alignment. This improves performance and reduces memory overhead.

  Example:

  .. code-block:: c

    typedef struct {
        int  a;   /* Aligns with the int size */
        char b;  /* Padding added here */
    } aligned_struct_t;

  Rearranged for better alignment:

  .. code-block:: c

    typedef struct {
        char b;  /* Now placed before the int */
        int  a;   /* Padding removed */
    } aligned_struct_t;

- **Consider Memory Layout for Large Structs**: For larger structs, consider the memory layout and how the data will be accessed. Group similar data types together to minimize cache misses and improve access speed.

Encapsulation and Struct Access
-------------------------------

- **Use Accessor Functions to Modify Struct Members**: When appropriate, use getter and setter functions to modify struct members. This allows for better encapsulation and flexibility, especially if the struct implementation changes over time.

  Example:

  .. code-block:: c

    void set_point_x(point_t *p, int x) {
        p->x_position = x;
    }

    int get_point_x(const point_t *p) {
        return p->x_position;
    }

- **Avoid Exposing Internal Structs in Public APIs**: In public APIs, avoid directly exposing the internal structure of a struct. Instead, use opaque types or provide accessor functions to interact with the struct, ensuring that internal implementation details can change without breaking API contracts.

  Example:

  .. code-block:: c

    /* Private definition of struct */
    typedef struct point_t point_t;

    /* Accessor functions */
    point_t *create_point(int x, int y);
    void destroy_point(point_t *p);
    int get_point_x(const point_t *p);

Naming Conventions
------------------

- **Use Meaningful Names**: Struct names should be descriptive and indicate the type of data they represent.

- **Follow Snake Case for Struct Members**: All struct members should use snake_case to maintain consistency.

- **Prefix with Module Name for Shared Structs**: When a struct is shared between multiple modules, prefix its name with the module's name to avoid naming collisions.

Example 1:
----------

Bad Example:

.. code-block:: c

    typedef struct {
        int width;
        int height;
    } rect;  /* INCORRECT: Non-descriptive name, does not end with _t */

Good Example:

.. code-block:: c

    typedef struct {
        int width;
        int height;
    } rectangle_t;  /* CORRECT: Descriptive name and follows naming convention */

Example 2:
----------

Bad Example:

.. code-block:: c

    typedef struct {
        int x;
        int y;
    } position_t;  /* INCORRECT: Poor documentation and lacks meaningful member names */

Good Example:

.. code-block:: c

    /**
     * @brief 2D position in space.
     */
    typedef struct {
        int x_position;  /**< X-coordinate */
        int y_position;  /**< Y-coordinate */
    } position_t;  /* CORRECT: Proper documentation and meaningful member names */

General Guidelines
------------------

- Always end struct names with `_t`.

- Use snake_case for struct members.

- Document each struct member for clarity and future maintenance.

- Minimize struct padding by ordering members based on their size.

- Use pointers for large structs when passing them as function arguments.

- Consider using accessor functions for encapsulation.

