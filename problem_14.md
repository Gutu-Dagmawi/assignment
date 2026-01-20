# Problem 14: Distributed File Compression Pipeline

## Problem Description
You are building the job manager for a distributed file compression service. Files arrive with varying sizes, and multiple compression workers are available. The system must optimize throughput, track job history, and support job cancellation.

### The System Rules
1.  **Job Properties**: Each file has:
    *   `File ID`
    *   `Size` (in MB)
    *   `Submission Time`
    *   `Status` (Pending, Processing, Completed, Cancelled)
2.  **Scheduling Policy**:
    *   **Smallest Job First (SJF)**: Prioritize smaller files as they complete faster, maximizing the number of completed jobs per unit time.
    *   **Worker Pool**: You have `W` workers. A worker picks the next smallest pending job and processes it for `Duration = Size / 10` time units.
3.  **Advanced Features**:
    *   **Cancellation**: A pending job can be cancelled. A processing job cannot be cancelled but can be marked to *not* retry on failure.
    *   **History Log**: Maintain a log of the last `H` completed/cancelled jobs for auditing.
    *   **Retry Queue**: If a job fails (simulate with a flag), it goes to a separate "Retry Queue" and is re-attempted after all pending jobs are done.

## Must Use Data Structures
*   **Min-Heap**: For the Pending Jobs queue (ordered by Size).
*   **Queue (FIFO)**: For the Retry Queue.
*   **Circular Array**: For the fixed-size History Log of completed/cancelled jobs.
*   **Array/List**: To track worker states (Idle, Busy with Job X).

## Operations to Implement (CLI Commands)
*   `SUBMIT <file_id> <size>`: Add a file to the pending queue.
*   `SET_WORKERS <w>`: Set number of workers.
*   `TICK`: Advance time. Assign jobs to free workers, process active jobs, check for completions.
*   `CANCEL <file_id>`: Cancel a pending job.
*   `STATUS`: Show pending jobs, active workers, retry queue, and history.

## Sample Execution

```text
> SET_WORKERS 2
> SUBMIT F1 50
> SUBMIT F2 20
> SUBMIT F3 10

> TICK (Time 0 -> 1)
- Worker 1 picks F3 (Size 10). Duration: 1.
- Worker 2 picks F2 (Size 20). Duration: 2.
- F1 (Size 50) remains pending.

> TICK (Time 1 -> 2)
- Worker 1 completes F3. History: [F3].
- Worker 1 picks F1 (Size 50). Duration: 5.
- Worker 2 processing F2 (1/2 done).

> CANCEL F1
Error: F1 is currently processing. Cannot cancel.

> STATUS
Pending: []
Workers: [1: F1, 2: F2]
Retry: []
History: [F3]
```
