# Day 27 - Load Balancer, Actuator & REST CRUD Example
*Tue, 4 Aug 2026*

## Load Balancer

A component that **distributes incoming network traffic or application requests** across multiple servers or service instances.

### Main Goals

- Availability
- Scalability
- Performance
- Reliability

### Types of Load Balancers

1. **Hardware Load Balancer**
2. **Software Load Balancer**
3. **Layer 4 (Transport Layer) Load Balancer**
4. **Layer 7 (Application Layer) Load Balancer**
5. **Cloud Load Balancer**

## Spring Cloud Load Balancer

A **client-side** load balancing library — the client itself decides which service instance to call, using data from the service registry (e.g. Eureka).

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-loadbalancer</artifactId>
</dependency>
```

---
## Spring Boot Actuator

Provides production-ready monitoring capabilities out of the box:

- Health monitoring
- Metrics collection
- Application info
- Environment details
- Logging management
- Thread and heap dumps

### Common Actuator Endpoints

| Endpoint | Purpose |
|---|---|
| `/actuator` | Lists all available actuator endpoints |
| `/actuator/health` | Application health status |
| `/actuator/info` | Custom application info |
| `/actuator/metrics` | Application metrics (memory, requests, etc.) |
| `/actuator/env` | Environment properties |
| `/actuator/loggers` | View/change logging levels at runtime |
| `/actuator/beans` | Lists all Spring beans in the context |
| `/actuator/mappings` | Lists all `@RequestMapping` paths |
| `/actuator/caches` | Cache information (see Day 23's caching) |

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

---
## Worked Example — REST CRUD Controller

A complete `@RestController` demonstrating `ResponseEntity`, `@PathVariable`, `@RequestBody`, and explicit `consumes`/`produces` content negotiation (tying back to Day 22).

```java
package com.accenture.ltt.controller;

import java.util.Collection;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.MediaType;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RestController;

import com.accenture.ltt.model.Employee;
import com.accenture.ltt.service.EmployeeServiceImpl;

@RestController
// @RestController extends @Controller — return values are automatically
// converted to JSON or XML instead of being resolved to a view name
public class EmployeeController {

    @Autowired
    private EmployeeServiceImpl employeeService;

    // GET — fetch all employees
    @RequestMapping(value = "emp/controller/getDetails",
            method = RequestMethod.GET,
            produces = MediaType.APPLICATION_JSON_VALUE)
    public ResponseEntity<Collection<Employee>> getEmployeeDetails() {
        Collection<Employee> listEmployee = employeeService.getEmployeeDetails();
        return new ResponseEntity<>(listEmployee, HttpStatus.OK);
    }

    // GET — fetch one employee by ID (path variable)
    @RequestMapping(value = "emp/controller/getDetailsById/{id}",
            method = RequestMethod.GET,
            produces = MediaType.APPLICATION_JSON_VALUE)
    public ResponseEntity<Employee> getEmployeeDetailByEmployeeId(@PathVariable("id") int myId) {
        Employee employee = employeeService.getEmployeeDetailByEmployeeId(myId);
        if (employee != null) {
            return new ResponseEntity<>(employee, HttpStatus.OK);
        } else {
            return new ResponseEntity<>(HttpStatus.NOT_FOUND);
        }
    }

    // POST — add a new employee
    @RequestMapping(value = "/emp/controller/addEmp",
            method = RequestMethod.POST,
            consumes = MediaType.APPLICATION_JSON_VALUE,
            produces = MediaType.TEXT_HTML_VALUE)
    public ResponseEntity<String> addEmployee(@RequestBody Employee employee) {
        int id = employeeService.addEmployee(employee);
        return new ResponseEntity<>("Employee added successfully with id:" + id, HttpStatus.CREATED);
    }

    // PUT — update an existing employee
    @RequestMapping(value = "/emp/controller/updateEmp",
            method = RequestMethod.PUT,
            consumes = MediaType.APPLICATION_JSON_VALUE,
            produces = MediaType.APPLICATION_JSON_VALUE)
    public ResponseEntity<Employee> updateEmployee(@RequestBody Employee employee) {
        Employee updated = employeeService.updateEmployee(employee);
        if (updated == null) {
            return new ResponseEntity<>(updated, HttpStatus.INTERNAL_SERVER_ERROR);
        }
        return new ResponseEntity<>(updated, HttpStatus.OK);
    }

    // DELETE — remove an employee by ID
    @RequestMapping(value = "/emp/controller/deleteEmp/{id}",
            method = RequestMethod.DELETE,
            produces = MediaType.APPLICATION_JSON_VALUE)
    public ResponseEntity<Employee> deleteEmployee(@PathVariable("id") int myId) {
        Employee removed = employeeService.deleteEmployee(myId);
        if (removed == null) {
            return new ResponseEntity<>(removed, HttpStatus.INTERNAL_SERVER_ERROR);
        }
        return new ResponseEntity<>(removed, HttpStatus.OK);
    }
}
```

### Key Points From This Example

| Element | Purpose |
|---|---|
| `@RestController` | Extends `@Controller`; return values auto-convert to JSON/XML instead of resolving a view name |
| `consumes` | The content type the endpoint **accepts** in the request body (e.g. `addEmp` only accepts JSON) |
| `produces` | The content type the endpoint **returns** (`addEmp` returns plain HTML text, the rest return JSON) |
| `ResponseEntity<>(body, HttpStatus)` | Wraps the response body **and** the exact HTTP status to send back |
| `HttpStatus.CREATED` (201) | Correct status for a successful POST/create |
| `HttpStatus.NOT_FOUND` (404) | Returned when a `@PathVariable` lookup finds nothing |
| `HttpStatus.INTERNAL_SERVER_ERROR` (500) | Returned when an update/delete operation unexpectedly fails |

### Matching JPA Entity

```java
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import javax.persistence.Table;

@Entity
@Table(name = "Employee")
public class EmployeeEntity {

    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Integer employeeId;

    private double salary;
    private Integer departmentCode;
    private String employeeName;

    public EmployeeEntity() {
        super();
    }

    public EmployeeEntity(String employeeName, Integer employeeId, double salary, Integer departmentCode) {
        super();
        this.employeeName = employeeName;
        this.employeeId = employeeId;
        this.salary = salary;
        this.departmentCode = departmentCode;
    }

    // getters and setters...

    @Override
    public String toString() {
        return "Employee [employeeName=" + employeeName + ", employeeId="
                + employeeId + ", salary=" + salary + ", departmentCode="
                + departmentCode + "]";
    }
}
```

> `@GeneratedValue(strategy = GenerationType.AUTO)` — unlike the manually-assigned IDs seen in earlier Day 13/15 examples, `AUTO` lets Hibernate pick the best ID generation strategy for the underlying database automatically.

### Service Layer (Imports Preview)

The corresponding service implementation uses `BeanUtils` (for copying properties between objects) alongside standard Spring/JPA imports:

```java
import java.util.ArrayList;
import java.util.Collection;
import java.util.List;
import java.util.Optional;

import org.springframework.beans.BeanUtils;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
```

`BeanUtils.copyProperties(source, target)` is a common shortcut for copying matching field values from one object to another (e.g. from a DTO to an Entity) without writing each setter call manually.
