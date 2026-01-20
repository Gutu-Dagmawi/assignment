# Problem 15: The Library Reservation System

## Problem Description
Manage the book circulation for a library. A popular book might have zero copies on the shelf and a long line of people waiting for it.

### The System Rules
1.  **Inventory**:
    *   Each Book Title has `N` copies total.
    *   Copies can be `AVAILABLE` or `BORROWED`.
2.  **Queuing**:
    *   If a user requests a book and `Available > 0`, they get it immediately.
    *   If `Available == 0`, they join a **specific waitlist** for that title.
3.  **Returns**:
    *   When a copy is returned:
    *   If Waitlist is empty -> Increment `Available`.
    *   If Waitlist exists -> Auto-assign to the first person in queue (Available stays 0).

## Must Use Data Structures
*   **Hash Map <BookTitle, BookDetailsOnly>**: To look up books efficiently.
*   **Queue (inside BookDetails)**: Each book object contains a Queue of `UserIDs` representing its waitlist.

## Operations to Implement (CLI Commands)
*   `ADD_BOOK <title> <copies>`
*   `BORROW <user> <title>`: Process request or queue user.
*   `RETURN <user> <title>`: Process return and notify next waiter.
*   `SHOW_BOOK <title>`: Show copies available and waitlist size.

## Sample Execution

```text
> ADD_BOOK "Dune" 1
> BORROW Alice "Dune"
Alice borrows "Dune".

> BORROW Bob "Dune"
no copies. Bob added to waitlist.

> RETURN Alice "Dune"
Alice returned. Assigned immediately to Bob.
Copies available: 0.

> RETURN Bob "Dune"
Bob returned. No waitlist.
Copies available: 1.
```
