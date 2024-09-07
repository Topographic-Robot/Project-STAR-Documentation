Static and Const
================

Using `static` and `const` effectively can improve code safety, performance, and readability. As a general rule, always use `static` and `const` when possible.

Using `const` over Macros
-------------------------

Using `const` globals is generally better than using macros for several reasons:

1. **Type Safety**: `const` variables have a defined type, so the compiler can catch type-related errors, whereas macros are simple text replacements without type checking.
  
2. **Scoping**: `const` globals respect C scoping rules, whereas macros are globally visible after being defined and can cause naming conflicts or unexpected behavior.

3. **Debugging**: `const` variables appear in debugging information, while macros do not, making it harder to trace issues with macros.

4. **Better readability**: `const` variables make the code clearer and more maintainable, as their intent is explicit compared to macros, which can be obscure.

For most situations, it's preferable to use `const` globals, unless you need text substitution or preprocessor directives, in which case macros might be more appropriate.

Example 1:
----------

Bad Example:

.. code-block:: c

    #define MAX_SIZE 100   /* INCORRECT, using a macro for a constant */

Good Example:

.. code-block:: c

    const int c_max_size = 100;   /* Correct, using a const global */

Using `static` for Internal Linkage
-----------------------------------

- **`static` Variables**: Variables and functions that are only used within a single source file should be declared `static`. This ensures internal linkage and avoids accidental linkage in other parts of the project.

Example 2:
----------

Bad Example:

.. code-block:: c

    int internal_counter = 0;   /* INCORRECT, lacks static for internal use */

    void increment_counter(void) {
        internal_counter++;
    }

Good Example:

.. code-block:: c

    static int s_internal_counter = 0;   /* Correct, using static for internal use */

    static void increment_counter(void) {
        s_internal_counter++;
    }

**General Guidelines**:

- Always prefer `const` to macros when declaring constants.

- Always use `static` for variables and functions that are only used within a single source file to limit scope and avoid name collisions.

