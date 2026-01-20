# Assignment Problems

## 1. Multi-Level Undo–Redo System (Text-Editor Core)

**Problem**
Design an undo–redo system for a text editor that supports:

- Insert character
- Delete character
- Undo
- Redo

Constraints:

- Unlimited undo/redo
- Redo stack clears on new action

**Must use**

- Two stacks (array or linked-list based)
- Linked list or array for text storage

**Key reasoning**

- Why stacks model history
- Trade-offs of array vs linked-list text representation

**Real-world value**
Core abstraction used in editors, IDEs, CAD software.

---

## 2. CPU Task Scheduler (Priority-Based)

**Problem**
Simulate a CPU scheduler where:

- Each task has an ID and priority
- Highest-priority task runs first
- Tasks can be added dynamically
- Completed tasks are removed

**Must use**

- Heap (priority queue)
- Queue (for completed tasks)

**Operations**

- Insert task
- Execute next task
- View pending tasks (sorted)

**Real-world value**
Operating systems, job schedulers, cloud task runners.

---

## 3. Call Center Simulation

**Problem**
Simulate a call center where:

- Incoming calls arrive with timestamps
- Calls are answered in FIFO order
- Track average waiting time
- Support call abandonment after a max wait

**Must use**

- Queue (circular preferred)
- Array for statistics

**Key reasoning**

- Why circular queues are memory-efficient
- Time-based simulation logic

**Real-world value**
Telecom systems, customer support analytics.

---

## 4. Browser History Navigation

**Problem**
Implement browser navigation supporting:

- Visit new page
- Back
- Forward

Constraints:

- Forward history clears on new visit

**Must use**

- Two stacks

**Extension**

- Show last _k_ visited pages

**Real-world value**
Classic application of stacks with clear semantics.

---

## 5. Memory Block Manager (First-Fit Allocation)

**Problem**
Simulate memory allocation:

- Free memory blocks are stored
- Requests ask for size
- Allocate using first-fit strategy
- Deallocate blocks and merge adjacent free blocks

**Must use**

- Linked list (free blocks)
- Sorting (to merge blocks)

**Key reasoning**

- Fragmentation
- Why linked lists outperform arrays here

**Real-world value**
Operating systems, embedded systems.

---

## 6. Hospital Patient Triage System

**Problem**
Patients arrive with severity scores.

- Highest severity treated first
- If severity ties, earlier arrival wins

**Must use**

- Heap (priority queue)
- Queue (tie-breaking)

**Key reasoning**

- Composite ordering
- Stable priority queues

**Real-world value**
Emergency systems, healthcare logistics.

---

## 7. Stock Price Analyzer (Streaming Data)

**Problem**
Process a stream of stock prices:

- Store last _N_ prices
- Support:
  - Min price
  - Max price
  - Sort prices on demand

**Must use**

- Circular array
- Sorting algorithms

**Key reasoning**

- Sliding window
- Memory constraints

**Real-world value**
Financial analytics, telemetry systems.

---

## 8. Expression Evaluator (Without Recursion)

**Problem**
Evaluate infix arithmetic expressions with:

- +, -, \*, /
- Parentheses

**Must use**

- Two stacks (operators & operands)

**Key reasoning**

- Operator precedence
- Stack-based parsing

**Real-world value**
Compilers, calculators, interpreters.

---

## 9. Event Log Processing System

**Problem**
System logs events with timestamps.

- Insert events
- Retrieve latest _k_ events
- Sort events by time

**Must use**

- Linked list or array
- Stack for recent events
- Sorting algorithms

**Real-world value**
Monitoring systems, observability tools.

---

## 10. Task Dependency Resolver (Simplified)

**Problem**
Tasks have execution times.

- Shortest task should execute first
- Tasks can be added dynamically

**Must use**

- Min-heap

**Extension**

- Show average waiting time

**Real-world value**
Build systems, CI pipelines.

---

## 11. Printer Job Management System

**Problem**
Print jobs have:

- Job ID
- Page count

Rules:

- Smaller jobs printed first
- Same size → FIFO

**Must use**

- Heap + Queue hybrid

**Key reasoning**

- Fair scheduling
- Multi-criteria ordering

**Real-world value**
Print servers, job schedulers.

---

## 12. Playlist Manager

**Problem**
Manage a music playlist:

- Add song
- Remove song
- Next / Previous song
- Loop playlist

**Must use**

- Circular doubly linked list

**Key reasoning**

- Bidirectional traversal
- Circularity benefits

**Real-world value**
Media players, streaming apps.

---

## 13. Online Exam Submission Queue

**Problem**
Students submit exams:

- Submissions queued
- Late submissions flagged
- Fastest submissions prioritized for grading

**Must use**

- Queue
- Heap (for grading priority)

**Real-world value**
Educational platforms, batch processing.

---

## 14. File Compression Job Manager

**Problem**
Files of varying sizes must be compressed.

- Smaller files first
- Track completed jobs

**Must use**

- Heap
- Stack or Queue for history

**Key reasoning**

- Throughput optimization

**Real-world value**
Backup systems, cloud storage.

---

## 15. Library Book Reservation System

**Problem**
Each book has a waiting list.

