# Day 11 - SOLID Principles & Design Patterns
*Mon, 13 Jul 2026 (Week 3)*

---
# Part A — SOLID Principles

A set of 5 object-oriented design principles that help create **maintainable, scalable, and flexible** Java applications.

## S — Single Responsibility Principle (SRP)
> A class should have only one reason to change.

```java
// ❌ Wrong
class Employee {
    void calculateSalary() { }
    void saveToDb() { }
    void generateReport() { }
}

// ✅ Right
class Employee { /* holds employee data */ }
class SalaryCalculator { void calculateSalary(Employee e) { } }
class EmployeeRepository { void save(Employee e) { } }
class ReportGenerator { void generateReport(Employee e) { } }
```

## O — Open/Closed Principle (OCP)
> Software entities should be **open for extension** but **closed for modification**.

```java
// ❌ Wrong
class PaymentProcessor {
    void processPayment(String type) {
        if (type.equals("CARD")) { }
        else if (type.equals("UPI")) { }
    }
}

// ✅ Right
interface PaymentMethod { void process(); }
class CardPayment implements PaymentMethod { public void process() { } }
class UpiPayment implements PaymentMethod { public void process() { } }
```

## L — Liskov Substitution Principle (LSP)
> Subclass objects should be substitutable for their superclass without breaking the app.

```java
// ❌ Wrong
class Bird { void fly() { } }
class Penguin extends Bird {
    @Override
    void fly() { throw new UnsupportedOperationException(); }
}

// ✅ Right
class Bird { }
interface Flyable { void fly(); }
class Sparrow extends Bird implements Flyable { public void fly() { } }
class Penguin extends Bird { }
```

## I — Interface Segregation Principle (ISP)
> Clients should not be forced to depend on interfaces they do not use.

```java
// ❌ Wrong
interface Worker { void work(); void eat(); }

// ✅ Right
interface Workable { void work(); }
interface Eatable { void eat(); }
class HumanWorker implements Workable, Eatable { }
class RobotWorker implements Workable { }
```

## D — Dependency Inversion Principle (DIP)
> High-level modules should not depend on low-level modules. Both should depend on abstractions.

```java
// ❌ Wrong
class MySqlDb { void connect() { } }
class UserService {
    MySqlDb db = new MySqlDb();
    void saveUser() { db.connect(); }
}

// ✅ Right
interface Database { void connect(); }
class MySqlDb implements Database { public void connect() { } }
class UserService {
    private final Database db;
    UserService(Database db) { this.db = db; } // injected
    void saveUser() { db.connect(); }
}
```

---
# Part B — Design Patterns

## What Is a Design Pattern?

A **proven, reusable solution** to a commonly occurring software design problem.

> Origin: the **Gang of Four (GoF)** book — *Design Patterns: Elements of Reusable Object-Oriented Software* — by Erich Gamma, Richard Helm, Ralph Johnson, and John Vlissides.

### Design Patterns vs SOLID Principles

| | Guides |
|---|---|
| **SOLID Principles** | *How to design classes* |
| **Design Patterns** | *How to solve recurring design problems* |

They work together — SOLID shapes the class design; patterns are the proven templates that satisfy those principles in practice.

### Which Pattern Reinforces Which Principle

| Principle | Related Pattern(s) |
|---|---|
| SRP | Factory, Builder |
| OCP | Strategy, Decorator |
| LSP | Template Method |
| ISP | Adapter |
| DIP | Factory, Dependency Injection |

## Benefits

- Reusability
- Maintainability
- Scalability
- Readability
- Loose coupling
- Testability

## Categories of Design Patterns

### 1. Creational Patterns (5) — Object Creation

| Pattern | Purpose |
|---|---|
| **Singleton** | Only one object can exist (e.g. Logger, Configuration, Cache) |
| **Factory Method** | Create objects without exposing creation logic |
| **Abstract Factory** | A factory of factories |
| **Builder** | Build complex objects step by step |
| **Prototype** | Clone existing objects |

