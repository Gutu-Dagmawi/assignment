# Problem 18: Network Traffic Shaper

## Problem Description
You are simulating a network router's Quality of Service (QoS) module. Packets arrive with different priority classes, and the router must manage buffer space, enforce fair bandwidth allocation, and track performance metrics.

### The System Rules
1.  **Priority Classes**: There are 3 traffic classes:
    *   **Real-Time** (e.g., VoIP): Highest priority. Dedicated buffer of size `B_rt`.
    *   **Interactive** (e.g., Web browsing): Medium priority. Buffer size `B_int`.
    *   **Bulk** (e.g., Downloads): Lowest priority. Buffer size `B_bulk`.
2.  **Packet Properties**: Each packet has:
    *   `Packet ID`
    *   `Class` (RT, INT, BULK)
    *   `Size` (bytes)
    *   `Arrival Time`
3.  **Processing Logic**:
    *   The router processes one packet per TICK.
    *   **Strict Priority**: Always process Real-Time first. If empty, process Interactive. If empty, process Bulk.
    *   **Buffer Overflow**: If a class buffer is full, incoming packets of that class are DROPPED.
4.  **Metrics**:
    *   `Packet Loss Rate` per class = Dropped / (Dropped + Processed).
    *   `Average Latency` per class = Average(ProcessTime - ArrivalTime).

## Must Use Data Structures
*   **Circular Queue (x3)**: One bounded queue per traffic class.
*   **Arrays/Counters**: To track metrics (drops, processed counts, latency sums).
*   **Heap** (Optional): If implementing Weighted Fair Queuing as an advanced variant.

## Operations to Implement (CLI Commands)
*   `SET_BUFFERS <rt_size> <int_size> <bulk_size>`: Configure buffer sizes.
*   `ARRIVE <packet_id> <class> <size>`: A packet arrives.
*   `TICK`: Process one packet (highest priority available).
*   `METRICS`: Print loss rate and average latency per class.

## Sample Execution

```text
> SET_BUFFERS 2 2 2

> ARRIVE P1 RT 100
> ARRIVE P2 INT 200
> ARRIVE P3 RT 150
> ARRIVE P4 RT 120  (Buffer RT is full!)

- P4 DROPPED.

> TICK (Time 1)
- Processing P1 (RT). Latency: 0.

> TICK (Time 2)
- Processing P3 (RT). Latency: 1.

> TICK (Time 3)
- Processing P2 (INT). Latency: 2.

> METRICS
RT:   Processed=2, Dropped=1, LossRate=33.3%, AvgLatency=0.5
INT:  Processed=1, Dropped=0, LossRate=0.0%, AvgLatency=2.0
BULK: Processed=0, Dropped=0, LossRate=N/A, AvgLatency=N/A
```
