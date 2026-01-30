# Problem 26: Multi-Priority Order Fulfillment Engine

## Problem Description

You are building the dispatch logic for a warehouse fulfillment center. Orders arrive with varying priority levels and must be processed efficiently while maintaining fairness guarantees.

### The System Rules

1. **Order Properties**: Each order has:
   - `Order ID`
   - `Priority` (1-5, where 5 is highest)
   - `Arrival Time`
   - `Items Count` (affects processing time)
2. **Priority Levels**: There are 5 priority tiers.
3. **Processing Logic**:
   - **Strict Priority**: Always process the highest priority order first.
   - **FIFO within Priority**: If multiple orders have the same priority, process in arrival order.
   - **Processing Time**: Each order takes `Items Count / 2` time units (rounded up).
4. **Fairness Constraint (Anti-Starvation)**:
   - If an order waits for more than `MAX_WAIT` time units without being processed, its priority is **boosted by 1** (up to a maximum of 5).
   - This prevents low-priority orders from starving indefinitely.

## Must Use Data Structures

- **Array of Queues**: One FIFO queue per priority level (5 queues total).
- **Min-Heap**: To track orders needing priority boost (keyed by `Arrival Time + MAX_WAIT`).
- **Array/Counters**: For statistics (total orders processed per priority, average wait time).

## Operations to Implement (CLI Commands)

- `ORDER <id> <priority> <items>`: Submit an order.
- `SET_MAX_WAIT <units>`: Configure the starvation threshold.
- `TICK`: Advance time. Apply boosts, pick next order, process.
- `REPORT`: Show orders processed, average wait by priority.

## Sample Execution

```text
> SET_MAX_WAIT 5

Assumptions for this trace:
- `ORDER` happens at the current time (sets `Arrival Time = current time`).
- Each `TICK` advances time by 1 and performs exactly 1 unit of work.
- At the start of each tick: apply any priority boosts, then (if idle) select the next order.
- An order's `wait time` is measured when it first starts processing: `start_time - arrival_time`.

> ORDER O1 1 4   (Priority 1, 4 items)   # needs ceil(4/2)=2 ticks
> ORDER O2 5 2   (Priority 5, 2 items)   # needs ceil(2/2)=1 tick
> ORDER O3 1 2   (Priority 1, 2 items)   # needs ceil(2/2)=1 tick

> TICK (Time 0 -> 1)
- Select O2 (Priority 5). Processing (1/1).
- O2 completes at Time 1. (Wait = 0)

> TICK (Time 1 -> 2)
- Select O1 (Priority 1, FIFO among Priority 1). Processing (1/2).

> ORDER O4 4 10  (Priority 4, 10 items)  # needs ceil(10/2)=5 ticks, Arrival Time = 2

> TICK (Time 2 -> 3)
- Continue O1. Processing (2/2).
- O1 completes at Time 3. (Wait = 1)

> TICK (Time 3 -> 4)
- Select O4 (Priority 4). Processing (1/5).

> TICK (Time 4 -> 5)
- Continue O4. Processing (2/5).

> TICK (Time 5 -> 6)
- Continue O4. Processing (3/5).

> TICK (Time 6 -> 7)
- O3 has waited 6 units (> MAX_WAIT=5). BOOSTED from Priority 1 -> Priority 2.
- Continue O4. Processing (4/5).

> TICK (Time 7 -> 8)
- Continue O4. Processing (5/5).
- O4 completes at Time 8. (Wait = 1)

> TICK (Time 8 -> 9)
- Select O3 (Priority 2, boosted). Processing (1/1).
- O3 completes at Time 9. (Wait = 8)

> REPORT
Priority 5: 1 processed. Avg Wait: 0.
Priority 4: 1 processed. Avg Wait: 1.
Priority 2: 1 processed (was boosted). Avg Wait: 8.
Priority 1: 1 processed. Avg Wait: 1.
```
