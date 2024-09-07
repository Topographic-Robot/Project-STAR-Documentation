Braces
======

Proper brace placement makes code cleaner and easier to read. Follow these guidelines for consistent use of braces in this project:

- **Always Use Braces for Control Statements**: Every `if`, `for`, `while`, or similar control structure must have braces, even if there is only one statement inside. Omitting braces for single statements is not allowed.

Example:

Bad Example:

.. code-block:: c

    if (foo) bar();  /* INCORRECT: Missing braces */

Good Example:

.. code-block:: c

    if (foo) {
        bar();       /* Correct: Braces added */
    }

- **Same Line for Control Structures and Blocks**: For control structures like `if`, `for`, `while`, and blocks like structs and enums, always place the opening brace `{` on the same line as the statement. This rule applies unless the line is excessively long, in which case you may split it, but still aim to keep the brace near the closing parenthesis.

Example 1:
----------

Bad Example:

.. code-block:: c

    if (condition)
    {
      /* INCORRECT */
    }

    for (int i = 0; i < c_const; ++i)
    {
      /* INCORRECT */
    }

Good Example:

.. code-block:: c

    if (condition) {
      /* ... */
    }

    for (int i = 0; i < c_const; ++i) {
      /* ... */
    }

    typedef struct {
      int member;
    } my_struct_t;

- **Functions Have Braces on a New Line**: The only exception to the same-line rule is for functions. For function definitions, place the opening brace `{` on a new line.

Example 2:
----------

Bad Example:

.. code-block:: c

    static void my_function(void) {
      /* INCORRECT */
    }

Good Example:

.. code-block:: c

    static void my_function(void)
    {
      /* Function logic */
    }

- **Long Statements or Complex Logic**: If a control structure or block has a very long or complex statement that requires multiple lines, you may split the statement but keep the brace close to the ending parenthesis `)` for readability.

Example 3:
----------

.. code-block:: c

    if (my_long_condition && another_condition &&
        some_more_complex_logic()) {
      /* Split statement, brace close to ')' */
    }

General Guidelines
------------------

- Always use braces, even for single statements.

- Keep braces next to the ending parenthesis when splitting long statements.

- Functions are the only structures that have the brace on a new line. All other blocks, including structs and control structures, should keep the brace on the same line.

