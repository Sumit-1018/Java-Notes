# QuantumCrew — MCQ Assessment Prep (Comprehensive)
### Part 3 of 3 — Days 18 to 25

---
## Day 18 — Spring ORM & Transaction Management Basics

**Q1.** Which of these is NOT a listed Spring module?
A) Spring Core  B) Spring MVC  C) Spring Data Access  D) **Spring Compiler**

**Q2.** Which DB integration approach is described as low-level with more manual coding?
A) JPA  B) **JDBC**  C) Hibernate  D) Spring Data JPA

**Q3.** Which DB integration approach is described as "Recommended" and framework-independent?
A) JDBC  B) **JPA**  C) Direct Hibernate use  D) Native SQL

**Q4.** Spring ORM's job is to:
A) Replace SQL entirely  B) **Integrate ORM tools with Spring, mapping Java objects to DB tables**  C) Only manage transactions  D) Handle only NoSQL

**Q5.** Which is NOT listed as an ORM tool?
A) Hibernate  B) EclipseLink  C) TopLink  D) **MongoDB**

**Q6.** Spring Data JPA is built:
A) Independently of JPA  B) **On top of JPA**  C) As a replacement for Hibernate  D) Only for NoSQL

**Q7.** A key benefit of Spring Data JPA is:
A) More boilerplate  B) **No need to write DAO implementation classes**  C) Manual SQL required everywhere  D) No pagination support

**Q8.** Transaction management ensures operations execute as:
A) Independent, unrelated tasks  B) **A single unit of work — all succeed or all fail**  C) Always asynchronous tasks  D) Background jobs only

**Q9.** Which is the RECOMMENDED transaction management style?
A) Programmatic  B) **Declarative (`@Transactional` or XML)**  C) Manual only  D) None — transactions are automatic

**Q10.** Programmatic transaction management involves:
A) Only annotations  B) **Manually controlling transaction start, commit, and rollback in code**  C) No code at all  D) XML configuration only

**Q11.** Which ACID property ensures the DB remains valid before and after a transaction?
A) Atomicity  B) **Consistency**  C) Isolation  D) Durability

**Q12.** Which ACID property ensures concurrent transactions don't interfere with each other?
A) Atomicity  B) Consistency  C) **Isolation**  D) Durability

**Q13.** Which ACID property ensures committed data survives even after an application crash?
A) Atomicity  B) Consistency  C) Isolation  D) **Durability**

**Q14.** Which ACID property means all operations commit, or none do?
A) **Atomicity**  B) Consistency  C) Isolation  D) Durability

**Q15.** `EntityManagerFactory` is:
A) Created many times per request  B) **Heavyweight, thread-safe, created once per application**  C) Lightweight and thread-unsafe  D) Not part of JPA

**Q16.** `EntityManager` is:
A) Thread-safe  B) **Lightweight and NOT thread-safe**  C) Created once per application  D) Used outside of transactions only

**Q17.** The entity lifecycle sequence is:
A) Managed → Transient → Removed → Detach  B) **Transient → Managed → Detach → Remove**  C) Remove → Detach → Managed → Transient  D) Detach → Transient → Managed

**Q18.** A Global Transaction typically uses:
A) `JpaTransactionManager`  B) **`JtaTransactionManager` with a JTA provider**  C) No transaction manager  D) `DataSourceTransactionManager` only

**Q19.** A Local Transaction typically works with:
A) Multiple databases and a JMS queue  B) **A single resource/database**  C) No database at all  D) Only distributed systems

**Q20.** Which is an example of a Global Transaction use case?
A) Simple online shopping cart  B) **Flight booking spanning Airline DB + Payment + JMS Queue**  C) A single-table update  D) Reading a config file

---
## Day 19 — Transaction Propagation & Spring Data JPA

**Q1.** Transaction Propagation defines:
A) How data is encrypted  B) **How Spring handles transactions when one `@Transactional` method calls another**  C) How beans are scanned  D) How exceptions are logged

