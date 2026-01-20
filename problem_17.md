# Problem 17: The Time-Traveling Queue

## Problem Description
Queue operations are usually permanent. You need to design a special queue for a transactional system where every action can be "rolled back" (undone) in reverse order.

### The System Rules
1.  **Core Operations**: `ENQUEUE(x)` and `DEQUEUE()`.
2.  **Undo Capability**:
    *   The system tracks the history of operations.
    *   `UNDO`: Reverts the *most recent* queue modification.
    *   **Logic**:
        *   Undo of `ENQUEUE(x)` -> Remove `x` from the back (Requires Deque).
        *   Undo of `DEQUEUE()` which returned `y` -> Push `y` back to the front.
3.  **Constraint**:
    *   You must handle generic data types.
    *   Unlimited undo history (bounded only by memory).

## Must Use Data Structures
*   **Double-Ended Queue (Deque)**: Actual storage (needs removal from back for undoing enqueue).
*   **Stack**: Stores `Operation` objects (Type: ADD/REMOVE, Value: Data) to track history.

## Operations to Implement (CLI Commands)
*   `ADD <val>`: Enqueue.
*   `REMOVE`: Dequeue.
*   `UNDO`: Revert last op.
*   `PRINT`: Show queue contents.

## Sample Execution

```text
> ADD 1
> ADD 2
Q: [1, 2]

> REMOVE
Returned 1.
Q: [2]

> UNDO
Reverting REMOVE(1)... Pushed 1 to front.
Q: [1, 2]

> UNDO
Reverting ADD(2)... Removed 2 from back.
Q: [1]
```
