# Day 15 - JPA Relationships
*Fri, 17 Jul 2026*

## Types of Relationships

1. One-to-One
2. One-to-Many
3. Many-to-One
4. Many-to-Many

## Cascade

A **parent operation automatically applied to the child** — e.g. saving the parent also saves the child.

| CascadeType | Effect |
|---|---|
| `PERSIST` | Save propagates to children |
| `MERGE` | Update propagates to children |
| `REMOVE` | Delete propagates to children |
| `REFRESH` | Refresh propagates to children |
| `DETACH` | Detach propagates to children |
| `ALL` | All of the above |

## Unidirectional vs Bidirectional

| Type | Meaning |
|---|---|
| **Unidirectional** | Only one entity knows about the other |
| **Bidirectional** | Both entities know about each other |

## Shared JPA Utility Class

```java
package com.demo;

import javax.persistence.EntityManagerFactory;
import javax.persistence.Persistence;

public class JpaUtil {
    private static final EntityManagerFactory emf =
            Persistence.createEntityManagerFactory("jpa-demo");

    public static EntityManagerFactory getEmf() {
        return emf;
    }
}
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<persistence xmlns="http://xmlns.jcp.org/xml/ns/persistence"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/persistence
             http://xmlns.jcp.org/xml/ns/persistence/persistence_2_1.xsd"
             version="2.1">

    <persistence-unit name="jpa-demo">
        <description>Hibernate JPA Configuration Example</description>
        <provider>org.hibernate.jpa.HibernatePersistenceProvider</provider>
        <properties>
            <property name="javax.persistence.jdbc.driver" value="com.mysql.cj.jdbc.Driver"/>
            <property name="javax.persistence.jdbc.url" value="jdbc:mysql://localhost:3306/jpademo"/>
            <property name="javax.persistence.jdbc.user" value="root"/>
            <property name="javax.persistence.jdbc.password" value="root"/>
            <property name="hibernate.show_sql" value="true"/>
            <property name="hibernate.hbm2ddl.auto" value="update"/>
            <property name="hibernate.dialect" value="org.hibernate.dialect.MySQL8Dialect"/>
            <property name="hibernate.format_sql" value="true"/>
        </properties>
    </persistence-unit>
</persistence>
```

> `hibernate.dialect` tells Hibernate which SQL flavor to generate for the target database — here, MySQL 8. `hibernate.format_sql` pretty-prints the generated SQL in the logs.

---
## 1. One-to-One — `Person` ↔ `Passport`

```java
package com.demo.onetoone.entity;

import javax.persistence.*;

@Entity
@Table(name = "person")
public class Person {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @OneToOne(cascade = CascadeType.ALL)
    @JoinColumn(name = "passport_id")   // FK column lives on the Person table
    private Passport passport;

    // getters and setters...
}
```

```java
package com.demo.onetoone.entity;

import javax.persistence.*;

@Entity
@Table(name = "passport")
public class Passport {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String passportNumber;

    // getters and setters...
}
```

```java
package com.demo.onetoone;

import javax.persistence.EntityManager;
import com.demo.JpaUtil;
import com.demo.onetoone.entity.Passport;
import com.demo.onetoone.entity.Person;

public class OneToOneDemo {
    public static void main(String[] args) {
        EntityManager em = JpaUtil.getEmf().createEntityManager();
        em.getTransaction().begin();

        Passport passport = new Passport();
        passport.setPassportNumber("IND123");

        Person person = new Person();
        person.setName("John Doe");
        person.setPassport(passport);   // cascade = ALL saves the Passport too

        em.persist(person);
        em.getTransaction().commit();
    }
}
```

`@JoinColumn` puts the foreign key (`passport_id`) on the `person` table. `cascade = CascadeType.ALL` means persisting `person` automatically persists its `passport` — no separate `em.persist(passport)` call needed.

---
## 2. One-to-Many / Many-to-One — `Department` ↔ `Employee`

