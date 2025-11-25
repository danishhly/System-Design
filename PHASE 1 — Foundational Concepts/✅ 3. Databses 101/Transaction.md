### **Transactions (in Databases)**

**Concept:** A transaction is a single, logical unit of work that comprises one or more database operations. It must be treated as a whole: either all its operations complete successfully, or none of them do. This is enforced by the **ACID properties** (Atomicity, Consistency, Isolation, Durability).

**Analogy:** Transferring money from Bank Account A to Bank Account B.

- **Steps involved:**
    1. Debit money from Account A.
    2. Credit money to Account B.
- **The Problem:** What if step 1 happens, but the system crashes before step 2? Money is gone from A but not in B! This is a disaster.
- **The Solution (Transaction):** These two steps are grouped into a single transaction.
    - If both steps succeed, the transaction is **committed**.
    - If *any* step fails (or the system crashes), the transaction is **rolled back**, and the database returns to its state *before* the transaction started (money is back in A).

**ACID Properties Revisited (Critical for Transactions):**

- **Atomicity:** "All or nothing." If the money transfer fails at any point, the entire operation is undone.
- **Consistency:** The transaction takes the database from one valid state to another. For example, the total amount of money in the bank must remain the same before and after the transfer.
- **Isolation:** If multiple people are transferring money simultaneously, each transaction appears to happen independently without interfering with others. You don't see half-completed transfers.
- **Durability:** Once the money transfer is successfully committed, it's permanently recorded and will survive power outages or system failures.

**Why are Transactions important?**

- **Data Integrity:** Guarantees that your data is always in a valid and consistent state.
- **Reliability:** Crucial for applications where data correctness is paramount (e.g., banking, e-commerce, inventory).
- **Concurrency Control:** Manages how multiple users or processes can access and modify the same data without corrupting it.