# Day 12 - DBMS, MySQL & JDBC
*Tue, 14 Jul 2026*

---
# Part A — DBMS

## What Is a DBMS?

**Database Management System** — used to create, store, manage, and retrieve data from databases.

### Features
- Data storage and retrieval
- Data security
- Backup and recovery
- Multi-user access
- Data consistency

## RDBMS

**Relational Database Management System**

- Relationships between tables
- Data stored in rows and columns
- Supports SQL
- Maintains data integrity

**Examples:** MySQL, Oracle, etc.

### Benefits
1. Reduced data redundancy
2. Data integrity
3. Security
4. Backup and recovery
5. Multi-user support
6. Data consistency

---
# Part B — MySQL

**Open-source relational database management system**, developed by Oracle.

### Features
- Open source
- Fast and reliable
- Uses SQL
- Supports large databases
- Cross-platform

### Common Uses
- Web applications
- Enterprise applications
- Banking systems
- E-commerce websites

---
# Part C — JDBC (Java Database Connectivity)

## What Is JDBC?

An **API** that allows Java applications to communicate with databases.

Using JDBC, Java programs can:
- Connect to a database
- Execute SQL queries
- Insert records
- Update records
- Delete records
- Retrieve records

### Architecture

```
App ---> JDBC API ---> JDBC Driver ---> Database
```

A collection of classes and interfaces in `java.sql` / `javax.sql`.

## JDBC Classes & Interfaces

| Type | Name | Role |
|---|---|---|
| Class | `DriverManager` | Used to establish a connection with the database |
| Interface | `Connection` | Represents a database connection |
| Interface | `Statement` | Used for executing plain SQL queries |
| Interface | `PreparedStatement` | Used for parameterized queries |
| Interface | `CallableStatement` | Used to call stored procedures |
| Interface | `ResultSet` | Stores data returned from `SELECT` queries |
| Class | `SQLException` | Handles database exceptions |

## Types of JDBC Drivers

| Type | Name | Notes |
|---|---|---|
| Type 1 | JDBC-ODBC Bridge Driver | Not available in Java 8+ |
| Type 2 | Native API Driver | Platform-independent (partially) |
| Type 3 | Network Protocol Driver | Supports multiple databases, requires a middleware server |
| Type 4 | Thin Driver | Fastest, fully platform-independent, most commonly used |

## Steps to Connect & Query a Database

1. Import packages
2. Load the driver
3. Establish a connection
4. Create a statement — `Statement` / `PreparedStatement` / `CallableStatement`
5. Execute the query — `executeQuery()`, `executeUpdate()`, `execute()`
6. Process the results

```java
import java.sql.*;

public class JdbcDemo {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/school";
        String user = "root";
        String password = "password";

        try (Connection conn = DriverManager.getConnection(url, user, password)) {

            // Statement — plain SQL
            Statement stmt = conn.createStatement();
            ResultSet rs = stmt.executeQuery("SELECT * FROM students");
            while (rs.next()) {
                System.out.println(rs.getString("name") + " - " + rs.getInt("marks"));
            }

            // PreparedStatement — parameterized query (prevents SQL injection)
            String sql = "INSERT INTO students (name, marks) VALUES (?, ?)";
            PreparedStatement ps = conn.prepareStatement(sql);
            ps.setString(1, "Riya");
            ps.setInt(2, 88);
            ps.executeUpdate();

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

### `executeQuery()` vs `executeUpdate()` vs `execute()`

| Method | Use For | Returns |
|---|---|---|
| `executeQuery()` | `SELECT` statements | `ResultSet` |
| `executeUpdate()` | `INSERT` / `UPDATE` / `DELETE` | int (rows affected) |
| `execute()` | Either — generic case | boolean |

---
# Part D — Project Structure (JDBC-Based Application)

| Package | Purpose |
|---|---|
| `com.jfs.training.bean` | All the model (POJO) classes |
| `com.jfs.training.entity` | JPA — mapping classes to database tables |
| `com.jfs.training.dao` | DAO interfaces + their implementation classes |
| `com.jfs.training.service` | Service interfaces + their implementation classes |
| `com.jfs.training.exceptions` | All custom exceptions |
| `com.jfs.training.utility` | Utility classes (e.g. `DBConnectionUtil`) |
| `com.jfs.training.uitester` | Main class — entry point for testing |

```java
// com.jfs.training.utility.DBConnectionUtil
package com.jfs.training.utility;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class DBConnectionUtil {
    private static final String URL = "jdbc:mysql://localhost:3306/school";
    private static final String USER = "root";
    private static final String PASSWORD = "password";

    public static Connection getConnection() throws SQLException {
        return DriverManager.getConnection(URL, USER, PASSWORD);
    }
}
```

```java
// com.jfs.training.dao.StudentDao
package com.jfs.training.dao;

import com.jfs.training.bean.Student;
import java.util.List;

public interface StudentDao {
    void addStudent(Student student);
    Student getStudentById(int id);
    List<Student> getAllStudents();
    void updateStudent(Student student);
    void deleteStudent(int id);
}
```
