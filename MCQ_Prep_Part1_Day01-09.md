# QuantumCrew — MCQ Assessment Prep (Comprehensive)
### Covering Day 1 – Day 25 | For assessment on 7th Aug 2026
### Part 1 of 3 — Days 1 to 9

> Every named concept, annotation, method, and table entry from the training notes gets its own question. Correct answer is **bolded**.

---
## Day 1 — OOP Fundamentals

**Q1.** In a full stack application, which layer handles business logic and APIs?
A) Frontend  B) **Backend**  C) Database  D) None of these

**Q2.** A class is best described as:
A) A running instance in memory  B) **A blueprint defining fields and behavior**  C) A method  D) A database table

**Q3.** An object is:
A) A blueprint  B) **A concrete instance of a class**  C) A static method  D) An interface

**Q4.** Which OOP pillar restricts direct access to fields via `private` + getters/setters?
A) Inheritance  B) **Encapsulation**  C) Polymorphism  D) Abstraction

**Q5.** Which keyword lets a subclass reuse a superclass's fields and methods?
A) implements  B) **extends**  C) inherits  D) uses

**Q6.** Compile-time polymorphism is achieved through:
A) Method overriding  B) **Method overloading**  C) Interfaces  D) Abstract classes

**Q7.** Runtime polymorphism is achieved through:
A) Method overloading  B) **Method overriding**  C) Constructors  D) Static methods

**Q8.** Which annotation indicates a subclass method is overriding a superclass method?
A) @Override  B) **@Override** (same, only correct answer)  C) @Overload  D) @Super

**Q9.** Which is a valid primitive type in Java?
A) String  B) **int**  C) Object  D) ArrayList

**Q10.** Java is:
A) Dynamically typed  B) **Statically typed**  C) Untyped  D) Loosely typed only

**Q11.** What is the correct main method signature?
A) `public void main(String[] args)`  B) **`public static void main(String[] args)`**  C) `static main(String[] args)`  D) `void main(String args)`

**Q12.** Which of these is NOT a primitive type?
A) boolean  B) char  C) **String**  D) long

---
## Day 2 — Loops, Arrays, Abstraction & Interfaces

**Q1.** Which loop structure checks the condition before executing the body?
A) do-while  B) **for**  C) Both check after  D) Neither checks

**Q2.** Which loop is guaranteed to execute its body at least once?
A) for  B) while  C) **do-while**  D) for-each

**Q3.** The enhanced for-each loop is best used for:
A) Counting iterations manually  B) **Iterating over arrays/collections directly**  C) Infinite loops  D) Conditional branching

**Q4.** Arrays in Java have:
A) Dynamic size  B) **Fixed size**  C) No default values  D) Only primitive elements allowed

**Q5.** What is the default value of an `int` array element?
A) null  B) **0**  C) -1  D) undefined

**Q6.** How do you declare a 2D array in Java?
A) `int[2][] arr`  B) **`int[][] arr`**  C) `int arr[2,2]`  D) `array2D int[][]`

**Q7.** A constructor is used to:
A) Destroy an object  B) **Initialize an object's state upon creation**  C) Override a method  D) Import a package

**Q8.** Abstraction in Java is primarily achieved via:
A) Loops and arrays  B) **Abstract classes and interfaces**  C) Static methods only  D) Constructors

**Q9.** An abstract method:
A) Has a complete body  B) **Has no body — must be implemented by a subclass**  C) Cannot exist in an abstract class  D) Is always static

**Q10.** Which is TRUE about abstract classes vs interfaces?
A) Interfaces can have constructors  B) **Abstract classes support single inheritance via `extends`, interfaces support multiple via `implements`**  C) Abstract classes can't have concrete methods  D) Interfaces can't have default methods

**Q11.** Fields in an interface are implicitly:
A) private final  B) **public static final**  C) protected  D) package-private

**Q12.** Which keyword introduces a default method in an interface?
A) static  B) **default**  C) virtual  D) abstract

**Q13.** A static method inside an interface is called using:
A) An instance of the interface  B) **`InterfaceName.methodName()`**  C) `this.methodName()`  D) It cannot be called

**Q14.** What is `MAX_SPEED` in `interface Vehicle { int MAX_SPEED = 180; }` implicitly?
A) A regular int variable  B) **`public static final int`**  C) A private field  D) A constructor argument

