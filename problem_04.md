# Problem 04: The Modern Browser Engine (Tabbed History Manager)

## Problem Description
You are building the core navigation engine for a modern web browser. Unlike simple browsers, this engine supports multiple open tabs, each with its own history, and a global "Closed Tab" recovery system.

### The System Rules
1.  **Tabs**: The browser can have multiple tabs open. Each tab has:
    *   A unique Title/ID.
    *   A `History` of visited URLs.
    *   A `Current` position in that history.
2.  **Navigation**:
    *   `VISIT (url)`: Helper clears "Forward" history in the active tab (if any) and adds the new URL.
    *   `BACK` / `FORWARD`: Navigate within the active tab's history.
3.  **Global Tab Management**:
    *   Tabs can be switched (Active Tab).
    *   Tabs can be closed.
    *   **Undo Close Tab**: The system must track the last `K` closed tabs (preserving their full history state) and allow restoring them in LIFO order (`CTRL+SHIFT+T`).
4.  **Memory Management (The "Hard" Part)**:
    *   The total number of history entries *across all open tabs* cannot exceed `MAX_HISTORY_SIZE` (e.g., 50).
    *   If the limit is exceeded, you must **evict** the oldest history entry from the *least recently used (LRU) inactive tab*.
    *   Note: The current page of any tab cannot be evicted.

## Must Use Data Structures
*   **Doubly Linked List**: To manage the list of Open Tabs (allowing efficient switching and reordering).
*   **Stack of Objects**: To handle the "Closed Tabs" history (each object contains a full tab state).
*   **Deque (Double-Ended Queue)** or **LRU Cache**: To track the usage order of tabs for memory eviction purposes.

## Operations to Implement (CLI Commands)
*   `NEW_TAB <title>`: Open a new blank tab and make it active.
*   `SWITCH_TAB <title>`: Make an existing tab active.
*   `VISIT <url>`: Visit URL in active tab.
*   `BACK`: Go back in active tab.
*   `FORWARD`: Go forward in active tab.
*   `CLOSE_TAB`: Close active tab.
*   `RESTORE_TAB`: Re-open the most recently closed tab.
*   `STATUS`: Show all open tabs, which is active, and total memory usage.

## Sample Execution

```text
> NEW_TAB "Research"
Tab 'Research' created. Active.

> VISIT "google.com"
> VISIT "wikipedia.org"
Current: wikipedia.org. History: [google.com, wikipedia.org].

> NEW_TAB "Social"
Tab 'Social' created. Active.

> VISIT "twitter.com"
Current: twitter.com.

> SWITCH_TAB "Research"
Switched to 'Research'.

> CLOSE_TAB
Closed 'Research'. Store in Closed History.
Active is now 'Social'.

> VISIT "facebook.com"
Current: facebook.com.

> RESTORE_TAB
Restored 'Research'. Active.
History Preserved: [google.com, wikipedia.org].
```