**Q2.** A "Physical Transaction" is typically associated with:
A) DAO layer, per method  B) **Service layer usage of `@Transactional`**  C) Controller layer only  D) No specific layer

**Q3.** A "Logical Transaction" is typically associated with:
A) Service layer only  B) **DAO layer, `@Transactional` on each method independently**  C) Controller layer  D) The database itself

**Q4.** Which propagation type is the default choice for typical business operations (Order, Payment)?
A) REQUIRES_NEW  B) **REQUIRED**  C) NEVER  D) NOT_SUPPORTED

**Q5.** Which propagation type ALWAYS creates a brand-new transaction, useful for audit logs?
A) REQUIRED  B) **REQUIRES_NEW**  C) SUPPORTS  D) MANDATORY

**Q6.** Which propagation type uses a savepoint within the same transaction, useful for partial rollback?
A) REQUIRED  B) REQUIRES_NEW  C) **NESTED**  D) SUPPORTS

**Q7.** Which propagation type requires an existing transaction, else it errors?
A) NEVER  B) **MANDATORY**  C) SUPPORTS  D) NOT_SUPPORTED

**Q8.** Which propagation type must NOT run inside a transaction, else it errors?
A) MANDATORY  B) **NEVER**  C) SUPPORTS  D) REQUIRED

**Q9.** Which propagation type uses a transaction if one exists, but runs fine without one too — good for read-only/search methods?
A) MANDATORY  B) NEVER  C) **SUPPORTS**  D) REQUIRES_NEW

**Q10.** Which propagation type suspends any existing transaction and runs without one — good for long reports/batch reads?
A) SUPPORTS  B) **NOT_SUPPORTED**  C) MANDATORY  D) NESTED

**Q11.** Spring Data JPA is:
A) A JPA provider itself  B) **A library adding abstraction on top of a JPA provider**  C) A replacement for Hibernate  D) Unrelated to JPA

**Q12.** Spring Data JPA eliminates boilerplate mainly through:
A) Manual SQL writing  B) **Repository abstraction**  C) XML configuration  D) Static utility classes

**Q13.** How is a Spring Data JPA DAO layer typically implemented?
A) A concrete class extending JpaRepository  B) **An interface extending a predefined repository interface**  C) A static utility method  D) An abstract class only

**Q14.** At runtime, the interface-based DAO is implemented via:
A) Manual coding  B) **A generated proxy object**  C) XML mapping only  D) Reflection-free static binding

**Q15.** What are the two required type parameters for the `Repository` marker interface?
A) Service class, DAO class  B) **Entity class, ID type**  C) Controller, View  D) Bean name, scope

**Q16.** Which interface provides basic CRUD operations for a managed entity?
A) Repository  B) **CrudRepository**  C) PagingAndSortingRepository  D) JpaRepository (only)

**Q17.** Which interface adds sorting and pagination support?
A) CrudRepository  B) **PagingAndSortingRepository**  C) Repository  D) JpaRepository (only)

**Q18.** Which interface combines all others AND exposes underlying JPA provider capabilities?
A) Repository  B) CrudRepository  C) PagingAndSortingRepository  D) **JpaRepository**

**Q19.** `CrudRepository` and `PagingAndSortingRepository` belong to:
A) Spring Data JPA specifically  B) **Spring Data Commons**  C) Hibernate  D) Spring MVC

**Q20.** `JpaRepository` belongs to:
A) Spring Data Commons  B) **Spring Data JPA**  C) Spring Core  D) Spring Security

**Q21.** A Named Query is:
A) Compiled at runtime, every call  B) **A predefined, reusable JPQL/SQL query, compiled at application startup**  C) Only usable once  D) Not reusable

**Q22.** How many types of Named Queries are there?
A) 1  B) **2 (JPQL and Native)**  C) 3  D) 4

**Q23.** `@NamedNativeQuery` executes:
A) JPQL against entity names  B) **Actual SQL against table names**  C) No query at all  D) Only stored procedures