**Q15.** Runtime polymorphism example: `Animal a = new Cat(); a.sound();` — which `sound()` executes?
A) Animal's version always  B) **Cat's overridden version**  C) Compilation error  D) Depends on IDE

---
## Day 3 — Coding Standards & Debugging

**Q1.** Coding standards primarily aim to make code:
A) Shorter  B) **Consistent, readable, maintainable, and less error-prone**  C) Faster to compile  D) Obfuscated

**Q2.** Which of these is NOT one of the 8 listed coding standard practices?
A) Meaningful variable names  B) Adequate documentation  C) **Maximizing code duplication**  D) Security checks

**Q3.** Maven's project structure philosophy is described as:
A) Configuration over Convention  B) **Convention over Configuration**  C) No configuration needed  D) Manual configuration only

**Q4.** Package names should follow which convention?
A) PascalCase  B) camelCase  C) **all lowercase, reverse domain**  D) UPPER_CASE

**Q5.** Class names should follow which convention?
A) camelCase  B) **PascalCase**  C) snake_case  D) kebab-case

**Q6.** `DataInputStream` is an example of correct:
A) camelCase  B) **PascalCase**  C) snake_case  D) UPPER_CASE

**Q7.** Method and variable names should follow:
A) PascalCase  B) **camelCase**  C) snake_case  D) UPPER_CASE

**Q8.** Constants and enums should be written in:
A) camelCase  B) PascalCase  C) **ALL CAPS**  D) lowercase

**Q9.** The standard Java indentation convention is:
A) 2 spaces  B) **4 spaces**  C) 1 tab (8 spaces)  D) No fixed rule

**Q10.** Which is the preferred way to use `Date`, instead of `java.util.Date d = new java.util.Date();`?
A) Keep it fully qualified always  B) **Use an `import` statement, then just `Date d = new Date();`**  C) Avoid using Date entirely  D) Use a static import

**Q11.** Which comment type is used to generate documentation automatically?
A) Single-line  B) Multi-line  C) **Javadoc**  D) Inline

**Q12.** Which Javadoc tag documents the return value of a method?
A) @param  B) **@return**  C) @throws  D) @see

**Q13.** Which Javadoc tag documents an exception a method might throw?
A) @param  B) @return  C) **@throws**  D) @since

**Q14.** Which Javadoc tag indicates the version a feature was introduced?
A) @version  B) **@since**  C) @author  D) @see

**Q15.** `// TODO` is used to indicate:
A) A known bug  B) **Work still pending**  C) Useful context  D) Deprecated code

**Q16.** `// FIXME` is used to indicate:
A) Pending work  B) **A known bug that needs fixing**  C) A completed task  D) A style suggestion

**Q17.** Which of these is a commenting best practice?
A) Comment every single line  B) **Explain why, not just what**  C) Never update comments  D) Avoid documenting public methods

**Q18.** Errors in Java (like `OutOfMemoryError`) occur at the level of:
A) The application only  B) **The JVM, and are usually unrecoverable**  C) The database  D) The network

**Q19.** Which is a checked exception?
A) NullPointerException  B) ArithmeticException  C) **FileNotFoundException**  D) ArrayIndexOutOfBoundsException

**Q20.** Checked exceptions are verified:
A) At runtime only  B) **At compile time**  C) Never  D) Only in production

**Q21.** Unchecked exceptions are verified:
A) At compile time  B) **At runtime**  C) Never  D) During code review only

**Q22.** What is a limitation of print-statement debugging?
A) It's too fast  B) **It clutters code and must be removed later**  C) It requires special tools  D) It's the most professional method

**Q23.** Which logging level indicates a critical failure?
A) INFO  B) WARNING  C) **SEVERE**  D) FINE

**Q24.** Which logging level provides the most detailed trace information?
A) INFO  B) CONFIG  C) FINE  D) **FINEST**

**Q25.** A key benefit of logging over print statements is:
A) It can't be disabled  B) **It can be disabled in production without code changes**  C) It's always faster  D) It requires no configuration

**Q26.** `if(age>18)` when it should check adulthood at 18 is an example of:
A) A syntax error  B) **A logical error**  C) A compile-time error  D) A runtime exception

**Q27.** What is the first step in problem isolation?
A) Identify root cause  B) **Reproduce the issue**  C) Test modules separately  D) Check inputs

**Q28.** In Eclipse, which shortcut resumes execution after a breakpoint?
A) F5  B) F6  C) F7  D) **F8**

