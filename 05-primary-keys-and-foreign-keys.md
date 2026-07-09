# 05 - Primary Keys & Foreign Keys

> **Goal**
>
> Understand how rows are uniquely identified, how tables are connected, and why primary and foreign keys are fundamental to relational databases.

---

# Table of Contents

1. Why Keys Exist
2. Primary Keys
3. Characteristics of a Good Primary Key
4. Types of Primary Keys
5. Choosing a Primary Key
6. Foreign Keys
7. Referential Integrity
8. Cascade Operations
9. Who Owns the Foreign Key?
10. Common Mistakes
11. Key Takeaways

---

# Why Keys Exist

Imagine a table like this.

| Name | Age |
|------|----:|
| Rahul | 20 |
| Rahul | 19 |
| Rahul | 22 |

Now suppose we want to update Rahul.

Which Rahul?

SQL has no way of knowing.

Every row must have something that uniquely identifies it.

That unique identifier is called a **Primary Key**.

---

# Primary Keys

A primary key is a column (or group of columns) whose value uniquely identifies every row in a table.

Example

Students

| id | name |
|---:|------|
| 1 | Rahul |
| 2 | Rahul |
| 3 | Rahul |

Although the names are identical, every student has a different ID.

The database always uses the primary key to uniquely identify a record.

---

# Characteristics of a Good Primary Key

A primary key should:

- Be unique.
- Never be NULL.
- Rarely change.
- Be simple.
- Uniquely identify one record.

Changing primary keys later can be expensive because other tables may depend on them.

---

# Types of Primary Keys

There are several ways to generate primary keys.

---

## Auto Increment Integer

Example

```text
1
2
3
4
5
```

Advantages

- Small
- Fast
- Easy to read
- Efficient indexes

Disadvantages

- Predictable
- Easy to guess IDs
- Doesn't work well across multiple databases without coordination

Most beginner applications use auto-increment IDs.

---

## UUID (Universally Unique Identifier)

Example

```text
550e8400-e29b-41d4-a716-446655440000
```

Advantages

- Globally unique
- Hard to guess
- Great for distributed systems
- Can be generated without contacting the database

Disadvantages

- Larger storage
- Slower indexes
- Harder for humans to read

Modern backend systems often prefer UUIDs, especially in distributed architectures.

---

## Natural Keys

Sometimes existing data is already unique.

Examples:

- Passport Number
- Aadhaar Number
- Email Address

These are called natural keys.

Although possible, they often make poor primary keys because real-world data can change.

---

## Composite Keys

Sometimes multiple columns together form the unique identifier.

Example

| StudentID | CourseID |
|-----------|-----------|

Neither column alone is unique.

Together they uniquely identify an enrollment.

Composite keys are common in bridge tables.

---

# Choosing a Primary Key

There is no universal best choice.

| Type | Best Used For |
|------|---------------|
| Auto Increment | Most applications |
| UUID | Distributed systems, public APIs |
| Natural Key | Rare, when guaranteed stable |
| Composite Key | Many-to-many relationship tables |

Choose a key based on the application's requirements.

---

# Foreign Keys

Primary keys identify rows.

Foreign keys connect tables.

Example

Students

| id | name |
|---:|------|
| 1 | Nitin |
| 2 | Rahul |

Orders

| id | student_id | amount |
|---:|------------|-------:|
| 1 | 1 | 500 |
| 2 | 2 | 800 |

Notice

Orders don't store names.

Instead they store:

```text
student_id
```

which points to:

```
Students.id
```

That is a foreign key.

---

# Referential Integrity

A foreign key guarantees that referenced data actually exists.

Suppose someone tries:

Orders

| student_id |
|------------|
| 999 |

But student 999 doesn't exist.

The database rejects it.

This prevents invalid relationships.

Maintaining these valid relationships is called **Referential Integrity**.

---

# Cascade Operations

Suppose a student is deleted.

What should happen to their orders?

Different applications need different behaviour.

---

## RESTRICT

Do not allow deletion.

Delete fails until related records are removed.

---

## CASCADE

Delete related rows automatically.

Delete Student

↓

Delete Orders

---

## SET NULL

Delete the parent.

Child row remains.

Foreign key becomes NULL.

---

The correct choice depends entirely on business rules.

---

# Who Owns the Foreign Key?

This is one of the most common beginner questions.

Rule:

**The table that depends on another table stores the foreign key.**

Example

A student belongs to a department.

Department

| id | name |
|---:|------|
| 1 | Computer Science |

Student

| id | name | department_id |
|---:|------|--------------:|
| 1 | Nitin | 1 |

Notice

A department does **not** need to store hundreds of student IDs.

Each student stores exactly one department ID.

This keeps the relationship simple and scalable.

A useful way to think about it is:

> **The "many" side usually stores the foreign key.**

---

# Common Mistakes

## Using Names Instead of IDs

Bad

```text
Orders

StudentName
```

Good

```text
Orders

StudentID
```

Names can change.

IDs should not.

---

## Changing Primary Keys

Primary keys should remain stable.

Changing them may require updating many related tables.

---

## Using Random Data as Keys

A phone number or email may seem unique today.

Tomorrow it may change.

Business data should rarely become a primary key.

---

# Key Takeaways

✔ Every table should have a primary key.

✔ Primary keys uniquely identify rows.

✔ Foreign keys connect tables.

✔ Foreign keys maintain referential integrity.

✔ UUIDs are globally unique but larger.

✔ Auto-increment integers are simple and efficient.

✔ The dependent table usually stores the foreign key.

✔ Good database design relies on stable keys.

---

# Summary

Primary keys and foreign keys form the foundation of relational databases.

Primary keys uniquely identify records, while foreign keys establish relationships between tables. Together they allow databases to store information without unnecessary duplication while ensuring that related data remains consistent.

Understanding keys is essential before learning joins, ORMs, JPA/Hibernate, and database relationships, since all of these technologies build upon the concepts introduced here.
