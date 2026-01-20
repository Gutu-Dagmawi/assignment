# Problem 21: The Real-Time Median Monitor

## Problem Description
Data analysts need to know the *median* transaction value flowing through a payment gateway at any millisecond. Sorting the entire history for every request is too slow.

### The System Rules
1.  **Input**: Stream of integer amounts.
2.  **Query**: `GET_MEDIAN`.
    *   If count is odd: Middle element.
    *   If count is even: Average of two middle elements.
3.  **Performance**:
    *   Insertion: O(log N).
    *   Median Retrieval: O(1).

## Must Use Data Structures
*   **Max-Heap**: Stores the smaller half of numbers (Root = Max of smaller half).
*   **Min-Heap**: Stores the larger half of numbers (Root = Min of larger half).
*   **Balancing**: The size difference between heaps must never exceed 1.

## Operations to Implement (CLI Commands)
*   `ADD <val>`
*   `MEDIAN`: Return current median.
*   `DEBUG`: Show contents of both heaps.

## Sample Execution

```text
> ADD 10
> ADD 20
> ADD 5
Sorted would be: [5, 10, 20]. Median 10.
LeftHeap (Max): [5]  <-- Wait. 10 is middle.
State: Left:[5], Right:[20]. 10 goes to Left.
Left:[10, 5], Right:[20].
Median = Left.Top (10).

> ADD 30
Sorted: [5, 10, 20, 30]. Median 15.
Right gets 30.
Left:[10, 5], Right:[20, 30].
Median = (10+20)/2 = 15.
```
