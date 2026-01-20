# Problem 47: The Social Feed Aggregator

## Problem Description
You are building the "News Feed" generation service. A user follows 500 friends. Each friend has a list of posts sorted by time. You must efficiently merge these into a single chronological feed.

### The System Rules
1.  **Input**: `K` sorted lists of posts.
2.  **Constraint**: You cannot simply concat all lists and sort (O(N log N)). You must use a "Merge K Sorted Lists" approach (O(N log K)).
3.  **Output**: Stream the posts one by one from most recent to oldest.

## Must Use Data Structures
*   **Max-Heap (Priority Queue)**: Size `K`. Stores the *current* latest post from each of the `K` friends.
*   **Iterator/Pointer**: Track position in each friend's list.

## Operations to Implement (CLI Commands)
*   `ADD_USER <id> <posts_list>`
*   `GET_NEXT_FEED`: Extract max from heap, fill spot with next post from that user.

## Sample Execution

```text
> ADD_USER U1 [Time 100, Time 90]
> ADD_USER U2 [Time 95, Time 80]
> ADD_USER U3 [Time 99]

Heap (Max): [100(U1), 95(U2), 99(U3)] -> Sorted [100, 99, 95] w/ logic.

> GET_NEXT_FEED
Post @ 100 (from U1).
(Refill U1: Next is 90).
Heap Now: [99(U3), 95(U2), 90(U1)].

> GET_NEXT_FEED
Post @ 99 (from U3).
(Refill U3: Empty).
Heap Now: [95(U2), 90(U1)].
```