---
## Day 20 — Spring MVC: Fundamentals, Views & Forms

**Q1.** MVC stands for:
A) Model View Component  B) **Model View Controller**  C) Multiple View Class  D) Model Verify Controller

**Q2.** In MVC, which part holds the data?
A) View  B) Controller  C) **Model**  D) DispatcherServlet

**Q3.** In MVC, which part acts as the UI, taking input and showing output?
A) Model  B) **View**  C) Controller  D) HandlerMapping

**Q4.** In MVC, which part performs the business logic?
A) Model  B) View  C) **Controller**  D) ViewResolver

**Q5.** In old Servlet MVC, what acted as the controller?
A) JSP  B) **The Servlet itself**  C) HTML  D) The database

**Q6.** In the Spring MVC workflow, which component receives EVERY incoming request first?
A) HandlerMapping  B) **DispatcherServlet**  C) Controller  D) ViewResolver

**Q7.** `HandlerMapping`'s role is to:
A) Render the final HTML  B) **Identify the specific controller for a request**  C) Store session data  D) Manage the database connection

**Q8.** After business logic runs, a Controller returns:
A) A full HTML page  B) **A view name (logical name)**  C) A database record directly  D) Nothing

**Q9.** `ViewResolver`'s job is to:
A) Execute business logic  B) **Map the logical view name to the actual view file**  C) Handle exceptions  D) Validate form data

**Q10.** In `InternalResourceViewResolver`, what does `setPrefix("/WEB-INF/views/")` do?
A) Sets the suffix  B) **Sets the folder path prepended to the view name**  C) Sets the controller path  D) Disables the resolver

**Q11.** If a controller returns `"home"`, and prefix=`/WEB-INF/views/`, suffix=`.jsp`, the resolved path is:
A) `home.jsp`  B) **`/WEB-INF/views/home.jsp`**  C) `/home`  D) `WEB-INF/home`

**Q12.** The Spring Form Tag binds form components in which direction?
A) Controller to View only  B) **View to Controller, one-way**  C) Bidirectional always  D) Database to View

**Q13.** `@ModelAttribute` at the method PARAMETER level is used to:
A) Send data from controller to view before any handler runs  B) **Map submitted form data to a Java object**  C) Configure a database  D) Handle exceptions

**Q14.** `@ModelAttribute` at the METHOD level (not parameter) runs:
A) After the handler method  B) **Before any handler (`@RequestMapping`) method executes**  C) Only once per application  D) Never, unless called explicitly

**Q15.** In Static UI, values are:
A) Pulled from the database at runtime  B) **Hardcoded in the JSP/HTML**  C) Always empty  D) Generated by AI

**Q16.** In Dynamic UI, values come from:
A) Hardcoded JSP  B) **The backend/Model, generated at runtime**  C) Nowhere  D) Only from URL parameters

**Q17.** `<form:radiobutton>` (singular) is typically used for:
A) Dynamic UI  B) **Static UI, one hardcoded option per tag**  C) File uploads  D) Session management

**Q18.** `<form:radiobuttons>` (plural, with `items="${...}"`) is typically used for:
A) **Dynamic UI, generating multiple options from backend data**  B) Static UI only  C) File uploads  D) Password fields

---
## Day 21 — Spring MVC: Validation, Exceptions & Sessions

**Q1.** Validations are classified into which two top-level categories?
A) Field and Method  B) **Standard and Custom**  C) Local and Global  D) Static and Dynamic

**Q2.** Custom validation is further split into:
A) Static and Dynamic  B) **Field and Cross-Field**  C) Local and Remote  D) Client and Server

**Q3.** Cross-field validation is needed when:
A) A single field needs a regex check  B) **One field's validity depends on another field (e.g. password = confirm password)**  C) No fields need checking  D) Only numeric fields are involved

**Q4.** Standard validation rules come from:
A) A custom Spring API  B) **The JSR Bean Validation API**  C) JDBC  D) Maven plugins

