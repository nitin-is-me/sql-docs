# 03 - Querying Data

> **Goal**
>
> Learn how SQL retrieves information from a database and understand the concepts behind filtering, sorting, grouping, and limiting data. The focus is on understanding how to ask meaningful questions from a database rather than memorizing SQL syntax.

---

# Table of Contents

1. Why Querying Matters
2. SELECT
3. WHERE
4. ORDER BY
5. ASC & DESC
6. LIMIT
7. COUNT()
8. GROUP BY
9. IN
10. Aliases
11. Combining Conditions
12. Key Takeaways

---

# Why Querying Matters

Most database interactions involve reading data rather than writing it.

Examples:

- Searching for a user
- Viewing products
- Listing transactions
- Displaying posts
- Finding unread notifications

These are all examples of querying.

The quality of an application often depends on how efficiently it retrieves information.

---

# SELECT

`SELECT` is the foundation of SQL querying.

It tells the database what information should be returned.

Example:

```sql
SELECT name
FROM students;
```

This returns only the `name` column.

Unlike spreadsheets, SQL allows selecting only the information that is needed.

Returning unnecessary data wastes memory, bandwidth, and processing time.

Whenever possible, avoid:

```sql
SELECT *
```

Instead, prefer selecting only the required columns.

---

# WHERE

Without a filter, SQL returns every row.

`WHERE` allows selecting only rows that satisfy a condition.

Example:

```sql
SELECT *
FROM students
WHERE age >= 18;
```

Think of `WHERE` as asking:

> "Only show me the rows that satisfy this condition."

Common comparison operators:

| Operator | Meaning |
|----------|---------|
| = | Equal |
| != | Not equal |
| > | Greater than |
| < | Less than |
| >= | Greater than or equal |
| <= | Less than or equal |

---

# ORDER BY

Databases do not guarantee the order of returned rows.

If ordering matters, it must be specified explicitly.

Example:

```sql
SELECT *
FROM students
ORDER BY marks;
```

This sorts the results.

Sorting can be performed on:

- numbers
- text
- dates

---

# ASC & DESC

Ordering may be:

Ascending:

```text
1
2
3
4
5
```

or

Descending:

```text
5
4
3
2
1
```

Example:

```sql
ORDER BY marks DESC;
```

Descending order is commonly used when showing:

- highest scores
- latest posts
- newest products
- largest transactions

---

# LIMIT

Sometimes only a few rows are needed.

Example:

```sql
SELECT *
FROM products
LIMIT 10;
```

This returns only the first ten rows.

Common use cases:

- Pagination
- Top results
- Dashboard widgets

---

# COUNT()

Sometimes we don't need the rows themselves.

We only need to know how many exist.

Example:

```sql
SELECT COUNT(*)
FROM students;
```

Result:

```
150
```

Aggregate functions summarize data instead of returning individual rows.

Examples include:

- COUNT()
- SUM()
- AVG()
- MIN()
- MAX()

CS50 focuses primarily on COUNT(), but SQL provides many aggregate functions.

---

# GROUP BY

Suppose we want to know:

> How many students belong to each department?

Instead of returning every student, SQL can group rows.

Example:

| Department | Students |
|------------|----------|
| Computer Science | 60 |
| Mathematics | 35 |
| Physics | 20 |

Grouping allows aggregate functions to operate on categories rather than the entire table.

Think of GROUP BY as creating temporary groups before performing calculations.

---

# IN

Suppose we want students from only three cities.

Instead of writing:

```sql
city = 'Delhi'
OR city = 'Mumbai'
OR city = 'Jaipur'
```

SQL allows:

```sql
WHERE city IN (...)
```

Conceptually,

`IN` asks:

> "Does this value belong to this collection?"

It improves readability and often makes queries easier to maintain.

---

# Aliases

Aliases give temporary names to columns or tables.

Instead of displaying:

```
COUNT(*)
```

we can display:

```
TotalStudents
```

Aliases improve readability.

They do **not** rename database columns permanently.

Their purpose is only to make the current query easier to understand.

---

# Combining Conditions

Conditions can be combined.

Example:

Find students who:

- belong to Delhi
- and have marks above 90

Multiple conditions make queries increasingly precise.

As conditions become more complex, SQL provides operators such as:

- AND
- OR
- NOT

These allow combining multiple filters into a single query.

---

# Thinking Like SQL

Rather than asking:

> "How do I write this SQL?"

Try asking:

> "What question am I asking the database?"

Examples:

Question:

> Which students scored above 90?

↓

WHERE

---

Question:

> Which student scored the highest?

↓

ORDER BY + LIMIT

---

Question:

> How many students are enrolled?

↓

COUNT()

---

Question:

> How many students belong to each department?

↓

GROUP BY + COUNT()

Thinking in terms of questions makes SQL much easier to understand.

---

# Key Takeaways

✔ SELECT retrieves data.

✔ WHERE filters rows.

✔ ORDER BY sorts results.

✔ ASC and DESC control sorting direction.

✔ LIMIT restricts the number of returned rows.

✔ COUNT() summarizes data instead of returning rows.

✔ GROUP BY creates groups before performing calculations.

✔ IN simplifies multiple equality comparisons.

✔ Aliases improve readability without modifying the database.

✔ SQL is fundamentally about asking questions of data.

---

# Summary

Querying is the heart of SQL.

While CRUD operations modify data, querying is how applications retrieve meaningful information.

Understanding how filtering, sorting, grouping, and aggregation work is far more valuable than memorizing individual SQL statements. Once you begin thinking of SQL as a language for asking questions, writing queries becomes significantly more intuitive.
