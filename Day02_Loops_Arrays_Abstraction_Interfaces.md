# Day 2 - Loops, Arrays, Abstraction & Interfaces
*Tue, 30 Jun 2026*

## Loops

```java
// for loop
for (int i = 0; i < 5; i++) {
    System.out.println(i);
}

// while loop
int i = 0;
while (i < 5) {
    System.out.println(i);
    i++;
}

// do-while loop — runs at least once
int j = 0;
do {
    System.out.println(j);
    j++;
} while (j < 5);

// enhanced for-each loop
int[] nums = {1, 2, 3};
for (int n : nums) {
    System.out.println(n);
}
```

## Arrays

Fixed-size, ordered collection of elements of the same type.

```java
int[] arr = new int[5];         // default values: 0
int[] arr2 = {10, 20, 30};      // array literal

arr2[0] = 99;                   // update
System.out.println(arr2.length); // 3

// 2D array
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6}
};
```

## Classes & Objects (Recap + Practice)

```java
class Student {
    String name;
    int marks;

    Student(String name, int marks) {  // constructor
        this.name = name;
        this.marks = marks;
    }

    void display() {
        System.out.println(name + " scored " + marks);
    }
}

Student s1 = new Student("Riya", 88);
s1.display();
```

## Polymorphism (Applied)

See Day 1 for overloading vs overriding — today's focus is applying it across class hierarchies with `@Override` and dynamic method dispatch.

```java
Animal a = new Cat(); // reference type Animal, object type Cat
a.sound();             // calls Cat's overridden sound() — runtime polymorphism
```

## Abstraction

Hiding implementation details and exposing only essential features. In Java, achieved via **abstract classes** and **interfaces**.

```java
abstract class Shape {
    abstract double area();       // no body — must be implemented

    void describe() {              // concrete method
        System.out.println("This is a shape with area " + area());
    }
}

class Circle extends Shape {
    double radius;
    Circle(double radius) { this.radius = radius; }

    @Override
    double area() {
        return Math.PI * radius * radius;
    }
}
```

**Abstract class vs Interface**

| | Abstract Class | Interface |
|---|---|---|
| Methods | Can have both abstract & concrete methods | All abstract by default (plus default/static since Java 8) |
| Fields | Any type of field | Implicitly `public static final` |
| Inheritance | `extends` (single) | `implements` (multiple allowed) |
| Constructors | Yes | No |

## Interface

A contract that defines *what* a class must do, not *how*.

```java
interface Vehicle {
    int MAX_SPEED = 180; // public static final by default

    void start();          // abstract method

    default void honk() {  // default method — has a body
        System.out.println("Beep beep!");
    }

    static Vehicle createDefault() { // static method
        return new Car();
    }
}

class Car implements Vehicle {
    @Override
    public void start() {
        System.out.println("Car starting...");
    }
}
```