**Q29.** In Eclipse, which shortcut performs "Step Into"?
A) **F5**  B) F6  C) F7  D) F8

**Q30.** In Eclipse, which shortcut terminates debugging?
A) F8  B) F5  C) **Ctrl+F2**  D) Ctrl+F5

---
## Day 4 — Code Quality & Static Analysis

**Q1.** Which of the following is NOT listed as a characteristic of good code?
A) Readable  B) Testable  C) **Highly duplicated**  D) Well documented

**Q2.** Static code analysis is performed:
A) During execution  B) **Without running the program**  C) Only after deployment  D) By the compiler only

**Q3.** Which tool is described as a free IDE plugin for static analysis?
A) SonarQube  B) **SonarLint**  C) JMeter  D) Eclipse MAT

**Q4.** `if(flag==true)` instead of `if(flag)` is flagged by SonarLint as a:
A) Bug  B) Vulnerability  C) **Code smell**  D) Security hotspot

**Q5.** `new ArrayList<String>()` instead of `new ArrayList<>()` is an example of:
A) A security hotspot  B) **A code smell (redundant type)**  C) A vulnerability  D) A bug

**Q6.** How many types of issues does SonarLint classify?
A) 2  B) 3  C) **4**  D) 6

**Q7.** Which SonarLint issue type requires manual security review rather than being automatically flagged as wrong?
A) Bug  B) Code smell  C) Vulnerability  D) **Security hotspot**

**Q8.** A "Bug" in SonarLint terms is:
A) A style preference  B) **Code that is demonstrably wrong**  C) A performance suggestion  D) A naming issue

**Q9.** A Quality Gate in SonarQube is used to:
A) Speed up compilation  B) **Define pass/fail release-readiness conditions for a project**  C) Replace unit tests  D) Generate Javadoc

**Q10.** Which of these would typically cause a Quality Gate to fail?
A) 0 new bugs  B) **Critical vulnerabilities present**  C) High test coverage  D) No code smells

**Q11.** SonarQube differs from SonarLint mainly by being:
A) Free only, no server  B) **A full server-based analysis platform** C) IDE-only  D) Limited to Java

**Q12.** "Less duplicated" code is considered:
A) A bad practice  B) **A characteristic of good code quality**  C) Irrelevant to quality  D) Only relevant for tests

---
## Day 5 — Multithreading & Exception Handling

**Q1.** The smallest unit of execution within a process is called a:
A) Process  B) **Thread**  C) Method  D) Object

**Q2.** Which method must be called to actually spawn a new thread of execution?
A) run()  B) **start()**  C) execute()  D) init()

**Q3.** Calling `run()` directly on a Thread object instead of `start()` will:
A) Start a new thread  B) **Execute in the current thread, not a new one**  C) Throw a compile error  D) Always fail

**Q4.** Which interface is generally preferred over extending `Thread` because it allows extending other classes too?
A) Callable  B) **Runnable**  C) Executor  D) Future

**Q5.** In Java 8+, a `Runnable` can be created using:
A) Only anonymous classes  B) **A lambda expression**  C) Only extending Thread  D) It cannot be simplified

**Q6.** What is the correct thread lifecycle order?
A) RUNNABLE → NEW → TERMINATED  B) **NEW → RUNNABLE → RUNNING → (BLOCKED/WAITING) → TERMINATED**  C) TERMINATED → NEW → RUNNING  D) RUNNING → NEW → RUNNABLE

**Q7.** The `synchronized` keyword is used to:
A) Speed up threads  B) **Prevent race conditions by allowing only one thread to execute a block at a time**  C) Kill a thread  D) Create a new thread

**Q8.** `wait()` and `notify()` are used for:
A) Starting threads  B) **Inter-thread communication**  C) Creating thread pools  D) Logging

**Q9.** `join()` is used to:
A) Merge two threads into one  B) **Make the calling thread wait for another thread to finish**  C) Start a thread  D) Kill a thread

**Q10.** A deadlock occurs when:
A) A single thread runs too fast  B) **Two or more threads wait on each other forever**  C) A thread finishes early  D) Memory runs out

**Q11.** `ExecutorService` is used to:
A) Replace exceptions  B) **Manage a pool of threads instead of creating them manually**  C) Log thread activity  D) Compile threads

