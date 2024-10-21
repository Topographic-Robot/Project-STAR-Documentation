Logging
=======

In this project, logging is handled using the ESP-IDF logging macros for different verbosity levels. These macros provide structured and meaningful logging to ensure efficient debugging and runtime analysis.

Several macros are available for different verbosity levels:

- **ESP_LOGE** - Error (lowest)

- **ESP_LOGW** - Warning

- **ESP_LOGI** - Info

- **ESP_LOGD** - Debug

- **ESP_LOGV** - Verbose (highest)

Use these macros in your code to provide relevant logging based on the severity of the message.

Guidelines
----------

- **Use Descriptive Log Messages**: Log messages should include relevant context (e.g., variable values, function names). Avoid vague log messages that lack useful information.

  Correct Example:

  .. code-block:: c

    ESP_LOGI("network", "Connection established to server at %s:%d", server_address, port);

  Incorrect Example:

  .. code-block:: c

    ESP_LOGI("network", "Connected");  /* Lacks essential context */

- **Log at Appropriate Levels**: Choose the correct logging level based on the importance of the message. The ESP logging macros support the following levels:

  - **ESP_LOGE**: Log errors that require immediate attention but do not stop the system.

  - **ESP_LOGW**: Log warnings indicating potential problems that might not immediately affect execution.

  - **ESP_LOGI**: Log informational messages about successful operations or system state.

  - **ESP_LOGD**: Log detailed debug information for development and debugging purposes.

  - **ESP_LOGV**: Log very detailed verbose messages, mainly for in-depth debugging.

  Example of Logging Levels:

  .. code-block:: c

    ESP_LOGD("input", "Processing input data: %d", input_data);
    ESP_LOGI("system", "Data processed successfully.");
    ESP_LOGW("input", "Input value close to maximum limit: %d", input_value);
    ESP_LOGE("memory", "Failed to allocate memory for buffer");
    ESP_LOGV("system", "Detailed system log for verbose debugging");

- **Avoid Excessive Logging**: Too many logs, especially at the `DEBUG` or `VERBOSE` level, can flood the log output and make important messages harder to find. Only log what's necessary, and ensure that verbose logging can be disabled in production environments.

  Correct Example:

  .. code-block:: c

    if (input_value > THRESHOLD) {
      ESP_LOGW("input", "Input value exceeded threshold: %d", input_value);
    }

  Incorrect Example:

  .. code-block:: c

    ESP_LOGD("input", "Checking input value...");
    ESP_LOGD("input", "Comparing input value with threshold...");
    ESP_LOGD("input", "Input value comparison done.");

- **Log Error Codes and Conditions**: Always log error codes or relevant conditions when logging errors, so the source of the issue is clear.

  Example:

  .. code-block:: c

    if (result == ERROR_CODE) {
      ESP_LOGE("operation", "Operation failed with error code %d", result);
    }

- **Include Timestamps in Logs**: ESP logging macros automatically include timestamps, which helps track when events occurred and aids in understanding the sequence of events.

- **Use Conditional Logging for Performance**: Avoid excessive logging in performance-critical sections of code. If logging is necessary, use conditional logging to reduce performance impact.

  Example:

  .. code-block:: c

    if (LOG_LOCAL_LEVEL >= ESP_LOG_DEBUG) {
      ESP_LOGD("performance", "Processing data: %d", data);
    }

Logging Format
--------------

In ESP-IDF, the log format includes:

1. **Timestamp**: The time the log message was generated.

2. **Log Level**: The severity of the message (e.g., ERROR, WARN, INFO).

3. **Tag**: The module or component generating the log (e.g., "network", "system").

4. **Message**: The log message itself, which should be clear and descriptive.

5. **Context**: Any relevant context, such as variable values or error codes.

Example:

.. code-block:: text

    [I][network:123] Connection established to server at 192.168.0.1:8080
    [E][memory:456] Operation failed with error code -2

When to Log
-----------

- **Initialization**: Log important initialization steps, such as starting modules or establishing connections.

- **State Changes**: Log state transitions, such as when a system starts or stops a service.

- **Errors and Exceptions**: Always log errors and exceptions, along with relevant context to aid debugging.

- **Warnings**: Log conditions that may cause problems, even if they don't immediately impact the system (e.g., near-limit conditions).

- **Critical Operations**: Log significant operations like database transactions or external API calls.

- **Shutdown**: Log when the system is shutting down or cleaning up resources.

General Guidelines
------------------

- Use descriptive log messages that include relevant context (e.g., variable values, error codes).

- Log at appropriate levels using ESP_LOGE, ESP_LOGW, ESP_LOGI, ESP_LOGD, and ESP_LOGV.

- Avoid excessive logging, especially at the `DEBUG` and `VERBOSE` levels.

- Include error codes and conditions in error logs.

- Use conditional logging in performance-critical code.

- Leverage ESP logging macros, which automatically include timestamps and tags for easier log tracking.

