
### Understanding Python's Logging System

#### Child and Parent Loggers

-   **Dual Handlers:** A log event sent to a **child logger** can be processed by **both the child's and parent's handlers**, depending on their respective levels and the child's **propagation setting**.

#### Logger Levels

-   **Severity Filtering:** The **level of a logger** determines which **severity of messages** it will handle. Messages with severity lower than the logger's level are ignored.

#### Handler Levels

-   **Output Filtering:** The **level of a handler** decides which messages it will format and output. Messages with severity lower than the handler's level are ignored.

#### Log Processing Flow

1.  **Message Arrival:** The message arrives at the logger.
2.  **Logger Level Check:** If the message's severity is lower than the logger's level, it's ignored. Otherwise, it's passed to all handlers.
3.  **Handler Level Check:** Each handler checks if the message's severity is lower than its level. If it is, the handler ignores the message. Otherwise, it passes the message to its formatter.
4.  **Formatting and Output:** The formatter formats the message, and the handler outputs it.
5.  **Propagation to Parent Handlers:** If propagation is enabled, the message is then sent to the parent logger's handlers.

#### Default Handler Behavior

-   **New Loggers:** New loggers created with `logging.getLogger(name)` don't have handlers attached by default.
-   **Propagation to Parent:** Log events from these loggers are propagated to parent loggers if `propagate` is `True`.

#### Handlers in Python's Logging Module

-   **Functionality:** Handlers manage the output of log messages to their final destinations (e.g., console, file).
-   **Multiple Handlers:** A logger can have multiple handlers, each with its own level and output format.

#### Hierarchy and Propagation

-   **Logger Hierarchy:** Loggers in Python form a hierarchy, with the root logger at the top.
-   **Event Propagation:** Log events are propagated up the hierarchy, controlled by the `propagate` attribute of loggers.

### Child loggers and their handlers:

A child logger is any logger that's not the root logger. A child logger can have its own handlers, which process log events handled by the child logger, and it inherits the handlers of its ancestors due to propagation. If a child logger doesn't have any handlers, and its propagate attribute is True, log events handled by the child logger are passed to its parent's handlers.

#### Root Logger and "Last Resort" Handler

-   **Top-Level Logger:** The root logger is at the top of the logger hierarchy.
-   **Fallback Handling:** If no handlers are configured in the hierarchy, the root logger's "last resort" handler, writing to `sys.stderr`, handles events. The default level of the "last resort" handler in Python's logging system is `WARNING`

#### Example: Logging with Child and Root Loggers


### Create a child logger with a handler
```
child = logging.getLogger('child')
child_handler = logging.StreamHandler()
child.addHandler(child_handler)
```

### Create a root logger with a different handler
```
root = logging.getLogger()
root_handler = logging.FileHandler('logfile.log')
root.addHandler(root_handler)
```

### Log a message with the child logger
```
child.warning("This is a warning message")
``` 

-   **Behavior:** The log event is processed by both the child's and the root's handlers, potentially leading to duplicate logs.

----------
