# Day 24 - Domain-Driven Design & Spring Batch
*Thu, 30 Jul 2026*

## Domain-Driven Design (DDD)

A software development approach that focuses on understanding the **business domain** and aligning software design with real-world business requirements.

### Goals

- Handle complex business problems effectively
- Improve communication between developers and domain experts
- Create software models that closely represent business processes
- Increase maintainability and scalability

### Core Concepts

1. **Domain** — the subject area the software is built for (e.g. banking, e-commerce)
2. **Domain Model** — the conceptual model representing the domain's entities, rules, and behavior
3. **Ubiquitous Language** — a shared vocabulary used by both developers and domain experts, reflected directly in code
4. **Domain Experts** — the people with deep knowledge of the business domain, who collaborate with developers to shape the model

---
## Strategic Design Concepts

Focuses on the **big picture** — how different parts of a large system relate to each other.

1. **Bounded Context** — a explicit boundary within which a particular domain model applies consistently (the same term can mean different things in different bounded contexts)
2. **Context Mapping** — defines relationships between bounded contexts
   - Common patterns: **Customer-Supplier**, and others (Shared Kernel, Anti-Corruption Layer, etc.)
3. **A Shared Language** — the Ubiquitous Language, applied consistently within each bounded context

## Tactical Design Patterns

Focuses on **implementing** the domain model itself, rather than the boundaries between contexts (that's strategic design's job).

### Layer Responsibilities

| Layer | Responsibility |
|---|---|
| **Domain Layer** | Entities, Value Objects, Aggregates, Domain Services, Repository interfaces |
| **Application Layer** | Orchestrates use cases — coordinates domain objects to fulfill a business operation |
| **Infrastructure Layer** | Technical concerns — database access, messaging, external APIs |
| **Interface Layer** | Entry points — REST controllers, UI, CLI |

```java
// Domain Layer — Entity
public class Order {
    private OrderId id;
    private List<OrderLine> lines;

    public void addLine(OrderLine line) {
        // business rule enforcement lives here, in the domain model
        lines.add(line);
    }
}

// Domain Layer — Repository interface (implementation lives in Infrastructure)
public interface OrderRepository {
    Order findById(OrderId id);
    void save(Order order);
}
```

---
## Types of Data Processing

| Type | Description |
|---|---|
| **OLTP** (Online Transaction Processing) | Real-time transaction processing — e.g. placing an order |
| **OLAP** (Online Analytical Processing) | Analytical processing on historical data — e.g. sales trend reports |
| **Batch Processing** | Processes huge amounts of data together, at scheduled intervals |

---
## Spring Batch

A framework for implementing **batch processing**.

### Key Features

1. **Chunk Processing** — processes data in fixed-size chunks rather than one record at a time
2. **Restartability** — a failed job can resume from where it left off
3. **Listener Support** — hooks into job/step lifecycle events
4. **Error Handling** — built-in skip/retry logic for faulty records

### Spring Batch Architecture

| Layer | Contains |
|---|---|
| **Application Layer** | Jobs, Steps, Business Logic |
| **Batch Core** | `JobLauncher`, `Job`, `Step`, the execution engine |
| **Infrastructure** | Readers, Writers, Transaction Manager, Job Repository |

### Spring Batch Components

| Component | Role |
|---|---|
| **Job** | Container for all the work — the top-level unit |
| **Step** | A single, independent business activity within a Job |
| **ItemReader** | Extracts data (from a file, DB, etc.) |
| **ItemProcessor** | Transforms/validates the extracted data |
| **ItemWriter** | Stores the processed data |

### Step Flow

```
Read ---> Process ---> Write
```

```java
@Bean
public Step importStep(ItemReader<Employee> reader,
                        ItemProcessor<Employee, Employee> processor,
                        ItemWriter<Employee> writer,
                        StepBuilderFactory stepBuilderFactory) {
    return stepBuilderFactory.get("importStep")
            .<Employee, Employee>chunk(10)   // process 10 records per chunk
            .reader(reader)
            .processor(processor)
            .writer(writer)
            .build();
}

@Bean
public Job importJob(JobBuilderFactory jobBuilderFactory, Step importStep) {
    return jobBuilderFactory.get("importJob")
            .start(importStep)
            .build();
}
```
