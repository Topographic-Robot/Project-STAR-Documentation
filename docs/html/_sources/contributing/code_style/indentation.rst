Indentation
===========

Consistent indentation is crucial for maintaining code readability and structure. This project follows the rule of **2 spaces** for indentation, without using tabs. Using spaces ensures uniformity across different environments and editors.

- **2-Space Rule**: Each level of indentation should use 2 spaces, ensuring the code is easy to read and properly nested. Avoid using tabs, as different editors may interpret them inconsistently, leading to misaligned code.


Bad Example
-----------

.. code-block:: c

  /* Incorrect example with 4-space indentation */
  
  static void process_input(int input_value)
  {    
    if (input_value > 0) {
      s_threshold = 10;
    } else {
      s_threshold = -1;
    }
  }

---

Good Example
------------

.. code-block:: c

  /* Example of good indentation with 2-space rule */

  static void process_input(int input_value)
  {  
    if (input_value > 0) {
      s_threshold = 10;
    } else {
      s_threshold = -1;
    }
  }

  static void calculate_output(void)
  {  
    int result = 0;
    result = s_threshold + 1;
  }

Notes:

- Make sure each indentation level is exactly 2 spaces.

- Mixing tabs and spaces should be avoided at all costs to prevent misalignment in different editors.

- Consistent indentation makes the structure of the code clear, improving maintainability and readability for all contributors.

