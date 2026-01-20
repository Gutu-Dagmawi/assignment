# Problem 39: The Sparse Polynomial Engine

## Problem Description
Scientific computing often involves adding massive polynomials where most coefficients are zero (e.g., $x^{1000} + 1$). Storing this in an array of size 1001 is wasteful.

### The System Rules
1.  **Representation**: List of Terms `(Coefficient, Exponent)`.
2.  **Ordering**: Terms must always be stored in descending order of Exponent.
3.  **Addition Logic**:
    *   Traverse two lists simultaneously (Merge algorithm).
    *   Equal exponents? Add coefficients.
    *   Unequal? Insert higher exponent term.
    *   Zero sum? Remove term entirely.

## Must Use Data Structures
*   **Singly Linked List**: Nodes `Term(coeff, exp, next)`.

## Operations to Implement (CLI Commands)
*   `NEW_POLY <id>`
*   `ADD_TERM <id> <coeff> <exp>`: Insert into sorted list.
*   `SUM <id1> <id2>`: Print result of P1 + P2.

## Sample Execution

```text
> NEW_POLY A
> ADD_TERM A 3 2  (3x^2)
> ADD_TERM A 5 0  (5)
A: 3x^2 + 5

> NEW_POLY B
> ADD_TERM B 4 2  (4x^2)
> ADD_TERM B 2 1  (2x)
B: 4x^2 + 2x

> SUM A B
Scanning...
Exp 2: 3+4=7.
Exp 1: 0+2=2.
Exp 0: 5+0=5.
Result: 7x^2 + 2x + 5
```
