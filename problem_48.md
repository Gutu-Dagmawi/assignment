# Problem 48: Adaptive Traffic Light Controller

## Problem Description
You are designing a smart traffic light controller for a multi-lane intersection that adjusts timing based on real-time traffic density.

### The System Rules
1.  **Intersection**:
    *   4 directions: North, South, East, West.
    *   Each direction has a queue of waiting vehicles.
2.  **Light Cycle**:
    *   Lights cycle through: GREEN → YELLOW → RED.
    *   Only one direction pair can be GREEN at a time (N/S or E/W).
    *   Standard timing: GREEN (10 ticks), YELLOW (2 ticks), then switch.
3.  **Adaptive Logic**:
    *   If a direction has more than `THRESHOLD` vehicles waiting, extend its GREEN phase by up to 5 extra ticks.
    *   If a direction has 0 vehicles, skip its phase entirely.
4.  **Processing**:
    *   Each tick, vehicles at the GREEN direction depart (1 vehicle per lane per tick).
    *   New vehicles can arrive at any direction at any time.

## Must Use Data Structures
*   **Circular Linked List**: For the light state cycle (GREEN → YELLOW → RED per direction).
*   **Array of Queues**: One queue per direction for waiting vehicles.
*   **Counters/Array**: For timing and vehicle counts.
*   **Min-Heap** (Optional): For priority-based phase ordering.

## Operations to Implement (CLI Commands)
*   `ARRIVE <direction> <count>`: Vehicles arrive at a direction.
*   `TICK`: Advance time. Process departures, update lights.
*   `SET_THRESHOLD <n>`: Configure adaptive threshold.
*   `STATUS`: Show current light states and queue lengths.

## Sample Execution

```text
> SET_THRESHOLD 5

> ARRIVE North 8
> ARRIVE South 3
> ARRIVE East 2

> STATUS
N/S: GREEN (8N, 3S waiting). E/W: RED (2E, 0W waiting).

> TICK (x10)
N/S phase: 10 vehicles departed.
Remaining: N=0, S=1.

> TICK (x2)
Yellow phase.

> TICK
E/W now GREEN. N/S RED.

> ARRIVE North 10
> STATUS
N/S: RED (10N, 1S waiting). E/W: GREEN (2E, 0W waiting).

(E/W has <5 vehicles, no extension)
(N/S has 10 > THRESHOLD, will get extended GREEN)
```
