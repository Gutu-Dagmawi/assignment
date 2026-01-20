# Problem 29: The 911 Dispatch Controller

## Problem Description
Optimize the dispatch of emergency units. Calls have severity (1=Critical to 5=Low). The system must always handle the most critical situation next.

### The System Rules
1.  **Priority**: Lower number = Higher Importance (1 > 5).
2.  **Stability**:
    *   If two calls have Severity 1, the one that arrived *earlier* must be handled first.
    *   Standard Heaps are unstable, so you must implement logic to preserve arrival order.
3.  **Dynamic Updates**:
    *   Condition worsening: A Severity 3 call might escalate to Severity 1 while waiting.

## Must Use Data Structures
*   **Min-Heap**: Organized by `Compare(Severity, ArrivalTime)`.
*   **Hash Map**: To locate specific calls in the heap for Escalation/Updates.

## Operations to Implement (CLI Commands)
*   `CALL <id> <severity>`: Incoming call.
*   `DISPATCH`: Assign unit to top call.
*   `ESCALATE <id> <new_severity>`: Update priority.

## Sample Execution

```text
> CALL A 3 (Time 0)
> CALL B 1 (Time 1)
> CALL C 1 (Time 2)

> DISPATCH
Handling B (Sev 1, Time 1) - Wait, why B? Because 1 < 3.
Between B and C? B arrived first.

> ESCALATE A 1
A is now Sev 1. Time was 0.
Heap state: [A(1,0), C(1,2)] (B is gone).

> DISPATCH
Handling A (Sev 1, Time 0).
```
