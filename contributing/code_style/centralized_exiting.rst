Centralized Exiting
===================

In this project, functions should have a **single, centralized exit point** whenever possible. Centralized exiting improves readability, simplifies debugging, and ensures proper cleanup of resources, such as freeing memory or closing file handles, before the function returns.

Guidelines
----------

- **One Return Statement**: Aim to have only one `return` statement at the end of the function to centralize the exit point.

- **Early Exits for Error Handling**: While centralized exiting is preferred, early exits for error handling can be acceptable if they improve clarity. However, ensure that the function still handles resource cleanup properly before exiting early.

- **Use Helper Functions**: If a function becomes too complex with a single exit point, consider breaking it into smaller helper functions to keep each function simple and readable.

Correct Example:

.. code-block:: c

  int my_function(int input)
  {
    int result = 0;
    
    /* Check for errors early */
    if (input < 0) {
      return -1;  /* Early exit for error handling */
    }

    /* Process input */
    result = input * 2;

    /* Perform any necessary cleanup */
    
    return result;  /* Single, centralized return point */
  }

Incorrect Example:

.. code-block:: c

  int my_function(int input)
  {
    int result = 0;

    /* Check for errors */
    if (input < 0) {
      return -1;  /* Return too early without cleanup */
    }

    /* Process input */
    if (input == 0) {
      return 0;  /* Multiple return points */
    }

    result = input * 2;

    return result;
  }

Resource Cleanup
----------------

When centralized exiting is used, it makes it easier to ensure that all resources, such as memory or file handles, are properly cleaned up before exiting the function.

- **Handle Resource Cleanup**: Before the centralized exit point (the final `return`), ensure that any resources allocated during the function (e.g., memory, file handles, network connections) are properly cleaned up.

Correct Example with Resource Cleanup:

.. code-block:: c

  int process_file(const char *file_name)
  {
    FILE *file = fopen(file_name, "r");
    if (!file) {
      return -1;  /* Early exit if file can't be opened */
    }

    /* Process the file here */

    fclose(file);  /* Cleanup resource */
    return 0;  /* Single exit point after resource cleanup */
  }

General Guidelines
------------------

- Use a single `return` statement at the end of the function when possible.

- Allow early exits for error handling, but ensure proper cleanup of resources.

- Break complex functions into smaller helper functions if needed.

- Always handle resource cleanup before the final exit.

