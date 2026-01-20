# Problem 37: The Gap Buffer Editor

## Problem Description
Text editors like Emacs use a "Gap Buffer" or "Two Stack" approach to make typing efficient. Inserting a character in the middle of a 1MB file shouldn't require shifting 500KB of data.

### The System Rules
1.  **State**:
    *   **Left Stack**: Characters to the left of the cursor.
    *   **Right Stack**: Characters to the right of the cursor.
2.  **Typing**: Pushes to Left Stack.
3.  **Navigation**:
    *   **Move Left**: Pop Left -> Push Right.
    *   **Move Right**: Pop Right -> Push Left.
4.  **Backspace**: Pop Left.
5.  **Delete**: Pop Right.

## Must Use Data Structures
*   **Two Stacks**: Standard LIFO.

## Operations to Implement (CLI Commands)
*   `TYPE <char>`
*   `LEFT`, `RIGHT`
*   `BACKSPACE`
*   `SHOW`: Print LeftStack + "|" + RightStack (reversed).

## Sample Execution

```text
> TYPE H
> TYPE E
> TYPE Y
State: HEY|

> LEFT
State: HE|Y

> TYPE L
State: HEL|Y

> SHOW
HEL|Y (Printed as HELY with cursor between L and Y)
```
