# Style Guide
In the opsbox repos, we like to enforce a specific coding style.

It helps with documentation, readability, and maintenance.

## Documenting
### **Docstrings**
All classes and functions must have docstrings in [Google style](https://google.github.io/styleguide/pyguide.html#38-comments-and-docstrings). This ensures consistency and helps others understand your code.
```python
def example_function(param1: int, param2: str) -> bool:
    """
    Example function that demonstrates Google style docstrings.

    Args:
        param1 (int): The first parameter.
        param2 (str): The second parameter.

    Returns:
        bool: The return value. True for success, False otherwise.

    Raises:
        ValueError: Condition where ValueError is returned.
    """
    return True
```


### **Comments**
Comments should be added:

- When it is unclear why a section of code is used.
- When the function of the code is unclear.
- When control flow is unclear.


### **Docs**
Docs should be added in this repo for plugins and changes to core.

This can be done by modifying the `mkdocs.yml` file located at the root of this repo, alongside the addition of new documentation markdown of *high quality*.

For more information on how to contribute to the documentation, refer to the [MkDocs documentation](https://www.mkdocs.org/user-guide/writing-your-docs/).

## Typing

***Whenever possible***, try to implement the proper python types you expect you function to give an return.

It helps with keeping code clean, avoiding simple type errors, and in the future can allow for optimization.

For more information on type hints in Python, refer to the [Python documentation on type hints](https://docs.python.org/3/library/typing.html).

## Logging
For logging, we use the excellent loguru package.

**Loguru** is an elegant and straightforward logging library for Python, designed to simplify logging without boilerplate code.

It provides a simple logger that can be imported from the package itself, and logs can be added by calling the `logger.<log_level>("message")` function.

```python
from loguru import logger

logger.debug("This is a debug message")
```

### Loguru Logging Levels

Loguru provides several logging levels to categorize log messages based on their severity and purpose. Properly using these levels ensures that logs are meaningful and manageable.


| Level    | Description                                                                 |
|----------|-----------------------------------------------------------------------------|
| TRACE    | Detailed information, typically of interest only when diagnosing problems.  |
| DEBUG    | General debugging information.                                              |
| INFO     | Confirmation that things are working as expected.                           |
| SUCCESS  | Confirmation of successful operations or significant milestones.            |
| WARNING  | An indication that something unexpected happened or indicative of some problem. |
| ERROR    | Serious problems preventing the software from performing some function.    |
| CRITICAL | Very serious errors that may lead the program to abort.                     |

### When to Use Each Level
`TRACE`

- **Purpose:** Fine-grained informational events useful for diagnosing problems.
- **Use Cases:**
    - State changes of commonly called, low-variability code or private functions.
    - Directly displaying variable values (though binding is preferred for very large data).
    - Tracing state throughout the code.

**Example:**

```python
logger.trace("Entering function calculate_sum with arguments: a={}, b={}", a, b)
```

`DEBUG`

- **Purpose:** General debugging information.
- **Use Cases:**
    - Function or class-level state changes.
    - Alerts of different branches taken by control flows relying on user configuration.

**Example:**

```python
logger.debug("User data loaded: {}", user_data)
```

`INFO`

- **Purpose:** Confirmation that things are working as expected.
- **Use Cases:**
    - User-notifying messages and high-level state changes.
    - Startup messages and other informational messages.

**Example:**

```python
logger.info("Server started on port {}", port)
```

`SUCCESS`

- **Purpose:** Indication of user-visible success of any task or significant milestone.
- **Use Cases:**
    - Indicating successful completion of tasks.
    - Milestone achievements in processes.

**Example:**

```python
logger.success("Data synchronization completed successfully")
```

`WARNING`

- **Purpose:** Indication that something unexpected happened or indicative of some problem.
- **Use Cases:**
    - Deprecated API usage.
    - Temporary issues that do not halt execution.
    - Potentially problematic situations.

**Example:**

```python
logger.warning("Disk space running low: {}% remaining", disk_space)
```

`ERROR`

- **Purpose:** Serious problems preventing the software from performing some function.
- **Use Cases:**
    - Exceptions that are caught but require attention.
    - Failed operations that do not crash the application.

**Example:**

```python
logger.error("Failed to connect to database: {}", error)
```

`CRITICAL`

- **Purpose:** Very serious errors that may lead the program to abort.
- **Use Cases:**
    - Unhandled exceptions.
    - System failures.
    - Critical resource unavailability.

**Example:**

```python
logger.critical("Application crashed due to unexpected error: {}", error)
```

### Using `extra` for Contextual Data

***Avoid putting large amounts of raw data directly in log messages.*** Instead, encapsulate data in a dictionary with corresponding keys and bind it to the logger using the `extra` parameter. 

This approach maintains log message clarity and structure.

This also allows for verbose logging using the `--verbose` argument, where these extra dictionaries will be shown to the user.

Using `extra` directly:

```python
logger.info("User logged in", extra={"user_id": 123})
```

### Structured Logging

Structured logging involves logging data in a structured format (like JSON), making it easier to parse and analyze.
This can be enabled with our `--log_file "PATH"` argument.

### Enriching Logs with Exception Information

Loguru automatically captures exception details when using `logger.exception` within an `except` block.

**Example:**

```python
try:
    risky_operation()
except Exception as e:
    logger.exception("An error occurred during risky_operation")
```


### Best Practices for Logging

Adhering to best practices ensures that your logging is effective, efficient, and secure.

- **Consistency:** Use logging levels consistently across the project to maintain clarity.
- **Avoid Overlogging:** Excessive logging, especially at lower levels like `TRACE` and `DEBUG`, can lead to performance issues and large log files.
- **Critical vs. Non-critical:** Reserve `CRITICAL` for issues that truly warrant immediate attention.
- **Clarity:** Messages should clearly describe what is happening.
- **Context:** Include relevant variables and state information using `extra`.
- **Avoid Redundancy:** Do not repeat information unnecessarily.

**Good Example:**

```python
logger.info("User {} created a new order with ID {}", user_id, order_id)
```

**Bad Example:**

```python
logger.info("Order created")
```