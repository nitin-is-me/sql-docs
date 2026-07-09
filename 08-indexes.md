# 08 - Indexes

> **Goal**
>
> Understand what database indexes are, how they work, why they dramatically improve query performance, and the trade-offs they introduce.

---

# Table of Contents

1. Why Indexes Exist
2. Searching Without an Index
3. What is an Index?
4. How Indexes Work
5. B-Tree Index
6. Hash Index
7. Advantages
8. Disadvantages
9. When Should You Create an Index?
10. Common Misconceptions
11. Key Takeaways

---

# Why Indexes Exist

Imagine a table containing one million users.

| id | name |
|---:|------|
| 1 | Alice |
| 2 | Bob |
| ... | ... |
| 1,000,000 | Nitin |

Now suppose someone searches for:

```
WHERE name = 'Nitin'
```

How does the database find that row?

Without any optimization, it has only one option:

Start from the first row.

↓

Compare.

↓

Move to the next.

↓

Compare.

↓

Repeat.

This process continues until the desired row is found.

This is called a **Full Table Scan**.

---

# Searching Without an Index

Imagine searching for a word in a 1000-page dictionary.

Without an index,

you would read:

Page 1

↓

Page 2

↓

Page 3

↓

...

↓

Page 1000

Eventually you'll find the word.

But it's painfully slow.

A database behaves the same way.

Without an index,

it may inspect every row.

---

# What is an Index?

An index is a separate data structure that helps the database locate rows much faster.

Instead of searching the table itself,

the database searches the index.

The index then tells the database exactly where the row is located.

Think of a book.

You don't search page by page.

You first look at:

```
Index

↓

Chapter

↓

Page Number
```

Then directly jump to that page.

A database index works similarly.

---

# How Indexes Work

Suppose the Users table looks like:

| id | name |
|---:|------|
| 1 | Alice |
| 2 | Bob |
| 3 | Charlie |
| 4 | David |
| 5 | Nitin |

An index on **name** may look conceptually like:

```
Alice  → Row 1

Bob    → Row 2

Charlie→ Row 3

David  → Row 4

Nitin  → Row 5
```

Now,

instead of checking every row,

the database quickly finds:

```
Nitin

↓

Row 5
```

The table itself remains unchanged.

The index is stored separately.

---

# B-Tree Index

The default index in most relational databases.

Instead of storing values in a long list,

they're organized into a balanced tree.

Conceptually:

```
               M

         /            \

     F                   T

   /   \              /      \

 A      J          P          Z
```

Searching becomes much faster because the database eliminates half of the remaining possibilities at each step.

This is similar to binary search.

B-Tree indexes are excellent for:

- Equality searches
- Range searches
- Sorting
- ORDER BY
- BETWEEN

Most indexes you'll create in PostgreSQL use B-Trees.

---

# Hash Index

Instead of organizing values into a tree,

Hash indexes compute a hash.

```
"Nitin"

↓

Hash Function

↓

Bucket 42
```

Advantages:

Very fast equality searches.

Example:

```
WHERE id = 25
```

Disadvantages:

Cannot efficiently perform:

- Range searches
- Sorting
- ORDER BY
- BETWEEN

For this reason,

B-Tree indexes are usually preferred.

---

# Advantages

## Faster Searching

The primary reason indexes exist.

---

## Faster Filtering

Queries using:

```
WHERE
```

often become dramatically faster.

---

## Faster Sorting

Indexes can improve:

```
ORDER BY
```

operations.

---

## Faster Joins

Since joins often compare indexed keys,

indexes improve join performance as well.

---

# Disadvantages

Indexes are not free.

---

## More Storage

Indexes consume disk space.

Every indexed column requires an additional data structure.

---

## Slower INSERT

Whenever a new row is inserted,

the index must also be updated.

---

## Slower UPDATE

If an indexed value changes,

the index changes too.

---

## Slower DELETE

Removing rows also requires updating indexes.

---

Every index speeds up reads,

but slows down writes slightly.

Database design is therefore a balance.

---

# When Should You Create an Index?

Indexes are most useful for columns that are:

Frequently searched.

Examples:

- Email
- Username
- Product ID
- Foreign Keys

Avoid indexing columns that:

- Change constantly.
- Have very few unique values.
- Are rarely queried.

Creating indexes on every column usually hurts performance rather than improving it.

---

# Common Misconceptions

## "Indexes make everything faster."

False.

Indexes improve reads.

They slow writes.

---

## "Every column should be indexed."

False.

Each index has a maintenance cost.

---

## "Primary Keys don't need indexes."

False.

Most relational databases automatically create an index for the primary key.

---

## "Foreign Keys automatically create indexes."

Depends on the database.

Some databases create them automatically.

Others recommend creating them manually.

Knowing your database system matters.

---

# Real-World Example

Imagine Instagram.

Searching:

```
username = "nitin"
```

must happen instantly.

Without an index,

the server could scan hundreds of millions of users.

With an index,

the username is found almost immediately.

This is one reason why indexes are essential for large applications.

---

# Key Takeaways

✔ Indexes improve query performance.

✔ They work like a book's index.

✔ B-Tree indexes are the most common.

✔ Hash indexes are optimized for equality searches.

✔ Indexes consume storage.

✔ Indexes slow INSERT, UPDATE, and DELETE operations.

✔ Good indexing is a balance between read and write performance.

✔ Primary keys are usually indexed automatically.

---

# Summary

Indexes are one of the most important performance features of relational databases.

Rather than changing how data is stored, indexes provide an additional structure that allows the database to locate rows much more efficiently.

Understanding indexes is essential for writing scalable applications, designing performant databases, and reasoning about why some SQL queries execute in milliseconds while others take several seconds.