**Q5.** Hibernate Validator is:
A) The specification itself  B) **The implementation of the JSR Bean Validation specification**  C) Unrelated to validation  D) A database validator only

**Q6.** `@NotEmpty`, `@Size(min=3,max=10)` are examples of:
A) Custom cross-field validation  B) **Standard validation annotations**  C) Exception handlers  D) SpEL expressions

**Q7.** `@AssertTrue` is used to ensure:
A) A string is not null  B) **A boolean field must be `true`**  C) A number is positive  D) A date is in the future

**Q8.** `@InitBinder` is mainly used for:
A) Standard validation only  B) **Custom/complex validation logic and data-binding customization**  C) Database connections  D) Session management

**Q9.** How many ways can validation messages be provided?
A) 1  B) 2  C) **3**  D) 5

**Q10.** Which validation message method uses an external `messages.properties` file?
A) Default message  B) Annotation-level message  C) **`messages.properties` file**  D) None of these

**Q11.** What is the first step in building a custom validation?
A) Use the annotation on a class  B) **Create the annotation**  C) Link validator and annotation  D) Create the validator

**Q12.** A Local Exception Handler is defined:
A) In a separate global class  B) **Inside the controller class itself, using `@ExceptionHandler`**  C) In the DAO layer  D) In `web.xml` only

**Q13.** `@ControllerAdvice` provides:
A) Local-only exception handling  B) **Global support across all controllers**  C) Only database configuration  D) Session cleanup only

**Q14.** Which of these is NOT a use of `@ControllerAdvice`?
A) Global exception handling  B) Common model data via `@ModelAttribute`  C) Global data binding via `@InitBinder`  D) **Compiling the application**

**Q15.** HTTP requests are, by nature:
A) Stateful  B) **Stateless**  C) Always encrypted  D) Session-bound automatically

**Q16.** To share data across multiple requests/submissions, data must be kept in:
A) Request scope  B) **Session scope**  C) Application-wide static variables only  D) Local variables

**Q17.** `HttpSession` holds data in the form of:
A) An array  B) **Key-value pairs (like a Map)**  C) A single string  D) XML

**Q18.** `@SessionAttributes` is applied at:
A) Method level  B) **Class level**  C) Field level  D) Parameter level only

---
## Day 22 — REST, Architecture Styles, Spring Boot & NoSQL

**Q1.** REST stands for:
A) Rapid External State Transfer  B) **Representational State Transfer**  C) Remote Entity State Transaction  D) Reliable External Server Transfer

**Q2.** `@RestController` is shorthand for combining:
A) @Controller + @RequestMapping  B) **@Controller + @ResponseBody**  C) @Service + @Repository  D) @Component + @Configuration

**Q3.** `@RequestBody` is used to:
A) Extract a URL path variable  B) **Map an incoming request body (e.g. JSON) to a Java object**  C) Set the HTTP status  D) Render a JSP

**Q4.** `@PathVariable` is used to:
A) Map JSON body  B) **Extract a value from the URL path**  C) Set response headers  D) Configure caching

**Q5.** `ResponseEntity<>` wraps:
A) Only the response body  B) **Both the response body and HTTP status code**  C) Only the status code  D) Nothing — it's just a marker

**Q6.** In a Monolithic architecture, a small change:
A) Only affects one microservice  B) **May require redeploying the entire application**  C) Never requires redeployment  D) Is always risk-free

**Q7.** Which architecture uses a centralized ESB for communication?
A) Monolithic  B) **SOA**  C) Microservices  D) Serverless

**Q8.** Which architecture style allows independent deployments and independent scaling per service?
A) Monolithic  B) SOA  C) **Microservices**  D) None of these

**Q9.** A key disadvantage of SOA is:
A) No reusability  B) **The ESB can become a bottleneck**  C) It can't support heterogeneous tech  D) It's simpler than microservices

**Q10.** A key disadvantage of Microservices is:
A) Poor fault isolation  B) **Complex deployment and distributed system challenges**  C) Can't scale independently  D) Locked into one technology

