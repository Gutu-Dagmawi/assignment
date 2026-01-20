# Problem 44: Real-Time Network Traffic Monitor

## Problem Description
You are building a network monitoring system that tracks packet sizes in a sliding time window and efficiently reports statistics (maximum, minimum, average).

### The System Rules
1.  **Packet Properties**:
    *   `Packet ID`
    *   `Size` (bytes)
    *   `Timestamp`
2.  **Sliding Window**:
    *   Window covers the last `W` time units.
    *   As time advances, old packets "expire" and are removed from the window.
3.  **Statistics (within the window)**:
    *   **Maximum**: Largest packet size.
    *   **Minimum**: Smallest packet size.
    *   **Average**: Mean packet size.
    *   **Count**: Number of packets.
4.  **Efficiency Requirement**:
    *   `MAX` and `MIN` must be O(1) retrieval (using monotonic queues).
    *   Updates (add packet, expire packets) should be O(log n) or better.

## Must Use Data Structures
*   **Deque (Monotonic Queue)**: For O(1) max/min tracking.
*   **Queue**: For the actual packet window (FIFO expiration).
*   **Array/Counters**: For sum and count (to calculate average).
*   **Min-Heap** (Optional): Alternative for min tracking.

## Operations to Implement (CLI Commands)
*   `SET_WINDOW <w>`: Set window size in time units.
*   `PACKET <id> <size> <timestamp>`: Record a packet.
*   `ADVANCE <time>`: Advance current time (expires old packets).
*   `STATS`: Show max, min, avg, count for current window.

## Sample Execution

```text
> SET_WINDOW 10

> PACKET P1 100 0
> PACKET P2 200 2
> PACKET P3 50 5
> PACKET P4 150 8

> STATS (Current time: 8)
Window: [0, 8]
Packets: P1, P2, P3, P4
Max: 200, Min: 50, Avg: 125.0, Count: 4

> ADVANCE 12

> STATS (Current time: 12)
Window: [2, 12]
Expired: P1
Packets: P2, P3, P4
Max: 200, Min: 50, Avg: 133.3, Count: 3

> ADVANCE 15

> STATS (Current time: 15)
Window: [5, 15]
Expired: P2
Packets: P3, P4
Max: 150, Min: 50, Avg: 100.0, Count: 2
```
