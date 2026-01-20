# Problem 41: The GPS Retracer

## Problem Description
A hiker is lost. They have a GPS log of every turn they made. Your system must calculate the exact reverse path to get them back to the start.

### The System Rules
1.  **Input Stream**: Steps like "Forward 10", "Turn Left", "Forward 5".
2.  **Reverse Logic**:
    *   The *last* action taken must be the *first* action reversed.
    *   **Inversion**:
        *   "Turn Left" -> "Turn Right"
        *   "Turn Right" -> "Turn Left"
        *   "Forward X" -> "Forward X"

## Must Use Data Structures
*   **Stack**: To store the path.

## Operations to Implement (CLI Commands)
*   `LOG <action>`
*   `CALCULATE_RETURN`: Read stack, invert, and print.

## Sample Execution

```text
> LOG FWD 100
> LOG LEFT
> LOG FWD 50

> CALCULATE_RETURN
1. FWD 50
2. RIGHT  (Inverse of LEFT)
3. FWD 100
```
