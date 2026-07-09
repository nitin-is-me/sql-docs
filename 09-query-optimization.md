# 09 - Query Optimization

> **Goal**
>
> Understand different ways of retrieving data, when to use joins, nested queries, multiple conditions, and why writing SQL is not just about getting the correct answer, but also about writing efficient queries.

---

# Table of Contents

1. What is Query Optimization?
2. One Problem, Multiple Solutions
3. Joins
4. Nested Queries (Subqueries)
5. Multiple Conditions (AND / OR)
6. IN
7. EXISTS
8. Does SQL Execute Top to Bottom?
9. How the Query Optimizer Works
10. Writing Better Queries
11. Key Takeaways

---

# What is Query Optimization?

Many SQL queries can produce exactly the same result.

For example,

suppose we want:

> Names of students enrolled in the Java course.

This can often be written using:

- Joins
- Nested Queries
- EXISTS
- IN

All of them may produce identical results.

However,

their performance can differ depending on:

- database engine
- indexes
- table size
- query optimizer

Optimization is therefore about finding an efficient solution, not just a correct one.

---

# One Problem, Multiple Solutions

Imagine two people driving to the same destination.

One chooses the highway.

Another chooses city roads.

Both eventually arrive.

One may simply reach earlier.

SQL queries are similar.

Different queries can produce the same output while taking different paths internally.

---

# Joins

Joins combine related tables directly.

Example

```
Students

↓

Enrollments

↓

Courses
```

Advantages

- Easy to read
- Efficient for related tables
- Usually preferred
- Database optimizers understand joins very well

Joins are generally the first choice when combining information from multiple related tables.

---

# Nested Queries (Subqueries)

Sometimes one query depends on another.

Example

Question:

> Find every student enrolled in Java.

Conceptually

```
Find Java Course ID

↓

Use that ID

↓

Find Students
```

The second query depends on the first.

This is a nested query.

Nested queries often make logical problems easier to understand because they break a large question into smaller questions.

---

# Multiple Conditions

Filtering data can require several conditions.

Example

```
Department = CS

AND

Age > 20

AND

Marks > 90
```

Combining conditions makes queries more specific.

Common operators include:

- AND
- OR
- NOT

Think of them as logical operators rather than SQL keywords.

---

# IN

Suppose we need students from:

Delhi

Mumbai

Jaipur

Instead of writing:

```
city = Delhi

OR

city = Mumbai

OR

city = Jaipur
```

SQL provides:

```
IN (...)
```

Conceptually,

IN asks:

> Does this value belong to this collection?

It usually improves readability.

---

# EXISTS

Suppose we only care whether related data exists.

Not the data itself.

Example

> Does this customer have at least one order?

Instead of counting orders,

SQL can simply ask:

```
Does at least one row exist?
```

This is often more efficient because the database can stop searching after finding the first match.

EXISTS is therefore commonly used for existence checks.

---

# Does SQL Execute Top to Bottom?

Many beginners imagine SQL executes exactly as written.

It doesn't.

Databases contain a **Query Optimizer**.

The optimizer examines the query and decides:

- Which indexes to use.
- Which join order is best.
- Which execution strategy is fastest.

This means two different SQL statements may ultimately produce very similar execution plans.

Modern databases spend considerable effort optimizing queries automatically.

---

# How the Query Optimizer Works

Conceptually,

the optimizer asks questions such as:

- Is there an index?
- Which table is smaller?
- Which filter removes the most rows?
- Is a nested query better than a join?
- Can this operation be skipped?

Developers describe *what* they want.

The database often decides *how* to retrieve it.

This separation is one of SQL's greatest strengths.

---

# Writing Better Queries

Good SQL is not only correct.

It is also:

- Easy to read.
- Easy to maintain.
- Efficient.
- Predictable.

General guidelines

Prefer:

- Clear joins for related tables.
- Readable conditions.
- Appropriate indexes.
- Simple queries.

Avoid:

- Unnecessary nesting.
- Returning unused columns.
- Complex queries without need.
- Premature optimization.

Readable SQL is usually easier to optimize than confusing SQL.

---

# Real-World Advice

When writing production SQL,

first make the query:

✔ Correct.

Then make it:

✔ Readable.

Only optimize after measuring performance.

Most applications spend far more time maintaining SQL than writing it.

---

# Key Takeaways

✔ SQL problems often have multiple valid solutions.

✔ Joins are usually preferred for combining related tables.

✔ Nested queries break complex problems into smaller ones.

✔ IN improves readability for multiple comparisons.

✔ EXISTS is useful for checking whether related data exists.

✔ The query optimizer decides how SQL is actually executed.

✔ Correctness comes first.

✔ Optimization should be driven by measurement, not guessing.

---

# Summary

Query optimization is not about memorizing which SQL statement is "fastest."

Instead, it is about understanding that multiple solutions often exist, each with different trade-offs.

Modern databases contain sophisticated optimizers capable of rewriting and improving queries automatically. As developers, our responsibility is to write clear, correct SQL and understand the situations in which different querying techniques are appropriate.
