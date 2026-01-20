# Problem 20: Bank Transaction Ledger with Rollback

## Problem Description
You are designing the core transaction engine for a banking system. The engine must process transactions in order, maintain account balances, and support auditable rollbacks of recent transactions.

### The System Rules
1.  **Accounts**: The system maintains multiple accounts, each with:
    *   `Account ID`
    *   `Balance`
2.  **Transactions**: Each transaction has:
    *   `Transaction ID`
    *   `Type` (DEPOSIT, WITHDRAW, TRANSFER)
    *   `Account(s)` involved
    *   `Amount`
    *   `Timestamp`
3.  **Processing Logic**:
    *   Transactions are queued and processed in FIFO order.
    *   **Validation**: WITHDRAW fails if balance is insufficient. TRANSFER fails if source balance is insufficient.
    *   **Audit Log**: Every processed transaction (success or failure) is logged.
4.  **Rollback Feature**:
    *   The system must support `ROLLBACK N` which reverses the last `N` *successful* transactions.
    *   Rollback must restore balances to their state before those transactions.
    *   Rolled-back transactions are marked in the audit log.

## Must Use Data Structures
*   **Queue**: For incoming transactions awaiting processing.
*   **Stack**: To enable LIFO rollback of successful transactions.
*   **Array/Hash Map**: To store account balances (keyed by Account ID).
*   **Linked List**: For the Audit Log (append-only, with rollback markers).

## Operations to Implement (CLI Commands)
*   `CREATE_ACCOUNT <id> <initial_balance>`: Create an account.
*   `TXN <type> <account> [to_account] <amount>`: Queue a transaction.
*   `PROCESS`: Process the next transaction in the queue.
*   `ROLLBACK <n>`: Reverse the last `n` successful transactions.
*   `BALANCE <account>`: Show account balance.
*   `AUDIT`: Show full transaction log.

## Sample Execution

```text
> CREATE_ACCOUNT A1 1000
> CREATE_ACCOUNT A2 500

> TXN DEPOSIT A1 200
> TXN WITHDRAW A1 300
> TXN TRANSFER A1 A2 400

> PROCESS
Success: DEPOSIT A1 200. Balance: 1200.

> PROCESS
Success: WITHDRAW A1 300. Balance: 900.

> PROCESS
Success: TRANSFER A1->A2 400. A1: 500, A2: 900.

> BALANCE A1
A1: 500

> ROLLBACK 1
Rolled back: TRANSFER A1->A2 400.
A1: 900, A2: 500.

> AUDIT
1. DEPOSIT A1 200 - SUCCESS
2. WITHDRAW A1 300 - SUCCESS
3. TRANSFER A1->A2 400 - ROLLED_BACK
```
