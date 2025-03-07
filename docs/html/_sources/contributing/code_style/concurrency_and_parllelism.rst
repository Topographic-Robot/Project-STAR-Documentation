Concurrency and Parallelism
===========================

Concurrency and parallelism allow a program to perform multiple tasks simultaneously or overlap I/O-bound tasks with computation. In embedded systems like ESP32, efficient use of concurrency is crucial to manage tasks such as networking, sensors, or interrupt handling. This section outlines the best practices for ensuring thread-safe and efficient concurrent programming, along with an explanation of when to use **RTOS types**, **mutexes**, **semaphores**, and **atomic operations**.

General Guidelines
------------------

- **Avoid Global State**: Global variables should be avoided, especially in multi-threaded environments, to prevent race conditions. Use thread-local storage or pass variables explicitly to functions.

- **Thread Safety**: Ensure that shared resources (e.g., data structures, hardware peripherals) are properly synchronized when accessed by multiple threads or tasks. This can be done using RTOS types, mutexes, semaphores, or atomic operations.

- **Minimize Lock Contention**: When using synchronization primitives like mutexes, hold locks for the shortest time possible to avoid contention between threads. Design critical sections carefully to reduce lock duration.

RTOS Types, Mutexes, Semaphores, and Atomic Operations
------------------------------------------------------

When dealing with concurrency, choosing the right synchronization mechanism is key. In embedded systems like ESP32, using RTOS types is often more efficient and suitable than traditional methods. Each has its strengths, limitations, and specific use cases.

**RTOS Types**
RTOS types, such as FreeRTOS tasks, queues, and semaphores, are specifically designed for embedded systems, providing efficient task management and synchronization.

- **What They Do**: RTOS types manage task scheduling, communication, and synchronization in a way that is optimized for embedded environments.

- **How They Work**: RTOS types leverage the real-time operating system's capabilities to ensure efficient and predictable task execution and resource management.

- **When to Use**: Use RTOS types when developing for embedded systems like ESP32, where efficient task management and low overhead are crucial.

  **Example**:

  .. code-block:: c

    void task1(void *pvParameters)
    {
      while (1) {
        /* Task code */
        vTaskDelay(1000 / portTICK_PERIOD_MS); /* Delay for 1 second */
      }
    }

    void app_main(void)
    {
      xTaskCreate(task1, "Task 1", 2048, NULL, 5, NULL);
    }

**Mutexes**
A **mutex** (mutual exclusion) is a synchronization primitive used to protect shared resources by ensuring that only one thread or task can access the resource at any given time. Mutexes are ideal for ensuring **exclusive access** to a critical section of code.

- **What It Does**: A mutex locks access to a resource. When one thread locks a mutex, other threads attempting to lock it must wait until the mutex is unlocked by the original thread.

- **How It Works**: When a thread or task locks a mutex, other threads attempting to lock the same mutex are blocked until the mutex is unlocked. Only the thread that locked the mutex can unlock it.

- **When to Use**: Use a mutex when you need **exclusive access** to a shared resource, such as when modifying shared data structures (e.g., linked lists, buffers) or hardware registers.

  **Example**:

  .. code-block:: c

    static pthread_mutex_t lock;

    void critical_function(void)
    {
      pthread_mutex_lock(&lock);
      /* Critical section */
      pthread_mutex_unlock(&lock);
    }

**Semaphores**
A **semaphore** is a signaling mechanism and can be used to synchronize threads or tasks. Unlike mutexes, semaphores allow multiple threads or tasks to access a resource concurrently, depending on the semaphore count.

- **What It Does**: A semaphore has a counter that allows it to manage access to a pool of resources. Threads can increment or decrement the counter to signal that a resource is available or has been used.

- **How It Works**: Semaphores can either signal threads to wait or proceed depending on the counter value. A binary semaphore (with a counter of 1) behaves similarly to a mutex, while a counting semaphore allows multiple threads to access a shared resource up to the limit set by the counter.

- **When to Use**: Use semaphores when you need to manage **shared resources** that multiple threads can access simultaneously (e.g., a pool of connections, worker threads). Use them in **producer-consumer** models, where one task produces data and another consumes it.

  **Example**:

  .. code-block:: c

    static sem_t semaphore;

    void producer(void)
    {
      /* Produce data */
      sem_post(&semaphore); /* Signal consumer */
    }

    void consumer(void)
    {
      sem_wait(&semaphore); /* Wait for producer */
      /* Consume data */
    }

**Atomic Operations**
**Atomic operations** are a low-level synchronization mechanism that allows certain operations (such as incrementing a counter) to be performed without interference from other threads, without the overhead of using mutexes or semaphores. Atomic operations work directly on the memory in a thread-safe manner.

- **What It Does**: An atomic operation ensures that a specific operation (such as incrementing or comparing) happens **atomically**, meaning without interruption.

- **How It Works**: Atomic operations leverage hardware support to ensure that the operation completes in a single step, without the risk of being interrupted by another thread.

