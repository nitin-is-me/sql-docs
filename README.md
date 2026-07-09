# SQL Notes

> A collection of long-form notes focused on understanding relational databases, SQL, and database design from a software engineering perspective.

---

## Purpose

This repository is **not** a SQL tutorial, nor is it a complete reference manual.

It is a collection of notes documenting concepts that are worth revisiting while building real-world software.

The focus is on understanding **how databases work**, **why certain design decisions exist**, and **how to write better database-driven applications**, rather than memorizing SQL syntax.

---

## Philosophy

I don't document syntax that can easily be looked up.

The official documentation already provides complete references for SQL statements, functions, and database commands.

Instead, these notes aim to answer questions such as:

- Why should a table be normalized?
- When should a JOIN be preferred over a nested query?
- Why do indexes improve performance?
- How do transactions prevent inconsistent data?
- Why are prepared statements immune to SQL injection?
- When should UUIDs be preferred over auto-incrementing IDs?

These are concepts that remain valuable long after the syntax has been memorized.

---

## What These Notes Are

- Concept-oriented rather than syntax-oriented.
- Written with long-term understanding in mind.
- Intended to be revisited throughout a backend development career.
- Focused primarily on relational databases and SQL.

Examples and syntax are included only when they improve understanding of a concept.

---

## What These Notes Are Not

These notes intentionally avoid becoming:

- A SQL cheat sheet
- A collection of every SQL function
- A copy of official documentation
- A list of syntax examples without explanation

If a topic is easy to remember or can be found within seconds in the official documentation, it generally doesn't belong here.

---

## Scope

The repository primarily covers topics such as:

- Relational databases
- Database design
- SQL querying
- Relationships
- Primary and foreign keys
- Normalization
- Joins
- Indexes
- Transactions
- ACID properties
- SQL Injection
- Query optimization
- ORMs
- Backend-oriented database concepts

While examples may use SQLite or PostgreSQL, the concepts apply to relational databases in general unless stated otherwise.

---

## Target Audience

These notes are written for developers who already know basic programming and want to develop a deeper understanding of databases.

Although they are being created while learning SQL, the intention is for them to remain useful during backend development with technologies such as Java, Spring Boot, JPA/Hibernate, and PostgreSQL.

---

## When a Topic Deserves a Note

A new note is created only if the topic:

- Explains an important database concept.
- Helps understand why SQL behaves a certain way.
- Appears repeatedly in real-world backend development.
- Is something worth revisiting months or years later.

Simple syntax or commands that can be easily looked up are intentionally left out.

---

## Future Direction

As my understanding of databases grows, this repository may expand to include more advanced topics such as:

- PostgreSQL internals
- Query execution plans
- Locks and isolation levels
- Advanced indexing strategies
- Database optimization
- Partitioning
- Replication
- Database architecture
- Distributed databases

The focus will always remain on concepts that provide long-term value rather than short-term memorization.

---

> **"A good database developer doesn't memorize SQL. They understand why the database behaves the way it does."**
