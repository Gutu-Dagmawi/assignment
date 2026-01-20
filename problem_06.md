# Problem 06: Disaster Response Triage System (Dynamic Resource Allocator)

## Problem Description
You are designing the dispatch engine for a field hospital during a major crisis. The system must match patients to limited medical resources (Surgeons, Nurses, General Wards) while handling dynamic severity changes and strict isolation protocols.

### The System Rules
1.  **Patient Data**: Each patient has:
    *   `Name`
    *   `Severity` (1-100, higher is worse)
    *   `Time Arrived`
    *   `Condition Type` (Trauma, Viral, General)
2.  **Resources**: The hospital has finite counts of:
    *   `Surgeons` (Can treat Trauma & General)
    *   `Nurses` (Can treat General only)
    *   `Isolation Units` (Required for Viral)
3.  **Dynamic Logic**:
    *   **Priority Formula**: `Effective Score = Severity + (Wait Time in Minutes * 0.5)`. This means patients waiting longer "become" more urgent.
    *   **Resource Locking**: A resource is "Locked" for `Treatment Duration` when assigned.
    *   **Contagion Protocol**:
        *   Viral patients *cannot* be treated by standard staff unless put in an `Isolation Unit`.
        *   If no Isolation Units are free, Viral patients must queue in a separate "Quarantine Queue" regardless of severity to protect others.

## Must Use Data Structures
*   **Max-Heap**: To manage the general Waiting List (ordered by `Effective Score`).
*   **Update-able Heap / Priority Queue**: You must support `IncreaseKey` to update patient scores as time passes.
*   **Queue**: For the Quarantine line (FIFO).
*   **Arrays/Counters**: To track available resource pools globally.

## Operations to Implement (CLI Commands)
*   `ADD_PATIENT <name> <severity> <type>`: Add a patient.
*   `ADD_RESOURCE <type> <count>`: Initialize or add staff/beds.
*   `TICK`: Advance time. Update effective scores. Try to assign free resources to the highest priority waiting patients.
*   `PATIENT_REPORT <name>`: Check status (Waiting, Treating, Discharged).
*   `STATUS`: Show resource usage and queue lengths.

## Sample Execution

```text
> ADD_RESOURCE Surgeon 1
> ADD_RESOURCE IsolationUnit 0

> ADD_PATIENT Alice 80 Trauma
> ADD_PATIENT Bob 85 Viral
> ADD_PATIENT Charlie 50 Trauma

> TICK
Time 1:
- Alice (Score 80): Assigned to Surgeon.
- Bob (Score 85): WAITING (No Isolation Unit).
- Charlie (Score 50): WAITING.

> TICK
Time 2:
- Alice still in surgery.
- Charlie (Score 50 + 0.5 = 50.5).
- Bob (Score 85 + 0.5 = 85.5) - Still WAITING (Quarantine).

> ADD_RESOURCE IsolationUnit 1
> TICK
Time 3:
- Bob (Score 86): Assigned to Isolation Unit.
```