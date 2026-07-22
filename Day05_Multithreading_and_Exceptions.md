# Day 5 - Multithreading & Exception Handling
*Fri, 3 Jul 2026*

---
# Part A — Multithreading

## What Is a Thread?

A thread is the smallest unit of execution within a process. **Multithreading** lets a program run multiple parts concurrently, improving responsiveness and throughput.

## Creating Threads

### 1. Extending `Thread`

```java
class MyThread extends Thread {
    @Override
    public void run() {
        System.out.println("Running in: " + Thread.currentThread().getName());
    }
}

MyThread t1 = new MyThread();
t1.start(); // never call run() directly — start() spawns a new thread
```

### 2. Implementing `Runnable` (preferred — allows extending other classes)

```java
class MyTask implements Runnable {
    @Override
    public void run() {
        System.out.println("Task running on: " + Thread.currentThread().getName());
    }
}

Thread t2 = new Thread(new MyTask());
t2.start();
```

### 3. Using Lambdas (Java 8+)

```java
Runnable task = () -> System.out.println("Lambda thread running");
new Thread(task).start();
```

## Thread Lifecycle

```
NEW → RUNNABLE → RUNNING → (BLOCKED / WAITING / TIMED_WAITING) → TERMINATED
```

## Synchronization

Prevents **race conditions** when multiple threads access shared data.

```java
class Counter {
    private int count = 0;

    public synchronized void increment() {
        count++;
    }
}
```

## Key Concepts

| Term | Meaning |
|---|---|
| `synchronized` | Ensures only one thread executes a block/method at a time |
| `wait()` / `notify()` | Inter-thread communication |
| `join()` | Waits for a thread to finish before continuing |
| Deadlock | Two or more threads waiting on each other forever |
| `ExecutorService` | Manages a pool of threads instead of creating them manually |

```java
ExecutorService executor = Executors.newFixedThreadPool(3);
executor.submit(() -> System.out.println("Task via thread pool"));
executor.shutdown();
```

---
# Part B — Exception Handling

## What Is an Exception?

An **unexpected event** that occurs during program execution and interrupts the normal flow.

## Exception Hierarchy

```
Object
  └── Throwable
        ├── Exception
        │     ├── Checked Exception
        │     └── Unchecked Exception (RuntimeException)
        └── Error
```

## Checked Exceptions
Checked at **compile time** — compiler forces you to handle or declare them.
`IOException`, `SQLException`, `FileNotFoundException`, `ClassNotFoundException`

## Unchecked Exceptions
Checked at **runtime**, not enforced by the compiler.

## Handling Keywords

| Keyword | Purpose |
|---|---|
| `try` | Block of code that might throw an exception |
| `catch` | Handles a specific exception type |
| `finally` | Always executes, used for cleanup |
| `throws` | Declares that a method might throw an exception |
| `throw` | Explicitly throws an exception |

```java
public void readFile(String path) throws IOException {
    try {
        FileReader reader = new FileReader(path);
    } catch (FileNotFoundException e) {
        System.out.println("File not found: " + e.getMessage());
    } finally {
        System.out.println("Cleanup complete.");
    }
}
```

## Custom Exceptions

```java
public class InsufficientBalanceException extends Exception {
    public InsufficientBalanceException(String message) {
        super(message);
    }
}

public class Account {
    private double balance;

    public void withdraw(double amount) throws InsufficientBalanceException {
        if (amount > balance) {
            throw new InsufficientBalanceException("Insufficient funds");
        }
        balance -= amount;
    }
}
```
