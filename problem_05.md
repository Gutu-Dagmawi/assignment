# Problem 05: The First-Fit Memory Auditor

## Problem Description
You are designing the memory management unit (MMU) for a simulated operating system. You must manage a finite block of memory, handling allocation requests and freeing memory while minimizing fragmentation.

### The System Rules
1.  **Memory Space**: The system starts with a single contiguous block of memory of size `TOTAL_SIZE`.
2.  **Allocation Strategy (First-Fit)**:
    *   When a request comes for `K` bytes:
    *   Scan the list of **Free Blocks** from the beginning.
    *   Pick the **first** block that is size `>= K`.
    *   Split the block: `K` bytes go to the user, the remainder stays as a new (smaller) free block.
    *   If no block is big enough, the allocation fails ("OUT OF MEMORY").
3.  **Deallocation & Coalescing**:
    *   When memory is freed, it is added back to the pool.
    *   **CRITICAL RULE**: If the freed block is immediately adjacent to other free blocks (left or right), they must be **merged** into a single larger free block to reduce fragmentation.
4.  **Aligned Access**:
    *   All allocations must be multiples of 4 bytes. If a user asks for 13 bytes, allocate 16.

## Must Use Data Structures
*   **Singly Linked List**: To store the **Free List** (sorted by memory address to facilitate merging).
*   **Map / Dictionary**: To track **Allocated Blocks** (Key: Pointer/ID, Value: Size/Start Address) so we know what to free.

## Operations to Implement (CLI Commands)
*   `INIT <total_size>`: Initialize memory.
*   `ALLOC <id> <size>`: Allocate memory for object `id`.
*   `FREE <id>`: Free memory associated with `id`.
*   `INSPECT`: Print the layout of memory (Free vs Used regions).

## Sample Execution

```text
> INIT 100
Memory: [0-100: FREE]

> ALLOC A 20
Allocated 20 bytes at 0.
Memory: [0-20: A] -> [20-100: FREE]

> ALLOC B 30
Allocated 30 bytes at 20.
Memory: [0-20: A] -> [20-50: B] -> [50-100: FREE]

> FREE A
Freed A.
Memory: [0-20: FREE] -> [20-50: B] -> [50-100: FREE]

> FREE B
Freed B. Coalescing...
Memory: [0-100: FREE]
(Blocks 0-20, 20-50, and 50-100 merged)
```
