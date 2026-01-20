# Problem 08: The Scientific Formula Processor (Symbolic Math Engine)

## Problem Description
You are building the kernel for a new scientific calculator. The system must not only evaluate individual arithmetic expressions but also maintain a persistent **Symbol Table** to support variable assignment, referencing, and function calls.

### The System Rules
1.  **Expression Support**:
    *   Standard Operators: `+`, `-`, `*`, `/`, `^` (Power).
    *   Parentheses for grouping: `(`, `)`.
    *   Functions: `min(a,b)`, `max(a,b)`, `pow(a,b)`.
2.  **Stateful Variables**:
    *   **Assignment**: `LET <var> = <expression>` stores the result.
    *   **Referencing**: Expressions can use previously defined variables (e.g., `5 * x + y`).
    *   **Immutability**: Once a variable is set, it can be overwritten, but the *old* value used in *past* computations isn't retroactively changed (Standard imperative behavior).
3.  **Validation**:
    *   Detect "**Undefined Variable**" errors.
    *   Detect "**Circular Reference**" (if you choose to implement lazy evaluation - optional but cool. For this problem, immediate evaluation is sufficient, so Circular Reference is less of an issue unless you implement `DEF f(x)`).

## Must Use Data Structures
*   **Two Stacks**: One for Operands (values), one for Operators (to handle precedence during the `Shunting Yard` or similar algorithm).
*   **Balanced Binary Search Tree (BST)** or **Sorted Array + Binary Search**: To implement the **Symbol Table** (Variable Name -> Value).
    *   *Constraint*: You **CANNOT** use a Hash Map. You must implement the lookup logic using O(log n) search.

## Operations to Implement (CLI Commands)
*   `EVAL <expression>`: Compute and print result.
*   `LET <var> = <expression>`: Compute and store result.
*   `DUMP`: Print all defined variables sorted by name.
*   `CLEAR`: Wipe state.

## Sample Execution

```text
> EVAL 3 + 5 * 2
Result: 13

> LET radius = 10
Variable 'radius' set to 10.

> LET area = 3.14 * radius ^ 2
Variable 'area' set to 314.0.

> EVAL min(area, 400)
Result: 314.0

> EVAL area + unknown
Error: Variable 'unknown' is not defined.

> DUMP
area: 314.0
radius: 10.0
```