**Q12.** An unrecoverable, serious JVM-level problem is called a(n):
A) Exception  B) **Error**  C) Warning  D) Bug

**Q13.** `10 / 0` for integers throws:
A) NullPointerException  B) **ArithmeticException**  C) ClassCastException  D) NumberFormatException

**Q14.** Which of these is a checked exception?
A) NullPointerException  B) ArithmeticException  C) **SQLException**  D) ArrayIndexOutOfBoundsException

**Q15.** The `finally` block:
A) Runs only if an exception occurs  B) Runs only if no exception occurs  C) **Always runs, exception or not**  D) Never runs

**Q16.** Which keyword declares that a method might throw a checked exception, without handling it there?
A) throw  B) **throws**  C) catch  D) finally

**Q17.** Which keyword is used to explicitly raise an exception in code?
A) **throw**  B) throws  C) raise  D) error

**Q18.** A custom exception class in Java typically extends:
A) RuntimeException always  B) **Exception (or RuntimeException)**  C) Error  D) Throwable directly, never Exception

**Q19.** In the hierarchy `Object → Throwable → ...`, what are the two direct children of `Throwable`?
A) Checked and Unchecked  B) **Exception and Error**  C) Runtime and Compile-time  D) Bug and Vulnerability

---
## Day 6 — Data Structures & Collections

**Q1.** Linear search requires the data to be:
A) Sorted  B) **In no particular order (works either way)**  C) In a HashMap  D) Numeric only

**Q2.** Binary search requires the data to be:
A) Unsorted  B) **Sorted**  C) In a linked list  D) Small only

**Q3.** Which sorting algorithm repeatedly compares adjacent elements and swaps them if out of order?
A) Selection Sort  B) **Bubble Sort**  C) Merge Sort  D) Radix Sort

**Q4.** Which sorting algorithm finds the smallest element and places it at the beginning, repeatedly?
A) Bubble Sort  B) **Selection Sort**  C) Insertion Sort  D) Quick Sort

**Q5.** Which sorting algorithm inserts each element into its correct position within the already-sorted part?
A) Selection Sort  B) **Insertion Sort**  C) Merge Sort  D) Radix Sort

**Q6.** Which sorting algorithm divides the array, sorts each part, then merges them?
A) Quick Sort  B) **Merge Sort**  C) Bubble Sort  D) Radix Sort

**Q7.** Which sorting algorithm picks a pivot and partitions the array recursively?
A) Merge Sort  B) **Quick Sort**  C) Insertion Sort  D) Radix Sort

**Q8.** Radix Sort sorts data by:
A) Comparing pairs of elements  B) **Digit by digit, starting from LSD or MSD**  C) Using a pivot  D) Merging sublists

**Q9.** Which List implementation is a legacy, synchronized class?
A) ArrayList  B) LinkedList  C) **Vector**  D) Stack (only, not Vector)

**Q10.** Which collection type does NOT allow duplicate elements?
A) List  B) **Set**  C) Queue  D) None of the above

**Q11.** Which Set implementation maintains sorted order?
A) HashSet  B) LinkedHashSet  C) **TreeSet**  D) ArraySet

**Q12.** Which principle does a Queue follow?
A) LIFO  B) **FIFO**  C) Random access  D) Sorted order

**Q13.** Which Map implementation maintains insertion order?
A) HashMap  B) **LinkedHashMap**  C) TreeMap (sorts, doesn't preserve insertion)  D) None do

**Q14.** How many null keys does `HashMap` allow?
A) 0  B) **1**  C) Unlimited  D) Depends on JVM

**Q15.** Which method returns all keys in a Map?
A) values()  B) entrySet()  C) **keySet()**  D) getKeys()

**Q16.** Which method returns key-value pairs from a Map for iteration?
A) keySet()  B) values()  C) **entrySet()**  D) pairs()

**Q17.** `Comparable` is used for:
A) Custom, external sort order  B) **A class's own natural sort order**  C) Only numeric types  D) Removing duplicates

**Q18.** `Comparator` is used for:
A) A class's natural order  B) **A custom sort order defined outside the class**  C) Only inside the class itself  D) Searching only

**Q19.** The method signature for `Comparable` is:
A) `int compare(T o1, T o2)`  B) **`int compareTo(T obj)`**  C) `boolean equals(T obj)`  D) `int sort(T obj)`

