# Problem 16: Tiered Log Archival System

## Problem Description
You are designing a log management system for a server cluster. Logs arrive continuously and must be stored, aged out, and archived based on a tiered retention policy.

### The System Rules
1.  **Tiers**: The system has 3 storage tiers:
    *   **Hot Tier**: Stores the most recent `N_hot` logs. Fast access.
    *   **Warm Tier**: Stores the next `N_warm` logs (overflow from Hot). Medium access.
    *   **Cold Tier**: Stores the next `N_cold` logs (overflow from Warm). Slow access. Logs older than Cold are permanently deleted.
2.  **Log Properties**: Each log has:
    *   `Timestamp`
    *   `Severity` (INFO, WARN, ERROR)
    *   `Message`
3.  **Operations**:
    *   **Insert**: New logs enter Hot. If Hot is full, the oldest Hot log moves to Warm. Warm overflow moves to Cold. Cold overflow is deleted.
    *   **Query by Severity**: Return all logs matching a severity, across all tiers, sorted by time (newest first).
    *   **Purge by Age**: Delete all logs older than a given timestamp (across all tiers).

## Must Use Data Structures
*   **Circular Array (x3)**: One for each tier (Hot, Warm, Cold).
*   **Linked List** or **Sorted Array**: To support efficient severity-based querying (e.g., maintain separate lists per severity, or scan and sort on demand using QuickSort).

## Operations to Implement (CLI Commands)
*   `LOG <timestamp> <severity> <message>`: Insert a new log.
*   `QUERY <severity>`: Return all logs of given severity.
*   `PURGE <timestamp>`: Delete logs older than given timestamp.
*   `STATUS`: Show count of logs in each tier.

## Sample Execution

```text
> SET_TIERS 3 3 3  (Hot=3, Warm=3, Cold=3)

> LOG 100 INFO "Server started"
> LOG 101 WARN "High memory"
> LOG 102 ERROR "Disk full"
> LOG 103 INFO "Request received"

> STATUS
Hot: [103, 102, 101] (3 logs)
Warm: [100] (1 log)
Cold: [] (0 logs)

> LOG 104 INFO "Request completed"

> STATUS
Hot: [104, 103, 102] (3 logs)
Warm: [101, 100] (2 logs)
Cold: [] (0 logs)

> QUERY ERROR
Results (sorted by time desc):
- [102] ERROR: Disk full

> PURGE 101
Deleted 1 log(s) older than 101.
```
