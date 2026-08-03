# QuantumCrew — MCQ Assessment Prep (Comprehensive)
### Part 2 of 3 — Days 10 to 17

---
## Day 10 — Performance Monitoring

**Q1.** The core purpose of performance monitoring is to:
A) Fix bugs after they happen  B) **Spot potential issues early, before users are impacted**  C) Replace unit testing  D) Only track uptime

**Q2.** Which of these is NOT something performance monitoring tracks?
A) CPU usage  B) Garbage Collection  C) **Code comment density**  D) Response time

**Q3.** Which tool shows heap memory, CPU usage, threads, and GC activity for a running JVM?
A) Eclipse MAT  B) **VisualVM**  C) JMeter  D) SonarQube

**Q4.** Which tool specifically generates memory leak reports from heap dumps?
A) VisualVM  B) **Eclipse MAT**  C) JMeter  D) SonarLint

**Q5.** Which tool is used for performance and load testing?
A) VisualVM  B) Eclipse MAT  C) **JMeter**  D) MAT

**Q6.** Which of these is NOT a goal of performance monitoring?
A) Identify memory leaks  B) Identify slow methods  C) Detect thread deadlocks  D) **Maximize garbage collection frequency**

**Q7.** In a typical performance-monitoring workflow, what comes right after reproducing the slow scenario?
A) Load-test with JMeter  B) **Take a heap dump**  C) Deploy to production  D) Disable logging

---
## Day 11 — SOLID Principles & Design Patterns

**Q1.** SRP states that a class should:
A) Implement multiple interfaces  B) **Have only one reason to change**  C) Extend only abstract classes  D) Avoid all methods

**Q2.** OCP states that software entities should be:
A) Open for modification, closed for extension  B) **Open for extension, closed for modification**  C) Closed for both  D) Open for both, always

**Q3.** LSP states that:
A) Interfaces should have one method  B) **Subclass objects should be substitutable for superclass objects without breaking the app**  C) A class should have one responsibility  D) High-level modules should depend on low-level modules

**Q4.** ISP states that:
A) A class should do everything  B) **Clients should not be forced to depend on interfaces they don't use**  C) All classes need a common interface  D) Interfaces should combine unrelated behaviors

**Q5.** DIP states that:
A) Low-level modules should depend on high-level modules  B) **Both high- and low-level modules should depend on abstractions**  C) Modules should never depend on each other  D) Interfaces should be avoided

**Q6.** A `Penguin` class throwing an exception when `fly()` is called (inherited from `Bird`) violates:
A) SRP  B) OCP  C) **LSP**  D) ISP

**Q7.** Splitting an `Employee` class into `Employee`, `SalaryCalculator`, and `ReportGenerator` demonstrates fixing:
A) OCP  B) **SRP**  C) LSP  D) DIP

**Q8.** Injecting a `Database` interface instead of a concrete `MySqlDb` class demonstrates:
A) ISP  B) LSP  C) **DIP**  D) SRP

**Q9.** The GoF Design Patterns book was authored by:
A) Robert Martin and Martin Fowler  B) **Gamma, Helm, Johnson, and Vlissides**  C) Kent Beck alone  D) Joshua Bloch

**Q10.** SOLID principles guide "how to design classes," while design patterns guide:
A) How to write comments  B) **How to solve recurring design problems**  C) How to name variables  D) How to configure servers

**Q11.** Which pattern(s) reinforce SRP?
A) Strategy, Decorator  B) **Factory, Builder**  C) Template Method  D) Adapter

**Q12.** Which pattern(s) reinforce OCP?
A) **Strategy, Decorator**  B) Factory, Builder  C) Template Method  D) Adapter

**Q13.** Which pattern reinforces LSP?
A) Adapter  B) Factory  C) **Template Method**  D) Strategy

**Q14.** Which pattern reinforces ISP?
A) Builder  B) **Adapter**  C) Decorator  D) Observer

**Q15.** How many Creational patterns are typically listed in this course's material?
A) 3  B) **5**  C) 7  D) 11

**Q16.** Which is a Creational pattern?
A) Adapter  B) Observer  C) **Singleton**  D) Facade

