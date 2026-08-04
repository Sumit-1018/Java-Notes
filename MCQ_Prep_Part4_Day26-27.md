# QuantumCrew — MCQ Assessment Prep (Comprehensive)
### Part 4 of 4 — Days 26 to 27

---
## Day 26 — Microservices Challenges & Spring Cloud

**Q1.** Which of these is NOT a listed challenge in Microservices architecture?
A) Data management  B) Distributed system issues  C) **Reduced operational overhead**  D) Version management

**Q2.** Which challenge specifically relates to services finding and calling each other correctly?
A) Version management  B) **Service Discovery and Load Balancing**  C) Testing difficulties  D) Deployment complexity

**Q3.** Spring Cloud is built:
A) Independently of Spring  B) **On top of the Spring ecosystem**  C) Only for monolithic apps  D) As a replacement for Spring Boot

**Q4.** Which Spring Cloud component provides Service Discovery?
A) Spring Cloud Config  B) **Eureka Server**  C) Spring Cloud Gateway  D) Resilience4j

**Q5.** Which Spring Cloud component provides Centralized Configuration Management?
A) Eureka Server  B) **Spring Cloud Config**  C) Spring Cloud Gateway  D) Spring Cloud Load Balancer

**Q6.** Which Spring Cloud component acts as the API Gateway?
A) Eureka Server  B) Spring Cloud Config  C) **Spring Cloud Gateway**  D) Resilience4j

**Q7.** Which Spring Cloud component provides fault tolerance and resilience?
A) Eureka Server  B) Spring Cloud Gateway  C) **Resilience4j**  D) Spring Cloud Config

**Q8.** Which of these is NOT a listed benefit of Spring Cloud?
A) Simplifies microservices development  B) Supports cloud-native design  C) **Requires no Spring Boot integration**  D) Ready-made components

**Q9.** Spring Cloud release trains are named using:
A) Version numbers only  B) **Alphabetical codenames (e.g. Angel, Brixton, Camden...)**  C) Random UUIDs  D) Company initials

**Q10.** Spring Cloud Netflix integrates components from:
A) Google  B) **Netflix OSS**  C) Amazon  D) Microsoft

**Q11.** Which legacy Netflix component has been replaced by Spring Cloud Load Balancer?
A) Eureka  B) **Ribbon**  C) Zuul  D) Feign

**Q12.** Which legacy Netflix component has been replaced by Resilience4j?
A) Eureka  B) Ribbon  C) **Hystrix**  D) Feign

**Q13.** Which legacy Netflix component has been replaced by Spring Cloud Gateway?
A) Eureka  B) Ribbon  C) Hystrix  D) **Zuul**

**Q14.** Which Netflix component is now known as OpenFeign?
A) Eureka  B) Ribbon  C) Hystrix  D) **Feign**

**Q15.** In the typical Spring Cloud request flow, what sits directly between the Client and the individual Services?
A) The database  B) **The API Gateway**  C) Resilience4j  D) The load balancer's UI

**Q16.** Eureka Server functions as a:
A) Message queue  B) **Service registry**  C) Load balancer only  D) Database

**Q17.** Which annotation enables a Spring Boot app to act as a Eureka Server?
A) @EnableEureka  B) **@EnableEurekaServer**  C) @EurekaServer  D) @ServiceRegistry

**Q18.** Which dependency is needed on a EUREKA SERVER project?
A) spring-cloud-starter-netflix-eureka-client  B) **spring-cloud-starter-netflix-eureka-server**  C) spring-cloud-starter-gateway  D) spring-cloud-starter-config

**Q19.** Which dependency is needed on a client service that wants to REGISTER with Eureka?
A) spring-cloud-starter-netflix-eureka-server  B) **spring-cloud-starter-netflix-eureka-client**  C) spring-cloud-starter-loadbalancer only  D) spring-boot-starter-actuator only

**Q20.** A Eureka "heartbeat" is:
A) A one-time registration call  B) **A periodic message indicating the client is alive and functioning**  C) A database backup  D) A load balancer health check only

**Q21.** Self-Preservation Mode in Eureka Server exists to:
A) Speed up service registration  B) **Prevent accidental removal of instances during network failures**  C) Disable all services temporarily  D) Encrypt service data

**Q22.** `eureka.server.enable-self-preservation=true` is set in:
A) Java code only  B) **Application configuration (e.g. application.properties)**  C) The database  D) The Eureka client only, never the server

**Q23.** A Circuit Breaker's main purpose is to:
A) Increase calls to a failing service  B) **Prevent repeated calls to a failing service**  C) Encrypt network traffic  D) Replace load balancers entirely

**Q24.** What are the three Circuit Breaker states, in typical order of transition under sustained failure?
A) Open → Closed → Half-Open  B) **Closed → Open → Half-Open**  C) Half-Open → Closed → Open  D) Open → Half-Open → Closed only

**Q25.** In which Circuit Breaker state are requests blocked immediately (fail fast)?
A) Closed  B) **Open**  C) Half-Open  D) None — requests always go through

**Q26.** In which Circuit Breaker state are a limited number of test requests allowed through to check recovery?
A) Closed  B) Open  C) **Half-Open**  D) Terminated

**Q27.** Which of these is NOT a listed Circuit Breaker benefit?
A) Prevents cascading failures  B) Improves application resilience  C) **Increases load on failing services**  D) Provides fallback responses when services are unavailable

