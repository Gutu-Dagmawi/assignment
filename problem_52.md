# Problem 52: Multi-Class Boarding Queue System

## Problem Description
You are designing a boarding system for an airline that handles multiple passenger classes with priority ordering and group boarding.

### The System Rules
1.  **Passenger Classes** (in priority order):
    *   Class 1: First Class
    *   Class 2: Business
    *   Class 3: Premium Economy
    *   Class 4: Economy
    *   Class 5: Basic Economy
2.  **Boarding Logic**:
    *   Board all passengers from Class 1 before Class 2, etc.
    *   **Within each class**: FIFO (first checked-in, first boarded).
    *   **Group Boarding**: Optionally, passengers can be in "groups" (e.g., families). When one member boards, all group members board together.
3.  **Special Handling**:
    *   **Wheelchair/Assistance**: These passengers board BEFORE Class 1 (Priority 0).
    *   **Standby**: These passengers board AFTER Class 5 (Priority 6).
4.  **Gate Capacity**: Maximum `G` passengers can board per tick.

## Must Use Data Structures
*   **Array of Queues**: One queue per class (indices 0-6).
*   **Heap** (Optional): For complex priority with group logic.
*   **Linked List**: For group membership (linking passengers).
*   **Array**: For tracking boarded passengers.

## Operations to Implement (CLI Commands)
*   `CHECKIN <name> <class> [group_id]`: Add passenger to queue.
*   `SET_GATE_CAPACITY <g>`: Set boarding rate.
*   `BOARD`: Board up to `G` passengers (highest priority first).
*   `STATUS`: Show queue lengths and boarded count.

## Sample Execution

```text
> SET_GATE_CAPACITY 3

> CHECKIN Alice 1
> CHECKIN Bob 3
> CHECKIN Carol 1
> CHECKIN Dave 2
> CHECKIN Eve 3 G1
> CHECKIN Frank 3 G1  (Same group as Eve)

> BOARD
Boarding (max 3):
- Alice (Class 1)
- Carol (Class 1)
- Dave (Class 2)

> BOARD
Boarding:
- Bob (Class 3)
- Eve (Class 3, Group G1) + Frank (Group G1) [Group boards together]

> STATUS
Boarded: 6
Remaining: 0
```
