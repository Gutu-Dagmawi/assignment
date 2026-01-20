# Problem 40: Dynamic Checkout Lane Optimizer

## Problem Description
You are managing a supermarket checkout system with dynamic lane opening/closing, customer routing, and performance tracking.

### The System Rules
1.  **Lane Properties**:
    *   Each lane has a unique ID and a status (OPEN/CLOSED).
    *   Each lane maintains a FIFO queue of customers.
    *   Processing time per customer = `Items Count / 5` time units (rounded up).
2.  **Customer Routing**:
    *   New customers join the lane with the **shortest queue** (fewest customers, not items).
    *   If tie, choose the lane with the lowest ID.
3.  **Dynamic Lane Management**:
    *   **Open Lane**: Add a new lane.
    *   **Close Lane**: Stop accepting new customers. Finish serving current queue, then fully close.
4.  **Metrics**:
    *   Average wait time per customer.
    *   Lane utilization (time busy / total time).

## Must Use Data Structures
*   **Array of Queues**: One queue per checkout lane.
*   **Min-Heap**: To quickly find the lane with the shortest queue.
*   **Linked List** (Optional): For dynamic lane addition/removal.
*   **Array/Counters**: For metrics tracking.

## Operations to Implement (CLI Commands)
*   `OPEN_LANE`: Open a new lane.
*   `CLOSE_LANE <id>`: Close a lane (finishes existing customers first).
*   `CUSTOMER <items>`: A customer arrives with a given item count.
*   `TICK`: Advance time. Process customers.
*   `METRICS`: Show wait times and utilization.

## Sample Execution

```text
> OPEN_LANE
Lane 1 opened.

> OPEN_LANE
Lane 2 opened.

> CUSTOMER 10
Customer C1 (10 items) -> Lane 1 (queue: 0).

> CUSTOMER 5
Customer C2 (5 items) -> Lane 2 (queue: 0).

> CUSTOMER 8
Customer C3 (8 items) -> Lane 1 (queue: 1).

> TICK (Time 0 -> 1)
Lane 1: Processing C1 (1/2 done).
Lane 2: Processing C2 (1/1 done). C2 served!

> TICK (Time 1 -> 2)
Lane 1: C1 served!
Lane 2: Idle.

> CLOSE_LANE 2
Lane 2 closing (0 customers remaining).

> METRICS
Avg Wait Time: 0.5 ticks
Lane 1 Utilization: 100%
Lane 2 Utilization: 50%
```
