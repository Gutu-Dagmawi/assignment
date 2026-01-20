# Problem 45: The Database Buffer Pool

## Problem Description
Simulate a database buffer pool using LRU (Least Recently Used) policy. This is distinct from a simple cache because pages can be "Dirty" (modified).

### The System Rules
1.  **Page Management**:
    *   Pool holds `N` pages.
    *   `GET(page_id)`: Pins page in memory.
    *   `SET(page_id, data)`: Marks page as **DIRTY**.
2.  **Eviction**:
    *   If pool full, choose LRU page.
    *   **Write-Back**: If the LRU page is Dirty, you must simulate `FLUSH_TO_DISK` before removing it.
    *   If Clean, just drop it.

## Must Use Data Structures
*   **Doubly Linked List**: LRU tracking.
*   **Hash Map**: Page lookup.
*   **Boolean Flag**: `is_dirty` on each node.

## Operations to Implement (CLI Commands)
*   `INIT <n>`
*   `READ <id>`
*   `WRITE <id> <val>`
*   `STATUS`: Show buffer pages and dirty status.

## Sample Execution

```text
> INIT 2
> READ P1
Pool: [P1(clean)]
> WRITE P2 "Data"
Pool: [P2(dirty), P1(clean)]
> READ P3 (Full!)
Evicting P1 (Clean). Dropped.
Pool: [P3(clean), P2(dirty)]
> READ P4 (Full!)
Evicting P2 (Dirty). FLUSHING P2 TO DISK... Dropped.
Pool: [P4(clean), P3(clean)]
```
