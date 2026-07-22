# Day 1 - Full Stack Introduction & OOP Fundamentals
*Mon, 29 Jun 2026*

## Full Stack Introduction

A full stack application spans:
- **Frontend** — what the user sees and interacts with (HTML/CSS/JS, React)
- **Backend** — business logic and APIs (Java, Spring)
- **Database** — persistent storage (MySQL, MongoDB)

## Object-Oriented Programming — Core Concepts

### Class & Object

- **Class** — a blueprint that defines properties (fields) and behavior (methods).
- **Object** — a concrete instance of a class, created in memory.

```java
class Car {
    String model;
    int speed;

    void accelerate() {
        speed += 10;
    }
}

Car myCar = new Car();   // object
myCar.model = "Sedan";
myCar.accelerate();
```

### Encapsulation

Bundling data (fields) and methods that operate on it into a single unit, while restricting direct access to internal state — usually via `private` fields and `public` getters/setters.

```java
class BankAccount {
    private double balance; // hidden from outside

    public double getBalance() {
        return balance;
    }

    public void deposit(double amount) {
        if (amount > 0) balance += amount;
    }
}
```

### Inheritance

A mechanism where one class (subclass) acquires the fields and methods of another (superclass), enabling code reuse.

```java
class Animal {
    void eat() {
        System.out.println("This animal eats food.");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Woof!");
    }
}

Dog d = new Dog();
d.eat();  // inherited
d.bark();
```

### Polymorphism

The ability of an object to take many forms — the same method call behaves differently depending on the object.

- **Compile-time (method overloading)** — same method name, different parameters.
- **Runtime (method overriding)** — subclass provides its own implementation of a superclass method.

```java
// Overloading
class Calculator {
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
}

// Overriding
class Animal {
    void sound() { System.out.println("Some sound"); }
}
class Cat extends Animal {
    @Override
    void sound() { System.out.println("Meow"); }
}
```

## Java Language Fundamentals

| Concept | Notes |
|---|---|
| Primitive types | `int`, `double`, `char`, `boolean`, `long`, `float`, `byte`, `short` |
| `main` method | `public static void main(String[] args)` — JVM entry point |
| Variables | Declared with a type; Java is statically typed |
| Operators | Arithmetic, relational, logical, assignment, bitwise |

```java
public class Main {
    public static void main(String[] args) {
        int age = 21;
        double price = 99.99;
        boolean isActive = true;
        System.out.println("Age: " + age);
    }
}
```
