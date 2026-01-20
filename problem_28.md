# Problem 28: Memory Block Manager (Mark-Sweep Simulation)

## Problem Description
You are simulating a simplified garbage collection system for a programming language runtime. The system must allocate memory blocks, track references between them, and periodically reclaim unreachable blocks.

### The System Rules
1.  **Memory Model**:
    *   Memory is a fixed-size array of `N` blocks.
    *   Each block can be FREE or ALLOCATED.
    *   Allocated blocks can hold **references** to other blocks (simulating object pointers).
2.  **Root Set**: A special list of block IDs that are "directly reachable" (e.g., global variables).
3.  **Allocation**:
    *   **First-Fit**: Find the first FREE block and allocate it.
    *   If no free block exists, trigger a garbage collection cycle.
4.  **Garbage Collection (Mark-Sweep)**:
    *   **Mark Phase**: Starting from the Root Set, traverse all reachable blocks using a Stack (simulating DFS). Mark each reachable block as "VISITED".
    *   **Sweep Phase**: Iterate through all blocks. Any block that is ALLOCATED but NOT VISITED is unreachable and should be freed.

## Must Use Data Structures
*   **Array**: The memory heap (each slot stores block metadata: status, references).
*   **Stack**: For the Mark Phase traversal (DFS from roots).
*   **Linked List (Free List)**: To track free blocks for efficient allocation.
*   **Array/Set**: Root Set of directly reachable block IDs.

## Operations to Implement (CLI Commands)
*   `ALLOC <block_id>`: Allocate a new block. Returns the block address/index.
*   `REF <from_block> <to_block>`: Create a reference from one block to another.
*   `ROOT <block_id>`: Add a block to the root set.
*   `UNROOT <block_id>`: Remove a block from the root set.
*   `GC`: Run a garbage collection cycle.
*   `STATUS`: Show all blocks, their status, and references.

## Sample Execution

```text
> SET_HEAP_SIZE 5

> ALLOC B1
Block B1 allocated at index 0.

> ALLOC B2
Block B2 allocated at index 1.

> ALLOC B3
Block B3 allocated at index 2.

> REF B1 B2  (B1 points to B2)
> ROOT B1

> STATUS
Heap: [B1*, B2, B3, FREE, FREE]  (* = root)
Roots: [B1]
B1 -> [B2]
B2 -> []
B3 -> []

> GC
--- Mark Phase ---
Visiting B1 (root).
Visiting B2 (referenced by B1).
--- Sweep Phase ---
B3 is unreachable. FREED.
Freed 1 block(s).

> STATUS
Heap: [B1*, B2, FREE, FREE, FREE]
```
