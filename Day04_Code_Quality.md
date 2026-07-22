# Day 4 - Code Quality & Static Analysis
*Thu, 2 Jul 2026*

## 1. Code Quality

Code quality means code that is: easy to read, easy to maintain, secure, efficient, free from bugs, and follows coding standards.

### Characteristics of Good Code
1. Readable
2. Simple
3. Reusable
4. Testable
5. Secure
6. Well documented
7. Properly formatted
8. Less duplicated
9. Properly named

## 2. Static Code Analysis

Checking source code **without running the program**.

### Popular Tools
1. **SonarLint** — free IDE plugin
2. **SonarQube** — full server-based analysis platform with quality gates

*Note: needs Java 17 for the SonarQube/quality-gates automation setup referenced in this batch's syllabus.*

### What SonarLint Highlights
- Bugs & vulnerabilities
- Code smells
- Duplicate code
- Bad practices

```java
// Flagged as a code smell
boolean flag;
if (flag == true) { }

// Preferred
if (flag) { }
```

```java
// Flagged: redundant generic type
List<String> names = new ArrayList<String>();

// Preferred: diamond operator
List<String> names = new ArrayList<>();
```

### 4 Types of Issues Detected

1. **Bug** — code that is demonstrably wrong
2. **Vulnerability** — code that is exploitable
3. **Code Smell** — maintainability issue, not necessarily a bug
4. **Security Hotspot** — code that needs manual security review

## Quality Gates (SonarQube)

A **quality gate** is a set of conditions a project must pass before it's considered "release-ready" — e.g. 0 new bugs, coverage above a threshold, no critical vulnerabilities. If any condition fails, the build can be configured to fail in CI/CD.
