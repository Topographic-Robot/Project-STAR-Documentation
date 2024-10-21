Memory Management
=================

Proper memory management is essential in any software project, but it becomes even more critical in embedded systems like the ESP32, where memory is a limited resource. This section outlines the best practices for managing memory efficiently and avoiding common pitfalls such as memory leaks, heap fragmentation, and stack overflows.

General Guidelines
------------------

- **Prefer Static Allocation**: Whenever possible, use static memory allocation instead of dynamic allocation (e.g., `malloc`/`free`) to prevent heap fragmentation and improve performance.

  - **Static Memory**: This memory is allocated at compile time and persists throughout the program's lifetime. It's ideal for variables that need to exist for the entire duration of the program.

  Example:

  .. code-block:: c

    static int buffer[1024];

  - **Dynamic Memory**: This memory is allocated at runtime using functions like `malloc` and `free`. While flexible, dynamic memory can lead to fragmentation over time, particularly in long-running applications.

  Example:

  .. code-block:: c

    int *buffer = malloc(1024 * sizeof(int));
    if (!buffer) {
      /* Handle allocation failure */
    }
    free(buffer);

- **Use Dynamic Memory Sparingly**: In memory-constrained environments, minimize the use of dynamic memory. If dynamic memory must be used, ensure that all allocations are matched with corresponding deallocations to prevent memory leaks.

- **Avoid Heap Fragmentation**: Fragmentation occurs when free memory is divided into small, non-contiguous blocks, making it difficult to allocate larger blocks of memory. Use dynamic memory only for objects with well-defined lifetimes, and consider static allocation for long-lived data.

- **Check for Memory Allocation Failures**: Always check the return value of `malloc`, `calloc`, or `realloc` to ensure that memory was successfully allocated. If memory allocation fails, handle the failure gracefully.

  Example:

  .. code-block:: c

    int *buffer = malloc(1024 * sizeof(int));
    if (!buffer) {
      /* Handle allocation failure */
      return -ENOMEM;
    }

- **Free Dynamically Allocated Memory**: Ensure that all dynamically allocated memory is properly deallocated using `free`. Failing to do so will lead to memory leaks.

  Example:

  .. code-block:: c

    free(buffer);

Stack vs. Heap
--------------

In embedded systems, memory is divided into the **stack** and the **heap**. Understanding the differences and when to use each is critical for efficient memory management.

- **Stack**: The stack is a region of memory used for local variables and function calls. It is fast, but limited in size. Exceeding the stack size can lead to stack overflows, which are difficult to debug.

  - Use the stack for small, short-lived variables (e.g., local variables in a function).

  - Be mindful of recursive functions or deep call chains, which can consume a lot of stack space.

  Example:

  .. code-block:: c

    void function(void) {
      int local_array[100];  /* Stored on the stack */
    }

- **Heap**: The heap is used for dynamically allocated memory (e.g., `malloc`). The heap offers more flexibility but is prone to fragmentation over time.

  - Use the heap for large or variable-sized data that needs to persist across function calls.

  Example:

  .. code-block:: c

    int *buffer = malloc(100 * sizeof(int));  /* Stored on the heap */
    if (buffer) {
      free(buffer);  /* Free the memory when no longer needed */
    }

- **Stack Size**: Pay attention to the stack size of each task in an embedded system. Underestimating the required stack size can lead to stack overflows, while overestimating it wastes valuable memory.

Memory Management in FreeRTOS (ESP32)
-------------------------------------

FreeRTOS provides flexible memory management for tasks, queues, and semaphores. Follow these best practices when using FreeRTOS:

- **Static vs. Dynamic Task Allocation**: FreeRTOS allows tasks to be created either with dynamic or static memory allocation. Use **static allocation** (`xTaskCreateStatic()`) for long-lived tasks to avoid heap fragmentation.

  Example:

  .. code-block:: c

    static StackType_t  task_stack[1024];
    static StaticTask_t task_buffer;

    void task1(void *pvParameters)
    {
      while (1) {
        /* Task code */
      }
    }

    void app_main(void)
    {
      xTaskCreateStatic(task1, "Task 1", 1024, NULL, 5, task_stack, &task_buffer);
    }

- **Use Heap Memory Efficiently**: FreeRTOS has multiple heap allocation schemes (e.g., heap_1, heap_2, heap_3, heap_4). Choose the heap memory management scheme that best fits your project's needs. For projects with long runtimes, consider using `heap_4` for its ability to handle fragmentation better.

Memory Leaks and Debugging
--------------------------

Memory leaks occur when dynamically allocated memory is not properly freed. Over time, memory leaks can deplete available memory, causing the system to crash or behave unpredictably. Follow these guidelines to prevent and detect memory leaks:

- **Ensure Balanced Allocation and Deallocation**: Every call to `malloc`, `calloc`, or `realloc` should have a corresponding call to `free`. Keep track of dynamically allocated memory, especially in complex systems.

- **Use Debugging Tools**: Use memory debugging tools like Valgrind, AddressSanitizer, or built-in logging mechanisms in ESP-IDF to detect memory leaks and improper memory usage.

  - In ESP-IDF, you can use `heap_caps_print_heap_info()` to get information on the state of the heap and detect potential memory issues.

- **Memory Leak Debugging in FreeRTOS**: FreeRTOS provides built-in mechanisms to help track memory usage, such as the `vTaskGetRunTimeStats()` function and FreeRTOS trace capabilities, which can help track down memory leaks and stack overflows.

Best Practices
--------------

- **Prefer Static Allocation**: Use static allocation for global or long-lived data to prevent heap fragmentation.

- **Use Dynamic Allocation Sparingly**: If dynamic memory must be used, ensure proper deallocation and avoid using dynamic memory for long-lived objects.

- **Check for Memory Allocation Failures**: Always verify that memory allocation was successful, and handle allocation failures gracefully.

- **Avoid Memory Leaks**: Track all memory allocations and ensure that every allocation has a corresponding deallocation.

- **Manage Stack Size**: Ensure that each task or function has enough stack space to avoid stack overflows.

- **Use FreeRTOS Static Allocation**: For FreeRTOS tasks, use static allocation where possible to avoid heap fragmentation in long-running tasks.

- **Monitor and Debug Memory Usage**: Use tools like Valgrind or ESP-IDF's heap monitoring functions to track memory usage and detect leaks or stack overflows.

