# Problem 34: Multi-Level Parking Garage System

## Problem Description
You are simulating a multi-level parking garage where each level operates as a stack (single-lane driveway), but the system must also optimize which level to use for new arrivals.

### The System Rules
1.  **Garage Structure**:
    *   `L` levels, each with capacity `C` (slots).
    *   Each level works as a **LIFO stack** — last car in is first car out.
2.  **Parking Logic**:
    *   New car arrives: Park on the level with the **most available space** (load balancing).
    *   If all levels are full, reject the car.
3.  **Retrieval Logic**:
    *   To retrieve a car from a level, all cars parked AFTER it must be temporarily moved out.
    *   These cars are moved to a **Temporary Holding Area** (another stack) and then re-parked.
4.  **Tracking**:
    *   Track total retrieval cost = number of cars moved out temporarily.
    *   Track average parking duration.

## Must Use Data Structures
*   **Array of Stacks**: One stack per parking level.
*   **Min-Heap** (or Sorted Structure): To quickly find the level with the most space.
*   **Stack**: Temporary holding area during retrieval.
*   **Queue** (Optional): For arrival order if implementing "valet queue".

## Operations to Implement (CLI Commands)
*   `ARRIVE <car_id>`: Park a car.
*   `RETRIEVE <car_id>`: Retrieve a specific car.
*   `STATUS`: Show each level's contents.
*   `STATS`: Show retrieval cost and average parking time.

## Sample Execution

```text
> SET_GARAGE 2 3  (2 levels, 3 slots each)

> ARRIVE C1
C1 parked on Level 1 (3 free -> 2 free).

> ARRIVE C2
C2 parked on Level 2 (3 free -> 2 free).

> ARRIVE C3
> ARRIVE C4
Level 1: [C1, C3] (bottom to top)
Level 2: [C2, C4]

> RETRIEVE C1
Level 1: C3 must be moved out.
- C3 -> Holding Area.
- C1 retrieved.
- C3 -> Level 1.
Retrieval Cost: 1 move.

> STATS
Total Retrieval Cost: 1
Average Parking Duration: 3.5 ticks
```
