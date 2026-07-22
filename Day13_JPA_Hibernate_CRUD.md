# Day 13 - JPA & Hibernate: Building a CRUD Application
*Wed, 15 Jul 2026*

Builds directly on the JDBC/project-structure fundamentals from Day 12 — here the raw JDBC calls are replaced with **JPA (Java Persistence API)**, backed by **Hibernate** as the provider.

## What Changed from Plain JDBC?

| JDBC (Day 12) | JPA/Hibernate (today) |
|---|---|
| Manual SQL strings | Auto-generated SQL from entity mappings |
| `Connection`, `Statement`, `ResultSet` | `EntityManager`, `EntityManagerFactory` |
| Manual result-set-to-object mapping | Automatic object-relational mapping (ORM) |
| Config in Java code | Config in `persistence.xml` |

## Project Structure (Employee CRUD Example)

```
com.jfs.training.bean         → plain model class (Employee)
com.jfs.training.entity       → JPA-mapped class (EmployeeEntity)
com.jfs.training.dao          → EmployeeDAO (interface) + EmployeeDAOImpl
com.jfs.training.service      → EmployeeService (interface) + EmployeeServiceImpl
com.jfs.training.exceptions   → EmployeeException
com.jfs.training.uitester     → UiTester (main class)
META-INF/persistence.xml      → JPA/Hibernate configuration
```

---
## 1. Bean — Plain Model Class

A simple POJO, used to move data around the app (not tied to JPA).

```java
package com.jfs.training.bean;

public class Employee {

    private int empId;
    private String empName;
    private double empSalary;
    private String empEmail;

    public Employee(int empId, String empName, double empSalary, String empEmail) {
        this.empId = empId;
        this.empName = empName;
        this.empSalary = empSalary;
        this.empEmail = empEmail;
    }

    // getters and setters...

    @Override
    public String toString() {
        return "Employee [empId=" + empId + ", empName=" + empName +
                ", empSalary=" + empSalary + ", empEmail=" + empEmail + "]";
    }
}
```

## 2. Entity — JPA-Mapped Class

Maps a Java class to a database table using JPA annotations.

```java
package com.jfs.training.entity;

import javax.persistence.*;

@Entity
@Table(name = "employee")
public class EmployeeEntity {

    @Id
    // @GeneratedValue(strategy = GenerationType.AUTO)
    @Column(name = "emp_id")
    private int empId;

    @Column(name = "emp_name")
    private String empName;

    @Column(name = "emp_salary")
    private double empSalary;

    @Column(name = "emp_email")
    private String empEmail;

    public EmployeeEntity() { }   // no-arg constructor required by JPA

    public EmployeeEntity(int empId, String empName, double empSalary, String empEmail) {
        this.empId = empId;
        this.empName = empName;
        this.empSalary = empSalary;
        this.empEmail = empEmail;
    }

    // getters and setters...
}
```

### Key JPA Annotations

| Annotation | Purpose |
|---|---|
| `@Entity` | Marks the class as a JPA-managed entity |
| `@Table(name = "...")` | Maps the class to a specific table |
| `@Id` | Marks the primary key field |
| `@GeneratedValue` | Auto-generates the primary key (commented out here — ID supplied manually) |
| `@Column(name = "...")` | Maps a field to a specific column |

> A no-arg constructor is **required** on every `@Entity` class — JPA uses reflection to instantiate it.

## 3. DAO Layer — Interface + Implementation

```java
package com.jfs.training.dao;

import java.util.List;
import com.jfs.training.bean.Employee;

public interface EmployeeDAO {
    void save(Employee employee);
    Employee findById(int id);
    List<Employee> findAll();
    void update(Employee employee);
    void delete(int id);
}
```

