# Problem 54: Call Stack Debugger Simulator

## Problem Description
You are building a debugging tool that visualizes and tracks the call stack of a running program, including variable scopes and stack overflow detection.

### The System Rules
1.  **Stack Frame Properties**:
    *   `Function Name`
    *   `Local Variables` (name-value pairs)
    *   `Return Address` (line number to return to)
    *   `Caller Frame` (reference to parent)
2.  **Operations**:
    *   **CALL**: Push a new frame onto the stack.
    *   **RETURN**: Pop the current frame and return to caller.
    *   **SET_VAR**: Set a variable in the current frame.
    *   **GET_VAR**: Get a variable (search current frame, then parent frames — scope chain).
3.  **Limits**:
    *   Maximum stack depth `D`. If exceeded, report "Stack Overflow".
4.  **Debug Features**:
    *   Print full stack trace at any point.
    *   Show current scope chain for variable lookup.

## Must Use Data Structures
*   **Stack**: The call stack itself (each element is a frame).
*   **Array/Hash Map per Frame**: To store local variables.
*   **Linked List** (Optional): For scope chain traversal.
*   **Queue** (Optional): For recording call history/trace.

## Operations to Implement (CLI Commands)
*   `SET_MAX_DEPTH <d>`: Configure stack limit.
*   `CALL <function>`: Enter a function.
*   `RETURN`: Exit current function.
*   `SET <var> <value>`: Set local variable.
*   `GET <var>`: Get variable (with scope chain lookup).
*   `TRACE`: Print full stack trace.

## Sample Execution

```text
> SET_MAX_DEPTH 5

> CALL main
Entered: main. Depth: 1.

> SET x 10
x = 10 in main.

> CALL helper
Entered: helper. Depth: 2.

> SET y 20
y = 20 in helper.

> GET x
x = 10 (found in parent frame: main).

> GET z
Error: Variable 'z' not found in scope chain.

> TRACE
Stack Trace:
  [2] helper (current)
      y = 20
  [1] main
      x = 10

> RETURN
Returned from helper. Depth: 1. Current: main.

> CALL foo
> CALL bar
> CALL baz
> CALL qux
Entered: qux. Depth: 5.

> CALL overflow
Error: Stack Overflow! Max depth (5) exceeded.
```
