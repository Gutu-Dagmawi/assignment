# Problem 43: The Stock Market Spanner

## Problem Description
Technical analysts need to know the "Span" of a stock price: the number of consecutive days immediately preceding the current day (including today) where the price was less than or equal to today's price.

### The System Rules
1.  **Naive Approach**: Looking back day-by-day is O(N^2) in worst case.
2.  **Optimized Approach**: Use a stack to jump over days that are already known to be smaller.
3.  **Constraint**: Complete the calculation for `N` days in O(N) time.

## Must Use Data Structures
*   **Stack**: Stores indices of days. The stack maintains a set of "dominant" days in descending price order.

## Operations to Implement (CLI Commands)
*   `PROCESS_BATCH <list_of_prices>`: Output spans.

## Sample Execution

```text
> PROCESS_BATCH 100 80 60 70 60 75 85

Day 0 (100): Stack empty. Span 1. Stack: [0]
Day 1 (80): 80 < 100. Span 1. Stack: [0, 1]
Day 2 (60): 60 < 80. Span 1. Stack: [0, 1, 2]
Day 3 (70): 70 > 60. Pop 2. 70 < 80. Span 2 (Days 2,3). Stack: [0, 1, 3]
Day 4 (60): 60 < 70. Span 1. Stack: [0, 1, 3, 4]
Day 5 (75): 75 > 60 (Pop 4). 75 > 70 (Pop 3). 75 < 80. Span 4 (Days 2-5). Stack: [0, 1, 5]
...
```
