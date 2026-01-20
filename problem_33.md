# Problem 33: The Syntax Validator

## Problem Description
Code compilers need to check if parentheses are balanced before attempting to parse logic.

### The System Rules
1.  **Supported Pairs**: `()`, `[]`, `{}`.
2.  **Logic**:
    *   Open brackets pushed to storage.
    *   Close brackets must match the most recent Open bracket.
3.  **Error Reporting**:
    *   If mismatch: "Expected ], found } at index 5".
    *   If stack empty on close: "Unexpected } at index 0".
    *   If stack not empty at end: "Unclosed ( at index 3".

## Must Use Data Structures
*   **Stack**: Stores `Token` objects `{ char priority, int index }`.

## Operations to Implement (CLI Commands)
*   `VALIDATE "<code_string>"`

## Sample Execution

```text
> VALIDATE "{ [ ( ) ] }"
Valid.

> VALIDATE "{ [ }"
Error: Expected ], found } at index 4.

> VALIDATE "("
Error: Unclosed ( at index 0.
```
