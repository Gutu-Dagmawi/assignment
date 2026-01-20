# Problem 51: The Build Dependency Resolver

## Problem Description
A build system (like Make) needs to compile files. File A includes File B, so B must be compiled before A. The system must find a valid order or report a cycle.

### The System Rules
1.  **Dependencies**: Directed edges `B -> A` (B comes before A).
2.  **Topological Sort**:
    *   Find a node with 0 dependencies.
    *   "Compile" it.
    *   Remove it and its outgoing edges.
    *   Repeat.
3.  **Cycle Detection**: If nodes remain but none have 0 dependencies, there is a circular dependency.

## Must Use Data Structures
*   **Graph (Adjacency List)**: `Map<Node, List<Dependents>>`.
*   **Array**: `InDegree` count for each node.
*   **Queue**: To process nodes with In-Degree 0.

## Operations to Implement (CLI Commands)
*   `DEPENDS <A> <B>`: A depends on B (B -> A).
*   `BUILD`: Output build order or error.

## Sample Execution

```text
> DEPENDS Main Utils
> DEPENDS Utils Core
Graph: Core -> Utils -> Main

> BUILD
1. Core (InDegree 0)
2. Utils (InDegree becomes 0)
3. Main (InDegree becomes 0)
```
