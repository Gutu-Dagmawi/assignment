# Problem 30: Interview Scheduling Optimizer

## Problem Description
You are building a scheduling system for a company's interview process. Candidates have availability windows, interviewers have slots, and the system must maximize the number of scheduled interviews while respecting constraints.

### The System Rules
1.  **Candidates**: Each candidate has:
    *   `Candidate ID`
    *   `Priority Score` (higher = more desirable to schedule first)
    *   `Availability Windows` (list of `[start, end]` time ranges)
2.  **Interviewers**: Each interviewer has:
    *   `Interviewer ID`
    *   `Available Slots` (list of `[start, end]` time ranges)
    *   `Max Interviews Per Day`
3.  **Scheduling Logic**:
    *   Process candidates in descending order of Priority Score.
    *   For each candidate, find an overlapping time slot with any available interviewer.
    *   If multiple interviewers are available, pick the one with the **most remaining capacity**.
    *   An interview takes exactly 1 hour.
4.  **Conflict Resolution**: A slot can only be used once. After scheduling, that hour is "consumed" for both candidate and interviewer.

## Must Use Data Structures
*   **Max-Heap**: To process candidates by Priority Score (highest first).
*   **Sorted Array + Binary Search**: To efficiently find overlapping time slots.
*   **Queue/List**: To store final scheduled interviews.
*   **Array of Linked Lists**: Interviewer availability as a list of free intervals (updated after each scheduling).

## Operations to Implement (CLI Commands)
*   `CANDIDATE <id> <priority> <windows>`: Add a candidate (windows as comma-separated ranges, e.g., "9-12,14-17").
*   `INTERVIEWER <id> <slots> <max_per_day>`: Add an interviewer.
*   `SCHEDULE`: Run the scheduling algorithm.
*   `REPORT`: Show all scheduled interviews and any candidates who could not be scheduled.

## Sample Execution

```text
> CANDIDATE C1 90 9-12,14-17
> CANDIDATE C2 85 10-11
> CANDIDATE C3 80 15-18

> INTERVIEWER I1 9-12,14-18 3
> INTERVIEWER I2 10-12 2

> SCHEDULE
Processing C1 (Priority 90)...
- Overlap with I1 at 9-12, 14-17. With I2 at 10-12.
- I1 has capacity 3, I2 has capacity 2. Picking I1.
- Scheduled: C1 with I1 at 9-10.

Processing C2 (Priority 85)...
- Overlap with I1 at 10-12. With I2 at 10-11.
- I1 capacity=2, I2 capacity=2. Tie. Picking I1 (first).
- Scheduled: C2 with I1 at 10-11.

Processing C3 (Priority 80)...
- Overlap with I1 at 15-18.
- Scheduled: C3 with I1 at 15-16.

> REPORT
Scheduled Interviews:
- C1 <-> I1 @ 9:00-10:00
- C2 <-> I1 @ 10:00-11:00
- C3 <-> I1 @ 15:00-16:00

Unscheduled Candidates: None.
I1 used 3/3 slots. I2 used 0/2 slots.
```