**Q11.** Spring Boot provides an embedded server. Which of these is NOT listed as an option?
A) Tomcat  B) Jetty  C) Undertow  D) **Apache HTTPD**

**Q12.** `SpringApplication.run(...)` is used to:
A) Only compile the app  B) **Bootstrap and launch a Spring Boot application**  C) Run database migrations only  D) Deploy to production automatically

**Q13.** `SpringApplicationBuilder` is useful for:
A) Writing SQL  B) **More customized startup, e.g. child contexts**  C) Managing threads  D) Handling exceptions

**Q14.** Content Negotiation determines:
A) Which database to use  B) **The format of the response, based on the client's request**  C) The logging level  D) The thread pool size

**Q15.** Which of these is NOT listed as a way a client can request a content format?
A) Accept Header  B) URL Parameter  C) File Extension  D) **Request Body Size**

**Q16.** NoSQL stands for:
A) No Structured Query Language  B) **Not Only SQL**  C) New Style Query Language  D) Non-Standard Query Logic

**Q17.** Which is NOT a listed NoSQL feature?
A) Schema-less  B) Horizontal scalability  C) **Mandatory fixed schema**  D) High availability

**Q18.** Which NoSQL data model stores data as JSON/BSON documents?
A) Key-Value  B) **Document-Based**  C) Column-Family  D) Graph

**Q19.** Which NoSQL data model stores data as nodes and relationships?
A) Document-Based  B) Key-Value  C) Column-Family  D) **Graph**

**Q20.** Which NoSQL data model stores data in columns rather than rows?
A) Document-Based  B) Key-Value  C) **Column-Family**  D) Graph

**Q21.** Which command starts the MongoDB server in the terminal?
A) mongosh  B) **mongod**  C) mongostart  D) mongorun

**Q22.** Which command opens the MongoDB shell?
A) mongod  B) **mongosh**  C) mongoconnect  D) mongoclient

**Q23.** Which command creates/selects a MongoDB database?
A) `db.create("name")`  B) **`use collegeDB`**  C) `new db("name")`  D) `select db collegeDB`

**Q24.** Which command inserts multiple documents at once in MongoDB?
A) insertOne()  B) **insertMany()**  C) insertAll()  D) bulkInsert()

**Q25.** Which command deletes ALL documents in a MongoDB collection?
A) `db.students.deleteOne({})`  B) **`db.students.deleteMany({})`**  C) `db.students.dropAll()`  D) `db.students.remove()` only

**Q26.** In Java, which class is used to connect to MongoDB?
A) DBConnection  B) **MongoClient**  C) MongoConnector  D) NoSQLClient

**Q27.** `MongoClients.create(uri)` is used to:
A) Delete a database  B) **Create a connection to the MongoDB server**  C) Insert data directly  D) Compile the driver

---
## Day 23 — Spring Boot Caching, YAML, RestTemplate, AOP & Testing

**Q1.** `@EnableCaching` is typically placed on:
A) The service class  B) **The primary configuration/application class**  C) The controller  D) The entity class

**Q2.** Which annotation caches a method's return value?
A) @CacheEvict  B) **@Cacheable**  C) @CachePut  D) @Cache

**Q3.** Which annotation updates the cache WITHOUT skipping method execution?
A) @Cacheable  B) **@CachePut**  C) @CacheEvict  D) @Caching

**Q4.** Which annotation removes entries from the cache?
A) @Cacheable  B) @CachePut  C) **@CacheEvict**  D) @EnableCaching

**Q5.** Which annotation combines multiple cache annotations on one method?
A) @Cacheable  B) @CachePut  C) @CacheEvict  D) **@Caching**

**Q6.** `ConcurrentMapCacheManager` internally uses:
A) Redis  B) Ehcache  C) **ConcurrentHashMap**  D) A relational database

