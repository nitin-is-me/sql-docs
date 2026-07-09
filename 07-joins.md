# 07 - Joins

> **Goal**
>
> Learn how SQL combines data from multiple tables using joins. Understanding joins is essential because relational databases store related information in separate tables rather than duplicating it.

---

# Table of Contents

1. Why Joins Exist
2. What is a Join?
3. INNER JOIN
4. LEFT JOIN
5. RIGHT JOIN
6. FULL OUTER JOIN
7. Self Join
8. Choosing the Correct Join
9. Common Mistakes
10. Key Takeaways

---

# Why Joins Exist

One of the biggest strengths of relational databases is that they avoid duplicate data.

Instead of storing everything inside one table, information is divided into multiple related tables.

Example

Students

| id | name |
|---:|------|
| 1 | Alice |
| 2 | Bob |

Departments

| id | department |
|---:|------------|
| 1 | Computer Science |
| 2 | Mathematics |

Students

| id | name | department_id |
|---:|------|--------------:|
| 1 | Alice | 1 |
| 2 | Bob | 2 |

Notice something.

The Students table does **not** contain department names.

It only stores:

```
department_id
```

To retrieve the department name, SQL combines both tables.

This process is called a **Join**.

---

# What is a Join?

A Join combines rows from two or more tables using related columns.

Think of it like connecting puzzle pieces.

```
Students

↓

department_id

↓

Departments
```

The database follows the relationship and combines matching rows.

---

# INNER JOIN

Definition

Returns **only matching rows** from both tables.

Suppose:

Students

| name | department_id |
|------|--------------:|
| Alice | 1 |
| Bob | 2 |
| Charlie | NULL |

Departments

| id | department |
|---:|------------|
| 1 | Computer Science |
| 2 | Mathematics |

Result

| Student | Department |
|----------|------------|
| Alice | Computer Science |
| Bob | Mathematics |

Charlie is missing because there is no matching department.

Think of INNER JOIN as:

> Show only rows that successfully match.

---

# LEFT JOIN

Definition

Return **every row from the left table**, even if no matching row exists on the right.

Same example.

Result

| Student | Department |
|----------|------------|
| Alice | Computer Science |
| Bob | Mathematics |
| Charlie | NULL |

Charlie appears because LEFT JOIN never removes rows from the left table.

Missing matches become NULL.

Use LEFT JOIN when the left table is more important than the right one.

Example:

Show every customer, even those who have never placed an order.

---

# RIGHT JOIN

Definition

Opposite of LEFT JOIN.

Return every row from the right table.

Missing matches on the left become NULL.

Example

Departments

| Department |
|------------|
| Computer Science |
| Mathematics |
| Physics |

Students

Only CS and Mathematics have students.

Result

| Student | Department |
|----------|------------|
| Alice | CS |
| Bob | Mathematics |
| NULL | Physics |

Physics still appears because it belongs to the right table.

---

# FULL OUTER JOIN

Definition

Return every row from both tables.

If a match exists,

combine them.

If no match exists,

fill the missing side with NULL.

Think of it as:

```
LEFT JOIN

+

RIGHT JOIN
```

Not every database supports FULL OUTER JOIN directly.

---

# Self Join

Sometimes a table relates to itself.

Example

Employees

| id | name | manager_id |
|---:|------|-----------:|
| 1 | Alice | NULL |
| 2 | Bob | 1 |
| 3 | Charlie | 1 |

Employees reference other employees.

To retrieve the manager's name,

the Employees table must join with itself.

This is called a Self Join.

Common examples:

- Employees and Managers
- Categories and Parent Categories
- Comments and Parent Comments

---

# Visualizing Joins

## INNER JOIN

```
Students

∩

Departments
```

Only the overlap.

---

## LEFT JOIN

```
Entire Left Table

+

Matching Right Rows
```

---

## RIGHT JOIN

```
Entire Right Table

+

Matching Left Rows
```

---

## FULL OUTER JOIN

```
Everything

Left

+

Right
```

---

# Choosing the Correct Join

Use INNER JOIN when:

- Both records must exist.

Examples:

- Orders with Customers
- Enrollments with Students

---

Use LEFT JOIN when:

- Left table is mandatory.
- Right table is optional.

Examples:

- Customers with Orders
- Users with Profile Pictures

---

Use RIGHT JOIN

Less common.

Can usually be rewritten as a LEFT JOIN by swapping table order.

Many developers simply prefer LEFT JOIN because it's easier to read consistently.

---

Use FULL OUTER JOIN

When every record from both tables matters.

---

# Common Mistakes

## Joining Without a Condition

Forgetting the join condition produces a Cartesian Product.

Every row joins with every other row.

Example

100 students

×

100 departments

↓

10,000 rows

Usually not what you want.

---

## Joining on the Wrong Column

Always join using related keys.

Correct

```
student.department_id

↓

department.id
```

Not

```
student.id

↓

department.id
```

unless that relationship actually exists.

---

## Overusing Joins

Joins are powerful,

but joining too many tables can make queries slower and harder to understand.

Keep queries as simple as possible.

---

# Joins vs Nested Queries

Sometimes the same result can be achieved using:

- Joins
- Nested Queries (Subqueries)

Neither is universally better.

General guideline:

Use joins when combining related tables.

Use nested queries when one query naturally depends on the result of another.

Query optimization is discussed separately because performance depends on the database engine, indexes, and the specific query.

---

# Joins in ORMs

Frameworks like Hibernate perform joins automatically.

For example:

```
Student

↓

Department
```

When you access:

```java
student.getDepartment().getName();
```

Hibernate may generate a SQL JOIN behind the scenes.

Understanding joins helps explain what the ORM is actually doing.

---

# Key Takeaways

✔ Joins combine information from multiple tables.

✔ INNER JOIN returns only matching rows.

✔ LEFT JOIN keeps every row from the left table.

✔ RIGHT JOIN keeps every row from the right table.

✔ FULL OUTER JOIN keeps every row from both tables.

✔ Self Joins connect a table with itself.

✔ Joins work by following relationships created through primary and foreign keys.

✔ ORMs generate joins automatically based on entity relationships.

---

# Summary

Relational databases intentionally separate related information into different tables to reduce duplication and improve consistency.

Joins are the mechanism that reconnect these pieces of information when querying data.

Understanding joins is essential not only for writing SQL, but also for understanding how ORMs like Hibernate retrieve related objects in Java applications.
