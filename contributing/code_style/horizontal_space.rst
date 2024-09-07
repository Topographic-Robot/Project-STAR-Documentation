Horizontal Space
================

Proper use of horizontal space helps make the code more readable and maintainable. Follow these guidelines for horizontal spacing:

- **Space After Conditional and Loop Keywords**: Always add a single space after keywords like `if`, `switch`, `for`, and `while`. The opening brace `{` should be on the same line as the keyword. This improves readability by keeping the code concise.

Example 1:
----------

Bad Example:

.. code-block:: c

    if(condition) {  /* INCORRECT */
      /* ... */
    }

    switch (n){
    case 0:
      /* ... */
    }

Good Example:

.. code-block:: c

    if (condition) {  /* correct */
      /* ... */
    }

    switch (n) {
    case 0:
      /* ... */
    }

- **Binary Operators**: Add a single space around binary operators like `+`, `-`, `=`, and `&&`. For multiplication (`*`) and division (`/`) operators, spaces should always be used for clarity.

Example 2:
----------

Bad Example:

.. code-block:: c

    const int y = y0+(x-x0)*(y1-y0)/(x1-x0);    /* INCORRECT */

Good Example:

.. code-block:: c

    const int y = y0 + (x - x0) * (y1 - y0) / (x1 - x0); /* correct */
    int y_cur  = -y;                                     /* correct */

- **Alignment of Variables, Assignments, and Comments**: Align the `=` signs when declaring multiple variables, and line up the comments for consistency.

Example 3:
----------

Bad Example:

.. code-block:: c

    int foo = 12; /* This is foo */
    int large_foo = 32;    /* This is large foo */

Good Example:

.. code-block:: c

    int foo       = 12; /* This is foo */
    int large_foo = 32; /* This is large foo */

- **Optional Alignment for Function Arguments**: Horizontal space can sometimes be used within a line to align function arguments, improving readability, but use this sparingly. Excessive alignment can cause issues if future lines need to be added or removed.

Example 4:
----------

.. code-block:: c

    esp_rom_gpio_connect_in_signal(PIN_CAM_D6,   I2S0I_DATA_IN14_IDX, false);
    esp_rom_gpio_connect_in_signal(PIN_CAM_D7,   I2S0I_DATA_IN15_IDX, false);
    esp_rom_gpio_connect_in_signal(PIN_CAM_HREF, I2S0I_H_ENABLE_IDX,  false);
    esp_rom_gpio_connect_in_signal(PIN_CAM_PCLK, I2S0I_DATA_IN15_IDX, false);

**General Guidelines**:

- Avoid using TAB characters for horizontal alignment.

- Never add trailing whitespace at the end of the line.

