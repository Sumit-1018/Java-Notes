# Day 20 - Spring MVC: Fundamentals, Views & Forms
*Fri, 24 Jul 2026*

## What Is Spring MVC?

A module of the Spring Framework used to develop **web applications**.

**MVC** stands for **Model, View, Controller** — a software design pattern that splits application logic into 3 parts:

| Part | Role | Examples |
|---|---|---|
| **Model** | Holds the data | JavaBean, POJO, DTO |
| **View** | Acts as the UI — takes input, shows output | HTML, JSP, Swing |
| **Controller** | Performs business logic | Servlet, class with `@Controller` |

## Servlet MVC (Pre-Spring Approach)

The Servlet **acts as the controller**.

```
Request (browser) --> Servlet --> Response --> JSP/HTML pages
```

Separate servlets per action, e.g.:
```
LoginServlet
ValidateServlet
PaymentServlet
```

Spring MVC replaces this with a single `@Controller` class handling multiple related requests:

```java
@Controller
class EmployeeController {

    @RequestMapping("emp/login")
    public String empLogin() {
        return "loginform"; // resolves to loginform.jsp
    }

    @RequestMapping("emp/register")
    public String registerEmp() {
        return "registerform"; // resolves to registerform.jsp
    }
}
```

## Spring MVC Workflow

```
Client (Browser) emp/login
     |
     v
[ DispatcherServlet ] --> [ HandlerMapping ] --> [ @Controller ]
                                                      |
                                                      v
                                          (Business Logic + Model)
                                                      |
                                                      v
                                              View Name ("show")
                                                      |
                                                      v
                                            [ ViewResolver ]
                                                      |
                                                      v   add prefix / and suffix .jsp
                                                 /show.jsp
                                                      |
                                                      v
                                                   [ View ]
                                                      |
                                                      v
Client (Browser)  <---------------------------------- Response
```

## Spring MVC Architecture

- **`DispatcherServlet`** — a servlet acting as the **front controller**, responsible for managing the flow of the whole application. Every request hits it first; it receives all incoming requests.
- **`HandlerMapping`** — identifies the right controller and passes control to it for processing.
- **`Controller`** — (1) performs business logic, (2) puts data in the model object, (3) returns the view name (output/response page name).
- The view name is passed to the **`ViewResolver`**, which adds a prefix (`/`) and suffix (`.jsp`) to generate the actual view path, e.g. `/show.jsp`.
- Model data is passed to the view object, and the response is generated.

### Core Components

| Component | Role |
|---|---|
| `DispatcherServlet` | Front controller — receives all requests |
| `HandlerMapping` | Identifies the specific controller |
| `Controller` | Business logic, puts data in Model, returns view name |
| `ViewResolver` | Attaches prefix & suffix — `hello` → `/hello.jsp` |
| `Model` | Holds data |
| `View` | Generates the response |

---
## ViewResolver

Maps the **logical view name** returned by a controller to the actual view file (JSP/HTML).

### Why We Need It

- **Removes hardcoding** — no need to write the full JSP path in the controller
- **Simplifies development** — controller returns only a logical name like `"home"`; view paths are configured in one place
- **Easy to change view technology** — can switch from JSP to Thymeleaf without touching controller code
- **Cleaner code** — controllers stay simple and readable

```java
// Controller returns:
return "home";

// ViewResolver converts it to:
// "/WEB-INF/views/home.jsp"
```

```java
@Bean
public InternalResourceViewResolver viewResolver() {
    InternalResourceViewResolver vr = new InternalResourceViewResolver();
    vr.setPrefix("/WEB-INF/views/");
    vr.setSuffix(".jsp");
    return vr;
}
```

---
## Spring Form Tag & `@ModelAttribute`

The **Spring Form Tag** binds form components to the model object exposed by the controller — it moves data **View → Controller**, one direction only.

Spring Form uses the **Spring Model** to access and submit data to `@Controller`. The `@ModelAttribute` annotation is used to access that Model.

`@ModelAttribute` can be placed at **2 levels** in a `@Controller` class:
1. Method parameter level
2. Method level

`@ModelAttribute` sends and receives data between controller and view — it's **bi-directional**.

### 1. View → Controller (Method Parameter Level)

> After executing the handler and before rendering the view, Spring MVC puts the data into the Spring Model as a request attribute, and makes it available to the view.

```java
@Controller
public class UserController {

    @PostMapping("/register")
    public String registerUser(@ModelAttribute("user") User user) {
        // form data is automatically mapped to the User object
        System.out.println(user.getName());
        System.out.println(user.getEmail());
        return "success";
    }
}
```

```jsp
<form:form method="post" action="register" modelAttribute="user">
    Name: <form:input path="name"/><br>
    Email: <form:input path="email"/><br>
    <input type="submit" value="Register"/>
</form:form>
```

### 2. Controller → View (Method Level)

All methods marked with `@ModelAttribute` execute **before** any handler method (marked with `@RequestMapping`) runs on the controller.

```java
@Controller
public class UserController {

    @ModelAttribute("countries")
    public List<String> getCountries() {
        return Arrays.asList("India", "USA", "UK");
    }

    @GetMapping("/register")
    public String showForm(Model model) {
        model.addAttribute("user", new User());
        return "register";
    }
}
```

```jsp
<form:form method="post" action="register" modelAttribute="user">
    Name: <form:input path="name"/><br>

    Country:
    <form:select path="country">
        <form:options items="${countries}"/>
    </form:select>

    <input type="submit" value="Register"/>
</form:form>
```

The `countries` list will populate in the dropdown automatically, coming straight from the controller.

---
## Static UI vs Dynamic UI

### Static UI

UI elements are **hardcoded** in the JSP/HTML — loaded at compile time. Called "static" because if values need to change tomorrow, someone has to manually update the UI components in the JSP.

- Options are written by hand
- Values are fixed
- No data comes from the backend

```jsp
<form:radiobutton path="gender" value="M" label="Male"/>
<form:radiobutton path="gender" value="F" label="Female"/>
```
"Male" and "Female" are written manually — nothing comes from the backend.

### Dynamic UI

UI elements are **generated from backend data** (the Model) — loaded at runtime. Called "dynamic" because if the backend values change tomorrow, the UI updates automatically, without touching the JSP.

- Data comes from the controller
- UI is created dynamically at runtime
- Useful for database-driven values

```java
@ModelAttribute("genders")
public List<String> getGenders() {
    return Arrays.asList("M", "F");
}
```

```jsp
<form:radiobuttons path="gender" items="${genders}"/>
```

Values come from the backend and can be changed without modifying the JSP.

### Comparison

| Static UI | Dynamic UI |
|---|---|
| Hardcoded in JSP | Comes from backend (Model) |
| Fixed values | Flexible / changeable |
| `<form:radiobutton>` | `<form:radiobuttons>` |
| Less reusable | More reusable |
