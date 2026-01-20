# Problem 58: Maze Solver with Path Visualization

## Problem Description
You are building a maze-solving engine that finds a path from start to goal using backtracking, tracking the solution path and dead ends.

### The System Rules
1.  **Maze Representation**:
    *   A 2D grid where each cell is either `.` (open) or `#` (wall).
    *   `S` marks the start, `G` marks the goal.
2.  **Movement**:
    *   From any cell, move UP, DOWN, LEFT, or RIGHT to an adjacent open cell.
    *   Cannot move into walls or outside grid boundaries.
    *   Cannot revisit a cell already in the current path (no loops).
3.  **Solving Logic (Depth-First Search)**:
    *   Start at `S`, try each direction.
    *   If stuck (all directions blocked or visited), backtrack to the last decision point.
    *   If goal `G` is reached, the current path is the solution.
4.  **Path Tracking**:
    *   Maintain the current path as a Stack.
    *   Mark visited cells to avoid revisiting.
    *   Count total cells explored and backtrack count.

## Must Use Data Structures
*   **Stack**: For the current path (DFS traversal).
*   **2D Array**: For the maze grid and visited markers.
*   **Queue** (Optional): For BFS alternative or for storing multiple solutions.
*   **Linked List** (Optional): For path representation.

## Operations to Implement (CLI Commands)
*   `LOAD_MAZE <rows>`: Input maze row by row.
*   `SOLVE`: Find a path from S to G.
*   `SHOW_PATH`: Display maze with solution path marked.
*   `STATS`: Show cells explored, backtracks, path length.

## Sample Execution

```text
> LOAD_MAZE 5
# # # # #
# S . . #
# # # . #
# . . . #
# # # G #

Maze loaded (5x5).

> SOLVE
Solving...
Start: (1,1). Goal: (4,3).
Exploring (1,1) -> (1,2) -> (1,3) -> (2,3) -> (3,3) -> (3,2) -> (3,1) -> Dead end!
Backtracking to (3,2)...
Exploring (3,2) -> (4,3) -> GOAL FOUND!

> SHOW_PATH
# # # # #
# S * * #
# # # * #
# . . * #
# # # G #

(* = solution path)

> STATS
Cells Explored: 9
Backtracks: 2
Path Length: 7
```
