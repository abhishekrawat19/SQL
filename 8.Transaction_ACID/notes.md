# 8. Transactions and ACID

A **transaction** is a sequence of operations performed as a single logical unit of work. All operations must succeed; if any operation fails, the entire transaction is rolled back. This "all or nothing" principle is fundamental for maintaining data integrity, especially in applications that handle financial or critical data.

**The Bank Transfer Analogy:** 🏦 The classic analogy is transferring money. Debiting money from Account A and crediting it to Account B must happen together. If the credit fails after the debit, the debit must be undone.

This guarantee is enforced by a set of properties known as **ACID**.

---

## The ACID Properties

ACID is an acronym for the four key properties that ensure reliable transaction processing.

| Property | Stands For | Description | Analogy (Bank Transfer) |
| :--- | :--- | :--- | :--- |
| **A** | **Atomicity** | Guarantees that all operations within a transaction are completed successfully. If not, the transaction is aborted, and the database is rolled back. It's "all or nothing." | The entire transfer (debit and credit) completes, or neither does. The money is never just "lost". |
| **C** | **Consistency** | Ensures the database remains in a valid state before and after the transaction. All data must be valid according to all defined rules and constraints. | The total amount of money in the bank remains the same after the transfer. Money is not created or destroyed. |
| **I** | **Isolation** | Ensures that concurrent transactions produce the same result as if they were executed sequentially. One transaction's intermediate state is hidden from others. | If someone checks balances during a transfer, they see the state *before* it started or *after* it finished, never an inconsistent intermediate state. |
| **D** | **Durability** | Guarantees that once a transaction has been committed, it will remain committed even in the case of a system failure (e.g., power outage). | Once the transfer is confirmed, the new balances are permanently saved and will survive a power outage at the bank. |

---

## Transaction Control Commands
* `BEGIN TRANSACTION` (or `START TRANSACTION`): Marks the beginning of a transaction.
* `COMMIT`: Saves all the changes made in the transaction to the database.
* `ROLLBACK`: Undoes all the changes made in the transaction.

---

## Practical SQL Example

Let's model the bank transfer scenario.

```sql
CREATE TABLE accounts (
    account_id INT PRIMARY KEY,
    owner_name VARCHAR(100),
    balance DECIMAL(10, 2) CHECK (balance >= 0)
);

INSERT INTO accounts (account_id, owner_name, balance) VALUES
(1, 'Alice', 1000.00),
(2, 'Bob', 500.00);
```

### 1. Successful Transaction with `COMMIT`
Transfer $200 from Alice to Bob. Both steps succeed, so we `COMMIT`.

```sql
BEGIN TRANSACTION;

-- Step 1: Debit Alice's account
UPDATE accounts
SET balance = balance - 200.00
WHERE account_id = 1;

-- Step 2: Credit Bob's account
UPDATE accounts
SET balance = balance + 200.00
WHERE account_id = 2;

-- Make the changes permanent
COMMIT;
```

### 2. Failed Transaction with `ROLLBACK`
Attempt to transfer $1500 from Alice (who now has $800). The operation would violate the `CHECK (balance >= 0)` constraint, so we `ROLLBACK`.

```sql
BEGIN TRANSACTION;

-- Attempt to debit Alice's account, which would result in a negative balance
UPDATE accounts
SET balance = balance - 1500.00 -- This would make her balance -700
WHERE account_id = 1;

-- In a real application, logic would detect the issue, or the database
-- would throw an error upon trying to commit a violated constraint.

-- We undo all changes made since the transaction began.
ROLLBACK;

-- After the rollback, Alice's balance is still $800. No changes were saved.
```

---

### 💡 Key Interview Takeaways

* **Bank Transfer Analogy:** This is the gold standard for explaining transactions and ACID. If you can walk through how each property applies to a bank transfer, you have demonstrated a solid understanding.
* **Why It Matters:** Explain that ACID compliance is crucial for applications that handle critical data, like e-commerce (orders, payments, inventory) or financial systems, because it guarantees data reliability.

### Common Interview Questions

1.  **What is a database transaction?**
    * *Answer:* It's a single, logical unit of work that may consist of one or more operations. It's treated as "all or nothing" to ensure data integrity, a property known as atomicity.
2.  **Can you explain the ACID properties?**
    * *Answer:* Use the bank transfer analogy to explain Atomicity (all or nothing), Consistency (data stays valid), Isolation (transactions don't interfere with each other), and Durability (committed changes are permanent).
3.  **What is the difference between `COMMIT` and `ROLLBACK`?**
    * *Answer:* `COMMIT` permanently saves all changes made during the current transaction. `ROLLBACK` discards all changes made during the transaction, restoring the database to the state it was in before the transaction began.