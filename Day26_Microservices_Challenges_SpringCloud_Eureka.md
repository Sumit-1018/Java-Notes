# Day 26 - Microservices Challenges & Spring Cloud
*Mon, 3 Aug 2026*

## Challenges in Microservices Architecture

Building on the Microservices advantages/disadvantages from Day 22, here are the specific challenges teams run into:

1. Server communication complexity
2. Data management
3. Distributed system issues
4. Monitoring and debugging
5. Deployment complexity
6. Security concerns
7. Testing difficulties
8. Version management
9. Operational overhead
10. Service discovery and load balancing

---
## Spring Cloud

Built **on top of** the Spring ecosystem — provides tools and solutions for common distributed-systems challenges: service discovery, configuration management, load balancing, fault tolerance, API gateways, and distributed tracing.

### Key Features

| Feature | Tool |
|---|---|
| Service Discovery | **Eureka Server** |
| Centralized Configuration Management | **Spring Cloud Config** |
| Load Balancing | **Spring Cloud Load Balancer** |
| API Gateway | **Spring Cloud Gateway** |
| Fault Tolerance and Resilience | **Resilience4j** |
| Distributed Tracing and Monitoring | (built-in tracing support) |

### Benefits

- Simplifies microservices development
- Improves scalability and reliability
- Supports cloud-native application design
- Ready-made components
- Integrates seamlessly with Spring Boot

### Spring Cloud Release Train Names

Spring Cloud versions ship under codenames (alphabetical), e.g.:
```
Angel, Brixton, Camden, Dalston, Edgware, Finchley, Greenwich, Hoxton...
```

---
## Spring Cloud Netflix

A sub-project of Spring Cloud that integrates several popular **Netflix OSS** components into Spring Boot applications.

| Netflix OSS Component | Modern Spring Cloud Equivalent |
|---|---|
| Eureka | Eureka (still used directly) |
| Ribbon | Spring Cloud Load Balancer |
| Hystrix | Resilience4j |
| Zuul | Spring Cloud Gateway |
| Feign | OpenFeign |

### Typical Request Flow

```
Client ---> API Gateway ---> Service A <---> Eureka Server <---> Service B (via Feign)
```

---
## Eureka Server

A **service registry** — maintains a registry of all available services and their locations, enabling efficient service discovery.

### Server Dependency

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
```

Enable it on the main application class:
```java
@EnableEurekaServer
@SpringBootApplication
public class EurekaServerApplication {
    public static void main(String[] args) {
        SpringApplication.run(EurekaServerApplication.class, args);
    }
}
```

### Client Dependencies (for services registering with Eureka)

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-bootstrap</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```

### Eureka Server Heartbeats

A **periodic message** sent by a Eureka client to indicate that it is alive and functioning. If heartbeats stop, the server eventually considers the instance down.

### Self-Preservation Mode

A safety mechanism in Eureka Server that prevents the **accidental removal** of service instances from the registry during network failures or temporary communication problems.

```properties
eureka.server.enable-self-preservation=true
```

---
## Circuit Breaker

A design pattern used in microservices/distributed systems to **prevent repeated calls to a failing service** — improves system stability and fault tolerance by stopping requests to a service experiencing failures.

### States

```
Closed State  →  Open State  →  Half-Open State
```

| State | Behavior |
|---|---|
| **Closed** | Requests flow normally; failures are counted |
| **Open** | Requests are blocked immediately (fail fast) once a failure threshold is hit |
| **Half-Open** | A limited number of test requests are allowed through to check if the service has recovered |

### Benefits

- Prevents cascading failures
- Improves application resilience
- Reduces unnecessary load on failing services
- Provides fallback responses when services are unavailable

---
## Resilience4j

A **lightweight fault tolerance library** — the modern replacement for Netflix Hystrix, used to implement Circuit Breakers, Retry, Rate Limiting, and Bulkheads.

```xml
<dependency>
    <groupId>io.github.resilience4j</groupId>
    <artifactId>resilience4j-spring-boot2</artifactId>
    <version>1.7.0</version>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-aop</artifactId>
</dependency>
```

> Resilience4j is built on **AOP** (see Day 23) — it wraps method calls with resilience logic (circuit breaking, retries) without touching the business logic itself.