```java
package com.demo.onetomany.entity;

import java.util.ArrayList;
import java.util.List;
import javax.persistence.*;

@Entity
@Table(name = "departments")
public class Department {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private int id;

    private String name;

    @OneToMany(mappedBy = "department", cascade = CascadeType.ALL)
    private List<Employee> employees = new ArrayList<>();

    // getters and setters...
}
```

```java
package com.demo.onetomany.entity;

import javax.persistence.*;

@Entity
@Table(name = "employees")
public class Employee {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private int id;

    private String name;

    @ManyToOne
    @JoinColumn(name = "department_id")   // FK column lives on the Employee (many) side
    private Department department;

    // getters and setters...
}
```

```java
package com.demo.onetomany;

import javax.persistence.EntityManager;
import com.demo.JpaUtil;
import com.demo.onetomany.entity.Department;
import com.demo.onetomany.entity.Employee;

public class OneToManyDemo {
    public static void main(String[] args) {
        EntityManager em = JpaUtil.getEmf().createEntityManager();
        em.getTransaction().begin();

        Department department = new Department();
        department.setName("IT");

        Employee employee1 = new Employee();
        employee1.setName("John Doe");

        Employee employee2 = new Employee();
        employee2.setName("Jane Doe");

        employee1.setDepartment(department);
        employee2.setDepartment(department);

        department.getEmployees().add(employee1);
        department.getEmployees().add(employee2);

        em.persist(department);   // cascades to both employees
        em.getTransaction().commit();
    }
}
```

`mappedBy = "department"` on the `Department` side marks it as the **inverse (non-owning)** side of the relationship — the `Employee.department` field is the owning side that actually controls the foreign key column. This is why both sides of the relationship are manually kept in sync in the demo (`employee1.setDepartment(department)` **and** `department.getEmployees().add(employee1)`).

---
## 3. Many-to-Many — `Student` ↔ `Course`

```java
package com.demo.manytomany.entity;

import java.util.HashSet;
import java.util.Set;
import javax.persistence.*;

@Entity
@Table(name = "course")
public class Course {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private int id;

    private String courseName;

    @ManyToMany(mappedBy = "courses")   // inverse side — Student owns the relationship
    private Set<Student> students = new HashSet<>();

    // getters and setters...
}
```

```java
package com.demo.manytomany.entity;

import java.util.HashSet;
import java.util.Set;
import javax.persistence.*;

@Entity
@Table(name = "student")
public class Student {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private int id;

    private String name;

    @ManyToMany(cascade = { CascadeType.PERSIST, CascadeType.MERGE })
    @JoinTable(
        name = "student_course",                                   // join table name
        joinColumns = @JoinColumn(name = "student_id"),             // FK to this entity
        inverseJoinColumns = @JoinColumn(name = "course_id")        // FK to the other entity
    )
    private Set<Course> courses = new HashSet<>();

    public void addCourse(Course course) {
        this.courses.add(course);
        course.getStudents().add(this);   // keep both sides in sync
    }

    // getters and setters...
}
```

```java
package com.demo.manytomany;

import javax.persistence.EntityManager;
import com.demo.JpaUtil;
import com.demo.manytomany.entity.Course;
import com.demo.manytomany.entity.Student;

public class ManyToManyDemo {
    public static void main(String[] args) {
        EntityManager em = JpaUtil.getEmf().createEntityManager();
        em.getTransaction().begin();

        Course java = new Course();
        java.setCourseName("Java");

        Course mysql = new Course();
        mysql.setCourseName("MySQL");

        Student student1 = new Student();
        student1.setName("John");
        student1.addCourse(java);
        student1.addCourse(mysql);

        em.persist(student1);   // cascade PERSIST saves both courses too
        em.getTransaction().commit();
        em.close();
    }
}
```

`@JoinTable` is needed here because a many-to-many relationship can't be represented with a single foreign key — it needs a **join table** (`student_course`) holding `student_id` / `course_id` pairs. `Student` is the **owning side** (it declares `@JoinTable`); `Course` is the **inverse side** (`mappedBy = "courses"`), just mirroring the relationship for convenient navigation.
