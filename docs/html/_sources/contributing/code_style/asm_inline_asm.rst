ASM and Inline ASM
==================

In this project, **Assembly code** and **Inline Assembly** should be used with extreme caution. While it can offer performance improvements or enable access to low-level hardware features, its use can make code harder to understand, maintain, and port. Always prefer writing in C unless absolutely necessary.

General Guidelines for ASM and Inline ASM
-----------------------------------------

- **Avoid ASM When Possible**: Always try to write in C before resorting to assembly language. C compilers are highly optimized and can often produce efficient machine code that rivals hand-written assembly.

- **Document ASM Code Thoroughly**: Assembly code is often harder to understand than C, so it should be accompanied by thorough comments that explain **why** ASM was used, as well as what the code does.

Example:

.. code-block:: asm

    /* Set register to zero using ASM */
    mov r0, #0      /* Initialize r0 to 0 */

- **Use Inline ASM Sparingly**: Inline assembly allows you to embed assembly instructions directly in C code. It should only be used when absolutely necessary, such as when interacting with hardware registers or performing CPU-specific optimizations. 

- **Constrain the Scope of Inline ASM**: When using inline assembly, constrain its scope to as few lines as possible and avoid intermixing it with complex C logic. This helps isolate potential issues and reduces the risk of bugs.

Example:

.. code-block:: c

    void set_flag(void)
    {
        asm volatile("mov r0, #1" : : : "r0");  /* Set flag in register r0 */
    }

- **Always Use `volatile` for Inline ASM**: Inline assembly should be marked as `volatile` to prevent the compiler from optimizing it out.

- **Do Not Use Inline ASM for Optimizations**: Modern C compilers perform aggressive optimizations. Inline ASM should not be used to try and optimize code performance unless absolutely necessary, as it is often more error-prone than compiler optimizations.

- **Use Constraints Correctly**: When using inline ASM in C, use the appropriate constraints to inform the compiler how the assembly instructions interact with C variables.

Example:

.. code-block:: c

    int add(int a, int b)
    {
        int result;
        asm volatile(
            "add %[r], %[a], %[b]"
            : [r] "=r" (result)    /* Output */
            : [a] "r" (a), [b] "r" (b) /* Inputs */
        );
        return result;
    }

- **Prefer Named Registers**: Always use named registers or C variable references in inline ASM instead of hardcoding register names. This improves portability and makes it easier to understand how the assembly interacts with C.

- **Platform-Specific ASM**: If inline assembly or standalone ASM is used, ensure that it is documented as platform-specific and cannot be easily ported to other architectures.

Bad Example:
------------

.. code-block:: c

    asm("mov r0, #1");    /* INCORRECT: No constraints, platform-specific */

Good Example:
-------------

.. code-block:: c

    int set_register(int value)
    {
        asm volatile(
            "mov r0, %[val]"
            :
            : [val] "r" (value)
            : "r0"   /* CORRECT: Specifying the register and constraint */
        );
        return value;
    }

When to Use ASM and Inline ASM
------------------------------

- **Hardware Access**: Use ASM when direct hardware access is required and C alone cannot provide the necessary control (e.g., setting or clearing specific registers).

- **Performance Critical Code**: ASM may be justified in performance-critical sections where C compiler optimizations fall short, but this should be documented and used as a last resort.

- **CPU-Specific Instructions**: Use ASM for executing instructions that are unique to the target CPU (e.g., specific ARM or x86 instructions that are not exposed in C).

General Guidelines
------------------

- Avoid ASM unless absolutely necessary. 

- Use inline ASM for simple tasks like setting hardware registers, not for optimizations.

- Always use `volatile` for inline ASM to prevent it from being optimized out.

- Ensure thorough documentation for any assembly code, explaining both what the code does and why ASM is required.

- Use constraints in inline ASM to inform the compiler about register usage and interactions with C variables.

- Isolate inline ASM code from complex C logic, and keep it as minimal as possible.

- Make sure all ASM or inline ASM code is portable or clearly marked as platform-specific if not.


