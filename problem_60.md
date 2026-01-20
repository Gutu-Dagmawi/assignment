# Problem 60: Prefix-Based Autocomplete Engine

## Problem Description
You are building an autocomplete system that suggests words based on a typed prefix, ranking suggestions by frequency and recency.

### The System Rules
1.  **Dictionary**:
    *   Words are stored in a tree structure where each node represents a character.
    *   Paths from root to leaf spell out words.
    *   Each word has a `frequency` count and `last_used` timestamp.
2.  **Prefix Lookup**:
    *   Given a prefix (e.g., "app"), find all words starting with that prefix.
    *   Return top `K` suggestions ranked by: **frequency** (descending), then **recency** (most recent first).
3.  **Learning**:
    *   When a word is selected/used, increment its frequency and update `last_used`.
    *   If a word doesn't exist, add it to the dictionary.
4.  **Memory Limit**:
    *   Maximum `M` words in dictionary.
    *   When limit reached, evict the word with the lowest frequency (ties: oldest last_used).

## Must Use Data Structures
*   **Tree (N-ary / Linked Nodes)**: The prefix tree structure.
*   **Min-Heap**: For efficient eviction of least frequent words.
*   **Max-Heap**: For ranking top-K suggestions.
*   **Queue/Array**: For collecting all words matching a prefix (via DFS/BFS traversal).

## Operations to Implement (CLI Commands)
*   `ADD_WORD <word>`: Add a word to the dictionary.
*   `SEARCH <prefix> <k>`: Return top K suggestions for prefix.
*   `USE <word>`: Mark a word as used (increment freq, update time).
*   `SET_LIMIT <m>`: Set dictionary size limit.
*   `STATUS`: Show dictionary size and top words.

## Sample Execution

```text
> SET_LIMIT 5

> ADD_WORD apple
> ADD_WORD application
> ADD_WORD apply
> ADD_WORD banana
> ADD_WORD band

> SEARCH app 3
Suggestions for "app":
1. apple (freq: 0)
2. application (freq: 0)
3. apply (freq: 0)

> USE apple
> USE apple
> USE apply

> SEARCH app 3
Suggestions for "app":
1. apple (freq: 2)
2. apply (freq: 1)
3. application (freq: 0)

> ADD_WORD appetizer
Dictionary full! Evicting: band (freq: 0, oldest).
Added: appetizer.

> SEARCH app 5
Suggestions for "app":
1. apple (freq: 2)
2. apply (freq: 1)
3. appetizer (freq: 0)
4. application (freq: 0)
```
