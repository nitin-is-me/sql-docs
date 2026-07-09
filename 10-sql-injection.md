# 10 - SQL Injection

> **Goal**
>
> Understand what SQL Injection is, how it exploits poorly written SQL queries, why it is dangerous, and how prepared statements completely eliminate the vulnerability.

---

# Table of Contents

1. What is SQL Injection?
2. Why SQL Injection Happens
3. Building SQL Incorrectly
4. How an Injection Works
5. Why It's Dangerous
6. Prepared Statements
7. Placeholders
8. Why Prepared Statements Prevent Injection
9. ORMs and SQL Injection
10. Common Mistakes
11. Key Takeaways

---

# What is SQL Injection?

SQL Injection is a security vulnerability where user input is interpreted as SQL code instead of ordinary data.

Instead of treating user input as a value,

the database mistakenly treats it as part of the SQL query itself.

This allows attackers to manipulate queries in unintended ways.

---

# Why SQL Injection Happens

Imagine a login system.

The application asks for:

- Username
- Password

The programmer builds the SQL query by combining strings.

Conceptually:

```
SELECT *
FROM users
WHERE username = '<user input>'
AND password = '<password input>'
```

At first glance,

this seems harmless.

The problem is that user input is being mixed directly into SQL.

---

# Building SQL Incorrectly

Suppose a user enters:

```
Nitin
```

The query becomes:

```
SELECT *
FROM users
WHERE username = 'Nitin'
```

Everything works.

Now imagine an attacker enters something entirely different.

The database doesn't know what was intended.

It simply executes whatever SQL it receives.

---

# How an Injection Works

Imagine a login page.

Instead of entering a normal username,

an attacker enters SQL syntax.

The final query no longer represents what the programmer intended.

Instead,

the attacker has changed the meaning of the SQL statement itself.

This is SQL Injection.

The attacker is not "breaking into the database."

The application is accidentally sending the attacker's SQL commands to the database.

---

# Why It's Dangerous

A successful SQL Injection can allow attackers to:

- Bypass login systems
- Read confidential data
- Modify records
- Delete data
- Access information belonging to other users

In severe cases,

an entire database can be compromised.

The database is not vulnerable.

The application is.

---

# The Root Cause

The real problem is simple.

```
SQL Code

+

User Input

↓

One String
```

The database cannot distinguish between:

- SQL written by the programmer.
- SQL written by the attacker.

Everything becomes part of the same command.

---

# Prepared Statements

Prepared Statements solve this problem completely.

Instead of mixing SQL and data,

they keep them separate.

Conceptually:

```
SQL

↓

Prepared

↓

Data Added Later
```

The database already understands the SQL structure before any user data is supplied.

---

# Placeholders

Instead of inserting values directly,

prepared statements use placeholders.

Conceptually:

```
SELECT *

FROM users

WHERE username = ?

AND password = ?
```

The question marks are placeholders.

They do **not** contain SQL.

They simply reserve space for values.

---

# Why Prepared Statements Prevent Injection

Suppose a user enters:

```
' OR 1=1 --
```

Without prepared statements,

that text becomes part of the SQL query.

With prepared statements,

the database treats it as ordinary text.

The input is stored as:

```
String

↓

Value

↓

Not SQL
```

The attacker cannot change the structure of the query.

They can only supply values.

This is the key reason prepared statements prevent SQL Injection.

---

# Visual Comparison

## Unsafe

```
SQL

+

User Input

↓

Single SQL Statement
```

The database cannot tell them apart.

---

## Safe

```
SQL

↓

Prepared

↓

User Values

↓

Executed
```

SQL and user input never mix.

---

# ORMs and SQL Injection

Modern ORMs such as:

- Hibernate
- JPA
- Entity Framework

use prepared statements internally.

This means developers automatically receive SQL Injection protection,

provided they use the ORM correctly.

However,

writing raw SQL by concatenating strings can still introduce vulnerabilities.

Understanding SQL Injection remains important even when using an ORM.

---

# Common Mistakes

## Escaping Characters Instead of Using Prepared Statements

Escaping quotes manually is unreliable.

Prepared statements should always be preferred.

---

## Assuming ORMs Eliminate Every Risk

Most ORMs generate prepared statements.

However,

raw SQL queries written incorrectly can still be vulnerable.

---

## Trusting User Input

Never assume user input is safe.

Every value coming from users should be treated as untrusted.

---

# Best Practices

Always:

✔ Use prepared statements.

✔ Use placeholders.

✔ Validate user input.

✔ Apply the principle of least privilege to database users.

Avoid:

✘ Building SQL using string concatenation.

✘ Executing SQL directly from user input.

---

# Key Takeaways

✔ SQL Injection occurs when user input becomes SQL code.

✔ The vulnerability exists in the application, not the database.

✔ Mixing SQL and user input causes the problem.

✔ Prepared statements separate SQL from data.

✔ Placeholders reserve positions for values.

✔ User input supplied through prepared statements is always treated as data, not SQL.

✔ Modern ORMs usually protect against SQL Injection automatically.

---

# Summary

SQL Injection is one of the most well-known and dangerous vulnerabilities in web applications.

Fortunately, its prevention is straightforward: never combine SQL code with user input. By using prepared statements and placeholders, developers ensure that the database always distinguishes between SQL commands and user-supplied data.

Understanding *why* prepared statements work is far more valuable than simply memorizing that they should be used, because the same principle applies across virtually every programming language, database, and backend framework.