**Q28.** Resilience4j is described as:
A) A heavyweight ORM tool  B) **A lightweight fault tolerance library**  C) A database driver  D) A testing framework

**Q29.** Resilience4j typically requires which additional starter dependency to function via method interception?
A) spring-boot-starter-web only  B) **spring-boot-starter-aop**  C) spring-boot-starter-data-jpa  D) spring-boot-starter-security

---
## Day 27 — Load Balancer, Actuator & REST CRUD

**Q1.** A Load Balancer's core job is to:
A) Store application data  B) **Distribute incoming traffic/requests across multiple servers or instances**  C) Compile source code  D) Generate documentation

**Q2.** Which of these is NOT a listed Load Balancer goal?
A) Availability  B) Scalability  C) Performance  D) **Code readability**

**Q3.** How many types of Load Balancers are listed?
A) 3  B) 4  C) **5**  D) 6

**Q4.** Which Load Balancer type operates at the Transport Layer?
A) Layer 7  B) **Layer 4**  C) Hardware only  D) Cloud only

**Q5.** Which Load Balancer type operates at the Application Layer?
A) **Layer 7**  B) Layer 4  C) Software only  D) Hardware only

**Q6.** Spring Cloud Load Balancer is described as a:
A) Server-side only library  B) **Client-side load balancing library**  C) Database connector  D) Testing tool

**Q7.** Spring Boot Actuator is primarily used for:
A) Compiling code  B) **Production-ready monitoring and management capabilities**  C) Writing unit tests  D) Generating UI components

**Q8.** Which Actuator endpoint shows the application's health status?
A) /actuator/env  B) **/actuator/health**  C) /actuator/beans  D) /actuator/mappings

**Q9.** Which Actuator endpoint lists environment properties?
A) /actuator/health  B) **/actuator/env**  C) /actuator/info  D) /actuator/caches

**Q10.** Which Actuator endpoint allows viewing/changing logging levels at runtime?
A) /actuator/metrics  B) /actuator/env  C) **/actuator/loggers**  D) /actuator/beans

**Q11.** Which Actuator endpoint lists all Spring beans in the application context?
A) /actuator/mappings  B) **/actuator/beans**  C) /actuator/info  D) /actuator/health

**Q12.** Which Actuator endpoint lists all `@RequestMapping` paths?
A) /actuator/beans  B) **/actuator/mappings**  C) /actuator/env  D) /actuator/metrics

**Q13.** Which dependency enables Spring Boot Actuator?
A) spring-boot-starter-web  B) **spring-boot-starter-actuator**  C) spring-boot-starter-aop  D) spring-boot-starter-data-jpa

**Q14.** `@RestController` automatically converts return values to:
A) Only plain text  B) **JSON or XML**  C) HTML forms only  D) Nothing — manual conversion required

**Q15.** In the `EmployeeController` example, which attribute defines what content type the endpoint ACCEPTS in the request body?
A) produces  B) **consumes**  C) accepts  D) requestType

**Q16.** In the `EmployeeController` example, which attribute defines what content type the endpoint RETURNS?
A) **produces**  B) consumes  C) responseType  D) accepts

**Q17.** In the `addEmployee` method, which HTTP status is returned on success?
A) 200 OK  B) **201 CREATED**  C) 204 NO CONTENT  D) 400 BAD REQUEST

**Q18.** In `getEmployeeDetailByEmployeeId`, what HTTP status is returned if the employee isn't found?
A) 200 OK  B) 500 INTERNAL_SERVER_ERROR  C) **404 NOT_FOUND**  D) 401 UNAUTHORIZED

**Q19.** In `updateEmployee`/`deleteEmployee`, what HTTP status is returned when the operation unexpectedly fails?
A) 404 NOT_FOUND  B) **500 INTERNAL_SERVER_ERROR**  C) 200 OK  D) 201 CREATED

**Q20.** `ResponseEntity<>(body, HttpStatus)` allows a controller method to return:
A) Only the body  B) **Both the response body and an explicit HTTP status code**  C) Only the status code  D) Neither — it's a marker interface

**Q21.** `@PathVariable("id")` is used in the example to:
A) Read a query string parameter  B) **Extract the `{id}` segment from the URL path**  C) Read the request body  D) Set a response header

**Q22.** `@RequestBody Employee employee` is used to:
A) Extract a URL segment  B) **Deserialize the incoming JSON request body into an `Employee` object**  C) Set the response content type  D) Query the database directly

**Q23.** In the `EmployeeEntity` example, `@GeneratedValue(strategy = GenerationType.AUTO)` means:
A) The ID must always be set manually  B) **Hibernate automatically picks the best ID generation strategy for the database**  C) No ID is generated at all  D) The ID is always a UUID

**Q24.** `BeanUtils.copyProperties(source, target)` is used to:
A) Delete an object's fields  B) **Copy matching field values from one object to another without writing each setter manually**  C) Compile Java beans  D) Validate bean properties

**Q25.** `BeanUtils` in the service layer imports come from which package?
A) java.util  B) **org.springframework.beans**  C) javax.persistence  D) org.springframework.stereotype

---
*End of Part 4. Combined with Parts 1–3, this now covers every topic from Day 1 through Day 27.*
