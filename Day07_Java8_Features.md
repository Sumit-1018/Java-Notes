# Day 7 - Java 8 Features
*Tue, 7 Jul 2026*

## 1. Functional Interfaces

An interface that contains **only one abstract method**.

```java
@FunctionalInterface
public interface Calculator {
    int calculate(int a, int b);
}
```

Recall: an interface can also carry **default** and **static** methods (Java 8+) alongside its single abstract method.

## 2. Lambda Expressions

An **anonymous function** — no name, no return type declaration, no access modifier.

```java
(parameters) -> {
    // body
};
```

```java
Calculator add = (a, b) -> a + b;
System.out.println(add.calculate(3, 4)); // 7
```

**Advantages:** less code, easier to read, no anonymous-class boilerplate, better performance, used heavily with Streams.

## 3. Method References

`::` is the **method reference operator** — shorthand for a lambda that just calls an existing method.

```java
ClassName::methodName
```

| Type | Example |
|---|---|
| Static method reference | `Math::max` |
| Instance method reference | `str::toUpperCase` |
| Constructor reference | `ArrayList::new` |

```java
List<String> names = Arrays.asList("bob", "alice");
names.forEach(System.out::println); // instance method reference
```

## 4. `forEach()`

```java
names.forEach(name -> System.out.println(name));
```

## 5. Standard Functional Interfaces

| Interface | Input | Output | Method |
|---|---|---|---|
| `Predicate<T>` | 1 | `boolean` | `boolean test(T t)` |
| `Function<T,R>` | 1 | 1 (different type) | `R apply(T t)` |
| `Consumer<T>` | 1 | none | `void accept(T t)` |
| `Supplier<T>` | none | 1 | `T get()` |
| `UnaryOperator<T>` | 1 | same type | `T apply(T t)` |
| `BinaryOperator<T>` | 2 (same type) | same type | `T apply(T t1, T t2)` |

```java
Predicate<Integer> isEven = n -> n % 2 == 0;
Function<String, Integer> length = String::length;
Consumer<String> printer = System.out::println;
Supplier<Double> random = Math::random;
UnaryOperator<Integer> square = n -> n * n;
BinaryOperator<Integer> sum = (a, b) -> a + b;
```

## 6. Stream API

A sequence of elements that supports processing operations — functional, efficient collection processing.

### Creating a Stream

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David", "Eve");

// 1. From a collection
List<String> result = names.stream()
        .filter(name -> name.startsWith("A"))
        .collect(Collectors.toList());

// 2. From an array
int[] arr = {1, 2, 3, 4};
Arrays.stream(arr);

// 3. Using Stream.of()
Stream<String> stream = Stream.of("a", "b", "c");
```

### Intermediate Operations (chainable, any number)
1. `filter()`
2. `map()`
3. `sorted()`
4. `distinct()`
5. `limit()`

### Terminal Operations (only one, ends the stream)
1. `collect()`
2. `count()`
3. `reduce()`
4. `findFirst()`

```java
long count = names.stream()
        .filter(n -> n.length() > 3)
        .map(String::toUpperCase)
        .distinct()
        .count();
```

## 7. `Optional<T>`

Represents a value that **may or may not be present** — helps avoid `NullPointerException`.

```java
Optional<String> optName = Optional.ofNullable(getName());

optName.ifPresent(System.out::println);
String name = optName.orElse("Default Name");
```
