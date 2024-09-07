Enums
=====

Enums (enumerations) should be used to define a set of named integer constants, improving code readability and maintainability. Enums group related constants and make the code more self-explanatory. Follow these guidelines for using enums in this project.

General Guidelines for Enums
----------------------------

- **Enum Names Should End in `_t`**: All enum types should end with `_t` to indicate that they are typedefs, ensuring consistency across the project.

  Example:

  .. code-block:: c

    typedef enum {
      status_success_e,
      status_failure_e
    } status_t;

- **Use Snake Case for Enum Values**: All enum values should follow snake_case naming conventions, just like variables and function names.

  Example:

  .. code-block:: c

    typedef enum {
      connection_open_e,
      connection_closed_e,
      connection_failed_e
    } connection_status_t;

- **Use Descriptive Names for Enum Members**: Enum members should have descriptive names that convey their meaning. Avoid abbreviations or ambiguous terms.

  Example:

  .. code-block:: c

    typedef enum {
      color_red_e,
      color_green_e,
      color_blue_e
    } color_t;

- **Enum Values Should End with `_e`**: To distinguish enum members from other constants or variables, enum values should end with `_e`. This helps with consistency and clarity in the code.

  Example:

  .. code-block:: c

    typedef enum {
      log_error_e,
      log_warning_e,
      log_info_e
    } log_level_t;

- **Assign Specific Values Only When Necessary**: Enum members are automatically assigned incremental values starting from `0`. Only assign specific values if they are necessary, such as for protocol definitions or when compatibility is required.

  Example:

  .. code-block:: c

    typedef enum {
      error_none_e  = 0,
      error_minor_e = 1,
      error_major_e = 2
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
      status_success_e,
      status_failure_e
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
      result_success_e,
      result_failure_e
    } result_t; /* CORRECT: Enum members following snake_case and ending with _e */

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
      door_open_e,
      door_closed_e
    } door_state_t; /* CORRECT: Enum members are descriptive, follow snake_case, and end with _e */

General Guidelines
------------------

- Always use snake_case for both enum names and members.

- Enum types should end with `_t` and values with `_e` for clarity and consistency.

- Use descriptive names for enum members to improve readability.

- Only assign specific values to enum members when necessary.

