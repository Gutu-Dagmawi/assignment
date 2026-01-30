# Problem 59: The VIP Spender Tracker (Top K)

## Problem Description

A CRM system monitors a live stream of purchases. It must identify the "Top 3" highest spending customers to offer them instant rewards.

### The System Rules

1.  **Data**: Stream of `(UserID, Amount)`.
2.  **Aggregation**:
    - `TotalSpend[User] += Amount`.
3.  **Leaderboard**:
    - Maintain the IDs of the top `K` spenders.
    - If a user's new total pushes them into the top K, update the board.

## Must Use Data Structures

- **Hash Map**: `User -> TotalMoney`.
- **Min-Heap (Size K)**: Stores `(Total, UserID)`.
  - The root is the "Poorest of the Rich".
  - If a user's total > Root.Total, we update the heap.

## Operations to Implement (CLI Commands)

- `PURCHASE <user> <amount>`
- `SHOW_VIP`: Print the Top K users.

## Sample Execution

```text
> PURCHASE U1 100
> PURCHASE U2 200
> PURCHASE U3 300
> PURCHASE U4 50  (Total 50. Heap Min is 100. Ignore)

> PURCHASE U1 250 (Total 350)
U1 is already in heap? Yes. update its value.
Heap re-sorts.
Top 3: U2(200), U3(300), U1(350).
```
