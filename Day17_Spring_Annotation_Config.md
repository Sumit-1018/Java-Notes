# Day 17 - Spring Framework: Annotation-Based Configuration & DI
*Tue, 21 Jul 2026*

## Creating a Spring Application — Annotation-Based Approach

We can provide configuration info to a Spring app via annotations instead of the `<bean>` tag in XML.

- Introduced in **Spring 2.5**
- Instead of defining beans with `<bean>`, we define them with annotations directly on the class
- Configuration info to *detect* the annotations is still provided in an XML file — but the bean definitions themselves are no longer written there

> **Note:** XML configuration overrides annotation-based injection if both are used for the same bean — it's a matter of **priority**, not which runs first.

> Unlike XML configuration, annotations will **not** work with `static` fields and methods.

---
## 1. Spring Core Annotations

| Annotation | Purpose |
|---|---|
| `@Autowired` | Dependency injection |
| `@Qualifier` | Resolve ambiguity between multiple beans of the same type |
| `@Value` | Inject values |
| `@Required` *(deprecated)* | Marks a mandatory property |
| `@PostConstruct` *(JSR-250)* | Init method — runs after construction |
| `@PreDestroy` *(JSR-250)* | Destroy method — runs before bean removal |
| `@Resource` *(JSR-250)* | Dependency injection |
| `@Inject` *(JSR-330)* | Dependency injection |

| Spec | Annotations |
|---|---|
| **JSR 250** | `@Resource`, `@PreDestroy`, `@PostConstruct` |
| **JSR 330** | `@Inject`, `@Named`, `@Singleton` |

To enable these annotations, add to the XML config:
```xml
<context:annotation-config />
```

---
## 2. Stereotype Annotations

Used to mark classes so they're detected during **component scanning** by the Spring container. Every marked class is treated as a **Component** — after scanning, Spring creates and manages an instance of it as a Spring bean.

| Annotation | Purpose |
|---|---|
| `@Component` | Generic Spring bean |
| `@Service` | Service layer |
| `@Repository` | DAO layer |
| `@Controller` | Spring MVC controller |
| `@RestController` | REST controller |
| `@Configuration` | Java-based config class |

Enable with:
```xml
<context:component-scan base-package="com.example"/>
```

> **Note:** Annotations don't replace XML configuration — they just reduce how much XML you have to write.

> `<context:component-scan>` already includes everything `<context:annotation-config />` does — don't include both unnecessarily. If you want both features, just use `<context:component-scan base-package="com.example"/>`.

---
## 3. `@Value` Annotation

- Used with **setters and fields** inside a class only, to set a **default value**
- **Not** used with constructors, getter methods, or static fields/methods

**Use case:** external configuration support.

```properties
# application.properties
db.url=jdbc:mysql://localhost:3306/testdb
db.username=root
```

```java
@Value("${db.url}")
private String url;
```

---
## 4. SpEL — Spring Expression Language

Used with `@Value` to query, manipulate, and evaluate objects **at runtime**.

**Main uses:**
- Inject dynamic values
- Access bean properties and methods
- Apply conditional logic
- Work with collections
- Provide flexible configuration

### Syntax

| Syntax | Meaning |
|---|---|
| `#{expression}` | Dynamic — evaluated at runtime |
| `${property}` | Static — read from a properties file, not evaluated |

```java
@Value("${db.url}")                 // static value from properties file
private String dbUrl;

@Value("#{employee.employeeName}")  // dynamic value using SpEL
private String name;
```

### Referencing With SpEL

| Target | Syntax |
|---|---|
| Bean | `#{beanName}` |
| Bean field | `#{beanName.fieldName}` |
| Bean method | `#{beanName.methodName()}` |

```java
@Value("#{myAddress.addressLine1}")
private String line1;

@Value("#{myAddress.getAddressLine1().toUpperCase()}")
private String line1Upper;

@Value("#{!(numberBean.no == 999)}")   // false, if numberBean.no == 999
private boolean testNot;
```

