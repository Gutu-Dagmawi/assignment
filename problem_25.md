# Problem 25: The Music App Smart Cache

## Problem Description
To save bandwidth, a music app caches recently played songs on the device. Storage is limited, so we need a smart eviction policy.

### The System Rules
1.  **Capacity**: Holds `N` songs.
2.  **Access Pattern**:
    *   When a song is played, it becomes the "Most Recently Used".
    *   If it was already in cache, move it to the front.
    *   If not in cache, load it (add to front).
3.  **Eviction**:
    *   If cache is full and new song loads, delete the "Least Recently Used" (End of list).

## Must Use Data Structures
*   **Doubly Linked List**: Stores Song IDs. Head = Most Recent, Tail = Least Recent.
*   **Hash Map <ID, NodePtr>**: Maps Song ID to its Node in the list for O(1) retrieval and distinct removal.

## Operations to Implement (CLI Commands)
*   `INIT <n>`
*   `PLAY <song_id>`: Updates cache state.
*   `SHOW_CACHE`: Print list from specific MRU to LRU.

## Sample Execution

```text
> INIT 3
> PLAY A
Cache: [A]
> PLAY B
Cache: [B, A]
> PLAY C
Cache: [C, B, A]
> PLAY A
Cache: [A, C, B]  (A moved to front)
> PLAY D
Evicting B (LRU).
Cache: [D, A, C]
```
