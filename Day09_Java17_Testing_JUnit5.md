# Day 9 - Java 17 Features, Unit Testing & JUnit 5
*Thu, 9 Jul 2026*

---
# Part A — Java 17 Features (LTS)

Builds on the JDEPS/JEP/JSR/JLS concepts introduced on Day 8:

| Term | Meaning |
|---|---|
| **JDEPS** | `jdeps` — a JDK command-line tool that analyzes class-level and package-level dependencies of your code |
| **JEP** | Java Enhancement Proposal — see Day 8 |
| **JSR** | Java Specification Request — see Day 8 |
| **JLS** | Java Language Specification — the formal, authoritative definition of the Java language's syntax and semantics |

### Key Java 17 Features

**Sealed Classes** — restrict which classes can extend/implement a type.
```java
public sealed interface Shape permits Circle, Square, Triangle {}

public final class Circle implements Shape { }
public final class Square implements Shape { }
public final class Triangle implements Shape { }
```

**Pattern Matching for `instanceof`**
```java
if (obj instanceof String s) {
    System.out.println(s.length()); // s already cast, no manual casting
}
```

**Enhanced `switch` (Pattern Matching Preview)**
```java
String description = switch (shape) {
    case Circle c -> "Circle with radius " + c.radius;
    case Square s -> "Square with side " + s.side;
    default -> "Unknown shape";
};
```

**Text Blocks** (finalized in Java 15, widely used from 17 onward)
```java
String json = """
    {
      "name": "Alice",
      "age": 30
    }
    """;
```

---
# Part B — Unit Testing & TDD

## Introduction to Unit Testing

Testing individual units (usually methods) of code in isolation to verify they behave as expected.

**Benefits:** catches bugs early, enables safe refactoring, documents expected behavior, speeds up long-term development.

## Test-Driven Development (TDD)

A development cycle where tests are written **before** the implementation:

```
1. Red    → write a failing test
2. Green  → write just enough code to pass
3. Refactor → clean up the code, tests stay green
```

---
# Part C — JUnit 5

## Assertions

```java
import static org.junit.jupiter.api.Assertions.*;

@Test
void additionTest() {
    assertEquals(5, 2 + 3);
    assertTrue(5 > 2);
    assertFalse(5 < 2);
    assertNotNull(new Object());
    assertThrows(ArithmeticException.class, () -> {
        int x = 10 / 0;
    });
}
```

## Assumptions

Skip a test unless a precondition holds — useful for environment-specific tests.

```java
import static org.junit.jupiter.api.Assumptions.*;

@Test
void onlyOnCI() {
    assumeTrue("CI".equals(System.getenv("ENV")));
    // test body runs only if the assumption passes
}
```

## Key Annotations

| Annotation | Purpose |
|---|---|
| `@Test` | Marks a method as a test case |
| `@BeforeEach` | Runs before every test method |
| `@AfterEach` | Runs after every test method |
| `@BeforeAll` | Runs once before all tests (must be `static`) |
| `@AfterAll` | Runs once after all tests (must be `static`) |
| `@Disabled` | Skips a test |

*(Legacy JUnit 4 equivalents referenced in the syllabus: `@Before`, `@After`, `@BeforeClass`, `@AfterClass`, `@Rule`.)*

```java
class CalculatorTest {

    Calculator calc;

    @BeforeEach
    void setUp() {
        calc = new Calculator();
    }

    @Test
    void testAdd() {
        assertEquals(7, calc.add(3, 4));
    }

    @AfterEach
    void tearDown() {
        calc = null;
    }
}
```

## Testing for Exceptions

```java
@Test
void testDivideByZero() {
    Calculator calc = new Calculator();
    ArithmeticException ex = assertThrows(ArithmeticException.class,
            () -> calc.divide(10, 0));
    assertEquals("/ by zero", ex.getMessage());
}
```
