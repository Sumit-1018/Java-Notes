# Day 18 - Spring ORM & Transaction Management Basics
*Wed, 22 Jul 2026*

## Spring Framework Modules (Recap)

Spring consists of many modules, including:

- **Spring Core**
- **Spring MVC**
- **Spring Data Access** — including **Spring Data JPA**

## How Spring Integrates With a Database

Spring supports database integration in multiple ways:

| Approach | Notes |
|---|---|
| **JDBC** | Low-level approach, more manual coding |
| **JPA** (Recommended) | Framework-independent, uses providers like Hibernate, EclipseLink |
| **Hibernate** (Direct use) | Specific to Hibernate, less flexible |

## What Is Spring ORM?

**Spring ORM** is a module of the Spring Framework that helps integrate ORM tools with Spring — it maps Java objects to relational database tables.

```
        ORM (Object Relational Mapping)

class Employee {              --------->   Employee table in DB

    int id;        --------->   col 1  id
    String name;   --------->   col 2  name
    double sal;    --------->   col 3  sal
}
```

### ORM Tools

- Hibernate
- EclipseLink
- TopLink

## What Is JPA?

- JPA is a **specification** (a set of rules)
- It does **not** perform operations directly
- It uses **implementations (providers)** internally — like Hibernate

> In this training, we use **JPA** with **Hibernate** as the underlying provider.

## Modern Approach: Spring Data JPA

Built **on top of** JPA:

- Simplifies JPA usage
- No need to write DAO classes
- Reduces boilerplate code

*(Covered in depth on Day 19.)*

---
## Transaction Management in Spring ORM

### What Is Transaction Management?

Ensures multiple database operations execute as **a single unit of work** — either all operations succeed (**Commit**), or all operations fail (**Rollback**).

### Types of Transaction Management

**1. Declarative Transaction Management** (Recommended)
- Using `@Transactional` annotation
- Using XML configuration

**2. Programmatic Transaction Management**
- Manually controls transaction start, commit, and rollback in code

```java
// Programmatic style — manual control
entityManager.getTransaction().begin();
entityManager.persist(product);
entityManager.getTransaction().commit();
```

### Benefits

- Reduces boilerplate code for transaction handling
- Maintains data consistency and integrity
- Automatically rolls back transactions when failures occur

### ACID Properties

Transaction management follows the **ACID** principles:

| Property | Description |
|---|---|
| **A — Atomicity** | Either all operations are committed, or all are rolled back |
| **C — Consistency** | Ensures the database remains valid and consistent before and after the transaction |
| **I — Isolation** | Ensures concurrent transactions do not interfere with each other |
| **D — Durability** | Once a transaction is committed, the data is permanently stored, even after an application crash |

---
## `EntityManagerFactory` & `EntityManager` (Recap)

### `EntityManagerFactory`

A JPA interface responsible for creating `EntityManager` objects.

- Created **once per application**
- Heavyweight and **thread-safe**
- Creates `EntityManager` instances

### `EntityManager`

A JPA interface that performs database operations and manages the **lifecycle of entity objects**.

```
Transient --> Managed --> Detached --> Removed
```

- Lightweight and **not thread-safe**
- Performs CRUD operations: `persist()`, `find()`, `merge()`, `remove()`
- Works **within a transaction**

---
## Global vs Local Transaction

| | Global Transaction | Local Transaction |
|---|---|---|
| Scope | Works across multiple resources (multiple DBs, DB + JMS) | Works with a single resource (one database) |
| Manager | Uses `JtaTransactionManager` with a JTA provider | Uses `JpaTransactionManager` or `DataSourceTransactionManager` |
| Coordination | Coordinates transactions across multiple systems | Managed using `@Transactional` |
| Example | Flight booking (Airline DB + Payment + JMS Queue) | Online shopping (Order + Inventory in one DB) |
| Advantages | Supports distributed transactions, maintains consistency | Simple, fast, easy to configure |
| Disadvantages | Complex setup, slower, requires JTA | Limited to a single database/resource |