- Reserve book
- Cancel reservation
- Serve next reader

**Must use**

- Queue per book
- Array of queues

**Key reasoning**

- Data structure composition
- Memory layout

**Real-world value**
Library systems, inventory management.

## 16. Log Rotation & Retention System

**Problem**
Design a system that:

- Stores incoming log entries
- Keeps only the most recent _N_ logs
- Discards older logs automatically
- Supports retrieval of logs in chronological order

**Must use**

- Circular array
- Queue semantics

**Key reasoning**

- Fixed-size memory design
- Overwrite policies

**Real-world value**
Server logging, embedded systems.

---

## 17. Undoable Queue Operations

**Problem**
Implement a queue that supports:

- Enqueue
- Dequeue
- Undo last operation

**Must use**

- Queue
- Stack (to store inverse operations)

**Key reasoning**

- Inverse operation modeling
- State recovery

**Real-world value**
Transactional systems, command processors.

---

## 18. Network Packet Buffer Simulation

**Problem**
Simulate a router buffer:

- Packets arrive continuously
- Fixed buffer size
- Drop packets when full
- Process packets FIFO

**Must use**

- Circular queue
- Arrays

**Metrics**

- Packet loss rate
- Average queue length

**Real-world value**
Networking, routers, OS kernels.

---

## 19. Leaderboard System (Top-K Scores)

**Problem**
Maintain a leaderboard:

- Insert player scores
- Retrieve top _K_ players
- Support frequent updates

**Must use**

- Min-heap (size K)
- Array or linked list for history

**Key reasoning**

- Why min-heap for top-K
- Space–time tradeoffs

**Real-world value**
Gaming platforms, analytics dashboards.

---

## 20. Bank Transaction Processing Engine

**Problem**
Simulate bank transactions:

- Deposits and withdrawals arrive
- Transactions processed in order
- Support rollback of last _N_ transactions

**Must use**

- Queue
- Stack
- Array for account balances

**Key reasoning**

- Ordered processing vs reversibility

**Real-world value**
Financial systems, ledgers.

---

## 21. Real-Time Median Finder

**Problem**
Process a stream of integers and:

- Return median after each insertion

**Must use**

- Two heaps (min-heap and max-heap)

**Key reasoning**

- Partitioning data
- Heap balancing

**Real-world value**
Statistics engines, real-time analytics.

---

## 22. Train Platform Scheduling System

**Problem**
Trains arrive and depart at different times.

- Assign platforms efficiently
- Minimize platform usage

**Must use**

- Sorting
- Heap

**Key reasoning**

- Interval management
- Greedy strategies

**Real-world value**
Transportation systems.

---

## 23. Multi-Queue Customer Service System

**Problem**
Customers choose:

- Express queue
- Normal queue

Rules:

- Express customers prioritized
- Fairness guaranteed

**Must use**

- Multiple queues
- Heap or stack for statistics

**Key reasoning**

- Queue arbitration
- Starvation prevention

**Real-world value**
Retail checkout systems.

---

## 24. Task Timeout Manager

**Problem**
Tasks have deadlines.

- Execute tasks before timeout
- Expired tasks discarded

**Must use**

- Heap (earliest deadline first)
- Queue

**Key reasoning**

- Deadline scheduling

**Real-world value**
Real-time systems, OS scheduling.

---

## 25. Music Streaming Cache

**Problem**
Cache recently played songs:

- Max cache size
- Remove least recently played song

**Must use**

- Doubly linked list
- Array or heap for indexing

**Key reasoning**

- Temporal locality
- Cache eviction policies

**Real-world value**
Streaming services, caching systems.

---

## 26. Warehouse Order Fulfillment System

**Problem**
Orders have:

- Priority
- Arrival time

Rules:

- High priority first
- FIFO for same priority

**Must use**

- Heap
- Queue

**Key reasoning**

- Stable priority queues

**Real-world value**
Logistics, supply chain software.

---

## 27. Command History with Search

**Problem**
Store executed commands.

- Undo commands
- Search for recent commands
- Replay commands

**Must use**

- Stack
- Array or linked list
- Sorting or searching

**Key reasoning**

- History compression
- Temporal access patterns

**Real-world value**
Shells, IDEs, terminals.

---

## 28. Garbage Collection Simulation (Mark–Sweep Lite)

**Problem**
Simulate memory blocks:

- Allocate blocks
- Mark reachable blocks
- Sweep unreachable blocks

**Must use**

- Arrays
- Stacks (for marking traversal)
- Linked lists

**Key reasoning**

- Memory lifecycle
- Reachability

**Real-world value**
Language runtimes, VM internals.

---

## 29. Emergency Alert Dispatch System

**Problem**
Alerts have severity levels.

- High severity dispatched first
- Preserve order for same severity

**Must use**

- Heap
- Queue

**Key reasoning**

- Multi-criteria prioritization

**Real-world value**
Disaster response systems.

---

## 30. Job Interview Scheduling System

**Problem**
Candidates have:

- Availability slots
- Priority scores

Rules:

- Schedule highest priority first
- Resolve conflicts

**Must use**

- Sorting
- Heap
- Queue

**Key reasoning**

- Constraint resolution

**Real-world value**
HR systems, scheduling engines.