**Q20.** The method signature for `Comparator` is:
A) **`int compare(T o1, T o2)`**  B) `int compareTo(T obj)`  C) `boolean lessThan(T obj)`  D) `void sort(T obj)`

---
## Day 7 — Java 8 Features

**Q1.** A functional interface contains:
A) Multiple abstract methods  B) **Exactly one abstract method**  C) Only static methods  D) No methods at all

**Q2.** Which annotation marks a functional interface (optional but recommended)?
A) @Functional  B) **@FunctionalInterface**  C) @Lambda  D) @SingleMethod

**Q3.** A lambda expression has:
A) A name and return type  B) **No name, no explicit return type, no access modifier**  C) Only a return type  D) Mandatory access modifiers

**Q4.** The lambda operator is:
A) `=>`  B) **`->`**  C) `::`  D) `~>`

**Q5.** The method reference operator is:
A) **`::`**  B) `->`  C) `=>`  D) `#`

**Q6.** `Math::max` is an example of:
A) Instance method reference  B) **Static method reference**  C) Constructor reference  D) Lambda expression

**Q7.** `str::toUpperCase` is an example of:
A) Static method reference  B) **Instance method reference**  C) Constructor reference  D) Field reference

**Q8.** `ArrayList::new` is an example of:
A) Static method reference  B) Instance method reference  C) **Constructor reference**  D) Field reference

**Q9.** Which functional interface takes one input and returns a boolean?
A) Function  B) Consumer  C) **Predicate**  D) Supplier

**Q10.** Which functional interface takes one input and produces a different-typed output?
A) Predicate  B) **Function<T,R>**  C) Consumer  D) Supplier

**Q11.** Which functional interface takes an input and returns nothing?
A) Supplier  B) Function  C) **Consumer**  D) Predicate

**Q12.** Which functional interface takes no input but returns a value?
A) Consumer  B) Predicate  C) **Supplier**  D) Function

**Q13.** Which functional interface has the same input and output type (single argument)?
A) BinaryOperator  B) **UnaryOperator**  C) Function  D) Predicate

**Q14.** Which functional interface takes two inputs of the same type and returns that same type?
A) UnaryOperator  B) **BinaryOperator**  C) Function  D) BiPredicate

**Q15.** Which of these is an intermediate Stream operation?
A) collect()  B) count()  C) **filter()**  D) reduce()

**Q16.** Which of these is a terminal Stream operation?
A) map()  B) sorted()  C) distinct()  D) **collect()**

**Q17.** How many terminal operations can be chained at the end of a stream?
A) As many as needed  B) **Only one**  C) Exactly two  D) Zero

**Q18.** What does `Optional<T>` primarily help avoid?
A) ArithmeticException  B) **NullPointerException**  C) ClassCastException  D) IOException

**Q19.** Which method retrieves an Optional's value or a fallback default?
A) get()  B) **orElse()**  C) getOrDefault()  D) fetch()

**Q20.** `Arrays.stream(arr)` is used to:
A) Sort an array  B) **Create a Stream from an array**  C) Convert a Stream to an array  D) Filter an array

---
## Day 8 — Java 11 Features

**Q1.** Java 11 is classified as:
A) A minor patch  B) **An LTS release**  C) A preview-only release  D) Deprecated

**Q2.** Since 2017, Java follows a release cycle of:
A) 12 months  B) **6 months**  C) 3 months  D) 24 months

**Q3.** Which of these Java versions is LTS?
A) Java 9  B) Java 10  C) **Java 17**  D) Java 18

**Q4.** A JEP is:
A) A database driver  B) **A Java Enhancement Proposal describing a new feature**  C) A testing framework  D) A build tool

**Q5.** A JSR is:
A) A Java runtime  B) **A Java Specification Request, standardizing APIs**  C) A logging tool  D) A GC algorithm

**Q6.** JDEP has been replaced by:
A) JSR  B) **JEP**  C) JLS  D) JDK

**Q7.** Which Java 11 API allows asynchronous HTTP calls, standardized into the JDK?
A) File API  B) **HTTP Client API**  C) Socket API  D) Stream API

**Q8.** In Java 11, lambda parameters can use which keyword for local variable syntax?
A) auto  B) **var**  C) let  D) dynamic

**Q9.** Which Java 11 String method checks whether a string is empty or all whitespace?
A) isEmpty()  B) **isBlank()**  C) trim()  D) isNull()

