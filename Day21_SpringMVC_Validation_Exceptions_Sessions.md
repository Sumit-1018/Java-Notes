# Day 21 - Spring MVC: Validation, Exception Handling & Session Management
*Mon, 27 Jul 2026 (Week 5)*

## Validation

Validations are required to improve the quality of data stored by an application. Spring MVC has a vast set of validations, classified into categories:

1. **Standard**
2. **Custom**
   - a. Field
   - b. Cross Field — e.g. password equals confirm password

### 1. Standard Validation

Predefined validation rules provided by the **JSR Bean Validation API**.

- **JSR Bean Validation** is the specification standard
- **Hibernate Validator** is the implementation of that specification

```java
@NotEmpty(message = "Name should not be empty")
private String name;
```

Common annotations: `@NotEmpty`, `@NotNull`, `@Size(min=3, max=10)`, `@Min()`, `@Max()`

### 2. Custom Validation

- **Field validation** — applied individually to validate that one field
- **Cross-field validation** — compares two or more fields together, used when one field depends on another

**Examples:**
- Password = Confirm Password
- Start Date must be before End Date

### Approach 1 — JSR 303 Bean Validation API

Mainly used for standard, annotation-based validation.

```java
@NotNull
@NotBlank
@Size
@Email
```

`@AssertTrue` is a Bean Validation (JSR-303) annotation used to ensure a boolean value must be `true`.

```java
@AssertTrue(message = "Please accept terms and conditions")
private boolean acceptTerms;
```
If `acceptTerms = false`, validation fails.

### Approach 2 — Spring `Validator` Interface with `@InitBinder`

Mainly used for **custom / complex** validation logic.

`@InitBinder` customizes how input data is bound to Spring model objects, and configures validation **before** the controller method executes.

```java
@InitBinder
public void initBinder(WebDataBinder binder) {
    System.out.println("Init Binder invoked for date formatting");
    SimpleDateFormat dateFormat = new SimpleDateFormat("dd-MMM-yyyy");
    binder.registerCustomEditor(Date.class, "joiningDate", new CustomDateEditor(dateFormat, true));
}
```

### Providing Validation Messages

Three ways to define validation messages:

**1. Default Message** — provided automatically by the Bean Validation framework.
```
Example: "must not be null"
```

**2. Annotation-Level Message** — directly inside the annotation.
```java
@NotNull(message = "Age is required")
```

**3. `messages.properties` File** — external, custom messages.
```properties
NotNull.employeeBean.age=Age is required
NotNull=This is a required field
```

### Steps to Build a Custom Validation

1. Create the annotation
2. Create the validator
3. Link the validator and the annotation
4. Use the annotation on the business object's class

---
## Exception Handling in Spring MVC

Exceptions are runtime errors that can arise from improper implementation of a business requirement. They're handled by either a **local** or a **global** exception handler.

### Local Exception Handler

Define a method with `@ExceptionHandler` **inside the controller class**. If an exception occurs, instead of throwing it, Spring catches it and returns a proper view or response.

```java
@Controller
public class EmployeeController {

    @RequestMapping("/save")
    public String save() {
        int x = 10 / 0;   // triggers an exception
        return "success";
    }

    @ExceptionHandler(Exception.class)
    public ModelAndView handleException(Exception ex) {
        ModelAndView mv = new ModelAndView();
        mv.setViewName("errorPage");
        mv.addObject("message", ex.getMessage());
        mv.addObject("exception", ex);
        return mv;
    }
}
```

### Global Exception Handler — `@ControllerAdvice`

`@ControllerAdvice` provides **global** support to all controller classes. It's mainly used for:

1. **Global Exception Handling** — handles exceptions from all controllers using `@ExceptionHandler`
2. **Common Model Data** — adds common attributes to all views using `@ModelAttribute`
3. **Global Data Binding** — applies common binder settings using `@InitBinder`

**Purpose:** avoids repeating the same exception-handling code in multiple controllers — keeps it centralized.

```java
@ControllerAdvice
public class GlobalHandler {

    @ExceptionHandler(Exception.class)
    public String handleError() {
        return "errorPage";
    }
}
```

---
## Session Attributes

### Why We Need Them

All HTTP requests are **stateless** — they don't hold data in a request attribute for more than one request. The solution is **session scope**: to share data across multiple submissions/requests, the data must be kept at the session level.

### What Is a Session?

- Request & response tied to a **single user**
- Everything done from login to logout is one session
- Whenever a user logs in, a user-specific object is created on the server — the **`HttpSession`** object

### Session Tracking With `HttpSession`

`HttpSession` is an implicit object.

1. A user-specific object created on the server whenever a user logs in
2. Holds user-specific data shared by all servlets
3. Holds data as key-value pairs (like a `Map`)
4. Any servlet can put/get data to/from the session object

### `@SessionAttributes` in Spring MVC

Spring MVC offers `@SessionAttributes` to put data into the session scope. It's used at the **class level**:

```java
@Controller
@SessionAttributes("employeeBean")
public class EmployeeController {
    // any model attribute named "employeeBean" is automatically
    // stored in the HTTP session, persisting across multiple requests
}
```
