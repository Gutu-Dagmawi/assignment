# Problem 56: Video Streaming Packet Reassembler

## Problem Description
You are implementing the packet reassembly buffer for a video streaming client. Packets arrive out of order and must be reordered before playback.

### The System Rules
1.  **Packet Properties**:
    *   `Sequence Number` (unique, sequential in original order)
    *   `Data` (video frame fragment)
    *   `Arrival Time`
2.  **Buffer Logic**:
    *   Packets arrive with gaps and out of order (e.g., 1, 3, 2, 5, 4).
    *   The player needs packets in sequence: 1, 2, 3, 4, 5...
    *   Buffer packets until a consecutive sequence starting from `next_expected` is available.
3.  **Playback**:
    *   Release packets for playback only when consecutive.
    *   Example: If `next_expected = 3` and buffer has [3,4,5], release all three.
4.  **Jitter / Timeout**:
    *   If a packet is missing for more than `TIMEOUT` ticks, skip it (mark as lost) and advance.
5.  **Metrics**:
    *   Packet loss rate.
    *   Average buffer size.

## Must Use Data Structures
*   **Min-Heap**: For buffering packets ordered by Sequence Number.
*   **Queue**: For the playback output stream.
*   **Array/Counters**: For tracking expected sequence, losses, metrics.
*   **Circular Buffer** (Optional): For fixed-size jitter buffer.

## Operations to Implement (CLI Commands)
*   `SET_TIMEOUT <t>`: Configure missing packet timeout.
*   `RECEIVE <seq> <data>`: A packet arrives.
*   `TICK`: Advance time. Check for timeouts, release consecutive packets.
*   `PLAY`: Show packets available for playback.
*   `METRICS`: Show loss rate and buffer stats.

## Sample Execution

```text
> SET_TIMEOUT 5

> RECEIVE 1 "FrameA"
> RECEIVE 3 "FrameC"
> RECEIVE 2 "FrameB"

> TICK (Time 1)
Buffer: [1,2,3]. Next expected: 1.
Released: 1, 2, 3. Playback ready!

> PLAY
Playing: FrameA, FrameB, FrameC

> RECEIVE 5 "FrameE"
> RECEIVE 6 "FrameF"
(Missing: 4)

> TICK (Time 2-6)
Waiting for Seq 4...

> TICK (Time 7)
Timeout for Seq 4! Marked as LOST.
Next expected: 5. Buffer: [5,6].
Released: 5, 6.

> METRICS
Packets Received: 5
Packets Lost: 1
Loss Rate: 16.7%
Avg Buffer Size: 2.0
```
