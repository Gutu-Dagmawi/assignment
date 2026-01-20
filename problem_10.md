# Problem 10: Build System Artifact Compiler (Parallel Job Scheduler)

## Problem Description
You are developing the core scheduler for a modern build system (like Make or Gradle) — build system is a program that automates the process of compiling source code into executable programs. The system must execute a set of tasks respecting their dependencies, while simulating parallel execution across a fixed number of "Workers".

### The System Rules
1.  **Task Graph**: Tasks have IDs, Duration (time units), and Dependencies (other tasks that must finish *before* this one starts).
2.  **Resources**: You have `K` independent workers.
3.  **Scheduling Logic**:
    *   **Dependency Resolution**: A task cannot be queued for execution until ALL its dependencies are completed.
    *   **Parallelism**: If multiple tasks are "Ready" (dependencies met) and workers are free, they run simultaneously.
    *   **Critical Path**: If multiple tasks are ready but workers are scarce, prioritize the task that unlocks the most future work (or just simple FIFO if simplified, but let's go with: **Prioritize tasks with more outgoing edges** or simple ID order for now).
4.  **Cycle Detection**: If dependencies form a cycle (A -> B -> A), the system must detect this on input and refuse to build.

## Must Use Data Structures
*   **Adjacency List (Graph)**: To represent the Task Dependency Graph.
*   **In-Degree Array/Map**: To efficiently identify "Ready" tasks (In-Degree 0).
*   **Min-Heap**: To manage the execution timeline. Stores `(FinishTime, WorkerID)` events to simulate when a worker becomes free.
*   **Queue**: For the "Ready Queue" of tasks waiting for a worker.

## Operations to Implement (CLI Commands)
*   `TASK <task_id> <duration>`: Define a task.
*   `DEPENDS <child_id> <parent_id>`: `child` cannot start until `parent` finishes.
*   `SET_WORKERS <k>`: Set number of parallel workers.
*   `BUILD`: Start the simulation. Output the start/finish time of each task and total build time.

## Sample Execution

```text
> TASK T_Lib 5
> TASK T_Core 10
> TASK T_App 2
> DEPENDS T_App T_Lib
> DEPENDS T_App T_Core (App needs Lib and Core)
> SET_WORKERS 2

> BUILD
Build Started with 2 workers.
Time 0: Worker 1 starts T_Lib (5s).
Time 0: Worker 2 starts T_Core (10s).
Time 5: Worker 1 finishes T_Lib. Worker 1 Idle.
Time 10: Worker 2 finishes T_Core.
Time 10: Dependencies met for T_App.
Time 10: Worker 1 starts T_App (2s).
Time 12: Worker 1 finishes T_App.
Total Build Time: 12 units.
```

