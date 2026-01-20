# Problem 32: Session-Aware Browser Tab Manager

## Problem Description
You are building a browser session manager that handles multiple tabs with advanced features: session persistence, tab grouping, and crash recovery.

### The System Rules
1.  **Tab Properties**: Each tab has:
    *   `Tab ID`
    *   `URL`
    *   `Group ID` (optional - tabs can belong to a named group)
    *   `Last Active Timestamp`
2.  **Navigation**:
    *   Switch to next/previous tab in a circular fashion.
    *   Jump to a specific tab by ID.
    *   Jump to a specific group (first tab in that group becomes active).
3.  **Session Features**:
    *   **Snapshot**: Save the current state of all tabs to a "Session Stack" (for crash recovery).
    *   **Restore**: Pop the last snapshot and restore all tabs to that state.
    *   **Prune Duplicates**: If multiple tabs have the same URL, keep only the most recently accessed one.
4.  **Memory Limit**: Maximum `M` tabs allowed. If exceeded, auto-close the least recently used (LRU) tab.

## Must Use Data Structures
*   **Circular Doubly Linked List**: For tab navigation.
*   **Stack**: For session snapshots.
*   **Array/Hash Map**: For group-to-tab mappings and LRU tracking.

## Operations to Implement (CLI Commands)
*   `OPEN <url> [group]`: Open a new tab.
*   `CLOSE`: Close current tab.
*   `NEXT` / `PREV`: Navigate tabs.
*   `SWITCH <tab_id>`: Switch to specific tab.
*   `SNAPSHOT`: Save session state.
*   `RESTORE`: Restore last session.
*   `PRUNE`: Remove duplicate URLs.
*   `STATUS`: Show all tabs and groups.

## Sample Execution

```text
> OPEN google.com
Tab T1 opened: google.com

> OPEN github.com work
Tab T2 opened: github.com (Group: work)

> OPEN google.com personal
Tab T3 opened: google.com (Group: personal)

> SNAPSHOT
Session saved (3 tabs).

> CLOSE
T3 closed. Active: T2.

> RESTORE
Session restored (3 tabs). Active: T1.

> PRUNE
Duplicate URL 'google.com': Kept T3 (most recent), Removed T1.
Remaining: 2 tabs.
```
