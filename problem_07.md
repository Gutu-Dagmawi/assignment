# Problem 07: The Streaming Stock Analyzer

## Problem Description
You are building a high-frequency trading analytics dashboard. The system receives a constant stream of stock price updates and must provide real-time statistics for a sliding time window.

### The System Rules
1.  **Data Stream**: Prices arrive as `(Price, Timestamp)`.
2.  **Sliding Window**: The system handles a fixed window size of `N` seconds (e.g., last 300 seconds).
    *   Data older than `CurrentTime - N` must be discarded immediately to save memory.
3.  **Real-Time Queries**:
    *   **Max Price**: What was the highest price in the current window?
    *   **Min Price**: What was the lowest price in the current window?
    *   **Average**: What is the simple moving average (SMA)?
4.  **Performance Constraint**: Queries must be faster than O(N). Ideally O(1) or O(log N). Scanning the entire array for every query is unacceptable.

## Must Use Data Structures
*   **Circular Queue / Array**: To store the raw price history of the current window (for calculating Average and handling expiration).
*   **Double-Ended Queue (Deque)**: To maintain the "Monotonic Queue" property for efficiently querying the Maximum (and Minimum) in O(1) amortized time.

## Operations to Implement (CLI Commands)
*   `SET_WINDOW <seconds>`: Define window size.
*   `UPDATE <price> <timestamp>`: Ingest new data point. Trigger expiration of old points.
*   `GET_MAX`: Return max price in window.
*   `GET_AVG`: Return average price.
*   `STATUS`: Show count of data points currently stored.

## Sample Execution

```text
> SET_WINDOW 10
> UPDATE 100 1
> UPDATE 105 2
> UPDATE 102 5

> GET_MAX
105

> UPDATE 110 12 (Time 12 > 10 window from Time 1? Wait, 12-10=2. Time 1 is expired)
- Expiring data point (100, @1)...

> GET_MAX
110
> GET_AVG
(105+102+110)/3 = 105.66
```
