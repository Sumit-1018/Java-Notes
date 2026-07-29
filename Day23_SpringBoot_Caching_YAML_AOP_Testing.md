# Day 23 - Spring Boot Caching, YAML, RestTemplate, AOP & Testing
*Wed, 29 Jul 2026*

## Spring Boot Caching

Used to store **frequently accessed data in memory**, avoiding repeated expensive calls (e.g. to the database).

### Setup

1. `@EnableCaching` — on the primary configuration/application class
2. On the service class:

| Annotation | Purpose |
|---|---|
| `@Cacheable` | Caches the method's return value |
| `@CachePut` | Updates the cache without skipping method execution |
| `@CacheEvict` | Removes entries from the cache |
| `@Caching` | Combines multiple cache annotations on one method |

```java
@Service
public class ProductService {

    @Cacheable(value = "products", key = "#id")
    public Product getProduct(Long id) {
        return repository.findById(id).orElse(null);
    }
}
```
A cache table is conceptually created with 2 columns: **key** and **value**.

### Cache Implementations

**1. `ConcurrentMapCacheManager`**
- Spring's simplest cache implementation
- Adds no external dependency
- Internally uses `ConcurrentHashMap`

```java
@Bean
public CacheManager cacheManager() {
    return new ConcurrentMapCacheManager("products");
}
```

**2. Ehcache**
- In-memory cache
- Dependency: `org.ehcache:ehcache`

**3. Redis Cache**
- An in-memory data store that supports **distributed** caching
- Good for microservices and clustered applications
- High-performance caching
- Dependency: `spring-boot-starter-data-redis`

---
## YAML (`application.yml`)

A **human-readable** format used to store configuration data.

- `SnakeYAML` is available by default in Spring Boot
- Works with `@ConfigurationProperties`
- Structured as key-value pairs and hierarchies via **indentation**

### Rules

- Indentation matters
- **Do not** use tabs — spaces only
- Keys are followed by a colon (`:`)
- Lists use a dash (`-`)

```yaml
server:
  port: 8090

spring:
  datasource:
    url: jdbc:mysql://localhost:3306/testdb
    username: root
    password: root
```

Profile-specific YAML files follow the same naming pattern as properties files, e.g. `application-Prod_Log.yml`.

---
## Runners

Run code **immediately after** the Spring application context has loaded — useful for startup tasks (seeding data, sanity checks).

| Interface | Method Signature |
|---|---|
| `ApplicationRunner` | `void run(ApplicationArguments args) throws Exception` |
| `CommandLineRunner` | `void run(String... args) throws Exception` |

```java
@Component
@Order(1)
public class StartupRunner implements CommandLineRunner {
    @Override
    public void run(String... args) throws Exception {
        System.out.println("Application started — running startup task");
    }
}
```
`@Order()` controls execution order when multiple runners are defined.

---
## Packaging as WAR

By default, Spring Boot packages as an executable **JAR** with an embedded server. To deploy to an **external** servlet container (like a standalone Tomcat) instead:

1. Provide an implementation of `SpringBootServletInitializer`
2. Override `configure()`
3. Change packaging to `war` in `pom.xml`
4. Mark the embedded-server dependency as `<scope>provided</scope>` (so it doesn't conflict with the external container)

```java
public class ServletInitializer extends SpringBootServletInitializer {
    @Override
    protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
        return application.sources(MyApp.class);
    }
}
```

Build command: `mvn package`

---
## `RestTemplate`

Used to establish the connection between REST components — i.e. call other REST APIs from Java code.

| Method | Purpose |
|---|---|
| `getForObject()` | Performs a GET request, returns the body as an object |
| `postForObject()` | Performs a POST request, returns the body as an object |
| `put()` | Performs a PUT request |
| `delete()` | Performs a DELETE request |
| `exchange()` | Generic — supports any HTTP method, headers, and full response access |

```java
RestTemplate restTemplate = new RestTemplate();

Employee emp = restTemplate.getForObject(
        "http://localhost:8080/api/employees/1", Employee.class);
```

### `ResponseErrorHandler`

Custom error handling for `RestTemplate` calls.

| Method | Purpose |
|---|---|
| `hasError()` | Checks whether the response indicates an error |
| `handleError()` | Defines what to do when an error is detected |

---
## AOP — Aspect-Oriented Programming

Used to separate **cross-cutting concerns** from business logic — concerns that would otherwise be scattered across many classes:

- Logging
- Security
- Transaction management
- Exception handling
- Performance monitoring

### Core Terminology

| Term | Meaning |
|---|---|
| `@Aspect` | Marks a class as containing cross-cutting logic |
| **Join Point** | A point in the program where an aspect can be applied (e.g. a method call) |
| **Pointcut** | An expression that selects which join points to intercept |
| **Advice** | The action taken by the aspect at a matched join point (before, after, around, etc.) |

```java
@Aspect
@Component
public class LoggingAspect {

    @Before("execution(* com.jfs.training.service.*.*(..))")
    public void logBefore() {
        System.out.println("Method execution starting...");
    }
}
```

---
## Testing

### Testing Layers

| Layer | Test Type | Tools |
|---|---|---|
| Service Layer | Unit testing | JUnit, Spring Test |
| Controller Layer | Integration testing | JUnit, Spring `MockMvc` |
| Controller Layer | Unit testing | JUnit, Spring `MockMvc`, Mockito |

### Service Layer — Unit Testing

- Dependency: `spring-boot-starter-test`
- `@ExtendWith(SpringExtension.class)`
- `@SpringBootTest(classes = Application.class)`
- Coverage reporting: `jacoco:report`

```java
@ExtendWith(SpringExtension.class)
@SpringBootTest(classes = Application.class)
class ProductServiceTest {

    @Autowired
    private ProductService productService;

    @Test
    void testGetProduct() {
        Product product = productService.getProduct(1L);
        assertNotNull(product);
    }
}
```

### Controller Layer — Integration Testing

1. Enable `WebApplicationContext` in the test case
2. Use `MockMvcBuilders` to create a `MockMvc` — a replica of the **actual** MVC, Controller, Service, and DAO layers
3. Use `MockHttpServletRequestBuilder` to construct a request
4. `MockMvc.perform()` executes the request, yielding `ResultActions` containing an `MvcResult`
5. Extract the actual response content and status from `MvcResult`, and compare against the expected content/status

```java
@SpringBootTest
@AutoConfigureMockMvc
class EmployeeControllerIntegrationTest {

    @Autowired
    private MockMvc mockMvc;

    @Test
    void testGetEmployee() throws Exception {
        mockMvc.perform(get("/api/employees/1"))
               .andExpect(status().isOk())
               .andExpect(jsonPath("$.name").value("John Doe"));
    }
}
```

### Controller Layer — Unit Testing

1. Declare Service Layer **mocks** and inject them into the controller
2. Use `MockMvcBuilders` to create a `MockMvc` — a replica of **just the controller** (no real service/DAO)
3. Use `MockHttpServletRequestBuilder` to construct a request
4. Define the mocking behavior (`when(...).thenReturn(...)`) for the mocked service
5. `MockMvc.perform()` executes the request, yielding `ResultActions` containing an `MvcResult`
6. Extract the actual response content/status from `MvcResult` and compare against expected values
7. Verify the controller correctly delegates the call to the mock

```java
@WebMvcTest(EmployeeController.class)
class EmployeeControllerUnitTest {

    @Autowired
    private MockMvc mockMvc;

    @MockBean
    private EmployeeService employeeService;

    @Test
    void testGetEmployee() throws Exception {
        Mockito.when(employeeService.findById(1L))
               .thenReturn(new Employee(1L, "John Doe"));

        mockMvc.perform(get("/api/employees/1"))
               .andExpect(status().isOk())
               .andExpect(jsonPath("$.name").value("John Doe"));

        Mockito.verify(employeeService).findById(1L);
    }
}
```
