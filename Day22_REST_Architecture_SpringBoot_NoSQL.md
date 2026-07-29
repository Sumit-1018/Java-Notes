# Day 22 - REST Services, Architecture Styles & NoSQL
*Tue, 28 Jul 2026*

## REST Service

**REST — Representational State Transfer**

Creates an object of the data requested by the client and sends the values of that object in response to the user.

### Spring REST — Key Building Blocks

| Annotation / Type | Purpose |
|---|---|
| `@Controller` + `@ResponseBody` | Returns data directly in the response body (instead of a view name) |
| `@RestController` | Shorthand for `@Controller` + `@ResponseBody` on every method |
| `@RequestBody` | Maps the incoming request body (e.g. JSON) to a Java object |
| `@PathVariable` | Extracts a value from the URL path |
| `@RequestMapping(value="/...", method="", produces="", consumes="")` | Maps a request to a handler, with method/format constraints |
| `ResponseEntity<>` | Wraps the response body **and** the HTTP status code |

```java
@RestController
@RequestMapping("/api/employees")
public class EmployeeController {

    @GetMapping("/{id}")
    public ResponseEntity<Employee> getEmployee(@PathVariable Long id) {
        Employee emp = employeeService.findById(id);
        return ResponseEntity.ok(emp);   // 200 OK + body
    }

    @PostMapping
    public ResponseEntity<Employee> addEmployee(@RequestBody Employee employee) {
        Employee saved = employeeService.save(employee);
        return ResponseEntity.status(HttpStatus.CREATED).body(saved);   // 201 Created
    }
}
```

---
## Application Architecture Styles

### Monolithic

Entire application built as a **single unit**, with modules tightly integrated.

```
UI + Logic → DB   (all in one deployable)
```

| Advantages | Disadvantages |
|---|---|
| Simple to develop and deploy initially | Difficult to scale |
| Easier testing | A small change may require redeploying the whole app |
| Easy to debug | Hard to maintain |
| Lower operational complexity | Technology stack is fixed |
| | Failure in one module can affect the whole application |

### SOA — Service-Oriented Architecture

Application divided into **reusable services** that communicate through a centralized mechanism, such as an **ESB** (Enterprise Service Bus).

| Advantages | Disadvantages |
|---|---|
| Reusability | ESB can become a bottleneck |
| Easier integration | More complex |
| Supports heterogeneous technologies | Higher governance costs |
| Better maintainability than monolithic | Latency |

### Microservices

Application split into many **small, independent services** that communicate through lightweight APIs.

| Advantages | Disadvantages |
|---|---|
| Independent deployments | Complex deployment |
| Scale independently | Distributed system challenges |
| Better fault isolation | More infrastructure requirements |
| Teams can work separately | Debugging is difficult |
| Supports different technologies per service | |

---
## Introduction to Spring Boot

Built for **Rapid Application Development** — production-ready applications with minimal setup.

- Auto-configured
- Embedded server (Tomcat, Jetty, Undertow) — no separate server install needed
- Starter dependencies — pre-bundled dependency sets (e.g. `spring-boot-starter-web`)
- Minimal configuration

### Bootstrapping Classes

| Class | Purpose |
|---|---|
| `SpringApplication` | Bootstraps and launches a Spring Boot application |
| `SpringApplicationBuilder` | Fluent builder API for more customized startup (e.g. child contexts) |

```java
@SpringBootApplication
public class MyApp {
    public static void main(String[] args) {
        SpringApplication.run(MyApp.class, args);
    }
}
```

## Content Negotiation

Determines the **format** of the response, based on the client's request.

Ways a client can request a format:
1. **Accept Header**
2. **URL Parameter**
3. **File Extension**

```java
@GetMapping(value = "/employees", produces = {
    MediaType.APPLICATION_JSON_VALUE,
    MediaType.APPLICATION_XML_VALUE
})
```

