# Day 8 - Java 11 Features
*Wed, 8 Jul 2026*

## 1. Java Version History

Since 2017, Java follows a **6-month release cycle** — March and September feature releases.

| Version | Release Date | LTS? |
|---|---|---|
| Java 8 | Mar 2014 | Yes |
| Java 9 | Sep 2017 | No |
| Java 10 | Mar 2018 | No |
| Java 11 | Sep 2018 | **Yes** |
| Java 12 | Mar 2019 | No |
| Java 13 | Sep 2019 | No |
| Java 14 | Mar 2020 | No |
| Java 15 | Sep 2020 | No |
| Java 16 | Mar 2021 | No |
| Java 17 | Sep 2021 | **Yes** |
| Java 18 | Mar 2022 | No |
| Java 19 | Sep 2022 | No |
| Java 20 | Mar 2023 | No |
| Java 21 | Sep 2023 | **Yes** |
| Java 22 | Mar 2024 | No |
| Java 23 | Sep 2024 | No |
| Java 24 | Mar 2025 | No |
| Java 25 | Sep 2025 | **Yes** |
| Java 26 | Mar 2026 | No |

**Notable milestones:** Java 5 (generics, annotations, enhanced for-loop), Java 8 (lambdas, streams, new Date/Time API), Java 9 (module system), Java 17 LTS (sealed classes, pattern matching), Java 21 LTS (virtual threads, record patterns), Java 25 LTS (baselined enterprise adoption).

## 2. JEP, JSR & JDEP

| Term | Full Form | Purpose |
|---|---|---|
| **JEP** | Java Enhancement Proposal | Describes a new feature, enhancement, or change for Java (e.g. JEP 323) |
| **JSR** | Java Specification Request | Defines official Java specifications — standardizes APIs so multiple vendors can implement the same spec (e.g. JSR 330) |
| **JDEP** | JDK Enhancement Proposal | Now replaced by JEP |

## 3. Java 11 — Key Features

### HTTP Client API (Standardized) — JEP 321
Allows **asynchronous** HTTP calls natively — no external library needed.

```java
HttpClient client = HttpClient.newHttpClient();
HttpRequest request = HttpRequest.newBuilder()
        .uri(URI.create("https://api.example.com/data"))
        .build();

client.sendAsync(request, HttpResponse.BodyHandlers.ofString())
      .thenApply(HttpResponse::body)
      .thenAccept(System.out::println);
```

### Local Variable Syntax for Lambda Parameters
```java
// Before
(x, y) -> x + y;

// Java 11 — using var
(var x, var y) -> x + y;
```

### New String Methods
```java
"  ".isBlank();      // true
"a\nb".lines();       // Stream<String>
"ab".repeat(3);        // "ababab"
"  hi  ".strip();      // "hi"
```

### `Files.readString()` / `Files.writeString()`
```java
String content = Files.readString(Path.of("data.txt"));
Files.writeString(Path.of("out.txt"), "Hello World");
```

### Running a Single Java File
```
java Demo.java
```
No separate compile step needed for quick scripts.

### Collection-to-Array
```java
List<String> list = List.of("a", "b", "c");
String[] arr = list.toArray(String[]::new);
```

### `Optional` Enhancements
New methods like `isEmpty()`, `ifPresentOrElse()`.

### Nest-Based Access Control
Nested classes can directly access each other's private members without synthetic bridge methods.

### Epsilon Garbage Collector — JEP 318
A "no-op" GC used for **performance testing** and **memory pressure testing** — it never actually reclaims memory.

### `Duration` (java.time)
Represents a time-based amount, useful for measuring elapsed time.
```java
Duration d = Duration.ofSeconds(90);
System.out.println(d.toMinutes()); // 1
```

### `Predicate.not()` — JEP 320-adjacent utility
```java
List<String> nonEmpty = list.stream()
        .filter(Predicate.not(String::isEmpty))
        .collect(Collectors.toList());
```
