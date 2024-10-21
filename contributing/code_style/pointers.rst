Pointers
========

Pointers are a powerful tool in C programming, but they can lead to bugs or undefined behavior if used incorrectly. Follow these guidelines for consistent, safe, and efficient use of pointers in this project.

Guidelines
----------

- **Pointer Declaration and Placement**: Always place the asterisk (`*`) adjacent to the variable name, not the type. This improves readability and consistency in the code.

Example 1:
----------

Bad Example:

.. code-block:: c

    int* ptr;  /* INCORRECT */
    char* str;

Good Example:

.. code-block:: c

    int  *ptr;  /* CORRECT */
    char *str;

- **Initialize Pointers**: Always initialize pointers, either to `NULL` or a valid memory location, to avoid using uninitialized pointers, which can lead to undefined behavior.

Example 2:
----------

Bad Example:

.. code-block:: c

    int *ptr;  /* INCORRECT: Uninitialized pointer */
    *ptr = 10;

Good Example:

.. code-block:: c

    int *ptr = NULL;  /* Correct initialization */
    ptr      = malloc(sizeof(int));  /* Or allocate memory */

- **Avoid Dangling Pointers**: A dangling pointer refers to a pointer that continues to reference a memory location after that memory has been freed. Always set a pointer to `NULL` after freeing the allocated memory.

Example 3:
----------

Bad Example:

.. code-block:: c

    int *ptr = malloc(sizeof(int));
    free(ptr);  /* INCORRECT: Dangling pointer */
    /* ptr still points to the now freed memory */

Good Example:

.. code-block:: c

    int *ptr = malloc(sizeof(int));
    free(ptr);
    ptr = NULL;  /* CORRECT: Pointer set to NULL after free */

- **Use `const` When Appropriate**: Use `const` with pointers when the data being pointed to should not be modified. This provides an extra layer of safety and makes the code easier to understand.

Example 4:
----------

.. code-block:: c

    const char *message = "Hello";  /* CORRECT: The pointer data can't be changed */

    char *const ptr = some_buffer;  /* The pointer can't be reassigned */

- **Pointer Arithmetic**: Be cautious with pointer arithmetic. It's only valid for pointers to elements in an array. Misuse of pointer arithmetic can lead to out-of-bounds access and undefined behavior.

Example 5:
----------

Bad Example:

.. code-block:: c

    int  arr[5];
    int *ptr = arr;
    ptr     += 10;  /* INCORRECT: Pointer out of bounds */

Good Example:

.. code-block:: c

    int  arr[5];
    int *ptr = arr;
    ptr     += 2;  /* CORRECT: Pointer remains within bounds */

- **Dereferencing Pointers**: Always ensure a pointer is non-NULL before dereferencing it to avoid segmentation faults or undefined behavior.

Example 6:
----------

Bad Example:

.. code-block:: c

    int *ptr = NULL;
    *ptr     = 42;  /* INCORRECT: Dereferencing NULL pointer */

Good Example:

.. code-block:: c

    if (ptr != NULL) {
      *ptr = 42;  /* CORRECT: Safe dereferencing */
    }

General Guidelines
------------------

- Use `*` next to the variable name when declaring pointers.

- Always initialize pointers to `NULL` or a valid memory location.

- Set pointers to `NULL` after freeing the memory they point to.

- Use `const` to specify when pointer data should not be modified.

- Be cautious with pointer arithmetic and avoid going out of bounds.

- Always check that a pointer is non-NULL before dereferencing it.

