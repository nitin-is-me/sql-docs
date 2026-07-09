# 06 - Database Relationships

> **Goal**
>
> Learn how real-world relationships are represented in relational databases. This document explains one-to-one, one-to-many, many-to-one, and many-to-many relationships, along with how they are implemented using foreign keys and bridge tables.

---

# Table of Contents

1. What is a Relationship?
2. Why Relationships Matter
3. One-to-One
4. One-to-Many
5. Many-to-One
6. Many-to-Many
7. Bridge (Junction) Tables
8. Choosing the Correct Relationship
9. Common Mistakes
10. Key Takeaways

---

# What is a Relationship?

Real-world objects rarely exist independently.

Examples:

- A student belongs to a department.
- A customer places orders.
- An employee works for a company.
- A post has comments.
- A book has an author.

A relationship describes **how one table is connected to another.**

Relational databases are built around these relationships.

---

# Why Relationships Matter

Without relationships, data would need to be duplicated repeatedly.

Imagine storing the customer's full information inside every order.

```
Order 1

Customer Name
Customer Address
Customer Phone
```

```
Order 2

Customer Name
Customer Address
Customer Phone
```

Now imagine the customer changes their address.

Every order must be updated.

Instead, store customer information once.

Orders simply reference the customer using a foreign key.

This avoids duplication and keeps data consistent.

---

# One-to-One (1:1)

Definition

One record in Table A is related to exactly one record in Table B.

Example

Person

| id | name |
|---:|------|
| 1 | Nitin |

Passport

| id | person_id | passport_no |
|---:|----------:|-------------|
| 1 | 1 | X123456 |

One person has one passport.

One passport belongs to one person.

---

Common Examples

- Person ↔ Passport
- User ↔ User Settings
- Employee ↔ Locker
- Student ↔ Library Card

---

Implementation

Usually one table stores a foreign key with a UNIQUE constraint.

---

# One-to-Many (1:N)

Definition

One record is related to many records.

Example

Department

| id | name |
|---:|------|
| 1 | Computer Science |

Students

| id | name | department_id |
|---:|------|--------------:|
| 1 | Alice | 1 |
| 2 | Bob | 1 |
| 3 | Charlie | 1 |

One department

↓

Many students

---

This is probably the most common relationship in relational databases.

Examples

- Customer → Orders
- Blog → Posts
- Post → Comments
- Teacher → Students
- Company → Employees

---

Implementation

The foreign key is stored on the **many side**.

---

# Many-to-One (N:1)

Many-to-One is simply the opposite perspective of One-to-Many.

Example

From the student's perspective:

Many students

↓

One department

Nothing changes in the database.

Only the viewpoint changes.

---

Example

```
Many Employees

↓

One Company
```

or

```
Many Books

↓

One Publisher
```

---

# Many-to-Many (M:N)

Definition

Many records from one table relate to many records from another.

Example

Students

| id | name |
|---:|------|
| 1 | Alice |
| 2 | Bob |

Courses

| id | course |
|---:|--------|
| 1 | Java |
| 2 | SQL |

Alice studies Java and SQL.

Bob studies SQL.

Java has many students.

Students study many courses.

Neither table can store this relationship directly.

---

# Bridge (Junction) Tables

Many-to-many relationships are solved using a third table.

Enrollment

| student_id | course_id |
|------------|-----------|
| 1 | 1 |
| 1 | 2 |
| 2 | 2 |

Now everything works.

Students

↓

Enrollment

↓

Courses

---

Notice

The Enrollment table contains **only relationships.**

It doesn't duplicate names.

It stores IDs.

This is one of the most common designs in relational databases.

---

# Visualizing Relationships

## One-to-One

```
Person

1

──────

1

Passport
```

---

## One-to-Many

```
Department

1

──────

∞

Students
```

---

## Many-to-Many

```
Students

∞

──────

∞

Courses
```

Implemented as

```
Students

↓

Enrollment

↓

Courses
```

---

# Choosing the Correct Relationship

Ask a simple question.

Can one record relate to many?

If yes,

One-to-Many.

---

Can many records relate to one?

Many-to-One.

---

Can both sides have many?

Many-to-Many.

---

Can each side have exactly one?

One-to-One.

---

# Common Mistakes

## Storing Lists in One Column

Bad

| Student | Courses |
|----------|----------------|
| Alice | Java, SQL |

Good

Separate Courses table

+

Enrollment table

---

## Putting the Foreign Key on the Wrong Side

Wrong

Department

```
Student1
Student2
Student3
```

Correct

Student

```
department_id
```

The "many" side stores the foreign key.

---

## Duplicating Data

Don't repeat names.

Repeat IDs.

IDs connect tables.

Names describe them.

---

# Relationships in ORMs

When using frameworks such as JPA/Hibernate, these relationships are represented using annotations.

For example:

- `@OneToOne`
- `@OneToMany`
- `@ManyToOne`
- `@ManyToMany`

Although the syntax changes, the underlying database relationships remain exactly the same.

Understanding the database design first makes ORMs much easier to learn.

---

# Key Takeaways

✔ Relationships connect tables.

✔ One-to-One links one record with one record.

✔ One-to-Many is the most common relationship.

✔ Many-to-One is simply the opposite perspective.

✔ Many-to-Many requires a bridge table.

✔ The "many" side usually stores the foreign key.

✔ IDs should connect tables—not names.

✔ ORMs simply represent these same relationships in code.

---

# Summary

Relationships are what transform isolated tables into a relational database.

Rather than storing duplicate information, relationships allow data to remain organized, consistent, and maintainable. Most backend applications spend far more time working with relationships than with individual tables, making this one of the most important concepts in SQL and database design.

Understanding relationships thoroughly also provides the foundation for learning joins, JPA/Hibernate, and object-relational mapping.
