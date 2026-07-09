# 11 - User Access & Permissions

> **Goal**
>
> Understand why databases implement users, roles, and permissions, and how restricting database access improves security and prevents accidental or malicious changes.

---

# Table of Contents

1. Why Access Control Exists
2. Database Users
3. Permissions (Privileges)
4. Roles
5. Principle of Least Privilege
6. Real-World Examples
7. Common Mistakes
8. Key Takeaways

---

# Why Access Control Exists

Imagine a company with hundreds of employees.

Should every employee be able to:

- Delete customer records?
- Drop tables?
- View salaries?
- Modify financial transactions?

Obviously not.

Different people require different levels of access.

Databases solve this using **users, roles, and permissions**.

---

# Database Users

A database user represents an identity that can connect to the database.

Examples:

- Backend application
- Database administrator (DBA)
- Developer
- Data analyst
- Reporting service

Each user authenticates with credentials before interacting with the database.

Unlike application users (customers using your website), database users are the identities that directly communicate with the database server.

---

# Permissions (Privileges)

Permissions determine **what a database user is allowed to do.**

Common permissions include:

| Permission | Purpose |
|------------|---------|
| SELECT | Read data |
| INSERT | Add new rows |
| UPDATE | Modify existing rows |
| DELETE | Remove rows |
| CREATE | Create database objects |
| ALTER | Modify existing tables |
| DROP | Delete database objects |

Permissions can be granted individually or as part of a role.

---

# Roles

Managing permissions one user at a time quickly becomes difficult.

Instead, databases group permissions into **roles**.

Think of a role as a collection of permissions.

Example:

```
ReadOnly

↓

SELECT
```

```
Editor

↓

SELECT

INSERT

UPDATE
```

```
Administrator

↓

All Permissions
```

Users are assigned roles instead of individual permissions.

This makes permission management much easier.

---

# Principle of Least Privilege

One of the most important security principles is:

> **Give users only the permissions they actually need.**

Examples:

A reporting service only generates reports.

It should have:

✔ SELECT

It does **not** need:

✘ DELETE

✘ DROP

✘ ALTER

Similarly,

your backend application may need to insert and update records,

but ordinary users should never have direct database access.

Limiting permissions reduces the damage caused by mistakes or security vulnerabilities.

---

# Real-World Examples

## Administrator (DBA)

Responsible for managing the database.

Typical permissions:

- Create databases
- Create users
- Grant permissions
- Backup data
- Restore data
- Modify schemas

---

## Backend Application

Used by your Java/Spring Boot application.

Typical permissions:

- SELECT
- INSERT
- UPDATE
- DELETE

Usually **not** allowed to:

- DROP tables
- Create users
- Modify database configuration

---

## Reporting Service

Only generates reports.

Typical permission:

- SELECT

Nothing else.

---

## Developer

Often receives broader access in development environments,

but significantly fewer permissions in production.

---

# Common Mistakes

## Using an Administrator Account Everywhere

Some beginners connect their application using the database administrator account.

This is dangerous.

If the application is compromised,

the attacker gains complete control of the database.

Applications should use dedicated accounts with limited permissions.

---

## Giving Every User Full Access

Not every service requires every permission.

Grant only what is necessary.

---

## Ignoring Roles

Managing permissions individually becomes difficult as systems grow.

Roles simplify administration and reduce mistakes.

---

# Relationship with SQL Injection

Earlier we learned that prepared statements prevent SQL Injection.

But imagine an attacker somehow still gains database access.

If the compromised account only has:

```
SELECT
```

the damage is limited.

If it has:

```
DROP DATABASE
```

the consequences become much more severe.

This is why permissions provide an additional layer of security.

Security should never rely on a single defense.

---

# Best Practices

✔ Use dedicated database users for each application.

✔ Assign permissions through roles whenever possible.

✔ Follow the Principle of Least Privilege.

✔ Avoid using administrator accounts in production applications.

✔ Regularly review granted permissions.

---

# Key Takeaways

✔ Database users represent identities that connect to the database.

✔ Permissions define what those users can do.

✔ Roles simplify permission management.

✔ Applications should not use administrator accounts.

✔ Least Privilege is one of the most important database security principles.

✔ Good permission management limits the impact of security vulnerabilities.

---

# Summary

Access control is a fundamental part of database security.

Rather than allowing every user unrestricted access, relational databases provide users, roles, and permissions to control who can view or modify data.

Combined with prepared statements and proper authentication, permission management helps build secure, maintainable, and production-ready database systems.
