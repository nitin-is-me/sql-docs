# 13 - ORMs (Object-Relational Mapping)

> **Goal**
>
> Understand why Object-Relational Mapping (ORM) exists, how it bridges object-oriented programming and relational databases, its advantages, limitations, and why frameworks such as Hibernate and JPA are built around it.

---

# Table of Contents

1. The Object-Relational Problem
2. What is an ORM?
3. Why ORMs Exist
4. How ORMs Work
5. ORM vs Raw SQL
6. Advantages
7. Disadvantages
8. Hibernate & JPA
9. Common Misconceptions
10. Best Practices
11. Key Takeaways

---

# The Object-Relational Problem

Applications and databases think differently.

Java works with:

- Objects
- Classes
- Fields
- Methods

Databases work with:

- Tables
- Rows
- Columns

Example

Java

```java
Student student = new Student();
student.setName("Nitin");
```

Database

```
Students

id | name
-----------
1  | Nitin
```

These are completely different ways of representing the same information.

Someone has to translate between them.

---

# What is an ORM?

ORM stands for

**Object-Relational Mapping.**

An ORM is a framework that automatically converts:

```
Java Objects

↓

Database Rows
```

and

```
Database Rows

↓

Java Objects
```

Instead of manually writing SQL for every operation,

the ORM performs most of the conversion automatically.

---

# Why ORMs Exist

Imagine writing SQL manually for every operation.

Create Student

↓

INSERT

Read Student

↓

SELECT

Update Student

↓

UPDATE

Delete Student

↓

DELETE

As applications grow,

this becomes repetitive.

ORMs automate much of this work.

Developers spend more time working with objects,

and less time writing boilerplate SQL.

---

# How ORMs Work

Suppose we have:

```java
Student student = new Student();
student.setName("Nitin");
```

When saved,

the ORM generates SQL behind the scenes.

Conceptually,

```
Java Object

↓

ORM

↓

INSERT INTO students...
```

Likewise,

```
SELECT

↓

ORM

↓

Java Object
```

The developer works with Java.

The ORM communicates with the database.

---

# ORM vs Raw SQL

## Raw SQL

Developer writes:

```
SELECT

INSERT

UPDATE

DELETE
```

Advantages

- Complete control
- Maximum flexibility
- Easier performance tuning

Disadvantages

- More boilerplate
- More repetitive code
- Easier to introduce bugs

---

## ORM

Developer writes Java objects.

ORM generates SQL.

Advantages

- Faster development
- Less repetitive code
- Easier maintenance
- Integrates naturally with object-oriented programming

Disadvantages

- Less direct control
- Generated SQL may not always be optimal
- Learning curve

---

# Advantages

## Less Boilerplate

Many repetitive CRUD operations disappear.

---

## Better Integration

Objects remain objects.

Developers don't constantly switch between Java and SQL.

---

## Easier Maintenance

Changing a class often requires fewer SQL changes.

---

## Database Independence

Most ORMs support multiple relational databases.

Switching databases usually requires fewer application changes.

---

## Built-in Features

Most ORMs include:

- Transactions
- Prepared Statements
- Relationship Mapping
- Caching
- Validation

These reduce the amount of infrastructure developers must write manually.

---

# Disadvantages

ORMs are powerful,

but they are not magic.

---

## Generated SQL

Sometimes the ORM generates SQL that is less efficient than carefully written manual SQL.

---

## Hidden Complexity

Developers may forget that SQL is still being executed.

Poor ORM usage can accidentally produce slow queries.

---

## Learning Curve

Understanding an ORM requires understanding both:

- Java
- SQL

Learning one without the other often leads to confusion.

---

# Hibernate & JPA

In Java,

the two names you'll encounter most often are:

## Hibernate

A popular ORM framework.

Hibernate performs the actual mapping between Java objects and database tables.

---

## JPA (Jakarta Persistence API)

JPA is **not** an ORM.

It is a specification.

It defines:

> How Java ORMs should behave.

Hibernate is one implementation of the JPA specification.

Think of it like this:

```
JPA

↓

Rules

↓

Hibernate

↓

Implementation
```

Spring Boot commonly uses Hibernate as its JPA implementation.

---

# Relationship Mapping

Earlier we learned about database relationships.

ORMs represent these using annotations.

Examples include:

```
@OneToOne

@OneToMany

@ManyToOne

@ManyToMany
```

These annotations do not create new concepts.

They simply describe the same database relationships inside Java classes.

This is why understanding database relationships first makes ORMs much easier to learn.

---

# Common Misconceptions

## "Using an ORM means I don't need SQL."

False.

ORMs generate SQL.

Understanding SQL remains essential for debugging and optimization.

---

## "ORMs replace databases."

False.

ORMs communicate with databases.

They do not replace them.

---

## "ORMs are always slower."

Not necessarily.

Most applications benefit significantly from ORMs.

Performance problems usually arise from incorrect usage rather than the ORM itself.

---

# Best Practices

✔ Learn SQL before learning an ORM.

✔ Understand the generated SQL.

✔ Use ORM for common CRUD operations.

✔ Don't hesitate to write raw SQL for complex queries when appropriate.

✔ Remember that every ORM operation ultimately becomes SQL.

---

# Key Takeaways

✔ ORMs bridge Java objects and relational databases.

✔ They automate much of the repetitive SQL required by applications.

✔ Hibernate is an ORM framework.

✔ JPA is a specification, not an implementation.

✔ ORMs improve productivity but do not eliminate the need to understand SQL.

✔ Every ORM operation eventually becomes one or more SQL queries.

---

# Summary

Object-Relational Mapping exists to bridge the gap between object-oriented programming and relational databases.

Rather than replacing SQL, ORMs automate many common database operations while allowing developers to work with familiar language constructs such as classes and objects.

For Java backend developers, understanding SQL first and ORMs second provides a much stronger foundation than relying solely on the framework. Hibernate, JPA, and Spring Boot all become significantly easier to understand once the underlying database concepts are already familiar.
