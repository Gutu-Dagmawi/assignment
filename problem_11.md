# Problem 11: The Smart Printer Spooler

## Problem Description
You are programming the firmware for a network printer shared by an entire office. The printer must balance fair usage with efficiency, ensuring small urgent jobs aren't blocked by massive unrelated reports.

### The System Rules
1.  **Job Attributes**: `ID`, `User`, `PageCount`, `IsColor`.
2.  **Scheduling Algorithm (Weighted Shortest Job First)**:
    *   Base Score = `PageCount`.
    *   Multiplier: Color jobs take 2x longer per page.
    *   **Priority Override**: Jobs from "Manager" role get their effective PageCount cut in half for scoring (processed sooner).
3.  **The Queue**:
    *   Jobs are executed based on lowest "Effective Cost" (Score).
    *   If scores are equal, First-Come-First-Serve (FIFO).
4.  **Interrupts**:
    *   The printer does NOT support preemption. Once a job starts, it finishes.

## Must Use Data Structures
*   **Min-Heap (Priority Queue)**: To store pending jobs, sorted by the calculated "Effective Cost" score.
*   **Hash Map**: To track total pages printed per User (for auditing/quota).

## Operations to Implement (CLI Commands)
*   `ADD_JOB <user> <pages> <color/bw>`: Submit a job.
*   `PRINT_NEXT`: Execute the highest priority job (smallest score).
*   `SHOW_QUEUE`: List pending jobs order.
*   `USER_STATS <user>`: Show total pages printed by user.

## Sample Execution

```text
> ADD_JOB Alice 50 BW      (Score: 50)
> ADD_JOB Bob 10 Color     (Score: 10 * 2 = 20)
> ADD_JOB Boss 40 BW       (Score: 40 / 2 = 20. Priority!)

> SHOW_QUEUE
1. Bob (Score 20) - Arrived first
2. Boss (Score 20)
3. Alice (Score 50)

> PRINT_NEXT
Printing Bob's job...
```
