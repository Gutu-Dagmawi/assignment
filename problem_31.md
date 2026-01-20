# Problem 31: The VIP Restaurant Manager

## Problem Description
A popular restaurant has a single waiting list. However, VIPs and Cancellations confuse the host. Build a robust tracker.

### The System Rules
1.  **Arrivals**:
    *   Regular walk-ins join at the **Back**.
    *   VIPs join at the **Front**.
2.  **Departures**:
    *   Anyone can leave the line at any time (Reneging).
3.  **Seating**:
    *   Host always takes the person at the **Front**.

## Must Use Data Structures
*   **Doubly Linked List**:
    *   `Head` (Front) for Seating and VIP interaction.
    *   `Tail` (Back) for Regulars.
    *   Nodes allow removing a person from the *middle* in O(1) without shifting an array.
*   **Hash Map <Name, NodePtr>**: To find "John" immediately when he says "I'm leaving".

## Operations to Implement (CLI Commands)
*   `ARRIVE <name>`
*   `ARRIVE_VIP <name>`
*   `LEAVE <name>`
*   `SEAT`: Remove head.
*   `SHOW_LINE`: Print order.

## Sample Execution

```text
> ARRIVE A
> ARRIVE B
Line: A -> B

> ARRIVE_VIP V1
Line: V1 -> A -> B

> LEAVE A
Line: V1 -> B

> SEAT
Seating V1.
Line: B
```
