# Problem 35: The Fault-Tolerant Load Balancer

## Problem Description
Distribute web traffic across a cluster of servers. If a server dies, the traffic must skip it efficiently.

### The System Rules
1.  **Round Robin**: Request 1 -> Server A, Req 2 -> Server B, Req 3 -> Server C, Req 4 -> Server A.
2.  **Health Check**:
    *   Servers can be marked `DEAD`.
    *   The balancer must **skip** dead servers and deliver to the next healthy one in the ring.
3.  **Resurrection**:
    *   Dead servers can come back `ALIVE`. They rejoin the rotation.

## Must Use Data Structures
*   **Circular Linked List**:
    *   Nodes represent Servers.
    *   Each node has status `Active/Dead`.
    *   Pointer `Current` moves `Next -> Next` until `Active` is found.

## Operations to Implement (CLI Commands)
*   `ADD_SERVER <ip>`
*   `KILL_SERVER <ip>`
*   `REVIVE_SERVER <ip>`
*   `DISPATCH_REQUEST`: Print which server gets it.

## Sample Execution

```text
> ADD_SERVER S1
> ADD_SERVER S2
> ADD_SERVER S3
Ring: S1 -> S2 -> S3 -> (Loop)

> DISPATCH
To S1
> DISPATCH
To S2

> KILL_SERVER S3
marked S3 dead.

> DISPATCH
(Currently at S2). Next is S3 (Dead). Skip. Next is S1.
To S1.
```