```java
package com.jfs.training.dao;

import javax.persistence.EntityManager;
import javax.persistence.EntityManagerFactory;
import javax.persistence.Persistence;
import java.util.ArrayList;
import java.util.List;

import com.jfs.training.bean.Employee;
import com.jfs.training.entity.EmployeeEntity;

public class EmployeeDAOImpl implements EmployeeDAO {

    private static EntityManagerFactory emf =
            Persistence.createEntityManagerFactory("unit1"); // matches persistence.xml unit name

    @Override
    public void save(Employee employee) {
        EntityManager em = emf.createEntityManager();
        EmployeeEntity entity = new EmployeeEntity(
                employee.getEmpId(), employee.getEmpName(),
                employee.getEmpSalary(), employee.getEmpEmail());
        try {
            em.getTransaction().begin();
            em.persist(entity);
            em.getTransaction().commit();
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            em.close();
        }
    }

    @Override
    public Employee findById(int id) {
        EntityManager em = emf.createEntityManager();
        Employee employee = null;
        try {
            EmployeeEntity entity = em.find(EmployeeEntity.class, id);
            if (entity != null) {
                employee = new Employee(entity.getEmpId(), entity.getEmpName(),
                        entity.getEmpSalary(), entity.getEmpEmail());
            }
        } finally {
            em.close();
        }
        return employee;
    }

    @Override
    public List<Employee> findAll() {
        EntityManager em = emf.createEntityManager();
        List<Employee> employeeList = new ArrayList<>();
        try {
            List<EmployeeEntity> entities = em.createQuery("FROM EmployeeEntity").getResultList();
            for (EmployeeEntity entity : entities) {
                employeeList.add(new Employee(entity.getEmpId(), entity.getEmpName(),
                        entity.getEmpSalary(), entity.getEmpEmail()));
            }
        } finally {
            em.close();
        }
        return employeeList;
    }

    @Override
    public void update(Employee employee) {
        EntityManager em = emf.createEntityManager();
        EmployeeEntity entity = new EmployeeEntity(
                employee.getEmpId(), employee.getEmpName(),
                employee.getEmpSalary(), employee.getEmpEmail());
        try {
            em.getTransaction().begin();
            em.merge(entity);   // merge = update an existing managed entity
            em.getTransaction().commit();
        } finally {
            em.close();
        }
    }

    @Override
    public void delete(int id) {
        EntityManager em = emf.createEntityManager();
        try {
            em.getTransaction().begin();
            EmployeeEntity entity = em.find(EmployeeEntity.class, id);
            if (entity != null) {
                em.remove(entity);
            }
            em.getTransaction().commit();
        } finally {
            em.close();
        }
    }
}
```

### `EntityManager` — Core Methods Used

| Method | Purpose |
|---|---|
| `persist(entity)` | Inserts a new entity |
| `find(Class, id)` | Fetches an entity by primary key |
| `merge(entity)` | Updates an existing entity |
| `remove(entity)` | Deletes an entity (must be a managed instance from `find()`) |
| `createQuery(jpql)` | Runs a JPQL query (queries entity names, not table names) |
| `getTransaction().begin()/commit()` | Wraps writes in a transaction |

> **Note:** `delete()` must call `em.find()` and pass the returned **managed** entity to `em.remove()` — passing a detached object (or the wrong class) throws an exception.

## 4. Custom Exception

```java
package com.jfs.training.exceptions;

public class EmployeeException extends Exception {
    public EmployeeException(String message) {
        super(message);
    }
}
```

## 5. Service Layer — Interface + Implementation

The service layer sits between the DAO and the caller — this is where business rules and custom exceptions typically get added.

```java
package com.jfs.training.service;

import java.util.List;
import com.jfs.training.bean.Employee;

public interface EmployeeService {
    void save(Employee employee);
    Employee findById(int id);
    List<Employee> findAll();
    void update(Employee employee);
    void delete(int id);
}
```

```java
package com.jfs.training.service;

import java.util.List;
import com.jfs.training.bean.Employee;
import com.jfs.training.dao.EmployeeDAO;
import com.jfs.training.dao.EmployeeDAOImpl;

public class EmployeeServiceImpl implements EmployeeService {

    private EmployeeDAO employeeDao = new EmployeeDAOImpl();

    @Override
    public void save(Employee employee) {
        employeeDao.save(employee);
    }

    @Override
    public Employee findById(int id) {
        return employeeDao.findById(id);
    }

    @Override
    public List<Employee> findAll() {
        return employeeDao.findAll();
    }

    @Override
    public void update(Employee employee) {
        employeeDao.update(employee);
    }

    @Override
    public void delete(int id) {
        employeeDao.delete(id);
    }
}
```

## 6. UI Tester — Entry Point

