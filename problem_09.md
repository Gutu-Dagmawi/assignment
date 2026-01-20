# Problem 09: The Distributed Event Logger

## Problem Description
Design a central logging service for a distributed microservices architecture. The system ingests logs from various sources, categorizes them, and enforces retention policies based on severity and storage limits.

### The System Rules
1.  **Log Structure**: `[ID, Timestamp, Severity, Message, Source]`.
    *   Severities: INFO, WARN, ERROR, CRITICAL.
2.  **Storage Tiers**:
    *   **Hot Storage**: Keep the last 100 logs in memory for instant retrieval.
    *   **Critical Archive**: Keep ALL "CRITICAL" logs indefinitely (until manually cleared).
3.  **Retention Policy**:
    *   If "Hot Storage" exceeds 100 entries, the oldest INFO/WARN logs are discarded.
    *   ERROR logs are moved to a secondary "Cold Store" (simulated) before eviction from Hot Storage.
4.  **Searchability**:
    *   Must support retrieving the last K logs for a specific Source (e.g., "AuthService").

## Must Use Data Structures
*   **Doubly Linked List**: For the "Hot Storage" cache (O(1) addition/removals).
*   **Hash Map <Source, List_Reference>**: To index logs by Source for fast searching without iterating the whole list.
*   **Separate List/Stack**: For "Critical Archive".

## Operations to Implement (CLI Commands)
*   `LOG <severity> <source> <message>`: Ingest a log.
*   `GET_RECENT <k>`: Show last k logs globally.
*   `SEARCH <source> <k>`: Show last k logs for a specific source.
*   `STATS`: Show count of logs in Hot vs Critical store.

## Sample Execution

```text
> LOG INFO Auth "User Login"
> LOG ERROR DB "Connection Failed"
> LOG CRITICAL Payment "Data Corruption"

> SEARCH Auth 1
[INFO] User Login

> STATS
Hot Storage: 3
Critical Archive: 1 (The payment log is referenced here too)
```
