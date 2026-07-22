# Day 14 - Drawbacks of JDBC & Introduction to JPA
*Thu, 16 Jul 2026*

## Drawbacks of JDBC

- Boilerplate code
- Manual object mapping
- Database dependency
- Poor maintainability
- Transaction management complexity
- No caching
- No relationship management

JPA exists specifically to solve these problems.

## What Is JPA?

**Java Persistence API** — a specification that provides a standard way to map Java objects to database tables.

- JPA is **not** an implementation — it's a spec.
- Popular implementations: **Hibernate**, **EclipseLink**, **OpenJPA**
- The underlying technique is called **ORM — Object Relational Mapping**

## Benefits of JPA

1. Less boilerplate code
2. Object-oriented approach
3. Database independence
4. Automatic mapping
5. Relationship handling (`OneToOne`, `OneToMany`, `ManyToOne`, `ManyToMany`)
6. Caching
7. Transaction support
8. JPQL support

## Core JPA Annotations

| Annotation | Purpose |
|---|---|
| `@Entity` | Marks a class as a JPA-managed entity |
| `@Table(name = "...")` | Maps the class to a specific table |
| `@Id` | Marks the primary key field |
| `@GeneratedValue(strategy = ...)` | Auto-generates the ID — strategies: `IDENTITY`, `AUTO`, `SEQUENCE`, `TABLE` |
| `@Column` | Maps a field to a specific column |
| `@Transient` | Excludes a field from persistence entirely |
| `@Temporal(TemporalType.DATE / TIME)` | Specifies how a `Date` field should be stored |
| `@OneToOne` | One-to-one relationship |
| `@OneToMany` | One-to-many relationship |
| `@ManyToOne` | Many-to-one relationship |
| `@ManyToMany` | Many-to-many relationship |

```java
@Temporal(TemporalType.DATE)
private Date joiningDate;   // stores both date and time internally, formatted as DATE
```

## Schema Generation: `hibernate.hbm2ddl.auto`

```xml
<property name="hibernate.hbm2ddl.auto" value="update"/>
```

| Value | Behavior |
|---|---|
| `create` | Drops the existing table and creates a new one |
| `create-drop` | Creates the schema on startup, drops it when the application stops |
| `update` | Updates the schema, existing data remains |
| `validate` | Checks that the table matches the entities — no changes made |
| `none` | No schema management at all |

## `EntityManagerFactory` & `EntityManager`

| Component | Role |
|---|---|
| `EntityManagerFactory` | Heavyweight — created once per application/persistence unit |
| `EntityManager` | Manages the entity lifecycle — created per unit of work |

### Key `EntityManager` Methods

| Method | Purpose |
|---|---|
| `persist()` | Inserts a new record |
| `find()` | Reads a single record by primary key |
| `merge()` | Updates an existing record (or inserts if not present) |
| `remove()` | Deletes a record |
| `createQuery()` | Runs a JPQL query |

## Entity Lifecycle

Every JPA entity moves through **4 main states**:

```
New (transient) --persist()/merge()--> Managed --remove()--> Removed
                                            |
                                      (detach / close)
                                            ↓
                                        Detached
```

| State | Meaning |
|---|---|
| **New / Transient** | Just created with `new`, not yet associated with a persistence context |
| **Managed** | Associated with a persistence context — tracked, changes auto-flushed to DB |
| **Detached** | Was managed, but the persistence context closed — no longer tracked |
| **Removed** | Marked for deletion, removed from DB on transaction commit |

```java
Employee emp = new Employee();  // New / Transient
em.persist(emp);                // Managed
em.detach(emp);                 // Detached
em.remove(emp);                 // Removed (only valid on a managed entity)
```
