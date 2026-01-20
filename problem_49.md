# Problem 49: The Recursive Disk Usage Calculator

## Problem Description
Your OS needs to show the size of a folder. A folder contains files and subfolders. The size of a folder is the sum of all files inside it, recursively.

### The System Rules
1.  **Entities**:
    *   **File**: Has `Name` and `Size`.
    *   **Directory**: Has `Name` and `List<Children>`.
2.  **Calculation**:
    *   `GetSize(Dir)` = Sum(`GetSize(child)`).
    *   `GetSize(File)` = `File.Size`.

## Must Use Data Structures
*   **N-ary Tree**: Nodes can have `N` children.
*   **Recursion (Implicit Stack)**: To traverse the depth.

## Operations to Implement (CLI Commands)
*   `MKDIR <name>` (inside current)
*   `TOUCH <name> <size>` (inside current)
*   `CD <name>`: Traverse down.
*   `CALC_SIZE`: Print total size of current folder.

## Sample Execution

```text
> MKDIR root
> CD root
> TOUCH file1 10
> MKDIR docs
> CD docs
> TOUCH report 20
> TOUCH image 30

root
├── file1 (10)
└── docs (20+30=50)

> CD ..
> CALC_SIZE
Total: 60 (10 + 50)
```