**Q17.** Which pattern ensures only one instance of a class exists, e.g. Logger or Config?
A) Factory Method  B) **Singleton**  C) Builder  D) Prototype

**Q18.** Which pattern is "a factory of factories"?
A) Factory Method  B) **Abstract Factory**  C) Builder  D) Prototype

**Q19.** Which pattern builds complex objects step by step?
A) Prototype  B) Factory Method  C) **Builder**  D) Singleton

**Q20.** Which pattern clones existing objects?
A) Builder  B) **Prototype**  C) Factory Method  D) Singleton

**Q21.** Which is a Structural pattern?
A) Observer  B) Strategy  C) **Adapter**  D) Command

**Q22.** Which Structural pattern separates abstraction from implementation?
A) Adapter  B) **Bridge**  C) Composite  D) Facade

**Q23.** Which Structural pattern represents objects in a tree structure?
A) Bridge  B) **Composite**  C) Flyweight  D) Proxy

**Q24.** Which Structural pattern adds functionality to an object dynamically?
A) Adapter  B) Facade  C) **Decorator**  D) Proxy

**Q25.** Which Structural pattern simplifies access to a complex subsystem?
A) Bridge  B) Composite  C) **Facade**  D) Flyweight

**Q26.** Which Structural pattern shares objects to save memory?
A) Proxy  B) **Flyweight**  C) Bridge  D) Adapter

**Q27.** Which Structural pattern controls access to another object?
A) Facade  B) Flyweight  C) **Proxy**  D) Composite

**Q28.** Which is a Behavioral pattern?
A) Singleton  B) Facade  C) **Observer**  D) Builder

**Q29.** Which Behavioral pattern passes a request through a chain of handlers?
A) Command  B) **Chain of Responsibility**  C) Mediator  D) State

**Q30.** Which Behavioral pattern encapsulates a request as an object?
A) **Command**  B) Iterator  C) Memento  D) Visitor

**Q31.** Which Behavioral pattern stores and restores an object's state?
A) State  B) **Memento**  C) Mediator  D) Observer

**Q32.** Which Behavioral pattern provides one-to-many notifications?
A) Mediator  B) **Observer**  C) State  D) Visitor

**Q33.** Which Behavioral pattern changes an algorithm at runtime?
A) State  B) Template Method  C) **Strategy**  D) Visitor

**Q34.** Which Behavioral pattern defines the skeleton of an algorithm, deferring some steps to subclasses?
A) Strategy  B) **Template Method**  C) State  D) Command

**Q35.** Which Behavioral pattern centralizes communication between objects?
A) Observer  B) **Mediator**  C) Command  D) Iterator

**Q36.** Which Behavioral pattern allows adding operations without modifying existing classes?
A) State  B) Strategy  C) **Visitor**  D) Command

---
## Day 12 — DBMS, MySQL & JDBC

**Q1.** DBMS stands for:
A) Data Backup Management System  B) **Database Management System**  C) Data Basic Model System  D) Database Model Server

**Q2.** RDBMS data is stored in the form of:
A) Documents  B) **Rows and columns**  C) Key-value pairs  D) Graph nodes

**Q3.** Which is NOT a listed RDBMS benefit?
A) Reduced data redundancy  B) Data integrity  C) **Increased redundancy**  D) Multi-user support

**Q4.** MySQL is developed by:
A) Microsoft  B) **Oracle**  C) IBM  D) Google

**Q5.** JDBC stands for:
A) Java Data Base Connector  B) **Java Database Connectivity**  C) Java Data Binding Class  D) Java Direct Base Class

**Q6.** The correct JDBC architecture flow is:
A) App → Database → JDBC API  B) **App → JDBC API → JDBC Driver → Database**  C) Database → JDBC Driver → App  D) JDBC Driver → App → Database

**Q7.** Which class is used to establish a connection with the database?
A) Connection  B) **DriverManager**  C) Statement  D) ResultSet

**Q8.** Which interface represents an active database connection?
A) **Connection**  B) DriverManager  C) Statement  D) SQLException

**Q9.** Which interface is used for parameterized (safer) SQL queries?
A) Statement  B) **PreparedStatement**  C) CallableStatement  D) ResultSet

**Q10.** Which interface is used to call stored procedures?
A) Statement  B) PreparedStatement  C) **CallableStatement**  D) ResultSet

