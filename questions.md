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

HR systems, scheduling engines.

---

## 31. Restaurant Waiting List Manager

**Problem**
Manage a restaurant waiting list where:

- Customers arrive and are added to the back
- VIP customers can be added to the front
- Customers can leave the queue (cancel) from any position
- Seat the next customer from the front

**Must use**

- Doubly Linked List

**Key reasoning**

- O(1) insertion at both ends
- O(1) deletion (if node reference is kept)

**Real-world value**
Reservation systems, support ticket escalation.

---

## 32. Browser Tab Manager

**Problem**
Simulate a browser's tab system:

- Open new tab
- Close current tab
- Switch to next/previous tab (wrapping around)

**Must use**

- Circular Doubly Linked List

**Key reasoning**

- Cyclic navigation
- Bidirectional traversal

**Real-world value**
Web browsers, carousel UI components.

---

## 33. Parenthesis Matching Verifier

**Problem**
Verify valid parenthesis usage in code:

- Support (), {}, []
- Input: String of characters
- Output: Valid/Invalid

**Must use**

- Stack

**Key reasoning**

- Nested structure validation
- Immediate failure detection

**Real-world value**
Compilers, linters, code editors.

---

## 34. Parking Garage System

**Problem**
A single-lane driveway parking garage:

- Cars enter and fill the garage
- To retrieve a car, all cars behind it must move out temporarily
- Last car in is the first one easily accessible

**Must use**

- Stack (or two stacks for retrieval simulation)

**Key reasoning**

- LIFO constraint physical modeling

**Real-world value**
Valet parking logistics, stack-based memory allocation.

---

## 35. Round-Robin Load Balancer

**Problem**
Distribute requests across servers:

- List of server IPs
- Assign request to next server in list
- Loop back to first server after the last

**Must use**

- Circular Queue or Linked List

**Key reasoning**

- Infinite cycling
- Fair distribution

**Real-world value**
Cloud infrastructure, traffic distribution.

---

## 36. Web Crawler URL Frontier

**Problem**
Manage URLs to visit during crawling:

- Add extracted links to list
- Visit links in order of discovery
- Avoid duplicates (optional constraint)

**Must use**

- Queue

**Key reasoning**

- BFS traversal strategy
- FIFO processing

**Real-world value**
Search engines, site archivers.

---

## 37. Text Editor Cursor Tracker

**Problem**
Track text relative to cursor:

- Type characters (left of cursor)
- Move cursor left/right
- Backspace (delete left of cursor)

**Must use**

- Two Stacks (Left and Right stacks)

**Key reasoning**

- O(1) operations for typing/deleting
- Gap buffer simulation

**Real-world value**
Text editors (Emacs), buffer management.

---

## 38. DNA Helix Storage

**Problem**
Store and analyze DNA sequences:

- Store base pairs (A, T, C, G)
- Support traversal 5' to 3' and 3' to 5'
- Match pairing (A-T, C-G)

**Must use**

- Doubly Linked List

**Key reasoning**

- Bidirectional reading
- Insertion/deletion of mutations

**Real-world value**
Bioinformatics, genomic sequencing tools.

---

## 39. Polynomial Addition System

**Problem**
Represent and add composed polynomials:

- Store coefficients and exponents (e.g., 3x^2 + 2x - 5)
- Add two polynomials efficiently

**Must use**

- Singly Linked List (sorted by exponent)

**Key reasoning**

- Sparse data handling (skips zero terms)
- Merging sorted lists logic

**Real-world value**
Computer algebra systems, scientific computing.

---

## 40. Supermarket Checkout Optimization

**Problem**
Multiple checkout counters:

- Customers choose shortest line
- Process customers FIFO
- Open/Close counters dynamically

**Must use**

- Array of Queues

**Key reasoning**

- Parallel resource management
- Load balancing

**Real-world value**
POS systems, bank teller logistics.

---

## 41. Navigation Route Retracer

**Problem**
GPS navigation system:

- Record turn-by-turn instructions
- "U-turn" or "Go Back" reverses the route steps

**Must use**

- Stack

**Key reasoning**

- Reversing a sequence
- Backtracking

**Real-world value**
Maps applications, robot path planning.

---

## 42. Snake Game Body Management

**Problem**
Track the snake's body segments:

- Head moves to new coordinate
- Tail segment removed (unless food eaten)
- Check for self-collision

**Must use**

- Queue (or Deque)

**Key reasoning**

- Sliding window of coordinates
- O(1) add/remove ends

**Real-world value**
Gaming logic, buffer streams.

---

## 43. Stock Span Problem

**Problem**
Calculate stock span:

- For each day, count consecutive prior days with lower price
- Efficient calculation (better than O(N^2))

**Must use**

- Stack

**Key reasoning**

- Nearest greater element logic
- Monotonic stack

**Real-world value**
Financial technical analysis.

---

## 44. Sliding Window Maximum (Network Traffic)

**Problem**
Monitor network packets:

- Fixed time window (e.g., last 5 seconds)
- Track maximum packet size in current window
- Update as window slides

**Must use**

- Dequeue (Double Ended Queue)

**Key reasoning**

- Monotonic queue property
- O(N) total time complexity

**Real-world value**
Network congestion control, signal processing.

---

## 45. LRU Cache Implementation

**Problem**
Cache limited number of items:

- Access item (promote to most recent)
- Insert item (evict least recent if full)

**Must use**

- Doubly Linked List
- (Hash Map mentioned for O(1) lookup typically, but focus here on the list structure)

**Key reasoning**

- O(1) move-to-front
- O(1) removal of tail

**Real-world value**
Database caching, OS page replacement.