**Q7.** Which cache option is best suited for distributed/clustered microservices?
A) ConcurrentMapCacheManager  B) Ehcache  C) **Redis Cache**  D) None support distribution

**Q8.** In YAML, what character follows a key?
A) Equals sign  B) **Colon**  C) Semicolon  D) Arrow

**Q9.** In YAML, lists are represented using:
A) Curly braces  B) Square brackets only  C) **A dash (`-`)**  D) Numbered indices

**Q10.** In YAML, which of these should NEVER be used for indentation?
A) Spaces  B) **Tabs**  C) Either is fine  D) No indentation is needed

**Q11.** `@ConfigurationProperties` works with:
A) Only XML files  B) **YAML/properties-based configuration**  C) Only Java annotations, no external config  D) Only database configs

**Q12.** Which Runner interface's method signature is `run(ApplicationArguments args)`?
A) **ApplicationRunner**  B) CommandLineRunner  C) JobRunner  D) StartupRunner

**Q13.** Which Runner interface's method signature is `run(String... args)`?
A) ApplicationRunner  B) **CommandLineRunner**  C) BatchRunner  D) InitRunner

**Q14.** `@Order()` on multiple Runners controls:
A) Their return type  B) **Their execution order**  C) Their thread safety  D) Their cache eviction

**Q15.** To package a Spring Boot app as a WAR for an external servlet container, you must:
A) Do nothing extra  B) **Extend `SpringBootServletInitializer` and override `configure()`**  C) Remove all dependencies  D) Use `mvn clean` only

**Q16.** When packaging as WAR, the embedded server dependency scope should be set to:
A) compile  B) **provided**  C) runtime  D) test

**Q17.** Which `RestTemplate` method performs a GET and returns the body as an object?
A) postForObject()  B) **getForObject()**  C) put()  D) delete()

**Q18.** `RestTemplate.exchange()` is notable because it:
A) Only supports GET  B) **Is generic — supports any HTTP method, headers, and full response access**  C) Cannot handle errors  D) Doesn't return a response body

**Q19.** In `ResponseErrorHandler`, which method checks if the response indicates an error?
A) **hasError()**  B) isError()  C) checkError()  D) errorFound()

**Q20.** AOP stands for:
A) Application-Oriented Programming  B) **Aspect-Oriented Programming**  C) Aggregated Object Programming  D) Asynchronous Object Processing

**Q21.** In AOP, which term describes a point in the program where an aspect can be applied?
A) Pointcut  B) **Join Point**  C) Advice  D) Aspect

**Q22.** In AOP, which term describes the ACTION taken at a matched join point?
A) Pointcut  B) Join Point  C) **Advice**  D) Aspect declaration

**Q23.** Which annotation marks a class as containing cross-cutting AOP logic?
A) @Cutpoint  B) **@Aspect**  C) @CrossCutting  D) @Advice

**Q24.** Which testing tools are used for Service Layer unit testing?
A) MockMvc only  B) **JUnit, Spring Test**  C) Mockito only  D) Postman

**Q25.** Which annotation is used for Service Layer Spring Boot testing?
A) @WebMvcTest  B) **@SpringBootTest**  C) @DataJpaTest  D) @RestClientTest

**Q26.** Which tool generates code coverage reports mentioned in this module?
A) SonarLint  B) **Jacoco**  C) Checkstyle  D) PMD

**Q27.** For Controller Layer INTEGRATION testing, `MockMvc` is built to replicate:
A) Only the controller  B) **The actual MVC, Controller, Service, and DAO layers**  C) Only the DAO  D) Nothing — it's a stub

**Q28.** For Controller Layer UNIT testing, what must be done to the Service layer first?
A) Nothing  B) **Declare Service Layer mocks and inject them into the controller**  C) Delete the service layer  D) Call the real database

**Q29.** Which annotation creates a MockMvc replica of JUST the controller layer?
A) @SpringBootTest  B) **@WebMvcTest**  C) @DataJpaTest  D) @Component

