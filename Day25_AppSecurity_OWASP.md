# Day 25 - Application Security & OWASP
*Fri, 31 Jul 2026*

## Application Security (AppSec)

The practice of protecting software applications from security threats **throughout their development, deployment, and maintenance lifecycle** — to prevent unauthorized access, data breaches, and vulnerabilities that attackers can exploit.

## Secure Coding Practices

1. **Input Validation** — never trust incoming data, validate everything at the boundary
2. **Output Encoding** — encode data before rendering it, to prevent injection into HTML/JS/SQL contexts
3. **Authentication and Authorization** — verify identity, then verify permissions
4. **Secure Error Handling** — don't leak stack traces or internal details in error responses
5. **Secure Session Management** — protect session tokens, use secure/httpOnly cookies, timeouts
6. **Protect Sensitive Data** — encrypt at rest and in transit
7. **Dependency Management** — keep libraries updated, scan for known vulnerabilities

## Secure Database Access

1. **Use Parameterized Queries** — prevents SQL injection (this is exactly why `PreparedStatement` exists — see Day 12)
2. **Use Stored Procedures Carefully** — they don't automatically prevent injection if built with string concatenation
3. **Principle of Least Privilege** — DB accounts should have only the permissions they actually need
4. **Encrypt Sensitive Data** — at the column or storage level, for things like PII
5. **Database Auditing and Logging** — track who accessed/changed what
6. **Secure Database Configuration** — disable unused features, change default credentials, restrict network access

```java
// Vulnerable — string concatenation allows SQL injection
String query = "SELECT * FROM users WHERE username = '" + userInput + "'";

// Secure — parameterized query
String query = "SELECT * FROM users WHERE username = ?";
PreparedStatement ps = conn.prepareStatement(query);
ps.setString(1, userInput);
```

## Secure Application & Web Practices

1. **HTTPS Everywhere** — encrypt all traffic, not just login pages
2. **Security Headers** — e.g. `Content-Security-Policy`, `X-Frame-Options`, `Strict-Transport-Security`
3. **Session Security** — rotate session IDs on login, expire idle sessions
4. **File Upload Security** — validate file type/size, store outside the web root, scan for malware
5. **API Security** — authentication tokens, rate limiting, input validation on every endpoint
6. **Logging and Monitoring** — detect and respond to suspicious activity in real time

---
## OWASP

**OWASP — Open Worldwide Application Security Project**

A nonprofit foundation that publishes the industry-standard list of the most critical web application security risks.

### OWASP Top 10

1. **Broken Access Control** — users acting outside their intended permissions
2. **Cryptographic Failures** — weak or missing encryption of sensitive data
3. **Injection** — SQL, command, or other injection attacks
4. **Insecure Design** — security flaws baked into the architecture itself, not just the code
5. **Security Misconfiguration** — default settings, unnecessary features left enabled, verbose error messages
6. **Vulnerable and Outdated Components** — using libraries/frameworks with known vulnerabilities
7. **Identification and Authentication Failures** — weak login/session mechanisms
8. **Software and Data Integrity Failures** — trusting unverified updates, plugins, or CI/CD pipelines
9. **Security Logging and Monitoring Failures** — insufficient detection of breaches in progress
10. **Server-Side Request Forgery (SSRF)** — tricking the server into making unintended requests on the attacker's behalf

> Spring Security — the framework-level implementation of these protections in a Spring application — is the next topic to cover.
