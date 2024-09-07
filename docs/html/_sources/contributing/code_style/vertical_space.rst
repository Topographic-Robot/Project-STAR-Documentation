Vertical Space
==============

Proper vertical space usage makes the code easier to read by clearly separating functions and logical blocks of code. Follow these guidelines:

- **One Empty Line Between Functions**: Always place one empty line between function definitions to improve readability. This helps visually distinguish where one function ends and the next begins.

- **No Empty Lines at the Beginning or End of Functions**: Do not place empty lines at the start or end of a function body. The opening and closing braces should be immediately adjacent to the function code.

Bad Example
-----------

.. code-block:: c

  void function1(void)
  {
  
    do_one_thing();
    do_another_thing();
  
  } /* INCORRECT, do not place an empty line here */

  
  void function2(void)
  {
  
    int var = 0;
    while (var < c_some_constant) { /* Correct constant naming */
      do_stuff(&var);
    }
  
  } /* INCORRECT, do not use an empty line here */

---

Good Example
------------

.. code-block:: c

  void function1(void)
  {
    do_one_thing();
    do_another_thing();
  }
  
  /* Place one empty line between functions */
  
  void function2(void)
  {
    int var = 0;
    while (var < c_some_constant) { /* Correct constant naming */
      do_stuff(&var);
    }
  }

**Line Length**: The maximum line length is **80** characters, as long as it does not seriously affect the readability of the code.