**Q11.** Which interface stores data returned from a SELECT query?
A) Statement  B) Connection  C) **ResultSet**  D) SQLException

**Q12.** Which JDBC driver type is NOT available in modern Java (8+)?
A) **Type 1 (JDBC-ODBC Bridge)**  B) Type 2  C) Type 3  D) Type 4

**Q13.** Which JDBC driver type is fastest and most commonly used?
A) Type 1  B) Type 2  C) Type 3  D) **Type 4 (Thin Driver)**

**Q14.** Which JDBC driver type requires a middleware server?
A) Type 1  B) Type 2  C) **Type 3**  D) Type 4

**Q15.** Which method executes a SELECT and returns a ResultSet?
A) executeUpdate()  B) execute()  C) **executeQuery()**  D) select()

**Q16.** Which method is used for INSERT/UPDATE/DELETE and returns the number of affected rows?
A) executeQuery()  B) **executeUpdate()**  C) execute()  D) modify()

**Q17.** Which of these is the correct step order for JDBC?
A) Execute → Connect → Load driver  B) **Import packages → Load driver → Connect → Create statement → Execute → Process results**  C) Process results → Execute → Connect  D) Load driver → Execute → Import packages

**Q18.** In the recommended project package structure, where do custom exceptions live?
A) `bean`  B) `dao`  C) **`exceptions`**  D) `utility`

**Q19.** In the recommended project package structure, where does JPA entity-to-table mapping live?
A) `bean`  B) **`entity`**  C) `service`  D) `uitester`

---
## Day 13 — JPA & Hibernate CRUD

**Q1.** In the CRUD project example, what's the key difference between the `bean` and `entity` classes?
A) They're identical  B) **The bean is a plain POJO; the entity carries JPA annotations for table mapping**  C) The bean has annotations, the entity doesn't  D) Beans are only for testing

**Q2.** Which annotation marks a class as JPA-managed?
A) @Table  B) **@Entity**  C) @Bean  D) @Component

**Q3.** Which annotation maps a class to a specific database table?
A) @Entity  B) **@Table(name="...")**  C) @Column  D) @Id

**Q4.** Which annotation marks the primary key field?
A) @Key  B) **@Id**  C) @Primary  D) @Unique

**Q5.** Every `@Entity` class must have:
A) A private constructor only  B) **A no-arg constructor**  C) At least 3 fields  D) A `main` method

**Q6.** Which `EntityManager` method inserts a new entity?
A) merge()  B) **persist()**  C) find()  D) save()

**Q7.** Which `EntityManager` method fetches an entity by primary key?
A) **find()**  B) get()  C) locate()  D) fetch()

**Q8.** Which `EntityManager` method is used to update an existing entity?
A) update()  B) **merge()**  C) persist()  D) refresh()

**Q9.** Which `EntityManager` method deletes an entity (requires a managed instance)?
A) delete()  B) drop()  C) **remove()**  D) erase()

**Q10.** `createQuery("FROM EmployeeEntity")` uses:
A) Native SQL  B) **JPQL, which queries entity names not table names**  C) XML config  D) A stored procedure

**Q11.** Where is JPA/Hibernate configuration typically defined?
A) `web.xml`  B) **`persistence.xml`**  C) `pom.xml`  D) `application.yml` only

**Q12.** `Persistence.createEntityManagerFactory("unit1")` looks up:
A) A database table  B) **The persistence unit named "unit1" in persistence.xml**  C) A Spring bean  D) An XML schema file

**Q13.** Which `hibernate.hbm2ddl.auto` value only checks the schema matches entities, without changing it?
A) update  B) create  C) **validate**  D) none

**Q14.** Which `hibernate.hbm2ddl.auto` value updates the schema but keeps existing data?
A) create  B) **update**  C) create-drop  D) validate

**Q15.** Which `hibernate.hbm2ddl.auto` value drops the schema both on startup AND shutdown?
A) update  B) create  C) **create-drop**  D) validate

**Q16.** In the service layer pattern used here, what does `EmployeeServiceImpl` primarily do?
A) Directly execute raw SQL  B) **Delegate calls to the DAO layer**  C) Replace the DAO entirely  D) Handle only exceptions

