Breaking Long Lines
===================

To maintain readability and prevent horizontal scrolling, it’s important to break long lines of code when they exceed the maximum line length. For this project, the maximum line length is **80 characters**. Lines longer than this should be split in a consistent and readable way.

Guidelines
----------

- **Maximum Line Length**: Ensure that no line of code exceeds roughly 80 characters. This includes comments, code, and declarations.
  
- **Break at Natural Points**: Break lines at natural points, such as after operators (`+`, `-`, `*`, `=`, etc.), commas, or logical groupings to improve readability.

- **Indentation for Continuation Lines**: When breaking lines, ensure the continued line is indented properly for readability. Line up indentation after the line break to maintain visual alignment.

Correct Example:

.. code-block:: c

  int sum = first_variable + second_variable + third_variable +
            fourth_variable;

Incorrect Example:

.. code-block:: c

  int sum = first_variable + second_variable + third_variable
  + fourth_variable;  /* Operator at the start of the next line */

- **Avoid Breaking Inside Function Calls**: Break long function call arguments at commas or logical points but avoid splitting a single argument across multiple lines.

Correct Example:

.. code-block:: c

  my_function(first_argument, second_argument, third_argument,
              fourth_argument);

Incorrect Example:

.. code-block:: c

  my_function(first_argument, second_argument, third_argument, fourth_
  argument);  /* Avoid breaking a single argument across lines */

- **Aligning with Open Parentheses**: If a long statement is broken, the subsequent lines should align with the opening parenthesis or after operators where possible for clarity.

Correct Example:

.. code-block:: c

  if (condition_one && condition_two &&
      condition_three) {  /* Alignment with opening parenthesis */
    /* Code here */
  }

Incorrect Example:

.. code-block:: c

  if (condition_one && condition_two
    && condition_three) {  /* Misaligned continuation */
    /* Code here */
  }

General Guidelines
------------------

- Always keep lines under 80 characters.

- Break at logical points like operators, commas, or parentheses.

- Indent continuation lines by two spaces.

- Avoid breaking single arguments across multiple lines.

- Align continuation lines with parentheses or logical grouping for clarity.

