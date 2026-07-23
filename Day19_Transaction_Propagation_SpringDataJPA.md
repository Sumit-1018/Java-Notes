# Day 19 - Transaction Propagation & Spring Data JPA
*Thu, 23 Jul 2026*

## Transaction Propagation in Spring

### Definition

**Transaction Propagation** defines how Spring handles transactions when one `@Transactional` method calls another `@Transactional` method.

| Term | Meaning |
|---|---|
| **Physical Transaction** | The actual transaction, typically when `@Transactional` is used at the **service layer** |
| **Logical Transaction** | When `@Transactional` is used at the **DAO layer**, on each method independently |

Transaction propagation controls whether the transactional scope should be **shared** or **independent** between physical and logical transactions.

- When logical transactions **share the same** physical transaction, failure of one causes **rollback of all**.
- When they are **independent**, failure of one **does not affect** the others.

```java
@Transactional
public void methodA() {
    methodB();
}

@Transactional
public void methodB() {
    // ...
}
```

Propagation decides:
- Join an existing transaction?
- Create a new transaction?
- Execute without a transaction?

```java
@Transactional(propagation = Propagation.REQUIRED)
public void placeOrder() {
    // ...
}
```

### Propagation Types

| Propagation | Shortcut Meaning | Typical Use Case |
|---|---|---|
| `REQUIRED` | Join existing or create new | Default choice for business operations (Order, Employee, Payment) |
| `REQUIRES_NEW` | Always create new | Audit logs, notifications, activity tracking |
| `NESTED` | Same TX + savepoint (Spring JDBC) | Partial rollback within a large transaction |
| `MANDATORY` | Must have a TX, else error | Validation or DAO method that must run inside a transaction |
| `NEVER` | Must NOT have a TX, else error | Non-transactional utilities, health checks |
| `SUPPORTS` | Use TX if it exists, else run without one | Read-only methods, search, report queries |
| `NOT_SUPPORTED` | Runs without a TX (suspends one if it exists) | Long-running reports, file export, batch reads |

---
## Spring Data JPA

An extra layer of abstraction **on top of** the JPA provider — it is **not** a JPA provider itself.

### What It Provides

- No need to write DAO implementation classes
- No need to write SQL queries
- No need to write logic for pagination and auditing

Spring Data JPA eliminates boilerplate code via its **Repository abstraction**.

### How It Works

- The DAO layer is implemented as an **interface** that extends a predefined Spring Data JPA repository interface
- That DAO interface is implemented **at runtime** — Spring generates the implementation in memory
- A **proxy object** is created for this runtime implementation and injected into your code
- The same proxy object is then used to perform CRUD operations and transactions

### Repository Interface Hierarchy

```
Repository
    ▲
    │
CrudRepository
    ▲
    │
PagingAndSortingRepository
    ▲
    │
JpaRepository
```

| Interface | Role |
|---|---|
| **`Repository`** | A marker interface — takes 2 type parameters: (1) the entity class to manage, (2) the type of its ID. Helps Spring discover other interfaces that extend it. |
| **`CrudRepository`** | Provides CRUD operations for the managed entity |
| **`PagingAndSortingRepository`** | Adds support for sorting and paginating entities |
| **`JpaRepository`** | Combines all of the above, plus exposes capabilities of the underlying JPA provider |

```java
public interface EmployeeRepository extends JpaRepository<Employee, Integer> {
    // CRUD, paging, and sorting methods available immediately — no implementation needed
}
```

> **Note:** `CrudRepository` and `PagingAndSortingRepository` belong to **Spring Data Commons**. `JpaRepository` belongs specifically to **Spring Data JPA**.

---
## Named Queries in JPA

### Definition

A **Named Query** is a predefined and reusable JPQL or SQL query, identified by a unique name.

### Key Features

- Defined once, used multiple times
- Compiled and validated at **application startup**
- Improves performance
- Reduces runtime errors

### Types

1. **JPQL Named Query**
2. **Native Named Query**

### Syntax — Single Named Query

```java
@NamedQuery(
    name = "Employee.findByName",
    query = "SELECT e FROM Employee e WHERE e.name = :name"
)
```

### Syntax — Multiple Named Queries

```java
@NamedQueries({
    @NamedQuery(name = "Employee.findAll", query = "SELECT e FROM Employee e"),
    @NamedQuery(name = "Employee.findBySalary", query = "SELECT e FROM Employee e WHERE e.salary > :sal")
})
```

### Execution — Using `EntityManager` Directly

```java
entityManager.createNamedQuery("Employee.findByName", Employee.class)
             .setParameter("name", "John")
             .getResultList();
```

### Execution — Using Spring Data JPA's `@Query`

```java
@Query(name = "Employee.findAll")
List<Employee> findByName(String name);
```

### Native Named Query

Runs actual SQL instead of JPQL.

```java
@NamedNativeQuery(
    name = "Employee.nativeFindAll",
    query = "SELECT * FROM employee_table",
    resultClass = Employee.class
)
```
