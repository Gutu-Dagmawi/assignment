# Problem 26: Multi-Priority Order Fulfillment Engine

## Problem Description
You are building the dispatch logic for a warehouse fulfillment center. Orders arrive with varying priority levels and must be processed efficiently while maintaining fairness guarantees.

### The System Rules
1.  **Order Properties**: Each order has:
    *   `Order ID`
    *   `Priority` (1-5, where 5 is highest)
    *   `Arrival Time`
    *   `Items Count` (affects processing time)
2.  **Priority Levels**: There are 5 priority tiers.
3.  **Processing Logic**:
    *   **Strict Priority**: Always process the highest priority order first.
    *   **FIFO within Priority**: If multiple orders have the same priority, process in arrival order.
    *   **Processing Time**: Each order takes `Items Count / 2` time units (rounded up).
4.  **Fairness Constraint (Anti-Starvation)**:
    *   If an order waits for more than `MAX_WAIT` time units without being processed, its priority is **boosted by 1** (up to a maximum of 5).
    *   This prevents low-priority orders from starving indefinitely.

## Must Use Data Structures
*   **Array of Queues**: One FIFO queue per priority level (5 queues total).
*   **Min-Heap**: To track orders needing priority boost (keyed by `Arrival Time + MAX_WAIT`).
*   **Array/Counters**: For statistics (total orders processed per priority, average wait time).

## Operations to Implement (CLI Commands)
*   `ORDER <id> <priority> <items>`: Submit an order.
*   `SET_MAX_WAIT <units>`: Configure the starvation threshold.
*   `TICK`: Advance time. Apply boosts, pick next order, process.
*   `REPORT`: Show orders processed, average wait by priority.

## Sample Execution

```text
> SET_MAX_WAIT 5

> ORDER O1 1 4   (Priority 1, 4 items)
> ORDER O2 5 2   (Priority 5, 2 items)
> ORDER O3 1 2   (Priority 1, 2 items)

> TICK (Time 0 -> 1)
- O2 (Priority 5) selected. Processing (0/1).

> TICK (Time 1 -> 2)
- O2 completed.
- O1 (Priority 1, waiting 1). O3 (Priority 1, waiting 1).
- Picking O1 (arrived first). Processing (0/2).

... (Time advances, O3 waits) ...

> TICK (Time 6 -> 7)
- O3 has waited 6 units (> MAX_WAIT=5). BOOSTED to Priority 2.
- Processing continues on current order...

> REPORT
Priority 5: 1 processed. Avg Wait: 0.
Priority 2: 1 processed (was boosted). Avg Wait: 6.
Priority 1: 1 processed. Avg Wait: 1.
```
