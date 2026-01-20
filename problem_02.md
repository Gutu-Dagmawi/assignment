# Problem 02: Hierarchical Task Processor

## Problem Description
You are designing a logic engine to process a stream of tasks with varying priorities. The system uses a multi-tiered queue structure to manage execution order efficiently.

### The System Rules
1.  **Queue Tiers**: The system maintains 3 distinct processing queues:
    *   **High Priority (Queue A)**
    *   **Medium Priority (Queue B)**
    *   **Low Priority (Queue C)**
2.  **Execution Policy**:
    *   The processor always selects the first task from **Queue A**.
    *   If Queue A is empty, it selects from **Queue B**.
    *   If both A and B are empty, it selects from **Queue C**.
3.  **Dynamic Movement Rules (Demotion)**:
    *   Tasks in **Queue A** are allowed **2 units** of processing time per turn. If a task is not finished after 2 units, it is paused and moved to the back of **Queue B**.
    *   Tasks in **Queue B** are allowed **4 units** of processing time. If not finished, it is paused and moved to the back of **Queue C**.
    *   Tasks in **Queue C** run until completion (or until a higher priority task arrives and preempts them, if you implement preemption).
4.  **Aging Rule (Promotion)**:
    *   To prevent tasks from being stuck in Queue C forever, any task that has been waiting in **Queue C** for more than **15 time units** (without running) must be effectively reset: move it to the back of **Queue A**.
5.  **Delayed Entry**:
    *   Some tasks are scheduled to arrive in the future. They sit in a "Pending Area" until the system clock reaches their `arrival_time`, at which point they are added to **Queue A**.

## Must Use Data Structures
*   **Array (or List) of Queues**: To perform the cascaded checks (Check A, then B, then C) in a structured way.
*   **Min-Heap**: To manage the "Pending Area" where tasks are stored sorted by their `arrival_time`.
*   **Hash Maps / Dictionary**: Optional, but useful if you need to track the "total wait time" of tasks in Queue C efficiently.

## Operations to Implement (CLI Commands)
*   `SCHEDULE_TASK <id> <total_work_needed> <arrival_time>`: Add a task to the Pending Area.
*   `TICK`: Advance the system clock by 1 unit.
    *   Check for arriving tasks (Pending -> Queue A).
    *   Run the selected task for 1 unit.
    *   Apply Demotion rules if the task used up its allowance.
    *   Apply Aging rules for tasks in Queue C.
*   `STATUS`: Print the contents of all 3 queues and the Pending Area.

## Sample Execution

```text
> SCHEDULE_TASK T1 10 0  (T1 needs 10 units, arrives at 0)
> SCHEDULE_TASK T2 4 2   (T2 needs 4 units, arrives at 2)

> TICK (Time 0 -> 1)
- T1 arrives -> Queue A.
- Processing T1 (Queue A). Remaining: 9. Used in tier: 1.

> TICK (Time 1 -> 2)
- Processing T1 (Queue A). Remaining: 8. Used in tier: 2.
- Limit Reached (2 units). T1 moved to Queue B.

> TICK (Time 2 -> 3)
- T2 arrives -> Queue A.
- System checks queues: Queue A has T2. Queue B has T1.
- Processing T2 (Queue A). Remaining: 3. Used in tier: 1.

...

> STATUS
Time: 5
Pending: []
Queue A: []
Queue B: [T1 (Remaining: 8)]
Queue C: []
Processing: T2
```
