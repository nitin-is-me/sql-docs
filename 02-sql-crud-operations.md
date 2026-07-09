# 02 - SQL CRUD Operations

> **Goal**
>
> Understand the four fundamental operations that every database application performs and the SQL statements used to achieve them.

---

# Table of Contents

1. What is CRUD?
2. Create
3. Read
4. Update
5. Delete
6. Other Schema Operations
7. Data Types
8. DDL vs DML
9. Key Takeaways

---

# What is CRUD?

Every application that stores data performs four basic operations.

These operations are collectively known as **CRUD**.

| Operation | Purpose |
|------------|---------|
| Create | Add new data |
| Read | Retrieve existing data |
| Update | Modify existing data |
| Delete | Remove existing data |

Think about any real application.

For example, a banking application:

- Opening an account → Create
- Viewing account details → Read
- Updating address → Update
- Closing an account → Delete

Nearly every backend API you build with Spring Boot will revolve around these four operations.

---

# CREATE

The word **Create** actually refers to two different things.

## Creating a Table

Before storing data, the structure must exist.

Example:

```sql
CREATE TABLE students (
    id INTEGER,
    name TEXT
);
```

Notice that this creates the **table**, not the data.

Think of it as constructing an empty spreadsheet.

---

## Inserting Data

Once the table exists, rows can be inserted.

```sql
INSERT INTO students (id, name)
VALUES (1, 'Nitin');
```

This creates a new record.

Result:

| id | name |
|---:|------|
| 1 | Nitin |

Unlike `CREATE TABLE`, `INSERT` adds data rather than creating database structures.

---

# READ

Reading data means retrieving information from the database.

The most commonly used SQL statement is:

```sql
SELECT
```

Example:

```sql
SELECT * FROM students;
```

Result:

| id | name |
|---:|------|
| 1 | Nitin |

Almost every application performs far more reads than writes.

For example:

- Viewing products
- Opening profiles
- Reading messages
- Displaying search results

Most user interactions are read operations.

---

# UPDATE

Data rarely stays the same forever.

Suppose a user changes their name.

```sql
UPDATE students
SET name = 'Rahul'
WHERE id = 1;
```

Result:

| id | name |
|---:|------|
| 1 | Rahul |

Without the `WHERE` clause, every row in the table would be updated.

This is one of the most common beginner mistakes.

---

# DELETE

Deletes remove rows from a table.

Example:

```sql
DELETE FROM students
WHERE id = 1;
```

The row disappears.

The table still exists.

Only its contents change.

---

# Other Schema Operations

CRUD mainly focuses on data.

However, databases also need structural changes.

---

## ALTER

Used to modify an existing table.

Examples include:

- Adding a column
- Removing a column
- Renaming a column
- Changing a data type

Rather than rebuilding a table, SQL allows modifying its structure.

---

## DROP

Deletes an entire database object.

Example:

```sql
DROP TABLE students;
```

This removes:

- the table
- its data
- its structure

Unlike `DELETE`, which removes rows, `DROP` removes the entire object.

---

# Data Types

Each column stores a specific kind of data.

Common SQL data types include:

| Data Type | Purpose |
|-----------|---------|
| INTEGER | Whole numbers |
| REAL | Decimal numbers |
| TEXT | Strings |
| BOOLEAN | True or False |
| DATE | Calendar dates |
| TIMESTAMP | Date and time |

Different databases provide many additional data types, but these form the foundation.

Choosing an appropriate data type improves:

- storage efficiency
- validation
- query performance

---

# DDL vs DML

SQL statements are commonly grouped into categories.

## DDL (Data Definition Language)

Defines database structure.

Examples:

- CREATE
- ALTER
- DROP

Think of DDL as designing the building.

---

## DML (Data Manipulation Language)

Manipulates stored data.

Examples:

- SELECT
- INSERT
- UPDATE
- DELETE

Think of DML as moving furniture inside the building.

---

# Why CRUD Matters

Frameworks such as Spring Boot expose CRUD operations through REST APIs.

For example:

| HTTP Method | SQL Operation |
|-------------|---------------|
| POST | INSERT |
| GET | SELECT |
| PUT / PATCH | UPDATE |
| DELETE | DELETE |

Understanding CRUD makes it much easier to understand backend development.

---

# Key Takeaways

✔ CRUD forms the foundation of nearly every database application.

✔ `CREATE TABLE` creates structures, while `INSERT` creates data.

✔ `SELECT` retrieves data.

✔ `UPDATE` modifies existing rows.

✔ `DELETE` removes rows without deleting the table.

✔ `DROP` removes an entire database object.

✔ `ALTER` changes an existing table's structure.

✔ Choosing appropriate data types is important for correctness and efficiency.

✔ SQL statements are commonly categorized as DDL or DML.

---

# Summary

CRUD is more than just four SQL operations—it represents the core lifecycle of data inside an application.

Almost every backend service, whether built with Java, Spring Boot, or another framework, ultimately translates user actions into one or more CRUD operations against a database.

Understanding CRUD thoroughly provides the foundation for everything that follows, including querying, relationships, transactions, and ORMs.