---

## 46. Blockchain Simple Ledger

**Problem**
Simulate a blockchain:

- Each block contains data and "hash" of previous
- Verify chain integrity (traverse and check hashes)
- Add block to end

**Must use**

- Singly Linked List

**Key reasoning**

- Dependency chain
- Tamper evidence structure

**Real-world value**
Cryptocurrency, secure logging strings.

---

## 47. Social Media Feed (Merge Sources)

**Problem**
Combine posts from multiple followed users:

- Users have sorted lists of posts (by time)
- Merge into one chronological feed

**Must use**

- Min-Heap (or Max-Heap)

**Key reasoning**

- Merge K sorted lists
- Efficient ordering

**Real-world value**
News feeds (Facebook/Twitter), aggregator apps.

---

## 48. Traffic Light Controller

**Problem**
Manage traffic lights at a junction:

- Cycle: Red -> Green -> Yellow -> Red
- Timer triggers change to next state

**Must use**

- Circular Linked List

**Key reasoning**

- Finite state machine representation
- Infinite loop logic

**Real-world value**
Embedded systems, intersection control.

---

## 49. File System Directory Structure

**Problem**
Represent folders and files:

- Folders can contain files or other folders
- Calculate total size of a directory
- List all files (traversal)

**Must use**

- Tree (N-ary) / Linked Nodes

**Key reasoning**

- Hierarchical data representation
- Recursive traversal

**Real-world value**
OS file systems, DOM structure.

---

## 50. Keyboard Input Buffer

**Problem**
Handle fast typing vs slow CPU:

- Keys pressed stored in buffer
- CPU processes keys FIFO
- Buffer has fixed size (ring buffer)

**Must use**

- Circular Queue

**Key reasoning**

- Producer-consumer problem
- Fixed memory reuse

**Real-world value**
Device drivers, input handling.

---

## 51. Job Scheduling with Dependencies

**Problem**
Schedule jobs where:

- Job A must finish before Job B
- Detect circular dependencies (impossible schedule)
- Output valid execution order

**Must use**

- Graph (Adjacency List)
- Stack (for topological sort)

**Key reasoning**

- Precedence resolution
- Cycle detection

**Real-world value**
Build tools (Make/Webpack), project management.

---

## 52. Flight Boarding Groups

**Problem**
Manage boarding passengers:

- Groups: First Class (1), Business (2), Economy (3)
- Process Group 1, then 2, then 3
- FIFO within same group

**Must use**

- Priority Queue (or Array of Queues)

**Key reasoning**

- Stable priority handling

**Real-world value**
Airline logistics, tiered service handling.

---

## 53. Online Auction Bid Tracker

**Problem**
Track bids in an active auction:

- Accept new higher bids
- View current highest bid instantaneously
- History of valid bids

**Must use**

- Stack (history)
- Variable for Max (or Stack implies Max at top if strict increase)

**Key reasoning**

- Temporal state tracking
- Max tracking

**Real-world value**
eCommerce bidding, stock high-water marks.

---

## 54. Recursive Function Call Visualizer

**Problem**
Simulate/Visualize recursion depth:

- Function calls push to stack
- Returns pop from stack
- Track current depth and variables

**Must use**

- Stack

**Key reasoning**

- LIFO execution flow
- Memory limit understanding (Stack Overflow)

**Real-world value**
Debuggers, language runtimes.

---

## 55. Word Processor Undo/Redo (Granular)

**Problem**
Advanced undo system:

- Save state after every word (not char)
- Max history size limits
- Oldest history drops when full

**Must use**

- Dequeue (Double Ended Queue)

**Key reasoning**

- Bounded history buffer
- Remove from front, add to back, remove from back (undo)

**Real-world value**
Office software, creative tools.

---

## 56. Packet Reassembly Buffer

**Problem**
Video streaming packets arrive out of order:

- Sequence IDs: 1, 2, 4, 3, 5...
- Buffer until consecutive sequence can be played
- Release 1, 2, 3, 4, 5...

**Must use**

- Min-Heap (or Sorted List)

**Key reasoning**

- Reordering stream
- Handling jitter

**Real-world value**
VoIP, video streaming (Netflix/Zoom).

---

## 57. Contact List (Phonebook)

**Problem**
Store contacts alphabetically:

- Add contact (maintain order)
- Remove contact
- Scroll Previous/Next from any contact

**Must use**

- Doubly Linked List (Sorted)

**Key reasoning**

- Ordered insertion
- Bidirectional browsing

**Real-world value**
Address books, older mobile UIs.

---

## 58. Maze Solver (Backtracking)

**Problem**
Find a path through a maze:

- Move forward until blocked
- Backtrack to last branch choice
- Store current path

**Must use**

- Stack

**Key reasoning**

- Depth First Search (DFS)
- Decision history

**Real-world value**
Robotics pathfinding, puzzle solvers.

---

## 59. Customer Churn Analysis (Top K)

**Problem**
Identify top K customers by spending:

- Stream of transactions comes in
- Maintain top K spenders at all times

**Must use**

- Min-Heap (size K)

**Key reasoning**

- Efficiently tracking "largest" subset
- Ejection of smallest of the top K

**Real-world value**
CRM systems, fraud detection outliers.

---

## 60. Keyword Autocomplete (Simple)

**Problem**
Suggest words based on prefix:

- Input: "ap"
- Output: "apple", "apply", "apt"
- Store dictionary efficiently for prefix lookups

**Must use**

- Tree (Trie) / N-ary Tree

**Key reasoning**

- Prefix sharing
- Fast lookup by character path

**Real-world value**
Search bars, mobile keyboards.