---
## 5. `@Autowired` Annotation

Automatically injects a dependency into a dependent class.

Can be used with: **field**, **setter**, **constructor**, or an **arbitrary method**.

```java
// 1. Field injection
@Autowired
private Address address;   // eliminates the need for a setter method

// 2. Setter injection
@Autowired
public void setAddress(Address address) {
    this.address = address;
}

// 3. Constructor injection
@Autowired
public Employee(Address address) {
    this.address = address;
}
```

- `@Autowired` **won't** work with `static` fields/methods
- You *can* use a static variable with `@Autowired` on a non-static setter — but it's not recommended

### `required` Attribute

```java
@Autowired(required = false)   // makes the dependency optional
private Address address;
```

- Used with **field** and **setter** only
- By default, `@Autowired(required = true)` — the dependency is **mandatory**
- **Not** used with constructors — constructor injection with `@Autowired` is mandatory by default

---
## 6. `@Qualifier` Annotation

`@Autowired` injects by **type** by default. `@Qualifier` removes ambiguity when there's more than one bean of the same type.

Can be used on: field | method | method parameter | constructor | class.

```java
@Autowired
@Qualifier("myAddress1")
private Address address;   // injects the specific "myAddress1" bean

// or on a method parameter
@Autowired
public void setAddress(@Qualifier("myAddress") Address address) {
    this.address = address;
}
```

---
## 7. `@Profile` Annotation

Introduced in **Spring 3.1** — used to load selective classes based on the **active environment** (production, testing, development).

- Loads specific classes for a selective environment, ignores the rest
- Lets you switch configuration per environment **without changing code**
- Applied at the **class level**

```java
@Component("empObject")
@Profile("myProfile")
class Employee {
}
```

This registers `empObject` into the `ApplicationContext` **only if** `myProfile` is the active profile.

**Benefits:** loads only the beans required per environment — memory-efficient, improves performance, useful for bigger applications.

### Activating a Profile

**1. Via System property (in the main class):**
```java
System.setProperty("spring.profiles.active", "myProfile");
```

**2. Via environment variable (in Eclipse):**
```
Right-click project → Run As → Run Configuration → Environment tab
→ New → name = spring.profiles.active, value = myProfile
```

**3. Via `application.properties`** (Spring Boot only, covered later):
```properties
spring.profiles.active=prod
```
Spring then looks for `application-prod.properties`, containing all production config properties. Swap for `dev` or `test` as needed.

### Priority Order
```
JVM System property  >  Environment Variable  >  application.properties
```

---
## 8. Bean Life Cycle

### When Do We Need It?

- To perform tasks **before** initializing a bean (e.g. validation)
- To perform operations **after** a bean is created and initialized
- To run **clean-up code** before a bean is deleted

### Bean Life Cycle Steps

```
Load Bean Definition & Create Bean Instance
        │
        ▼
BeanFactoryPostProcessor  ──►  Modify Bean Definitions (Metadata)
        │
        ▼
Create  ──►  Create Bean Instance
        │
        ▼
Inject  ──►  Perform Dependency Injection
        │
        ▼
Aware  ──►  Provide Bean/Container Context Information
        │
        ▼
Before Init  ──►  BeanPostProcessor (Before Initialization)
        │
        ▼
Initialize  ──►  @PostConstruct / afterPropertiesSet() / initMethod()
        │
        ▼
After Init  ──►  BeanPostProcessor (After Initialization)
                  Proxy Creation, AOP, Transactions
        │
        ▼
   Bean Ready for Use
        │
        ▼
Destroy  ──►  @PreDestroy / destroy() / destroyMethod()
              Execute Cleanup Logic (Close DB Connections, Release Resources, Stop Threads)
```

```java
@Component
public class ConnectionPool {

    @PostConstruct
    public void init() {
        System.out.println("Opening DB connections...");
    }

    @PreDestroy
    public void cleanup() {
        System.out.println("Closing DB connections...");
    }
}
```