```java
// Singleton
class Logger {
    private static final Logger INSTANCE = new Logger();
    private Logger() { }
    public static Logger getInstance() { return INSTANCE; }
    public void log(String msg) { System.out.println("[LOG] " + msg); }
}

// Factory Method
interface Shape { void draw(); }
class Circle implements Shape { public void draw() { System.out.println("Drawing Circle"); } }
class Square implements Shape { public void draw() { System.out.println("Drawing Square"); } }

class ShapeFactory {
    static Shape create(String type) {
        return switch (type) {
            case "CIRCLE" -> new Circle();
            case "SQUARE" -> new Square();
            default -> throw new IllegalArgumentException("Unknown type");
        };
    }
}

// Builder
class Pizza {
    private final String size;
    private final boolean cheese;

    private Pizza(Builder b) {
        this.size = b.size;
        this.cheese = b.cheese;
    }

    static class Builder {
        private String size;
        private boolean cheese;

        Builder size(String size) { this.size = size; return this; }
        Builder cheese(boolean cheese) { this.cheese = cheese; return this; }
        Pizza build() { return new Pizza(this); }
    }
}

Pizza pizza = new Pizza.Builder().size("Large").cheese(true).build();
```

### 2. Structural Patterns — Class/Object Composition

| Pattern | Purpose |
|---|---|
| **Adapter** | Convert one interface into another |
| **Bridge** | Separates abstraction from implementation |
| **Composite** | Tree structure of objects |
| **Decorator** | Adds functionality dynamically |
| **Facade** | Simplifies subsystem access |
| **Flyweight** | Share objects to save memory |
| **Proxy** | Controls access to an object |

```java
// Adapter
interface MediaPlayer { void play(String fileName); }

class LegacyPlayer { void playOldFormat(String fileName) {
    System.out.println("Playing old format: " + fileName);
} }

class MediaAdapter implements MediaPlayer {
    private final LegacyPlayer legacyPlayer = new LegacyPlayer();
    public void play(String fileName) { legacyPlayer.playOldFormat(fileName); }
}

// Decorator
interface Coffee { double cost(); }
class SimpleCoffee implements Coffee { public double cost() { return 2.0; } }
class MilkDecorator implements Coffee {
    private final Coffee base;
    MilkDecorator(Coffee base) { this.base = base; }
    public double cost() { return base.cost() + 0.5; }
}

// Facade
class CPU { void start() { System.out.println("CPU started"); } }
class Memory { void load() { System.out.println("Memory loaded"); } }
class ComputerFacade {
    private final CPU cpu = new CPU();
    private final Memory memory = new Memory();
    void startComputer() { cpu.start(); memory.load(); }
}
```

### 3. Behavioral Patterns — Communication Between Objects

| Pattern | Purpose |
|---|---|
| **Chain of Responsibility** | Pass a request through a chain of handlers |
| **Command** | Encapsulates a request as an object |
| **Interpreter** | Evaluates grammar/expressions |
| **Iterator** | Sequential traversal of a collection |
| **Mediator** | Centralizes communication between objects |
| **Memento** | Stores/restores an object's state |
| **Observer** | One-to-many notifications |
| **State** | Behavior changes based on internal state |
| **Strategy** | Change the algorithm at runtime |
| **Template Method** | Defines the skeleton of an algorithm |
| **Visitor** | Add operations without modifying existing classes |

```java
// Observer
interface Observer { void update(String event); }
class EmailSubscriber implements Observer {
    public void update(String event) { System.out.println("Email alert: " + event); }
}
class EventPublisher {
    private final List<Observer> observers = new ArrayList<>();
    void subscribe(Observer o) { observers.add(o); }
    void publish(String event) { observers.forEach(o -> o.update(event)); }
}

// Strategy
interface DiscountStrategy { double apply(double price); }
class NoDiscount implements DiscountStrategy { public double apply(double p) { return p; } }
class TenPercentOff implements DiscountStrategy { public double apply(double p) { return p * 0.9; } }

class Checkout {
    private DiscountStrategy strategy;
    Checkout(DiscountStrategy strategy) { this.strategy = strategy; }
    double finalPrice(double price) { return strategy.apply(price); }
}

// Template Method
abstract class DataProcessor {
    final void process() {   // skeleton — steps fixed, details vary
        readData();
        processData();
        saveData();
    }
    abstract void readData();
    abstract void processData();
    void saveData() { System.out.println("Saving to DB..."); } // default step
}
```

---
# Part C — Introduction to Asynchronous Patterns in Java

Asynchronous patterns let code continue running without blocking on a slow operation (I/O, network calls).

```java
CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> {
    // simulate slow work
    return "Result from async task";
});

future.thenAccept(result -> System.out.println("Got: " + result));
```

**Common async building blocks:** `CompletableFuture`, `ExecutorService`, callbacks, and (later in the course) reactive/non-blocking patterns used with Spring WebFlux.
