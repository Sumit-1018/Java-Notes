# Day 6 - Data Structures & Collections API
*Mon, 6 Jul 2026 (Week 2)*

---
# Part A — Searching & Sorting

## Searching

| Algorithm | How it works | Prerequisite |
|---|---|---|
| **Linear Search** | Check every element one by one | None |
| **Binary Search** | Repeatedly halve the search range | Data must be sorted |

```java
public static int linearSearch(int[] arr, int target) {
    for (int i = 0; i < arr.length; i++) {
        if (arr[i] == target) return i;
    }
    return -1;
}

public static int binarySearch(int[] arr, int target) {
    int low = 0, high = arr.length - 1;
    while (low <= high) {
        int mid = (low + high) / 2;
        if (arr[mid] == target) return mid;
        else if (arr[mid] < target) low = mid + 1;
        else high = mid - 1;
    }
    return -1;
}
```

## Sorting

| Algorithm | Core Idea |
|---|---|
| **Bubble Sort** | Compare adjacent elements repeatedly, swap if out of order |
| **Selection Sort** | Find the smallest element, place it at the beginning |
| **Insertion Sort** | Insert each element into its correct position in the sorted part |
| **Merge Sort** | Divide the array into parts, sort each, then merge |
| **Quick Sort** | Choose a pivot, partition the array, recursively sort both sides |
| **Radix Sort** | Non-comparison based — sorts digit by digit (LSD or MSD) |

### Radix Sort Walkthrough

Starting array: `170, 45, 75, 90, 802, 24, 2, 66`

```
Sort by 1's digit:   170, 90, 802, 2, 24, 75, 66
Sort by 10's digit:  802, 2, 24, 45, 66, 170, 75, 90
Sort by 100's digit: 2, 24, 45, 66, 75, 90, 170, 802
```

### Built-in Java Utility Methods

```java
Arrays.sort(arr);
Collections.sort(list);
boolean found = list.contains(element);
int index = Arrays.binarySearch(arr, target);
```

---
# Part B — Java Collections Framework

## Overview

```
Iterable → Collection
              ├── List   (ordered, allows duplicates, index-based)
              ├── Set    (no duplicates, not index-based)
              └── Queue  (FIFO)

Map (separate interface — key/value pairs)
```

## List — Ordered, Allows Duplicates

- Maintains insertion order, allows duplicates, allows multiple `null` values.
- **Implementations:** `ArrayList`, `LinkedList`, `Vector`, `Stack`

## Set — Unique Elements Only

- No duplicates, one `null` allowed, fast lookup.
- **Implementations:** `HashSet`, `LinkedHashSet`, `TreeSet` (sorted)

## Queue — First In, First Out

- **Implementations:** `LinkedList`, `PriorityQueue`, `ArrayDeque` (Deque)

## Map — Key/Value Pairs

- Values can be duplicated. Only **one** null key allowed (`HashMap`). Multiple null values allowed.
- **Implementations:** `HashMap`, `LinkedHashMap`, `TreeMap`

```java
Map<String, Integer> scores = new HashMap<>();

scores.put("Alice", 90);
scores.get("Alice");
scores.remove("Alice");
scores.containsKey("Alice");
scores.containsValue(90);
scores.keySet();
scores.entrySet();
scores.values();
scores.size();
```

## Comparable vs Comparator

| | Comparable | Comparator |
|---|---|---|
| Package | `java.lang` | `java.util` |
| Purpose | Defines a class's **natural** sort order | Defines a **custom** sort order, outside the class |
| Method | `int compareTo(T obj)` | `int compare(T o1, T o2)` |

```java
// Comparable — natural ordering (inside the class)
public class Employee implements Comparable<Employee> {
    int salary;

    @Override
    public int compareTo(Employee other) {
        return this.salary - other.salary;
    }
}

// Comparator — custom ordering (outside the class)
Comparator<Employee> byNameDesc = (e1, e2) -> e2.name.compareTo(e1.name);
employees.sort(byNameDesc);
```
