# Problem 50: Buffered Keyboard Input Handler

## Problem Description
You are implementing a keyboard input buffer for an embedded system where keystrokes arrive faster than the CPU can process them.

### The System Rules
1.  **Buffer Properties**:
    *   Fixed-size circular buffer of capacity `C`.
    *   Keystrokes are added to the buffer as they arrive.
    *   If the buffer is full, new keystrokes are DROPPED.
2.  **Processing**:
    *   The CPU processes `P` keystrokes per tick (configurable).
    *   Processed keystrokes are removed from the buffer (FIFO).
3.  **Special Keys**:
    *   **BACKSPACE**: Removes the most recently ADDED key (not processed yet) — requires Stack-like behavior on the buffer tail.
    *   **ENTER**: Flushes all buffered keys to output immediately.
4.  **Metrics**:
    *   Keystroke drop rate.
    *   Average buffer occupancy.

## Must Use Data Structures
*   **Circular Array (Deque)**: Allows both FIFO processing and LIFO backspace.
*   **Queue**: For the output stream of processed characters.
*   **Counters**: For metrics tracking.
*   **Stack** (Optional): For undo history of processed keys.

## Operations to Implement (CLI Commands)
*   `CONFIG <capacity> <process_rate>`: Set buffer size and processing rate.
*   `KEY <char>`: A keystroke arrives.
*   `BACKSPACE`: Remove last unprocessed key.
*   `ENTER`: Flush buffer to output.
*   `TICK`: Process keys.
*   `OUTPUT`: Show processed output.
*   `METRICS`: Show drop rate and occupancy.

## Sample Execution

```text
> CONFIG 5 2

> KEY H
> KEY E
> KEY L
> KEY L
> KEY O
Buffer: [H, E, L, L, O] (5/5)

> KEY !
DROPPED: Buffer full.

> BACKSPACE
Removed: O
Buffer: [H, E, L, L] (4/5)

> TICK
Processed: H, E
Buffer: [L, L] (2/5)

> KEY !
Buffer: [L, L, !] (3/5)

> ENTER
Flushed: L, L, !
Buffer: [] (0/5)

> OUTPUT
Output Stream: H E L L !

> METRICS
Dropped: 1, Total: 7, Drop Rate: 14.3%
Avg Occupancy: 3.5/5
```
