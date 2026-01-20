# Problem 19: The Live Gaming Leaderboard

## Problem Description
You are building the backend for a massive multiplayer game. You need to maintain a "Top 10" leaderboard that updates in real-time as millions of players score points.

### The System Rules
1.  **Input Stream**: `(PlayerID, Score)`.
2.  **Leaderboard Logic**:
    *   Always maintain the Top `K` highest scores.
    *   If a new score comes in:
        *   If it's lower than the current K-th best score, ignore it.
        *   If it's higher, remove the K-th score and insert the new one.
3.  **Update Policy**:
    *   Player scores are cumulative? Let's assume **High Score** mode (one best score per player). *Correction*: For simplicity in this structure, treat every score submission as a unique event to qualify for the daily top list.

## Must Use Data Structures
*   **Min-Heap (Size K)**:
    *   The root of the heap represents the *smallest* of the Top K scores (the "Gatekeeper").
    *   New score > Root? Replace Root and Heapify.
    *   New score <= Root? Ignore.
*   (Optional: Hash Map if tracking unique player updates).

## Operations to Implement (CLI Commands)
*   `INIT <k>`: Set leaderboard size.
*   `SCORE <player> <val>`: Submit score.
*   `SHOW_TOP`: Print elements in heap (sorted).

## Sample Execution

```text
> INIT 3
> SCORE P1 100
> SCORE P2 500
> SCORE P3 300
Heap: [100, 500, 300] (Logically sorted: 100, 300, 500)

> SCORE P4 50
Ignored (50 < 100).

> SCORE P5 200
200 > 100. Evict 100. Insert 200.
Heap: [200, 500, 300] -> Top 3 are 200, 300, 500.
```
