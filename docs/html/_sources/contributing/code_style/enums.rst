Enums
=====

Enums (enumerations) should be used to define a set of named integer constants, improving code readability and maintainability. Enums group related constants and make the code more self-explanatory. Follow these guidelines for using enums in this project.

General Guidelines for Enums
----------------------------

- **Enum Names Should End in `_t`**: All enum types should end with `_t` to indicate that they are typedefs, ensuring consistency across the project.

  Example:

  .. code-block:: c

    typedef enum {
      k_status_success,
      k_status_failure
    } status_t;

- **Use Snake Case for Enum Values**: All enum values should follow snake_case naming conventions, just like variables and function names.

  Example:

  .. code-block:: c

    typedef enum {
      k_connection_open,
      k_connection_closed,
      k_connection_fail
    } connection_status_t;

- **Use Descriptive Names for Enum Members**: Enum members should have descriptive names that convey their meaning. Avoid abbreviations or ambiguous terms.

  Example:

  .. code-block:: c

    typedef enum {
      k_color_red,
      k_color_green,
      k_color_blue
    } color_t;

- **Enum Values Should Start with `k_`**: To distinguish enum members from other constants or variables, enum values should start with `k_`. This helps with consistency and clarity in the code.

  Example:

  .. code-block:: c

    typedef enum {
      k_log_error,
      k_log_warning,
      k_log_info
    } log_level_t;

- **Assign Specific Values Only When Necessary**: Enum members are automatically assigned incremental values starting from `0`. Only assign specific values if they are necessary, such as for protocol definitions or when compatibility is required.

  Example:

  .. code-block:: c

    typedef enum {
      k_error_none  = 0,
      k_error_minor = 1,
      k_error_major = 2
    } error_level_t;

Example 1:
----------

Bad Example:

.. code-block:: c

    typedef enum {
      SUCCESS,
      FAILURE
    } STATUS; /* INCORRECT: Not using snake_case, enum name not ending with _t */

Good Example:

.. code-block:: c

    typedef enum {
      k_status_success,
      k_status_failure
    } status_t; /* CORRECT: Using snake_case and _t suffix */

Example 2:
----------

Bad Example:

.. code-block:: c

    typedef enum {
      SUCCESS,
      FAILURE
    } result_t; /* INCORRECT: Enum members not following snake_case */

Good Example:

.. code-block:: c

    typedef enum {
      k_result_success,
      k_result_failure
    } result_t; /* CORRECT: Enum members following snake_case and starting with k_ */

Example 3:
----------

Bad Example:

.. code-block:: c

    typedef enum {
      OPEN,
      CLOSED
    } door_state_t; /* INCORRECT: Enum values not descriptive and not following snake_case */

Good Example:

.. code-block:: c

    typedef enum {
      k_door_open,
      k_door_closed
    } door_state_t; /* CORRECT: Enum members are descriptive, follow snake_case, and starting with k_ */

General Guidelines
------------------

- Always use snake_case for both enum names and members.

- Enum types should end with `_t` and values should start with `k_` for clarity and consistency.

- Use descriptive names for enum members to improve readability.

- Only assign specific values to enum members when necessary.

