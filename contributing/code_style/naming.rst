Naming
======

Choosing clear and meaningful names for variables, functions, classes, and other identifiers is crucial in any project, especially one with many contributors:

- **Clarity**: Good names provide clarity about the purpose and functionality of code elements. Descriptive names make it easier for others (and your future self) to understand the code without needing to dig through the implementation.

- **Consistency**: Using a consistent naming convention across the project ensures that all developers follow the same rules, making the codebase uniform. The following conventions should be followed:

  - **Static Declarations**: Any variable or function that is only used in a single source file should be declared `static`. Static variables should be prefixed with `s_` for easy identification (e.g., `static bool s_invert`).
  
  - **Namespacing**: Public names (non-static variables and functions) should be namespaced with a per-component or per-unit prefix to avoid naming collisions. For example, use `mycomp_vfs_register()` or `mycomp_console_run()` to clearly indicate the source of the function or variable. If a prefix like `mycomp_` is chosen, it should be consistent across all names within that component.
  
  - **Enum and Struct Typedefs**: All enums and structs should use snake_case and end with `_t` to indicate they are typedefs (e.g., `error_code_t`, `my_struct_t`).

  - **Enum Values**: Enum values should start with `k_` to distinguish them from other identifiers (e.g., `k_success`, `k_failure`).

  - **Variable and Function Naming**: Use snake_case for variable and function names (e.g., `my_function`, `my_variable`).

  - **Constants**: Constants should always be used where applicable (e.g., `max_length`).

  - **Avoid Abbreviations**: Avoid unnecessary abbreviations (e.g., shortening `data` to `dat`) unless the resulting name would be excessively long. This ensures that names remain clear and understandable.

- **Avoiding Conflicts**: Clear and distinct names reduce the likelihood of naming conflicts, which can lead to bugs or confusion. Names should avoid being too generic (e.g., `temp` or `data`) and instead reflect the specific role of the entity.

- **Contextual Meaning**: Names should reflect the context in which they are used. For instance, a variable holding a user's first name should be called `first_name` instead of something vague like `str1`. This helps other developers quickly grasp the intent of the code.

- **Searchability**: Meaningful names make the codebase easier to search through. Contributors can quickly locate relevant code by searching for terms related to the functionality they are working on.

- **Scalability**: As the project grows, a thoughtful naming convention ensures the code remains understandable. Properly named classes, methods, and variables contribute to a well-structured, scalable codebase that can accommodate new features and improvements without confusion.

Bad Example
-----------

.. code-block:: c

    /* Bad code with inconsistent naming and unclear purpose */

    int  temp;  /* Unclear variable name */
    bool invert;  /* Should be static since it is only used in this file */
    enum Status { OK, ERROR };  /* Enum without suffix and unclear names */

    void doSomething(int a)
    {  
      if (a > 0) {
        temp = 10;
      } else {
        temp = -1;
      }
    }

    int foo;  /* Global variable without a clear prefix or name */

    void function(void)
    {
      foo = temp + 1;  /* Vague variable usage */
    }


Issues in the bad example:

- The variable `temp` is too vague, giving no context about what it represents.

- `invert` should be declared as `static` because it's only used in this file.

- Enum values `OK` and `ERROR` lack proper suffixes and are too generic.

- Function name `doSomething` doesn't describe its action.

- The global variable `foo` has no clear purpose or prefix to indicate its scope or function.

---

Good Example
------------

.. code-block:: c

    /* Good code with consistent naming and clarity */

    static bool s_invert;  /* Static variable with s_ prefix to indicate file scope */

    typedef enum status_t {  /* Enum with snake_case and _t suffix */
      k_success,
      k_failure
    } status_t;

    static int s_threshold = 0;  /* Declare static threshold at file scope */

    static void process_input(int input_value)
    {  
      /* Clear variable name and static scope for file use */
      if (input_value > 0) {
        s_threshold = 10;
      } else {
        s_threshold = -1;
      }
    }

    static void calculate_output(void)
    {  
      int result = 0;  /* Clear, descriptive variable usage */
      result     = s_threshold + 1;
    }


In the good example:

- `s_invert` is declared static with a clear prefix.

- The `status_t` enum uses snake_case and ends with `_t`, with enum values starting with `k_`.

- The function name `process_input` clearly describes its purpose.

- Variables like `s_threshold` and `result` have meaningful names, indicating their roles in the logic.

- No unnecessary global variables are used, and static variables are properly prefixed for clarity.

