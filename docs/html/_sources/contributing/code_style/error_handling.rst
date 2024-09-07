Error Handling
==============

Effective error handling is critical for building robust and maintainable software. This section outlines the best practices for handling errors in this project, ensuring that all modules use a consistent approach. The general principles of error handling should be applied throughout the codebase, focusing on clear communication of errors and minimizing crashes.

General Guidelines for Error Handling
-------------------------------------

- **Return Error Codes**: Functions should return error codes whenever an error occurs. Use negative values for failure and zero for success. Avoid returning `-1` or `1` generically—use specific error codes to indicate the nature of the failure.

- **Use `errno.h` Error Codes**: Where appropriate, use standard POSIX error codes from `errno.h` (e.g., `EINVAL`, `ENOMEM`, `EIO`). These standardized codes help communicate common error conditions clearly.

  Example:

  .. code-block:: c

    #include <errno.h>

    int process_data(void *data)
    {
      if (!data) {
        return -EINVAL; /* Invalid argument */
      }
      /* Process the data */
      return 0;
    }

- **Handle Errors at the Point of Failure**: Always handle errors as close as possible to where they occur. If a function returns an error code, the caller should check that value and handle the error appropriately. 

  Example:

  .. code-block:: c

    int ret = process_data(data);
    if (ret < 0) {
      /* Handle error, log message or clean up */
      return ret;
    }

- **Never Ignore Return Values**: Always check the return value of a function, particularly when dealing with I/O, memory allocation, or any function that could fail.

  Bad Example:

  .. code-block:: c

    malloc(100); /* No check if memory allocation succeeded */

  Good Example:

  .. code-block:: c

    void *ptr = malloc(100);
    if (!ptr) {
      /* Handle memory allocation failure */
      return -ENOMEM;
    }

- **Use `NULL` for Pointer Return Failures**: When a function returns a pointer, return `NULL` to indicate failure. Ensure the caller checks for `NULL` before dereferencing the pointer.

  Example:

  .. code-block:: c

    void *allocate_buffer(size_t size)
    {
      void *buffer = malloc(size);
      if (!buffer) {
        return NULL; /* Return NULL on allocation failure */
      }
      return buffer;
    }

- **Error Propagation**: If a function cannot resolve an error condition, propagate the error code back to the caller rather than masking it.

- **Clean Up on Failure**: Ensure that any allocated resources (e.g., memory, file handles, network sockets) are cleaned up appropriately when an error occurs. Use a consistent strategy, such as `goto` for clean-up sections at the end of functions, to handle error exits efficiently.

  Example:

  .. code-block:: c

    int do_something(void)
    {
      int *ptr = malloc(sizeof(int));
      if (!ptr) {
        return -ENOMEM;
      }

      FILE *file = fopen("data.txt", "r");
      if (!file) {
        free(ptr);
        return -EIO;
      }

      /* Do some work */

      fclose(file);
      free(ptr);
      return 0;
    }

Using `goto` for Clean-up
-------------------------

In C, the `goto` statement can be useful for simplifying error handling when dealing with resource cleanup. Use `goto` to jump to a clean-up section at the end of the function where all allocated resources are safely released.

  Example:

  .. code-block:: c

    int read_file(const char *path)
    {
      FILE *file   = NULL;
      char *buffer = NULL;

      file = fopen(path, "r");
      if (!file) {
        return -EIO;
      }

      buffer = malloc(1024);
      if (!buffer) {
        fclose(file);
        return -ENOMEM;
      }

        /* Do work with file and buffer */

    cleanup:
      if (file) {
        fclose(file);
      }
      if (buffer) {
        free(buffer);
      }

      return 0;
    }

ESP32-Specific Error Handling
-----------------------------

When working with ESP32 and **ESP-IDF**, you should use ESP32’s built-in macros and functions for error handling:

- **ESP_ERROR_CHECK()**: Use `ESP_ERROR_CHECK()` to check return values from ESP-IDF functions that return `esp_err_t`. This macro will terminate the program if an error occurs and log the error message.

  Example:

  .. code-block:: c

    esp_err_t ret = esp_wifi_init(&cfg);
    ESP_ERROR_CHECK(ret);

- **ESP_ERROR_CHECK_WITHOUT_ABORT()**: This macro works like `ESP_ERROR_CHECK()` but logs the error without terminating the program. Use this when you want to handle the error gracefully without stopping the system.

  Example:

  .. code-block:: c

    esp_err_t ret = esp_wifi_init(&cfg);
    if (ESP_ERROR_CHECK_WITHOUT_ABORT(ret) != ESP_OK) {
      /* Handle the error */
    }

- **Error Return Codes in ESP-IDF**: The ESP-IDF uses its own set of return codes, usually starting with `ESP_ERR_`. Always return these codes directly when writing ESP-IDF functions, and check them using the macros above.

Best Practices
--------------

- **Consistent Error Handling**: Always return specific error codes and handle them consistently in your code.
  
- **Use Standard Error Codes**: Where possible, use standard POSIX error codes from `errno.h` to avoid ambiguity.

- **Never Ignore Return Values**: Always check the return values of functions, especially those that can fail (e.g., `malloc`, `fopen`).

- **Clear and Actionable Error Messages**: Log clear and actionable error messages to help diagnose issues quickly.

- **Clean Up on Failure**: Always free allocated memory or close file handles when an error occurs.

General Guidelines
------------------

- **Return Error Codes**: Functions should return error codes where applicable.
  
- **Use `NULL` for Pointer Failures**: Return `NULL` for pointer failures to indicate allocation issues.

- **ESP32 Macros**: Use `ESP_ERROR_CHECK()` for ESP-IDF error handling to log errors and terminate or handle gracefully.

- **Resource Cleanup**: Use `goto` for clean-up at the end of functions when handling errors.

