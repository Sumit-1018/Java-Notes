# Day 32 - Distributed Tracing & Swagger API Documentation
*Tue, 11 Aug 2026*

## Distributed Tracing

A single request often travels through **multiple services**:

```
client ---> order service + payment service + inventory service + notification service
```

Tracking that request's journey across all these services is hard — **distributed tracing** solves this problem.

## Need for Spring Cloud Sleuth

Sleuth automatically adds IDs to every request.

**Spring Cloud Sleuth** is a distributed tracing library that:
- Generates **Trace IDs** and **Span IDs**
- Adds them automatically to logs
- Propagates tracing information between microservices
- Integrates with **Zipkin** for visualization

### Core Terminology

| Term | Meaning |
|---|---|
| **Trace** | The complete journey of one request, end to end |
| **Span** | A single operation within a trace (e.g. one service call) |
| **Trace ID** | A unique ID for the entire request |
| **Span ID** | A unique ID for each individual service call within that request |

## Zipkin

An **open-source distributed tracing system** — it collects tracing information from Sleuth and displays it in a Web UI.

### Dependencies

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-sleuth-zipkin</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-sleuth</artifactId>
</dependency>
```

---
## API Documentation

### Why Documentation Matters

- APIs are easy to understand
- Enables testing APIs directly from the docs
- Request and response formats are clearly known
- Improves collaboration between backend and frontend teams

## Swagger

An **open-source framework** for generating interactive API documentation — automatically documents REST APIs.

### Dependencies

```xml
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-boot-starter</artifactId>
    <version>3.0.0</version>
</dependency>

<!-- Swagger UI Dependencies -->
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger-ui</artifactId>
    <version>3.0.0</version>
</dependency>
```

### Swagger Configuration Class

```java
package com.accenture.lkm.swagger.conf;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import springfox.documentation.builders.ApiInfoBuilder;
import springfox.documentation.builders.PathSelectors;
import springfox.documentation.builders.RequestHandlerSelectors;
import springfox.documentation.service.ApiInfo;
import springfox.documentation.service.Contact;
import springfox.documentation.spi.DocumentationType;
import springfox.documentation.spring.web.plugins.Docket;
import springfox.documentation.swagger2.annotations.EnableSwagger2;

@Configuration
@EnableSwagger2
public class SwaggerConfig {

    @Bean
    public Docket api() {
        return new Docket(DocumentationType.SWAGGER_2).select()
                .apis(RequestHandlerSelectors.any())
                .paths(PathSelectors.any())
                .build().apiInfo(apiInfo());
    }

    // custom API info
    private ApiInfo apiInfo() {
        return new ApiInfoBuilder()
                .title("Spring REST Sample with Swagger")
                .description("Spring REST Sample with Swagger")
                .termsOfServiceUrl("http://www-03.ibm.com/software/sla/sladb.nsf/sla/bm?Open")
                .contact(new Contact("LKM", "LKM", "LKM@123"))
                .license("LKM License")
                .licenseUrl("LKM.com")
                .version("2.0")
                .build();
    }
}
```

### How It Works

- Swagger 2 is enabled via the `@EnableSwagger2` annotation
- The `Docket` bean's `select()` method returns an `ApiSelectorBuilder`, which controls which endpoints Swagger exposes
- `RequestHandlerSelectors` and `PathSelectors` configure predicates for which request handlers get documented
- Using `.any()` for both makes documentation for your **entire API** available through Swagger
- This configuration alone is enough to integrate Swagger 2 into an existing Spring Boot project

> Once configured, Swagger UI is typically available at `/swagger-ui.html`, giving a live, testable interface for every documented endpoint.