**Q30.** In controller unit testing, the final verification step confirms:
A) The database was updated  B) **The controller correctly delegates the call to the mock**  C) The JSON schema is valid  D) The server started correctly

---
## Day 24 — Domain-Driven Design & Spring Batch

**Q1.** DDD primarily focuses on:
A) Database schema optimization  B) **Aligning software design with real-world business requirements**  C) UI styling  D) Network protocols

**Q2.** Which is NOT a listed goal of DDD?
A) Handle complex business problems  B) Improve dev-to-domain-expert communication  C) **Minimize documentation**  D) Increase maintainability and scalability

**Q3.** The shared vocabulary between developers and domain experts is called:
A) Domain Model  B) **Ubiquitous Language**  C) Bounded Context  D) Context Map

**Q4.** People with deep business knowledge who collaborate with developers are called:
A) Stakeholders only  B) **Domain Experts**  C) QA Testers  D) Product Owners exclusively

**Q5.** Which of these is a Strategic Design concept?
A) Entities  B) Aggregates  C) **Bounded Context**  D) Repository interfaces

**Q6.** Bounded Context is defined as:
A) A database table  B) **An explicit boundary within which a domain model applies consistently**  C) A single class  D) A UI component

**Q7.** Context Mapping defines:
A) UI layouts  B) **Relationships between bounded contexts**  C) Database indexes  D) Thread pools

**Q8.** Tactical Design focuses on:
A) Boundaries between contexts  B) **Implementing the domain model itself**  C) UI wireframing  D) Server deployment

**Q9.** Which DDD layer contains Entities, Value Objects, Aggregates, and Repository interfaces?
A) Application Layer  B) **Domain Layer**  C) Infrastructure Layer  D) Interface Layer

**Q10.** Which DDD layer handles technical concerns like DB access and messaging?
A) Domain Layer  B) Application Layer  C) **Infrastructure Layer**  D) Interface Layer

**Q11.** Which DDD layer contains REST controllers or UI entry points?
A) Domain Layer  B) Application Layer  C) Infrastructure Layer  D) **Interface Layer**

**Q12.** OLTP refers to:
A) Historical analytics  B) **Real-time transaction processing**  C) Batch scheduling  D) File compression

**Q13.** OLAP refers to:
A) Real-time processing  B) **Analytical processing on historical data**  C) Thread management D) Caching

**Q14.** Batch Processing is characterized by:
A) Instant, one-record-at-a-time processing  B) **Processing huge amounts of data together, at scheduled intervals**  C) No scheduling at all  D) Only used for logging

**Q15.** Spring Batch's "Chunk Processing" means:
A) Processing one record at a time always  B) **Processing data in fixed-size groups**  C) No processing at all  D) Only reading, never writing

**Q16.** "Restartability" in Spring Batch means:
A) The app restarts automatically every hour  B) **A failed job can resume from where it left off**  C) Jobs cannot be restarted  D) Only manual restarts are logged

**Q17.** Which Spring Batch component is the top-level container for all the work?
A) Step  B) **Job**  C) ItemReader  D) ItemWriter

**Q18.** Which Spring Batch component represents a single business activity within a Job?
A) Job  B) **Step**  C) ItemProcessor  D) JobLauncher

**Q19.** Which Spring Batch component extracts data?
A) ItemWriter  B) ItemProcessor  C) **ItemReader**  D) JobRepository

**Q20.** Which Spring Batch component transforms/validates data?
A) ItemReader  B) **ItemProcessor**  C) ItemWriter  D) StepExecution

**Q21.** Which Spring Batch component stores the processed data?
A) ItemReader  B) ItemProcessor  C) **ItemWriter**  D) JobLauncher

**Q22.** The Spring Batch step flow is:
A) Write → Process → Read  B) **Read → Process → Write**  C) Process → Write → Read  D) Write → Read → Process

**Q23.** In Spring Batch's layered architecture, which layer contains Readers, Writers, and Job Repository?
A) Application Layer  B) Batch Core  C) **Infrastructure**  D) Domain Layer

