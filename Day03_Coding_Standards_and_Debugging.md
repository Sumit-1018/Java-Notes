# Day 3 - Coding Standards & Debugging
*Wed, 1 Jul 2026*

---
# Part A — Coding Standards

## 1. Coding Standards

A set of guidelines and best practices that help write code that is **consistent, readable, maintainable, and less error-prone**.

- Meaningful variable names
- Consistent formatting
- Proper exception handling
- No duplicate code
- Adequate comments / documentation
- Unit tests included
- Security checks
- Code review

## 2. Project Structure

- **Maven** → "Convention over Configuration" (standard folder layout so every project looks familiar).

## 3. Naming Conventions

| Element | Convention | Example |
|---|---|---|
| Package | all lowercase, reverse domain | `com.company.student;` |
| Class / Interface | PascalCase | `DataInputStream` (not `Datainputstream`) |
| Method / Variable | camelCase | `printData()` |
| Constant / Enum | ALL CAPS | `MAX_VALUE` |

## 4. Code Formatting

### Indentation
- Standard Java convention: **4 spaces per indentation level**.

### Braces & Whitespace
- `{ }` mark the beginning and end of a block.
- Use spaces, tabs, and blank lines to visually separate logical sections.

### Import Statement Guidelines

```java
// Avoid
java.util.Date d = new java.util.Date();

// Prefer
import java.util.Date;
Date d = new Date();
```

## 5. Comments & Documentation

### Types of Comments
1. **Single-line** — `// comment`
2. **Multi-line** — `/* comment */`
3. **Javadoc** — generates documentation automatically

### Javadoc Tags

| Tag | Meaning |
|---|---|
| `@author` | Author name |
| `@version` | Version number |
| `@param` | Method parameter |
| `@return` | Return value |
| `@throws` | Exception description |
| `@see` | Related classes/methods |
| `@since` | Version introduced |

```java
/**
 * Divides two numbers.
 *
 * @param a dividend
 * @param b divisor
 * @return result of a / b
 * @throws ArithmeticException if divisor is zero
 */
public static int divide(int a, int b) {
    return a / b;
}
```

### Special Markers
- **TODO** → work still pending
- **FIXME** → known bug that needs fixing
- **NOTE** → useful contextual information

### Best Practices
1. Explain **why**, not just what
2. Document business rules
3. Explain complex logic
4. Warn other developers about gotchas
5. Document public methods
6. Avoid commenting every single line
7. Keep comments updated as code changes

---
# Part B — Debugging

## 1. Errors vs Exceptions

### Errors
Serious problems occurring in the **JVM**, usually **not recoverable**.
- `OutOfMemoryError`, `StackOverflowError`

### Exceptions
Conditions that an application **can** handle.
```java
int result = 10 / 0; // ArithmeticException
```
- `NullPointerException`, `ArithmeticException`, `FileNotFoundException`

### Checked vs Unchecked

| Type | When checked | Notes |
|---|---|---|
| Checked Exception | Compile time | Must be handled/declared |
| Unchecked Exception | Runtime | Occurs during execution |

## 2. Debugging Using Print Statements

Simplest technique. **Pros:** easy, no tools needed. **Limitations:** clutters code, unmanageable at scale, must be removed later.

## 3. Tracing and Logging

| Level | Meaning |
|---|---|
| `SEVERE` | Critical failures |
| `WARNING` | Potential issues |
| `INFO` | General information |
| `CONFIG` | Configuration details |
| `FINE` | Debug information |
| `FINER` | Detailed debugging |
| `FINEST` | Most detailed trace |

**Benefits:** permanent audit trail, easy troubleshooting, can be disabled in production without code changes.

## 4. Code Review & Problem Isolation

Reviews look for logical errors, performance issues, security vulnerabilities, standard violations.

```java
if (age > 18)   // logical error
if (age >= 18)  // correct
```

**Problem isolation steps:** reproduce → narrow down the code area → check inputs → test modules separately → identify root cause.

## 5. Eclipse Debugger

Core capabilities: breakpoints, step execution, variable inspection, call stack analysis, exception tracking.

| Action | Shortcut |
|---|---|
| Resume | `F8` |
| Step Into | `F5` |
| Step Over | `F6` |
| Step Return | `F7` |
| Terminate | `Ctrl + F2` |
