# 12 - Transactions & ACID

> **Goal**
>
> Understand how databases guarantee data consistency when multiple operations occur together. Learn transactions, COMMIT, ROLLBACK, ACID properties, race conditions, and database locking.

---

# Table of Contents

1. Why Transactions Exist
2. What is a Transaction?
3. COMMIT
4. ROLLBACK
5. The Bank Transfer Problem
6. ACID Properties
7. Race Conditions
8. Database Locks
9. Transactions in ORMs
10. Best Practices
11. Key Takeaways

---

# Why Transactions Exist

Imagine a banking application.

Alice transfers ₹500 to Bob.

At first glance, the process seems simple.

```
Alice Balance

↓

Subtract ₹500

↓

Bob Balance

↓

Add ₹500
```

But imagine something goes wrong halfway through.

Alice loses ₹500.

Bob never receives it.

Money has disappeared.

The database has become inconsistent.

Transactions exist to prevent situations like this.

---

# What is a Transaction?

A transaction is a group of database operations that are treated as a **single unit of work**.

Either:

✔ Every operation succeeds.

or

✔ None of them succeed.

There is no middle ground.

Think of it like a package.

Instead of executing each statement independently,

the database treats them as one logical operation.

---

# Example

Suppose we transfer money.

Step 1

```
Subtract ₹500

from Alice
```

Step 2

```
Add ₹500

to Bob
```

These two operations belong together.

If either one fails,

both should be cancelled.

That's exactly what a transaction does.

---

# COMMIT

COMMIT tells the database:

> Everything succeeded.

Save these changes permanently.

After a COMMIT,

the changes become permanent.

They cannot be automatically undone.

Think of COMMIT as:

```
Approve

↓

Save Forever
```

---

# ROLLBACK

ROLLBACK does the opposite.

It tells the database:

> Something went wrong.

Undo everything.

Suppose:

```
Subtract ₹500

↓

Server crashes
```

Instead of leaving Alice with less money,

ROLLBACK restores the database to its previous state.

The transfer never happened.

Think of ROLLBACK as:

```
Cancel

↓

Restore Previous State
```

---

# The Bank Transfer Problem

Suppose Alice has:

```
₹5000
```

Bob has:

```
₹1000
```

Alice transfers:

```
₹500
```

Without transactions

```
Alice

₹5000

↓

₹4500

↓

Server Crash

↓

Bob

Still ₹1000
```

Money disappears.

---

With transactions

```
Start Transaction

↓

Subtract ₹500

↓

Crash

↓

ROLLBACK

↓

Alice still has ₹5000

Bob still has ₹1000
```

Nothing is lost.

---

# ACID Properties

Every reliable relational database follows the ACID principles.

---

## A — Atomicity

Atomic means:

Indivisible.

Either everything happens.

Or nothing happens.

Never half.

Example:

Money transfer.

Not:

```
Subtract only
```

Instead:

```
Subtract

+

Add

↓

Together
```

---

## C — Consistency

A transaction must always leave the database in a valid state.

Rules should never be broken.

Example

A foreign key cannot suddenly reference a row that doesn't exist.

Constraints remain satisfied before and after every transaction.

---

## I — Isolation

Multiple users may access the database simultaneously.

Isolation ensures that one transaction does not interfere with another.

Imagine two people trying to buy the last concert ticket at exactly the same time.

Without isolation,

both purchases might succeed.

Isolation prevents these conflicts.

---

## D — Durability

Once COMMIT completes,

the data is permanent.

Even if:

- Power fails
- Server crashes
- Application stops

the committed data remains stored.

Durability protects successfully completed transactions.

---

# Race Conditions

A race condition occurs when two or more operations compete to modify the same data simultaneously.

Example

Account Balance

```
₹1000
```

Person A

Withdraws ₹800

Person B

Withdraws ₹500

If both read the balance before either update completes,

both think:

```
₹1000 available
```

Result

```
₹1300 withdrawn

from ₹1000
```

Impossible.

Transactions and locking mechanisms help prevent these situations.

---

# Database Locks

To prevent conflicting updates,

databases temporarily lock data.

Conceptually

```
Transaction A

↓

Locks Row

↓

Updates

↓

Unlocks
```

While the row is locked,

other conflicting transactions must wait.

Locks help maintain consistency.

---

# Transactions in ORMs

Frameworks like:

- Spring Boot
- Hibernate
- JPA

support transactions directly.

For example,

Spring provides:

```java
@Transactional
```

The annotation tells Spring:

> Execute this method as one transaction.

If an exception occurs,

Spring automatically rolls back the transaction.

Although the syntax changes,

the underlying database transaction is exactly the same.

---

# Best Practices

✔ Keep transactions as short as possible.

Long transactions hold locks for longer,

reducing concurrency.

---

✔ Only include operations that truly belong together.

Not every SQL statement needs its own transaction.

---

✔ Always handle failures.

Successful software assumes failures will happen eventually.

---

✔ Never ignore rollback.

Being able to recover safely is just as important as succeeding.

---

# Common Misconceptions

## "Transactions make queries faster."

False.

Transactions improve correctness,

not performance.

---

## "ROLLBACK only undoes one statement."

False.

It undoes the **entire transaction**.

---

## "Every SQL statement needs a transaction."

Not necessarily.

Simple reads usually don't.

Transactions are most important when multiple operations must succeed together.

---

# Key Takeaways

✔ A transaction groups multiple operations into one unit.

✔ COMMIT permanently saves changes.

✔ ROLLBACK undoes all operations in the transaction.

✔ Transactions prevent inconsistent data.

✔ ACID guarantees reliability.

✔ Atomicity means all or nothing.

✔ Consistency keeps data valid.

✔ Isolation prevents transactions from interfering.

✔ Durability keeps committed data safe.

✔ Locks help prevent conflicting updates.

---

# Summary

Transactions are one of the defining features of relational databases.

Rather than treating SQL statements independently, transactions allow multiple operations to behave as a single logical unit, ensuring that either all changes are applied or none are.

Combined with the ACID properties, transactions provide the reliability required by banking systems, e-commerce platforms, financial software, and virtually every production backend application.

For any backend developer, understanding transactions is essential—not because of the SQL syntax, but because they explain **how databases maintain correctness even when multiple users access the same data simultaneously.**