`ContentNegotiationManager` is the underlying component that resolves which format to actually send.

## Profiles (Spring Boot Context)

Used for **selective loading** of application components — same `@Profile` concept from Day 17, now applied with Spring Boot's `application-<profile>.properties` / `.yml` files.

```java
@Component
@Profile("logging")
public class LoggingConfig {
    // only loaded when the "logging" profile is active
}
```

```
application-Logging_Profile.properties
```

---
## NoSQL

**NoSQL — Not Only SQL**

Non-relational databases designed to store and manage large volumes of **structured, semi-structured, and unstructured** data — built for flexibility, scalability, and high performance in modern applications.

### Features

- Schema-less
- Horizontal scalability
- High availability
- Fast data access
- Supports distributed architecture

### Advantages

- Handles big data efficiently
- Easy to scale
- Flexible data models
- Suitable for real-time applications

**Examples:** MongoDB, Cassandra, Redis, CouchDB, HBase

### NoSQL Data Models

| Model | Description |
|---|---|
| **Document-Based** | Stores data as documents (JSON/BSON format) |
| **Key-Value** | Stores data as key-value pairs |
| **Column-Family** | Stores data in columns rather than rows |
| **Graph** | Stores data as nodes and relationships |

## MongoDB Shell Commands

```bash
mongod                          # start the MongoDB server (in terminal)
mongosh                         # open the MongoDB shell

use collegeDB                   # create/select a database

db.createCollection("students") # create a collection
```

```javascript
// insert one document
db.students.insertOne({
    name: "Rahul",
    age: 20,
    department: "CSE"
})

// insert multiple documents
db.students.insertMany([
    { name: "Priya", age: 21, department: "IT" },
    { name: "Kumar", age: 22, department: "ECE" }
])

// display all documents
db.students.find()

// display matching documents
db.students.find({ name: "Rahul" })

// display one document
db.students.findOne({ age: 21 })

// update one document
db.students.updateOne(
    { name: "Rahul" },
    { $set: { age: 23 } }
)

// update many documents
db.students.updateMany(
    { department: "IT" },
    { $set: { status: "Active" } }
)

// replace an entire document
db.students.replaceOne(
    { name: "Kumar" },
    { name: "Kumar", age: 22, department: "EEE" }
)

// delete one document
db.students.deleteOne({ name: "Rahul" })

// delete many documents
db.students.deleteMany({ department: "IT" })

// delete all documents
db.students.deleteMany({})
```

## Connecting Java to MongoDB

`MongoClient` is the main class used to connect a Java application to MongoDB. `MongoClients.create()` creates a connection to the server.

```java
package com.jfs.training;

import org.bson.Document;
import com.mongodb.client.FindIterable;
import com.mongodb.client.MongoClient;
import com.mongodb.client.MongoClients;
import com.mongodb.client.MongoCollection;
import com.mongodb.client.MongoDatabase;

public class MongoDbConnection {

    public static void main(String[] args) {

        String uri = "mongodb://localhost:27017";

        try (MongoClient mongoClient = MongoClients.create(uri)) {

            MongoDatabase database = mongoClient.getDatabase("collegeDB");

            System.out.println("Connected to the database successfully");
            System.out.println("Database Name: " + database.getName());

            MongoCollection<Document> collection = database.getCollection("students");

            Document student = new Document("name", "John Doe")
                    .append("age", 20)
                    .append("major", "Computer Science");

            // collection.insertOne(student);
            // System.out.println("Inserted a document into the collection successfully");

            // update
            collection.updateOne(
                new Document("name", "John Doe"),
                new Document("$set", new Document("age", 21))
            );

            // read
            FindIterable<Document> documents = collection.find();
            for (Document doc : documents) {
                System.out.println(doc.toJson());
            }

        } catch (Exception e) {
            System.err.println("An error occurred while connecting to the database: " + e.getMessage());
        }
    }
}
```