---
## Day 14 — JDBC Drawbacks & Introduction to JPA

**Q1.** Which of these is a genuine drawback of plain JDBC?
A) Automatic caching  B) **Boilerplate code**  C) Built-in relationship management  D) No database dependency

**Q2.** JPA is described as:
A) A concrete implementation  B) **A specification (set of rules)**  C) A database engine  D) A build tool

**Q3.** JPA implementations are also called:
A) Drivers  B) **Providers**  C) Connectors  D) Adapters

**Q4.** Which of these is a JPA provider?
A) MySQL  B) **Hibernate**  C) Maven  D) Tomcat

**Q5.** ORM stands for:
A) Object Relational Model only  B) **Object Relational Mapping**  C) Ordered Record Mapping  D) Object Reference Manager

**Q6.** Which JPA benefit directly addresses JDBC's manual object mapping problem?
A) Database dependency  B) **Automatic mapping**  C) More boilerplate  D) No caching

**Q7.** `@GeneratedValue(strategy = GenerationType.IDENTITY/AUTO/SEQUENCE/TABLE)` is used to:
A) Set a fixed ID manually  B) **Auto-generate the primary key**  C) Delete an entity  D) Map a table name

**Q8.** `@Transient` is used to:
A) Mark the primary key  B) **Exclude a field from persistence entirely**  C) Map a relationship  D) Enable caching

**Q9.** `@Temporal(TemporalType.DATE)` is used with which Java type?
A) String  B) **Date**  C) Integer  D) Boolean

**Q10.** In the entity lifecycle, a brand-new object created with `new` but not yet persisted is in which state?
A) Managed  B) **Transient (New)**  C) Detached  D) Removed

**Q11.** After calling `em.persist(entity)`, the entity moves to which state?
A) Transient  B) **Managed**  C) Detached  D) Removed

**Q12.** After the persistence context closes, a previously managed entity becomes:
A) Removed  B) Transient  C) **Detached**  D) Still managed

**Q13.** `EntityManagerFactory` is created:
A) Once per request  B) **Once per application**  C) Once per entity  D) Never — it's static only

**Q14.** `EntityManager` is:
A) Heavyweight and thread-safe  B) **Lightweight and NOT thread-safe**  C) A singleton across the whole app  D) Only used for reads

---
## Day 15 — JPA Relationships

**Q1.** How many main relationship types are covered?
A) 2  B) 3  C) **4**  D) 6

**Q2.** Cascade means:
A) Deleting all data on every save  B) **A parent operation automatically applied to the child**  C) Disabling relationships  D) Only applies to reads

**Q3.** Which CascadeType propagates a save operation to children?
A) MERGE  B) **PERSIST**  C) REMOVE  D) DETACH

**Q4.** Which CascadeType propagates all operations?
A) PERSIST  B) MERGE  C) **ALL**  D) REFRESH

**Q5.** In a unidirectional relationship:
A) Both entities reference each other  B) **Only one entity knows about the other**  C) Neither entity has a reference  D) It's always many-to-many

**Q6.** In a bidirectional relationship:
A) Only one side has a reference  B) **Both entities know about each other**  C) No foreign key is needed  D) It's not supported in JPA

**Q7.** `@JoinColumn` is used to:
A) Create a join table  B) **Specify the foreign key column, usually on the owning side**  C) Mark a field transient  D) Define cascade behavior

**Q8.** In `@OneToMany(mappedBy = "department")`, `mappedBy` indicates:
A) This is the owning side  B) **This is the inverse (non-owning) side**  C) A cascade setting  D) A join table name

**Q9.** In a One-to-Many/Many-to-One relationship, which side typically owns the foreign key?
A) The "One" side  B) **The "Many" side**  C) Neither side  D) Both sides equally

**Q10.** A Many-to-Many relationship in JPA requires:
A) A single shared foreign key  B) **A join table with `@JoinTable`**  C) No mapping at all  D) Two separate `@OneToMany`s

**Q11.** In `@JoinTable`, `joinColumns` refers to:
A) The other entity's foreign key  B) **This entity's foreign key**  C) The primary key of the join table  D) Nothing specific

