# Problem 42: Snake Game Engine

## Problem Description
You are implementing the core logic for the classic Snake game. The system must track the snake's body, handle movement, detect collisions, and manage food spawning.

### The System Rules
1.  **Grid**: The game is played on an `N x M` grid.
2.  **Snake**:
    *   The snake is a sequence of body segments (coordinates).
    *   The head moves in the current direction each tick.
    *   The tail is removed each tick (unless food is eaten).
3.  **Movement**:
    *   Directions: UP, DOWN, LEFT, RIGHT.
    *   The snake cannot reverse direction (no instant 180° turns).
4.  **Collisions**:
    *   **Wall**: If head goes out of bounds, game over.
    *   **Self**: If head overlaps any body segment, game over.
    *   **Food**: If head reaches food position, grow (don't remove tail this tick), score increases.
5.  **Food**: After food is eaten, spawn new food at a random empty cell.

## Must Use Data Structures
*   **Deque (Double-Ended Queue)**: For the snake body (add at head, remove at tail).
*   **Array (2D Grid)**: To track occupied cells for collision detection.
*   **Stack** (Optional): For undo/replay functionality.
*   **Queue** (Optional): For buffering multiple direction inputs.

## Operations to Implement (CLI Commands)
*   `INIT <n> <m>`: Initialize grid and spawn snake at center.
*   `DIRECTION <dir>`: Set movement direction.
*   `TICK`: Advance one step.
*   `SPAWN_FOOD <x> <y>`: Place food (or random if not specified).
*   `STATUS`: Show grid, snake position, score.

## Sample Execution

```text
> INIT 5 5
Grid: 5x5. Snake at (2,2). Length: 1.

> SPAWN_FOOD 2 4
Food at (2,4).

> DIRECTION RIGHT
> TICK
Snake moved to (3,2). Length: 1.

> TICK
Snake moved to (4,2). Length: 1.

> DIRECTION DOWN
> TICK
Snake moved to (4,3). Length: 1.

> DIRECTION LEFT
> TICK
> TICK
Snake at (2,3). Approaching food...

> TICK
Snake ate food at (2,4)! Score: 1. Length: 2.
New food spawned at (0,1).

> STATUS
. . . . .
F . . . .
. . H . .   (H = Head)
. . T . .   (T = Tail)
. . . . .
Score: 1
```
