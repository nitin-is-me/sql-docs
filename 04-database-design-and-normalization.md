# 04 - Database Design & Normalization

> **Goal**
>
> Learn why databases are designed the way they are, why duplicate data causes problems, and how normalization helps create maintainable, consistent, and efficient database structures.

---

# Table of Contents

1. Why Database Design Matters
2. Data Redundancy
3. What is Normalization?
4. Why Normalize?
5. First Normal Form (1NF)
6. Second Normal Form (2NF)
7. Third Normal Form (3NF)
8. Advantages of Normalization
9. Disadvantages of Normalization
10. Denormalization
11. Practical Advice
12. Key Takeaways

---

# Why Database Design Matters

Writing SQL queries is only part of working with databases.

Before a single query is written, someone must decide:

- What tables should exist?
- What columns belong in each table?
- How should tables relate to one another?
- Which data should be stored only once?

These decisions determine how maintainable and scalable a database will be.

A poorly designed database eventually becomes difficult to maintain, even if the SQL queries are correct.

---

# Data Redundancy

Data redundancy means storing the same information multiple times.

Example:

| Student | Course | Teacher |
|----------|---------|----------|
| Alice | Java | John |
| Bob | Java | John |
| Charlie | Java | John |

Notice something?

The teacher's name appears repeatedly.

Now imagine John changes his name.

Every row must be updated.

Miss one row...

↓

The database becomes inconsistent.

This is called an **update anomaly**.

---

# Problems Caused by Duplicate Data

Poor database design can lead to several problems.

## Update Anomaly

Updating the same information in many places.

Example:

Teacher changes name.

Must update 500 rows.

Miss one...

Database becomes inconsistent.

---

## Insert Anomaly

Sometimes new information cannot be added without unrelated data.

Example:

A new teacher joins.

But no students have enrolled yet.

Where do we store the teacher?

---

## Delete Anomaly

Deleting one row accidentally removes unrelated information.

Example:

Only one student studies Physics.

If that student is deleted...

The Physics teacher disappears from the database too.

---

# What is Normalization?

Normalization is the process of organizing a database to reduce redundancy and improve consistency.

Instead of repeating information many times,

store it once.

Then connect related data using relationships.

---

Instead of

| Student | Teacher |
|----------|----------|
| Alice | John |
| Bob | John |
| Charlie | John |

Create two tables.

Teachers

| id | name |
|---:|------|
| 1 | John |

Students

| id | name | teacher_id |
|---:|------|-----------:|
| 1 | Alice | 1 |
| 2 | Bob | 1 |
| 3 | Charlie | 1 |

Now John's name exists only once.

---

# First Normal Form (1NF)

Rule:

Each column should contain only one value.

Bad

| Student | Subjects |
|----------|-----------|
| Alice | Java, SQL |

Good

| Student | Subject |
|----------|----------|
| Alice | Java |
| Alice | SQL |

Each cell contains exactly one value.

---

# Second Normal Form (2NF)

Rule:

Every non-key column should depend on the entire primary key.

In simple terms,

don't mix unrelated information into the same table.

Separate different entities into different tables.

---

# Third Normal Form (3NF)

Rule:

Columns should depend only on the primary key.

Not on another non-key column.

Example

Bad

Student

| StudentID | Department | HOD |
|-----------|------------|-----|
| 1 | CS | Dr. Sharma |
| 2 | CS | Dr. Sharma |

HOD depends on Department,

not Student.

Better

Departments

| id | name | hod |
|---:|------|-----|
| 1 | CS | Dr. Sharma |

Students

| id | name | department_id |
|---:|------|--------------:|
| 1 | Alice | 1 |
| 2 | Bob | 1 |

Now information exists only once.

---

# Advantages of Normalization

Normalization provides several benefits.

## Less Duplicate Data

Store information only once.

---

## Easier Updates

Change data in one place.

Every related record stays correct.

---

## Better Consistency

Less chance of contradictory information.

---

## Smaller Database

Repeated values consume unnecessary storage.

Normalization reduces duplication.

---

## Easier Maintenance

A well-designed database is much easier to extend.

---

# Disadvantages of Normalization

Normalization isn't free.

Highly normalized databases often require:

- More tables
- More joins
- Slightly more complex queries

However,

for most applications,

the benefits greatly outweigh the costs.

---

# Denormalization

Sometimes duplicate data is added intentionally.

Why?

Performance.

Example:

Suppose every request needs

User Name

Instead of joining tables every time,

some systems duplicate the username.

This speeds up reads,

but now updates become more difficult.

Denormalization is therefore a trade-off between:

Consistency

↓

and

Performance.

Large systems sometimes denormalize specific parts of their databases after identifying performance bottlenecks.

---

# Practical Advice

For most applications,

follow normalization.

Don't duplicate data unless there is a proven performance reason.

Premature denormalization usually creates more problems than it solves.

As a beginner,

it's far more important to design clean databases than to optimize early.

---

# Key Takeaways

✔ Good database design is as important as writing SQL queries.

✔ Duplicate data leads to update, insert, and delete anomalies.

✔ Normalization reduces redundancy.

✔ 1NF ensures atomic values.

✔ 2NF separates unrelated information.

✔ 3NF removes transitive dependencies.

✔ Normalization improves consistency and maintainability.

✔ Denormalization intentionally duplicates data for performance.

✔ Optimize only after identifying real bottlenecks.

---

# Summary

Normalization is one of the most important ideas in relational database design.

Rather than focusing on SQL syntax, it focuses on how information should be organized.

A well-normalized database is easier to maintain, less prone to bugs, and forms the foundation of scalable backend applications. While denormalization has its place in high-performance systems, normalization should be the default approach for most software projects.