**Q12.** In `@JoinTable`, `inverseJoinColumns` refers to:
A) This entity's foreign key  B) **The other (related) entity's foreign key**  C) A cascade rule  D) A column type

**Q13.** In `Person`/`Passport` one-to-one example, which entity holds the `@JoinColumn`?
A) Passport  B) **Person**  C) Both  D) Neither

**Q14.** `hibernate.dialect` is set to tell Hibernate:
A) Which logging level to use  B) **Which SQL flavor to generate for the target database**  C) Which entity to load first  D) The connection pool size

**Q15.** `hibernate.format_sql=true` does what?
A) Encrypts SQL  B) **Pretty-prints the generated SQL in logs**  C) Validates SQL syntax  D) Disables SQL logging entirely

---
## Day 16 — Introduction to Maven

**Q1.** Maven is best described as:
A) A testing framework  B) **A build automation and project management tool**  C) A database  D) An IDE

**Q2.** Maven's philosophy is described as:
A) Configuration over Convention  B) **Convention over Configuration**  C) No standard structure  D) Manual builds only

**Q3.** Which is NOT one of Maven's dependency sources?
A) Local Repository  B) Central Repository  C) Remote Repository  D) **Personal Repository**

**Q4.** POM stands for:
A) **Project Object Model**  B) Package Object Model  C) Project Order Management  D) Plugin Object Model

**Q5.** Which POM type is provided by Maven itself and inherited by all projects?
A) Simple POM  B) Parent POM  C) Child POM  D) **Super POM**

**Q6.** Which POM type shares common configuration across multiple projects?
A) Simple POM  B) **Parent POM**  C) Child POM  D) Super POM

**Q7.** A Child POM:
A) Overrides the Super POM only  B) **Inherits settings from a Parent POM**  C) Cannot have dependencies  D) Replaces the artifactId

**Q8.** `<groupId>` in a pom.xml represents:
A) The project name  B) **A unique organization/company identifier**  C) The Java version  D) The packaging type

**Q9.** `<artifactId>` in a pom.xml represents:
A) The organization ID  B) **The project name**  C) The version number  D) The plugin list

**Q10.** Which packaging values are valid for `<packaging>`?
A) Only jar  B) **jar, war, ear, pom**  C) Only war  D) exe, dll

**Q11.** Which Maven archetype creates a simple Java application?
A) Web Application Archetype  B) **Quickstart Archetype**  C) Site Archetype  D) Enterprise Archetype

**Q12.** Which Maven archetype is used for documentation projects?
A) Quickstart  B) Web Application  C) **Site Archetype**  D) None of these

**Q13.** How many built-in Maven lifecycles are there?
A) 2  B) **3**  C) 5  D) 7

**Q14.** Which Maven lifecycle removes previous build files?
A) Default  B) Site  C) **Clean**  D) Build

**Q15.** What is the correct order of phases in the Default/Build lifecycle?
A) Package → Compile → Test → Install  B) **Validate → Compile → Test → Package → Install → Deploy**  C) Deploy → Install → Package  D) Test → Compile → Validate

**Q16.** Which command removes previous build artifacts?
A) mvn package  B) mvn test  C) **mvn clean**  D) mvn compile

**Q17.** Which command produces a distributable format like a JAR?
A) mvn compile  B) mvn test  C) **mvn package**  D) mvn validate

**Q18.** In the example pom.xml, which plugin sets the main class for an executable JAR?
A) maven-compiler-plugin  B) **maven-jar-plugin**  C) maven-surefire-report-plugin  D) maven-project-info-reports-plugin

**Q19.** `maven-surefire-report-plugin` is used to:
A) Compile code  B) **Generate an HTML report from test results**  C) Package a WAR  D) Manage dependencies

---
## Day 17 — Spring Annotation-Based Configuration

**Q1.** Spring's annotation-based configuration approach was introduced in version:
A) 2.0  B) **2.5**  C) 3.0  D) 4.0

**Q2.** If both XML and annotation-based configuration are used for the same bean, which wins?
A) Annotation always wins  B) **XML configuration overrides annotation-based injection**  C) It causes a runtime error always  D) Whichever loads first

**Q3.** Annotations generally do NOT work with:
A) Instance fields  B) Instance methods  C) **Static fields and methods**  D) Constructors