```java
package com.jfs.training.uitester;

import java.util.List;
import com.jfs.training.bean.Employee;
import com.jfs.training.service.EmployeeService;
import com.jfs.training.service.EmployeeServiceImpl;

public class UiTester {

    public static void main(String[] args) {
        EmployeeService employeeService = new EmployeeServiceImpl();

        addEmployee(employeeService);
        getEmployee(employeeService);
        getAllEmployees(employeeService);
        // updateEmployee(employeeService);
        // deleteEmployee(employeeService);
    }

    private static void addEmployee(EmployeeService employeeService) {
        try {
            Employee employee1 = new Employee(103, "John Doe", 60000, "jhondoe@gmail.com");
            employeeService.save(employee1);
        } catch (Exception e) {
            System.err.println("Error adding employees: " + e.getMessage());
        }
    }

    private static void getEmployee(EmployeeService employeeService) {
        try {
            Employee employee = employeeService.findById(103);
            if (employee != null) {
                System.out.println("Employee found: " + employee);
            } else {
                System.out.println("Employee not found with ID: 103");
            }
        } catch (Exception e) {
            System.err.println("Error retrieving employee: " + e.getMessage());
        }
    }

    private static void getAllEmployees(EmployeeService employeeService) {
        try {
            System.out.println("All Employees:");
            List<Employee> employees = employeeService.findAll();
            for (Employee emp : employees) {
                System.out.println(emp);
            }
        } catch (Exception e) {
            System.err.println("Error retrieving employees: " + e.getMessage());
        }
    }

    private static void updateEmployee(EmployeeService employeeService) {
        try {
            Employee employeeToUpdate = employeeService.findById(103);
            if (employeeToUpdate != null) {
                employeeToUpdate.setEmpSalary(68000);
                employeeService.update(employeeToUpdate);
                System.out.println("Employee updated successfully: " + employeeToUpdate);
            } else {
                System.out.println("Employee not found with ID: 103");
            }
        } catch (Exception e) {
            System.err.println("Error updating employee: " + e.getMessage());
        }
    }

    private static void deleteEmployee(EmployeeService employeeService) {
        try {
            employeeService.delete(103);
        } catch (Exception e) {
            System.err.println("Error deleting employee: " + e.getMessage());
        }
    }
}
```

## 7. `persistence.xml` — JPA/Hibernate Configuration

Lives under `src/main/resources/META-INF/persistence.xml`. Defines the persistence unit that `Persistence.createEntityManagerFactory("unit1")` looks up by name.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<persistence xmlns="http://xmlns.jcp.org/xml/ns/persistence"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/persistence
             http://xmlns.jcp.org/xml/ns/persistence/persistence_2_1.xsd"
             version="2.1">

    <persistence-unit name="unit1">
        <description>Hibernate JPA Configuration Example</description>
        <provider>org.hibernate.jpa.HibernatePersistenceProvider</provider>
        <class>com.jfs.training.entity.EmployeeEntity</class>

        <properties>
            <property name="javax.persistence.jdbc.driver" value="com.mysql.cj.jdbc.Driver"/>
            <property name="javax.persistence.jdbc.url" value="jdbc:mysql://localhost:3306/companydb"/>
            <property name="javax.persistence.jdbc.user" value="root"/>
            <property name="javax.persistence.jdbc.password" value="root"/>
            <property name="hibernate.show_sql" value="true"/>
            <property name="hibernate.hbm2ddl.auto" value="update"/>
        </properties>
    </persistence-unit>
</persistence>
```

### Key Properties

| Property | Purpose |
|---|---|
| `provider` | Which JPA implementation to use — here, Hibernate |
| `<class>` | Registers each `@Entity` class with the persistence unit |
| `jdbc.driver` / `jdbc.url` / `jdbc.user` / `jdbc.password` | Standard DB connection details |
| `hibernate.show_sql` | Logs the generated SQL to the console — useful for debugging |
| `hibernate.hbm2ddl.auto` | Schema management strategy: `update` auto-alters the table to match the entity |

### `hibernate.hbm2ddl.auto` Values

| Value | Behavior |
|---|---|
| `validate` | Checks schema matches entities, makes no changes |
| `update` | Updates the schema to match entities (adds columns, never drops) |
| `create` | Drops and recreates the schema on every startup |
| `create-drop` | Same as `create`, plus drops the schema on shutdown |
