# Day 10 - Performance Monitoring
*Fri, 10 Jul 2026*

## Purpose

The purpose isn't just to tell us when something has **already** failed — it's to help identify and spot potential issues early, so systems keep running smoothly before users are impacted.

## What Gets Monitored

1. CPU
2. Memory (Heap)
3. Threads
4. Garbage Collection (GC)
5. Response Time
6. Throughput
7. Database calls

## Goals

Identify:
- Memory leaks
- Slow methods
- High CPU usage
- Thread deadlocks
- Excessive garbage collection

## Tools

| Tool | Use |
|---|---|
| **VisualVM** | Java monitoring tool — heap memory, CPU usage, threads, loaded classes, GC, heap dumps |
| **Eclipse MAT** | Memory Analyzer Tool — generates **memory leak reports** from heap dumps |
| **JMeter** | Performance and load testing |

### VisualVM — What It Shows
- Heap memory
- CPU usage
- Threads
- Classes loaded
- Garbage collection activity
- Heap dumps

### Typical Workflow
1. Attach VisualVM to a running JVM process
2. Reproduce the slow/leaking scenario
3. Take a heap dump
4. Analyze the dump in Eclipse MAT to find retained objects and leak suspects
5. Load-test the fix with JMeter to confirm improved throughput/response time
