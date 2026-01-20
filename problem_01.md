# Problem 01: The Advanced Text Editor Engine

## Problem Description
You are tasked with building the core logic for a text editor that supports infinite undo/redo history and efficient text manipulation. The editor must maintain the current state of the text while processing a stream of user actions.

### The System Rules
1.  **Text Buffer**: The editor maintains a single line of text.
2.  **Cursor System**:
    *   The cursor is always positioned *between* characters (or at the start/end).
    *   User actions (Insert/Delete) happen relative to the cursor.
3.  **History Management**:
    *   Every modification (Insert/Delete) is a "Action".
    *   **Undo**: Reverts the last action and moves it to the "Redo" stack.
    *   **Redo**: Re-applies the last undone action.
    *   **Destructive Action**: If a generic new action is performed while the Redo stack is non-empty, the Redo stack is **cleared** (standard editor behavior).
4.  **Batch Undo (Feature)**:
    *   If consecutive actions are of the same type (e.g., typing "Hello" is 5 insertions), they should be logically grouped so that a single `UNDO` removes the entire word "Hello".
    *   *Constraint*: A batch is broken if more than 2 seconds passes between keystrokes or the action type changes.

## Must Use Data Structures
*   **Doubly Linked List**: To store the text characters (allows O(1) insertions/deletions at cursor).
*   **Two Stacks**: `UndoStack` and `RedoStack` to manage history states.
*   **Custom "Action" Object**: To store details needed for reversal (e.g., "Deleted 'x' at index 5").

## Operations to Implement (CLI Commands)
*   `WRITE <char>`: Insert character at current cursor position.
*   `DELETE`: Delete character previous to cursor (Backspace).
*   `MOVE <left|right>`: Move cursor position.
*   `UNDO`: Revert last action (or batch).
*   `REDO`: Redo last reverted action.
*   `DISPLAY`: Show current text state and cursor position (e.g., `Hello|World`).

## Sample Execution

```text
> WRITE 'A'
> WRITE 'B'
> WRITE 'C'
Display: ABC|

> UNDO
Display: |
(Note: If batched, all ABC removed. If not, only C removed. Assume batched for this example)

> REDO
Display: ABC|

> MOVE left
Display: AB|C

> DELETE
Display: A|C

> UNDO
Display: AB|C
```
