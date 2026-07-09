# 01 - Introduction to Databases

> **Goal**
>
> This document introduces databases, why they exist, different types of databases, and when each should be used. Before learning SQL, it is important to understand what problem databases solve.

---

# Table of Contents

1. What is a Database?
2. Why Databases Exist
3. Types of Databases
4. Relational Databases
5. NoSQL Databases
6. Common Database Systems
7. CSV & TSV Files
8. Creating a Database
9. Choosing the Right Database
10. Summary

---

# What is a Database?

A database is an organized collection of data that allows information to be stored, retrieved, updated, and deleted efficiently.

Unlike ordinary files, databases are designed to handle:

- Large amounts of data
- Fast searching
- Concurrent users
- Data consistency
- Relationships between data

For example, instead of storing users inside a text file:

```text
Nitin
Rahul
Aman
```

a database stores structured records that can be searched, filtered, updated, and connected with other data.

---

# Why Databases Exist

Imagine building an e-commerce website without a database.

You would need to manually store:

- Users
- Products
- Orders
- Payments
- Reviews

inside files.

Problems quickly appear:

- Searching becomes slow.
- Updating data is difficult.
- Multiple users can overwrite each other's data.
- Relationships become complicated.
- Data gets duplicated.

Databases solve these problems by providing efficient storage and management of data.

---

# Types of Databases

Databases can broadly be divided into two categories.

## Relational Databases (SQL)

Store data inside tables.

Example:

| id | name | age |
|---:|------|----:|
| 1 | Nitin | 21 |
| 2 | Rahul | 20 |

Characteristics:

- Structured
- Tables
- Rows and columns
- Relationships between tables
- Uses SQL

Examples:

- PostgreSQL
- MySQL
- SQLite
- Oracle Database
- Microsoft SQL Server

---

## NoSQL Databases

NoSQL databases don't necessarily store data in tables.

Instead they may use:

- Documents
- Key-Value pairs
- Graphs
- Wide-column storage

Example (Document Database)

```json
{
    "name": "Nitin",
    "age": 21,
    "skills": [
        "Java",
        "SQL"
    ]
}
```

Examples:

- MongoDB
- Redis
- Cassandra
- Neo4j

---

# Relational Databases

Relational databases organize information into tables.

Example

## Users

| id | name |
|---:|------|
| 1 | Nitin |
| 2 | Rahul |

## Orders

| id | user_id | amount |
|---:|---------|--------|
| 1 | 1 | 500 |
| 2 | 2 | 800 |

Notice that Orders don't store usernames.

Instead, they store the **user's ID**.

This relationship allows databases to avoid duplicate information while keeping data connected.

Relational databases are excellent when:

- Data has relationships.
- Data consistency is important.
- Transactions are required.
- Complex querying is common.

---

# NoSQL Databases

NoSQL databases sacrifice some structure in exchange for flexibility or scalability.

Example use cases:

- Caching
- Real-time analytics
- Chat applications
- Session storage
- Large-scale distributed systems

They are often preferred when data structure changes frequently or horizontal scaling is required.

NoSQL does **not** mean "No SQL."

It generally means "Not Only SQL."

Many modern systems use both SQL and NoSQL together.

---

# Common Database Systems

## SQLite

- Lightweight
- Entire database stored in a single `.db` file
- No server required
- Extremely easy to use

Best for:

- Learning SQL
- Small applications
- Local tools
- Mobile apps
- Desktop software

Limitations:

- Not designed for many concurrent users.
- Limited scalability.

---

## PostgreSQL

An advanced open-source relational database.

Features:

- ACID compliant
- Powerful indexing
- Advanced SQL support
- JSON support
- Extensions
- Excellent reliability

Best for:

- Backend applications
- Enterprise software
- APIs
- Financial systems

This will be the primary database used alongside Java and Spring Boot.

---

## MySQL

Another extremely popular relational database.

Known for:

- Simplicity
- Speed
- Large ecosystem

Commonly used for:

- Websites
- CMS platforms
- Web applications

---

## MariaDB

A community-driven fork of MySQL.

Designed to remain fully open source while maintaining MySQL compatibility.

---

## Microsoft SQL Server

Developed by Microsoft.

Often used inside:

- Large enterprises
- Windows environments
- Corporate applications

---

## Oracle Database

One of the oldest and most powerful enterprise databases.

Frequently used by:

- Banks
- Governments
- Large corporations

Known for:

- Reliability
- Security
- High-end enterprise features

---

## MongoDB

A document database.

Stores JSON-like documents instead of tables.

Example:

```json
{
    "name": "Nitin",
    "city": "Delhi"
}
```

Useful when:

- Data structure changes frequently.
- Documents naturally represent the data.

---

## Redis

An in-memory key-value database.

Designed for speed.

Common uses:

- Cache
- Session storage
- Rate limiting
- Message queues

Redis is usually used **alongside** another database rather than replacing it.

---

# CSV & TSV Files

Before importing data into a database, data often exists as plain files.

## CSV

Comma-Separated Values

Example:

```csv
id,name,age
1,Nitin,21
2,Rahul,20
```

Columns are separated by commas.

---

## TSV

Tab-Separated Values

Example:

```text
id    name    age
1     Nitin   21
2     Rahul   20
```

Columns are separated using tabs instead of commas.

Both CSV and TSV are commonly imported into SQL databases.

---

# Creating a Database

Many database systems allow creating a new database with a single command.

SQLite simply creates a new `.db` file.

For example:

```
school.db
```

contains the entire database.

Server-based databases (PostgreSQL, MySQL, SQL Server, Oracle) create databases inside a running database server rather than as a single standalone file.

---

# Choosing the Right Database

There is no universally "best" database.

The correct choice depends on the application's requirements.

| Database | Best Used For |
|-----------|---------------|
| SQLite | Learning, local apps, prototypes |
| PostgreSQL | Backend applications, APIs, enterprise software |
| MySQL | General web applications |
| MariaDB | Open-source MySQL alternative |
| SQL Server | Microsoft ecosystem |
| Oracle Database | Large enterprise systems |
| MongoDB | Flexible document storage |
| Redis | Caching and high-speed data access |

Modern applications often combine multiple databases to leverage the strengths of each.

---

# Key Takeaways

✔ Databases organize and manage large amounts of data.

✔ Relational databases store data in tables.

✔ NoSQL databases use alternative data models such as documents or key-value pairs.

✔ PostgreSQL is one of the most powerful relational databases and is widely used for backend development.

✔ SQLite stores an entire database inside a single file.

✔ CSV and TSV files are common formats for importing data.

✔ Different databases solve different problems.

Choosing the right database depends on the application's requirements rather than popularity.

---

# Summary

Databases are the foundation of modern software.

Understanding the differences between relational and NoSQL databases—and knowing when each is appropriate—is more valuable than simply memorizing SQL syntax.

Before learning how to query data, it is important to understand why databases exist, what problems they solve, and why different database systems were created.