- **When to Use**: Use atomic operations when working with **simple data types** such as counters, flags, or booleans that multiple threads modify. They are highly efficient and should be preferred when the operation is simple and does not require more complex synchronization.

  **Example**:

  .. code-block:: c

    static atomic_int counter;

    void increment(void)
    {
      atomic_fetch_add(&counter, 1);
    }

When to Use RTOS Types, Mutexes, Semaphores, or Atomic Operations
-----------------------------------------------------------------

- **Use RTOS Types** when:
  
  - Developing for embedded systems like ESP32, where efficient task management and low overhead are crucial.
  
  - You need to leverage the real-time operating system's capabilities for task scheduling and synchronization.

- **Use Mutexes** when:
  
  - You need **exclusive access** to a shared resource (e.g., modifying a shared data structure).
  
  - The resource must only be accessed by one thread at a time.
  
  - The operation involves multiple steps that must all be done without interruption.

- **Use Semaphores** when:
  
  - You need to manage **multiple shared resources** that several threads can access concurrently (e.g., a pool of database connections).
  
  - You are implementing **producer-consumer** scenarios where tasks signal each other to proceed.

- **Use Atomic Operations** when:
  
  - You need to perform simple operations (e.g., incrementing a counter, flipping a flag) that need to be **thread-safe** without using locks.
  
  - The performance overhead of mutexes or semaphores is unnecessary due to the simplicity of the operation.

Task Management in ESP32
------------------------

In ESP32, FreeRTOS is the operating system that handles task scheduling, making it easy to create and manage multiple tasks.

- **FreeRTOS Tasks**: Tasks in FreeRTOS are lightweight threads that run concurrently. Each task should have its own stack, and the task's priority should be set based on its importance.

  Example:

  .. code-block:: c

    void task1(void *pvParameters)
    {
      while (1) {
        /* Task code */
        vTaskDelay(1000 / portTICK_PERIOD_MS); /* Delay for 1 second */
      }
    }

    void app_main(void)
    {
      xTaskCreate(task1, "Task 1", 2048, NULL, 5, NULL);
    }

- **Task Prioritization**: Set task priorities according to their criticality. Higher priority tasks will preempt lower priority ones, so avoid setting all tasks to high priority unless necessary.

- **Task Notifications and Queues**: Use task notifications or queues to communicate between tasks. This ensures that tasks can safely pass data to each other without race conditions.

  Example:

  .. code-block:: c

    static xQueueHandle queue;

    void producer_task(void *pvParameters)
    {
      int data = 42;
      while (1) {
        xQueueSend(queue, &data, portMAX_DELAY);
        vTaskDelay(1000 / portTICK_PERIOD_MS);
      }
    }

    void consumer_task(void *pvParameters)
    {
      int received_data;
      while (1) {
        xQueueReceive(queue, &received_data, portMAX_DELAY);
        /* Process data */
      }
    }

    void app_main(void)
    {
      queue = xQueueCreate(10, sizeof(int));
      xTaskCreate(producer_task, "Producer Task", 2048, NULL, 5, NULL);
      xTaskCreate(consumer_task, "Consumer Task", 2048, NULL, 5, NULL);
    }

Concurrency Best Practices
--------------------------

- **Use RTOS Types for Embedded Systems**: Leverage RTOS types like tasks, queues, and semaphores for efficient task management and synchronization in embedded systems.

- **Use Mutexes for Shared Resources**: Protect access to shared resources with mutexes or semaphores to avoid race conditions.

- **Minimize Critical Section Length**: Keep the duration of critical sections short to reduce lock contention between threads.

- **Use Atomic Operations for Simple Data**: When possible, use atomic operations for simple shared variables instead of mutexes to avoid the overhead of locking.

- **Task Prioritization**: Assign proper task priorities in multi-tasking environments. Avoid giving all tasks the same priority, as this can lead to task starvation or inefficient scheduling.

- **Avoid Deadlocks**: Be mindful of potential deadlocks when using multiple mutexes. Ensure that locks are acquired in a consistent order across different parts of the program.

- **Handle Interrupts Carefully**: Interrupt Service Routines (ISRs) should avoid performing complex tasks. Instead, use task notifications or queues to signal a task to handle the actual work after the ISR completes.

- **Concurrency Debugging**: Use FreeRTOS tracing or logging features to monitor task switching and detect issues like priority inversion, starvation, or excessive blocking.

General Guidelines
------------------

- **Minimize Use of Global State**: Avoid global variables to prevent race conditions. Instead, pass data through function arguments or use thread-local storage.

- **Prioritize Task Management**: Use task prioritization wisely to avoid starvation or inefficient scheduling. Ensure that critical tasks run at appropriate priority levels.

- **Protect Shared Resources**: Always use mutexes or semaphores when multiple tasks or threads access shared resources.

- **Use Atomic Operations for Simple Data**: For simple operations like counter increments, use atomic operations instead of mutexes for better performance.

- **Keep ISRs Simple**: Avoid complex logic in interrupt service routines. Use ISRs only to signal tasks, and let tasks handle the logic.