**Q4.** Which annotations belong to JSR 250?
A) @Inject, @Named  B) **@Resource, @PreDestroy, @PostConstruct**  C) @Autowired, @Qualifier  D) @Component, @Service

**Q5.** Which annotations belong to JSR 330?
A) @Resource, @PostConstruct  B) **@Inject, @Named, @Singleton**  C) @Autowired only  D) @Controller, @Repository

**Q6.** Which XML tag enables JSR-250/330 style annotations?
A) `<context:component-scan/>`  B) **`<context:annotation-config/>`**  C) `<context:enable/>`  D) `<bean:annotation/>`

**Q7.** Stereotype annotations are used to:
A) Format code  B) **Mark classes for detection during component scanning**  C) Handle exceptions  D) Configure the database

**Q8.** Which stereotype annotation marks the DAO layer?
A) @Service  B) **@Repository**  C) @Controller  D) @Component

**Q9.** Which stereotype annotation marks the service layer?
A) @Repository  B) **@Service**  C) @Controller  D) @RestController

**Q10.** Which stereotype annotation marks a Java-based configuration class?
A) @Component  B) @Service  C) **@Configuration**  D) @Bean

**Q11.** `<context:component-scan base-package="com.example"/>` already includes the functionality of:
A) @Autowired only  B) **`<context:annotation-config/>`**  C) @Value  D) @Profile

**Q12.** `@Value` can be used with:
A) Constructors and getters  B) **Setters and fields**  C) Static fields  D) Interfaces only

**Q13.** In SpEL, `${property}` represents:
A) A dynamic runtime expression  B) **A static value read from a properties file**  C) A method call  D) A bean reference

**Q14.** In SpEL, `#{expression}` represents:
A) A static properties value  B) **A dynamic expression evaluated at runtime**  C) A comment  D) An import statement

**Q15.** In SpEL, how do you reference a bean's method?
A) `${beanName.methodName}`  B) **`#{beanName.methodName()}`**  C) `@beanName.methodName()`  D) `beanName->methodName()`

**Q16.** `@Autowired` can be applied to:
A) Only fields  B) Only constructors  C) **Field, setter, constructor, or arbitrary method**  D) Only static methods

**Q17.** By default, `@Autowired` dependencies are:
A) Optional  B) **Mandatory (`required=true`)**  C) Ignored if missing  D) Only used with XML

**Q18.** `@Autowired(required=false)` can be used with:
A) Constructors only  B) **Field and setter**  C) Static methods  D) Interfaces only

**Q19.** `@Autowired` with a constructor is:
A) Optional by default  B) **Mandatory by default, and can't be made optional**  C) Never allowed  D) Only for static constructors

**Q20.** `@Autowired` injects dependencies:
A) By name only  B) **By type, by default**  C) Randomly  D) Only via XML

**Q21.** `@Qualifier` is used to:
A) Mark a bean as a singleton  B) **Resolve ambiguity when multiple beans of the same type exist**  C) Set a default value  D) Enable component scanning

**Q22.** `@Qualifier` can be applied at which levels?
A) Field only  B) **Field, method, method parameter, constructor, class**  C) Only class level  D) Only constructor

**Q23.** `@Profile` was introduced in Spring version:
A) 2.5  B) 3.0  C) **3.1**  D) 4.0

**Q24.** `@Profile` is applied at:
A) Method level  B) **Class level**  C) Field level  D) Package level

**Q25.** What is the priority order for activating a Spring profile?
A) application.properties > Environment Variable > JVM System property  B) **JVM System property > Environment Variable > application.properties**  C) All are equal priority  D) Environment Variable always wins

**Q26.** Which bean lifecycle annotation runs cleanup logic before a bean is destroyed?
A) @PostConstruct  B) **@PreDestroy**  C) @Init  D) @Before

**Q27.** In the Spring bean lifecycle, which step comes right after "Create Bean Instance"?
A) Destroy  B) **Inject (Dependency Injection)**  C) After Init  D) Load Bean Definition

**Q28.** `BeanPostProcessor (After Initialization)` is typically responsible for:
A) Loading XML  B) **Proxy creation, AOP, and transactions**  C) Destroying beans  D) Compiling code
