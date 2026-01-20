# Problem 27: The Shell Command History

## Problem Description
Implement the history feature of a shell (like Bash or Zsh). It tracks commands and allows recalling them using specific patterns.

### The System Rules
1.  **Storage**: Store every executed command string.
2.  **Navigation**: Users can press Up/Down (simulated) to traverse history.
3.  **Bang Commands (!)**:
    *   `!!`: Re-run the very last command.
    *   `!N`: Re-run command #N (by index).
    *   `!prefix`: Re-run the *most recent* command starting with "prefix".
4.  **Deduplication (Smart History)**:
    *   If the user runs the exact same command twice in a row, do not store duplicates.

## Must Use Data Structures
*   **Dynamic Array / List**: To store the command strings indexed by ID.
*   **Iterator/Pointer**: To track current position during Up/Down navigation.

## Operations to Implement (CLI Commands)
*   `EXEC <cmd>`: Run and store cmd.
*   `HISTORY`: List last 10.
*   `BANG_LAST`: Simulates `!!`.
*   `BANG_PREFIX <str>`: Simulates `!str`.

## Sample Execution

```text
> EXEC "ls -la"
> EXEC "git status"
> EXEC "make build"

> BANG_PREFIX "git"
Found "git status". Executing...

> EXEC "make build"
Ignored duplicate (same as prev).

> HISTORY
1: ls -la
2: git status
3: make build
4: git status
```