---
## Day 25 — Application Security & OWASP

**Q1.** AppSec (Application Security) is the practice of protecting applications:
A) Only during development  B) **Throughout development, deployment, and maintenance**  C) Only after a breach  D) Only in production

**Q2.** Which of these is NOT a listed Secure Coding Practice?
A) Input Validation  B) Output Encoding  C) **Maximizing error detail shown to users**  D) Secure Session Management

**Q3.** Which secure coding practice directly prevents leaking stack traces to end users?
A) Input Validation  B) **Secure Error Handling**  C) Output Encoding  D) Dependency Management

**Q4.** Which practice keeps libraries updated and scans for known vulnerabilities?
A) Secure Session Management  B) **Dependency Management**  C) Output Encoding  D) Authentication

**Q5.** Which practice prevents SQL injection most directly?
A) Stored procedures always  B) **Parameterized queries**  C) String concatenation  D) Disabling logging

**Q6.** The Principle of Least Privilege means:
A) Giving every account full access  B) **Giving accounts only the permissions they actually need**  C) Disabling all accounts  D) Encrypting all traffic only

**Q7.** Which of these is a Secure Database Access practice?
A) Use string concatenation for queries  B) **Database Auditing and Logging**  C) Grant all users admin rights  D) Never encrypt sensitive data

**Q8.** Which of these is a Secure Application/Web Practice?
A) HTTP everywhere  B) **HTTPS Everywhere**  C) Disable all security headers  D) Never validate file uploads

**Q9.** Which security header helps prevent clickjacking?
A) Content-Type  B) **X-Frame-Options**  C) Cache-Control  D) Accept-Language

**Q10.** File upload security includes:
A) Accepting any file type  B) **Validating file type/size and storing outside the web root**  C) Skipping malware scans  D) Storing uploads in the web root directly

**Q11.** OWASP stands for:
A) Open Web Application Software Panel  B) **Open Worldwide Application Security Project**  C) Online World Application Software Program  D) Open Web App Security Practice

**Q12.** How many risks are on the OWASP Top 10 list?
A) 5  B) 8  C) **10**  D) 12

**Q13.** Which OWASP risk involves users acting outside their intended permissions?
A) Injection  B) **Broken Access Control**  C) Security Misconfiguration  D) Cryptographic Failures

**Q14.** Which OWASP risk involves weak or missing encryption of sensitive data?
A) Injection  B) **Cryptographic Failures**  C) Insecure Design  D) SSRF

**Q15.** Which OWASP risk covers SQL/command injection attacks?
A) Broken Access Control  B) **Injection**  C) Security Misconfiguration  D) Identification Failures

**Q16.** Which OWASP risk refers to flaws baked into the architecture itself, not just the code?
A) Security Misconfiguration  B) **Insecure Design**  C) Injection  D) Logging Failures

**Q17.** Which OWASP risk involves using libraries/frameworks with known vulnerabilities?
A) Insecure Design  B) **Vulnerable and Outdated Components**  C) SSRF  D) Broken Access Control

**Q18.** Which OWASP risk covers weak login/session mechanisms?
A) Cryptographic Failures  B) **Identification and Authentication Failures**  C) Injection  D) SSRF

**Q19.** Which OWASP risk involves trusting unverified updates, plugins, or CI/CD pipelines?
A) Injection  B) **Software and Data Integrity Failures**  C) Security Misconfiguration  D) Broken Access Control

**Q20.** Which OWASP risk covers insufficient detection of breaches in progress?
A) Insecure Design  B) **Security Logging and Monitoring Failures**  C) Injection  D) Cryptographic Failures

**Q21.** Which OWASP risk involves tricking the server into making unintended requests on the attacker's behalf?
A) Injection  B) Broken Access Control  C) **Server-Side Request Forgery (SSRF)**  D) Cryptographic Failures

---
*End of Part 3. Combined with Parts 1 and 2, this covers every topic from Day 1 through Day 25.*
