# Problem 57: The Sorted Contact Browser

## Problem Description
Before touchscreens, phones had physical "Up/Down" buttons to scroll through contacts. The list had to remain sorted at all times.

### The System Rules
1.  **Storage**: Contact `Name` and `Phone`.
2.  **Ordering**: Alphabetical by Name.
3.  **Cursor**: System remembers the "Selection".
    *   `ADD`: Insert "Charlie" into the correct spot.
    *   `NEXT/PREV`: Move cursor.
    *   `DELETE`: Remove currently selected contact.

## Must Use Data Structures
*   **Doubly Linked List**:
    *   Reason: Arbitrary insertion (once location found) is O(1).
    *   Reason: Bi-directional traversal.

## Operations to Implement (CLI Commands)
*   `ADD <name> <phone>`: Find spot, insert.
*   `SCROLL_DOWN`: Move cursor to next.
*   `SCROLL_UP`: Move cursor to prev.
*   `DELETE_CURRENT`
*   `SHOW_CURRENT`: Display details of selection.

## Sample Execution

```text
> ADD "Alice" ...
> ADD "Charlie" ...
> ADD "Bob" ...
Internal List: Alice <-> Bob <-> Charlie

> SCROLL_DOWN (starts at Head=Alice)
Now at Bob.
> SCROLL_DOWN
Now at Charlie.

> DELETE_CURRENT
Charlie deleted. Cursor moves to Bob (or null).
```