**Q10.** Which Java 11 String method repeats a string N times?
A) copy()  B) duplicate()  C) **repeat()**  D) times()

**Q11.** Which Java 11 String method removes leading/trailing whitespace (Unicode-aware)?
A) trim()  B) **strip()**  C) clean()  D) blank()

**Q12.** Which Java 11 method reads an entire file into a String directly?
A) `Files.read()`  B) **`Files.readString()`**  C) `Files.load()`  D) `Files.getText()`

**Q13.** In Java 11, you can run a single `.java` file:
A) Only after separate compilation  B) **Directly with `java Demo.java`**  C) Never without an IDE  D) Only if it's under 10 lines

**Q14.** The Epsilon Garbage Collector in Java 11 is used for:
A) Production memory optimization  B) **Performance/memory-pressure testing (it never reclaims memory)**  C) Multi-threaded apps only  D) Replacing G1

**Q15.** Nest-Based Access Control in Java 11 allows:
A) External classes to access private members  B) **Nested classes to directly access each other's private members**  C) Removal of access modifiers  D) Public-only access

**Q16.** `Predicate.not()` is used to:
A) Create a new Predicate B) **Negate an existing Predicate/method reference** C) Combine two predicates  D) Convert Predicate to Function

**Q17.** Which Java feature/version introduced Generics, annotations, and the enhanced for-loop?
A) Java 8  B) **Java 5**  C) Java 9  D) Java 11

**Q18.** Which Java version introduced the Module System?
A) Java 8  B) **Java 9**  C) Java 11  D) Java 17

**Q19.** Which Java version introduced Virtual Threads and Record Patterns?
A) Java 17  B) **Java 21**  C) Java 11  D) Java 25

---
## Day 9 — Java 17 Features, Testing & JUnit 5

**Q1.** `jdeps` is used to:
A) Compile code  B) **Analyze class/package-level dependencies**  C) Run tests  D) Package a JAR

**Q2.** JLS stands for:
A) Java Logging Spec  B) **Java Language Specification**  C) Java Library System  D) Java Lifecycle Spec

**Q3.** Sealed classes (Java 17) are used to:
A) Prevent all inheritance  B) **Restrict exactly which classes can extend/implement a type**  C) Make a class final only  D) Enable multiple inheritance

**Q4.** Which keyword is used with sealed classes to list allowed subclasses?
A) allows  B) **permits**  C) extends-only  D) restrict

**Q5.** `if (obj instanceof String s)` in Java 17 demonstrates:
A) A syntax error  B) **Pattern matching for instanceof**  C) Reflection  D) Sealed classes

**Q6.** Text blocks in Java are delimited by:
A) Single quotes  B) Double quotes  C) **Triple double-quotes (`"""`)**  D) Backticks

**Q7.** In TDD, what is the correct 3-step cycle?
A) Green-Refactor-Red  B) **Red-Green-Refactor**  C) Refactor-Green-Red  D) Red-Refactor-Green

**Q8.** In TDD's "Red" step, you:
A) Refactor code  B) **Write a failing test**  C) Deploy the app  D) Delete old tests

**Q9.** Which JUnit 5 annotation marks a test method?
A) @TestCase  B) **@Test**  C) @UnitTest  D) @Check

**Q10.** Which JUnit 5 annotation runs before EVERY test method?
A) @BeforeAll  B) **@BeforeEach**  C) @Before  D) @Setup

**Q11.** Which JUnit 5 annotation runs ONCE before all tests, and must be static?
A) @BeforeEach  B) **@BeforeAll**  C) @Before  D) @Init

**Q12.** Which JUnit 5 annotation skips a test?
A) @Ignore  B) @Skip  C) **@Disabled**  D) @Off

**Q13.** Which JUnit 5 assertion checks that an exception is thrown?
A) **assertThrows**  B) assertException  C) expectThrows  D) verifyThrows

**Q14.** `assumeTrue(...)` is used to:
A) Fail a test immediately  B) **Skip a test unless a precondition holds**  C) Assert equality  D) Mock a dependency

**Q15.** Which legacy JUnit 4 annotation is equivalent to JUnit 5's `@BeforeEach`?
A) @BeforeAll  B) **@Before**  C) @Init  D) @Setup

**Q16.** Which method asserts that two values are equal in JUnit 5?
A) isEqual()  B) **assertEquals()**  C) checkEqual()  D) same()
