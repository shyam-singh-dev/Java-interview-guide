<div align="center">

# ☕ Core Java + Advanced Java — Complete Interview Guide (Hinglish)
### Zero Se Placement/Job Tak — Har Topic Deep Mein, Interview-Ready Q&A Ke Saath

> OOPs se leke Spring Boot, Collections se leke Microservices —  
> sab kuch ek jagah, real interview questions ke saath.

</div>

---

## Table of Contents

### Core Java
1. [Java Basics — JVM, JRE, JDK, JIT](#1-java-basics)
2. [OOPs Concepts — Deep Dive](#2-oops-concepts)
3. [Data Types, Variables & Operators](#3-data-types-variables)
4. [Control Flow Statements](#4-control-flow)
5. [Strings in Java — String Pool, Immutability, StringBuilder vs StringBuffer](#5-strings)
6. [Arrays & Varargs](#6-arrays)
7. [Exception Handling — Complete Guide](#7-exception-handling)
8. [equals() & hashCode() — Contract & Pitfalls](#8-equals-hashcode)
9. [Comparable vs Comparator](#9-comparable-vs-comparator)
10. [Collections Framework — Deep Dive](#10-collections-framework)
11. [Generics in Java](#11-generics)
12. [Java 8 Features — Lambda, Stream, Optional, Date/Time](#12-java-8-features)
13. [File I/O & Serialization](#13-file-io)
14. [Reflection & Annotations](#14-reflection-annotations)
15. [Garbage Collection — How It Works](#15-garbage-collection)
16. [Java Memory Model (JMM) — Brief](#16-jmm-brief)

### Advanced Java / Frameworks
17. [JDBC — Java Database Connectivity](#17-jdbc)
18. [Servlet & JSP Basics](#18-servlet-jsp)
19. [Design Patterns — Most Asked](#19-design-patterns)
20. [Maven & Gradle Basics](#20-maven-gradle)
21. [JUnit & Mockito — Unit Testing](#21-junit-mockito)

### Spring Ecosystem
22. [Spring Core — IOC, DI, Bean Lifecycle](#22-spring-core)
23. [Spring AOP — Aspect-Oriented Programming](#23-spring-aop)
24. [Spring Boot — Auto-Configuration, Starters, Actuator](#24-spring-boot)
25. [Spring Data JPA & Hibernate](#25-spring-data-jpa)
26. [Spring Transactions — @Transactional Deep Dive](#26-spring-transactions)
27. [Spring Security — JWT, OAuth2 Basics](#27-spring-security)
28. [REST API Design — Best Practices](#28-rest-api-design)
29. [Microservices Architecture](#29-microservices)
30. [Caching — Redis Basics](#30-caching)
31. [Message Queues — Kafka/RabbitMQ Basics](#31-message-queues)

---

# PART 1: CORE JAVA

---

# 1. Java Basics — JVM, JRE, JDK, JIT

## 1.1 JVM (Java Virtual Machine)

JVM ek abstract machine hai jo Java bytecode ko execute karti hai. Ye platform-independent hai — same `.class` file Windows pe bhi chalegi, Linux pe bhi, Mac pe bhi.

```
Java Source (.java)
    │ javac
    ▼
Bytecode (.class)
    │ JVM loads
    ▼
JIT Compiler → Native Machine Code
    ▼
CPU executes
```

**JVM ke components:**
- **Class Loader**: `.class` files ko load karta hai memory mein
- **Runtime Data Areas**: Method Area, Heap, Stack, PC Register, Native Method Stack
- **Execution Engine**: Interpreter + JIT Compiler + Garbage Collector

## 1.2 JRE (Java Runtime Environment)

JRE = JVM + Libraries (rt.jar) + Other files. Ye sirf Java programs **run** karne ke liye hai. Development ke liye nahi.

## 1.3 JDK (Java Development Kit)

JDK = JRE + Development Tools (javac, javadoc, jar, debugger, etc.). Agar tum Java code **compile** aur **run** dono karna chahte ho, to JDK chahiye.

```
JDK
├── JRE
│   ├── JVM
│   └── Libraries
└── Development Tools (javac, javadoc, etc.)
```

## 1.4 JIT (Just-In-Time) Compiler

Interpreter bytecode ko line-by-line execute karta hai — slow hota hai. JIT "hot" methods (jo frequently call hote hain) ko native machine code mein compile kar deta hai. Next time wo method call hota hai, to directly machine code execute hota hai — much faster.

**JIT vs Interpreter:**
| Aspect | Interpreter | JIT Compiler |
|--------|-------------|--------------|
| Speed | Slow (line-by-line) | Fast (compiled code) |
| Memory | Less | More (compiled code cache) |
| Startup | Fast | Slower (compilation overhead) |
| When | Cold methods | Hot methods |

---

## Interview Q&A

**Q: JDK, JRE, aur JVM mein kya farq hai?**

JVM = Java bytecode execute karne wali virtual machine. JRE = JVM + Libraries (run Java apps). JDK = JRE + Development tools (compile + run + debug Java apps). Simple analogy: JVM = engine, JRE = car, JDK = car + garage + tools.

**Q: Java platform-independent kaise hota hai?**

Java source code ko `javac` se platform-independent bytecode (`.class`) mein compile karte hain. Ye bytecode kisi bhi OS pe JVM ke through run ho sakta hai. "Write Once, Run Anywhere" (WORA) principle.

**Q: JIT compiler ka kaam kya hai?**

JIT frequently executed methods (hot methods) ko runtime pe native machine code mein compile karta hai aur cache kar deta hai. Agla call pe directly cached machine code execute hota hai, bajaye bytecode interpret karne ke. Isse performance significantly improve hoti hai.

**Q: Can we have multiple main methods in a single Java class?**

Haan, method overloading ke through — different parameters ke saath. Lekin `public static void main(String[] args)` hi JVM entry point hai. Baaki overloaded main methods normal methods ki tarah treat hote hain.

**Q: Why is Java not 100% object-oriented?**

Java primitive types (int, char, boolean, etc.) ko directly support karti hai — ye objects nahi hain. Also, static methods/variables class se associated hote hain, object se nahi. Pure OOP languages mein sab kuch object hota hai (jaise Smalltalk).

---

# 2. OOPs Concepts — Deep Dive

## 2.1 Encapsulation (Data Hiding)

Data aur methods ko ek unit (class) mein bundle karna, aur data ko direct access se protect karna using private access modifier + getters/setters.

```java
public class BankAccount {
    private double balance;  // direct access nahi

    public double getBalance() { return balance; }

    public void deposit(double amount) {
        if (amount > 0) {
            this.balance += amount;
        }
    }
}
```

**Benefits:**
- Data validation possible hai (setters mein)
- Implementation details hide ho jate hain
- Loose coupling — internal changes se external code affect nahi hota

## 2.2 Inheritance (IS-A Relationship)

Ek class doosri class ki properties aur methods inherit kar sakti hai using `extends` keyword.

```java
class Animal {
    void eat() { System.out.println("Eating..."); }
}

class Dog extends Animal {  // Dog IS-A Animal
    void bark() { System.out.println("Barking..."); }
}
```

**Types:**
- **Single**: Class A extends Class B
- **Multilevel**: A → B → C
- **Hierarchical**: A → B, A → C
- **Multiple**: Java mein classes ke liye nahi (diamond problem), interfaces ke liye haan

## 2.3 Polymorphism (Many Forms)

Same action different ways mein perform ho sakti hai.

**Compile-time (Method Overloading):**
```java
class Calculator {
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
    int add(int a, int b, int c) { return a + b + c; }
}
```

**Runtime (Method Overriding):**
```java
class Animal {
    void sound() { System.out.println("Some sound"); }
}

class Dog extends Animal {
    @Override
    void sound() { System.out.println("Bark"); }  // runtime pe decide hoga
}

Animal a = new Dog();
a.sound();  // "Bark" — runtime polymorphism
```

## 2.4 Abstraction (Hiding Complexity)

Implementation details hide karke sirf functionality show karna.

**Abstract Class:**
```java
abstract class Shape {
    abstract void draw();  // no body — subclass implement karegi
    void display() { System.out.println("Displaying shape"); }
}
```

**Interface:**
```java
interface Drawable {
    void draw();  // implicitly public abstract
    default void print() { System.out.println("Printing..."); }  // Java 8+
}
```

**Abstract Class vs Interface:**
| Feature | Abstract Class | Interface |
|---------|---------------|-----------|
| Methods | Abstract + Concrete | Abstract (Java 7), Default/Static (Java 8+) |
| Variables | Instance variables | public static final (constants) |
| Constructor | Yes | No |
| Multiple Inheritance | No | Yes |
| Access Modifiers | Any | public (implicitly) |

---

## Interview Q&A

**Q: Encapsulation aur Abstraction mein kya farq hai?**

Encapsulation = data ko hide karna (private fields + getters/setters). Abstraction = implementation details ko hide karna (abstract classes/interfaces). Encapsulation "how to protect data" batata hai, Abstraction "what to show" batata hai.

**Q: Method Overloading aur Overriding mein kya farq hai?**

Overloading = same method name, different parameters, same class mein. Compile-time polymorphism. Overriding = same method name + same parameters, parent-child class mein. Runtime polymorphism. Overloading mein return type different ho sakta hai, Overriding mein same ya covariant return type chahiye.

**Q: Can we override static methods?**

Nahi. Static methods class level pe belong karte hain, object level pe nahi. Tum unhe "hide" kar sakte ho (same signature parent mein aur child mein), lekin ye overriding nahi hai. Runtime polymorphism static methods pe kaam nahi karti.

**Q: Why Java doesn't support multiple inheritance in classes?**

Diamond problem. Agar Class A mein method `show()` hai, aur Class B aur Class C dono A ko extend karte hain, aur Class D B aur C dono ko extend karta hai — to D ko `show()` kiska call karna chahiye? Ambiguity. Java mein classes ke liye multiple inheritance nahi hai, lekin interfaces ke through possible hai.

**Q: Interface mein default method kyun introduce hua Java 8 mein?**

Backward compatibility. Agar ek interface mein naya method add karna hai, to saari implementing classes break ho jati hain. Default method se interface mein method add kar sakte hain bina existing classes ko break kiye.

**Q: Can an interface extend another interface?**

Haan, interface multiple interfaces extend kar sakta hai. `interface A extends B, C {}` — ye allowed hai kyunki interface mein sirf method declarations hain, implementation nahi.

**Q: Abstract class ka object kyun nahi ban sakta?**

Abstract class incomplete hoti hai — usme abstract methods hain jinka body nahi hai. JVM ko pata nahi ki un methods ka actual implementation kya hoga. Isliye instantiation allowed nahi hai.

---

# 3. Data Types, Variables & Operators

## 3.1 Primitive Data Types

| Type | Size | Default Value | Range |
|------|------|---------------|-------|
| byte | 1 byte | 0 | -128 to 127 |
| short | 2 bytes | 0 | -32,768 to 32,767 |
| int | 4 bytes | 0 | -2³¹ to 2³¹-1 |
| long | 8 bytes | 0L | -2⁶³ to 2⁶³-1 |
| float | 4 bytes | 0.0f | ~6-7 decimal digits |
| double | 8 bytes | 0.0d | ~15 decimal digits |
| char | 2 bytes | '\u0000' | 0 to 65,535 (Unicode) |
| boolean | 1 bit (JVM dependent) | false | true/false |

## 3.2 Wrapper Classes

Primitive types ke object versions. Java 5 se autoboxing/unboxing automatic hai.

```java
Integer i = 10;      // autoboxing: int → Integer
int x = i;           // unboxing: Integer → int
```

**Primitive vs Wrapper:**
- Primitives stack pe store hote hain (fast), Wrapper objects heap pe (slow)
- Primitives default values hain, Wrappers null ho sakte hain
- Collections (ArrayList, HashMap) mein sirf Wrappers use kar sakte hain

## 3.3 Type Casting

**Implicit (Widening):** chhote type se bade type mein automatic
```java
int i = 100;
long l = i;  // automatic
```

**Explicit (Narrowing):** bade type se chhote type mein manually
```java
long l = 100;
int i = (int) l;  // manual cast — data loss possible
```

---

## Interview Q&A

**Q: int aur Integer mein kya farq hai?**

`int` primitive type hai — stack pe store hota hai, fast hai, null nahi ho sakta. `Integer` wrapper class hai — heap pe object banata hai, null ho sakta hai, collections mein use hota hai. Autoboxing/unboxing se dono interchangeably use kar sakte hain.

**Q: Why char is 2 bytes in Java?**

Java Unicode support karta hai (UTF-16). ASCII sirf 128 characters support karta hai, lekin Unicode 65,535+ characters support karta hai (including Hindi, Chinese, Arabic, etc.). Isliye 2 bytes chahiye.

**Q: float aur double mein kya farq hai?**

`float` 4 bytes (32-bit), ~7 decimal digits precision. `double` 8 bytes (64-bit), ~15 decimal digits precision. Financial calculations ke liye `BigDecimal` use karo — floating point precision issues hote hain.

```java
System.out.println(0.1 + 0.2);  // 0.30000000000000004 — floating point issue!
```

**Q: What happens if we don't initialize a local variable?**

Compile error. Local variables ka koi default value nahi hoti. Tumhe explicitly initialize karna padta hai. Instance variables ka default value hota hai (0, false, null).

**Q: `==` vs `.equals()` for Strings?**

`==` reference compare karta hai (same object hai?). `.equals()` content compare karta hai (same characters hai?). String literals ko String pool mein reuse kiya jata hai, isliye `==` sometimes true de deta hai literals ke liye, lekin `new String()` ke liye false.

```java
String s1 = "hello";
String s2 = "hello";
String s3 = new String("hello");

System.out.println(s1 == s2);  // true (same pool reference)
System.out.println(s1 == s3);  // false (different heap objects)
System.out.println(s1.equals(s3));  // true (same content)
```

---

# 4. Control Flow Statements

## 4.1 if-else-if ladder

```java
if (condition1) {
    // code
} else if (condition2) {
    // code
} else {
    // default
}
```

## 4.2 switch-case

Java 7+ mein Strings allowed hain. Java 12+ mein `switch` expressions.

```java
// Traditional
switch (day) {
    case 1: System.out.println("Monday"); break;
    case 2: System.out.println("Tuesday"); break;
    default: System.out.println("Other");
}

// Java 12+ Switch Expression
String result = switch (day) {
    case 1, 2, 3, 4, 5 -> "Weekday";
    case 6, 7 -> "Weekend";
    default -> throw new IllegalArgumentException();
};
```

## 4.3 Loops

```java
// for loop
for (int i = 0; i < 10; i++) { }

// enhanced for-each
for (String s : list) { }

// while
while (condition) { }

// do-while (at least once execute hota hai)
do { } while (condition);
```

## 4.4 break, continue, return

- `break`: loop ya switch se bahar nikalo
- `continue`: current iteration skip karo, next pe jao
- `return`: method se value ke saath ya bina wapas jao

---

## Interview Q&A

**Q: `break` aur `continue` mein kya farq hai?**

`break` loop/switch se completely bahar nikalti hai. `continue` sirf current iteration skip karti hai, loop ke next iteration pe jump karti hai.

**Q: Can we use `String` in switch-case?**

Java 7 se haan. Pehle sirf int, char, short, byte, enum allowed thi. Java 12+ mein switch expressions bhi aaye hain jo multiple cases ko comma se separate kar sakte hain aur arrow syntax (`->`) support karte hain.

**Q: `for` vs `while` vs `do-while` — kab kya use karein?**

`for` jab iterations fixed/known hain. `while` jab condition-based loop chahiye aur pehle check karna hai. `do-while` jab at least ek baar loop body chalani hai chahe condition false ho.

---

# 5. Strings in Java — String Pool, Immutability, StringBuilder vs StringBuffer

## 5.1 String Immutability

Java mein `String` objects immutable hain — ek baar create hone ke baad unka content change nahi ho sakta. Har "modification" naya String object banata hai.

```java
String s = "hello";
s = s + " world";  // "hello world" naya object hai, purana "hello" garbage collect hoga
```

**Why immutable?**
1. **String Pool**: Same literals reuse hote hain, memory save hoti hai
2. **Security**: Passwords aur sensitive data change nahi ho sakte
3. **Thread Safety**: Multiple threads safely share kar sakte hain bina synchronization ke
4. **HashCode Caching**: HashCode ek baar compute ho kar cache ho jata hai (HashMap performance)

## 5.2 String Pool

String literals String Pool (Method Area/Heap mein) mein store hote hain. Same literal ko reuse kiya jata hai.

```java
String s1 = "hello";  // pool mein create hua
String s2 = "hello";  // pool se reuse kiya gaya
String s3 = new String("hello");  // heap pe naya object

System.out.println(s1 == s2);  // true (same pool reference)
System.out.println(s1 == s3);  // false (different objects)
```

`intern()` method explicitly String Pool mein add kar sakti hai:
```java
String s4 = s3.intern();  // pool mein reference return karega
System.out.println(s1 == s4);  // true
```

## 5.3 StringBuilder vs StringBuffer

| Feature | StringBuilder | StringBuffer |
|---------|---------------|--------------|
| Thread-Safe | No | Yes (synchronized methods) |
| Speed | Faster | Slower (locking overhead) |
| Introduced | Java 5 | Java 1.0 |
| Use Case | Single thread | Multiple threads |

```java
// StringBuilder — faster, not thread-safe
StringBuilder sb = new StringBuilder();
sb.append("Hello").append(" ").append("World");
String result = sb.toString();

// StringBuffer — thread-safe, slower
StringBuffer sbf = new StringBuffer();
sbf.append("Hello").append(" ").append("World");
```

**Rule:** Single-threaded code mein hamesha `StringBuilder` use karo. `StringBuffer` sirf tab jab multiple threads same object modify kar rahe hain.

---

## Interview Q&A

**Q: String immutable kyun hai?**

Security (sensitive data change nahi ho sakta), String Pool (reuse possible), Thread Safety (bina sync ke share kar sakte hain), aur HashCode caching (HashMap performance). Agar String mutable hoti, to ek thread ne change kiya to doosre thread ko stale data dikhta.

**Q: `new String("hello")` aur `"hello"` mein kya farq hai?**

`"hello"` String Pool mein create hota hai (ya reuse hota hai). `new String("hello")` heap pe naya object banata hai, chahe pool mein same string already ho. `new String()` extra memory use karta hai — generally avoid karo unless specific reason ho.

**Q: String concatenation loop mein kyun slow hoti hai?**

```java
String s = "";
for (int i = 0; i < 10000; i++) {
    s += i;  // HAR BAAR naya String object ban raha hai!
}
```

`+` operator strings ko concatenate karne ke liye internally `StringBuilder` use karta hai, lekin har iteration mein naya `StringBuilder` aur naya `String` object ban raha hai. 10,000 iterations = 10,000 objects. Iske bajaye directly `StringBuilder` use karo.

**Q: `StringBuilder` ka capacity kya hoti hai?**

Default capacity 16 characters. Jab append karne se capacity exceed hoti hai, to capacity double ho jati hai + 2 (`oldCapacity * 2 + 2`). Ye array copy involve karta hai, isliye initial capacity estimate karna achha practice hai.

```java
StringBuilder sb = new StringBuilder(100);  // initial capacity 100
```

**Q: `String.join()` ka use kab karein?**

Java 8 se. Multiple strings ko delimiter ke saath join karne ke liye:
```java
String result = String.join(", ", "A", "B", "C");  // "A, B, C"
List<String> list = Arrays.asList("A", "B", "C");
String result = String.join(", ", list);
```

---

# 6. Arrays & Varargs

## 6.1 Arrays

Fixed-size, same-type elements. Stack mein reference, heap mein actual array.

```java
int[] arr = new int[5];           // default 0 se initialize
int[] arr2 = {1, 2, 3, 4, 5};   // direct initialization
int[][] matrix = new int[3][3];  // 2D array
```

**Arrays class utilities:**
```java
Arrays.sort(arr);           // quicksort/dual-pivot quicksort
Arrays.binarySearch(arr, 5); // sorted array mein search
Arrays.fill(arr, 0);        // sab elements 0 se fill
Arrays.toString(arr);       // [1, 2, 3] format
Arrays.equals(arr1, arr2);  // content compare
Arrays.copyOf(arr, 10);     // copy with new length
```

## 6.2 Varargs (Variable Arguments)

Java 5 se. Method ko variable number of arguments pass karne deta hai. Internally array ban jata hai.

```java
public void printNames(String... names) {
    for (String name : names) {
        System.out.println(name);
    }
}

// Call karo:
printNames("A", "B");
printNames("A", "B", "C", "D");
```

**Rules:**
- Varargs hamesha last parameter hona chahiye
- Ek method mein sirf ek varargs parameter ho sakta hai

---

## Interview Q&A

**Q: ArrayList aur Array mein kya farq hai?**

Array fixed-size hota hai, resize nahi ho sakta. `ArrayList` dynamic size hota hai — internally array use karta hai, lekin jab full hota hai to new array (1.5x size) banata hai aur elements copy karta hai. Array primitive types aur objects dono store kar sakta hai, `ArrayList` sirf objects (autoboxing se primitives bhi).

**Q: Can we increase array size after initialization?**

Nahi. Array ka size fixed hota hai. Agar zyada chahiye, to naya array bana kar elements copy karne padte hain (exactly `ArrayList` kya karta hai internally).

**Q: `Arrays.asList()` mein kya gotcha hai?**

Ye fixed-size list return karta hai. `add()` ya `remove()` call karne se `UnsupportedOperationException` aata hai. Mutable list chahiye to `new ArrayList<>(Arrays.asList(arr))` use karo.

---

# 7. Exception Handling — Complete Guide

## 7.1 Exception Hierarchy

```
Throwable
├── Error (unchecked)          → Serious problems, don't catch
│   ├── OutOfMemoryError
│   ├── StackOverflowError
│   └── ...
└── Exception
    ├── RuntimeException (unchecked) → Programming errors
    │   ├── NullPointerException
    │   ├── ArrayIndexOutOfBoundsException
    │   ├── IllegalArgumentException
    │   ├── ClassCastException
    │   └── ...
    └── Checked Exception        → Must handle or declare
        ├── IOException
        ├── SQLException
        ├── FileNotFoundException
        └── ...
```

## 7.2 try-catch-finally

```java
try {
    // risky code
    int result = 10 / 0;
} catch (ArithmeticException e) {
    // specific exception handle
    System.out.println("Cannot divide by zero");
} catch (Exception e) {
    // general exception
    e.printStackTrace();
} finally {
    // hamesha execute hota hai (chahe exception aaye ya na aaye)
    System.out.println("Cleanup code");
}
```

## 7.3 try-with-resources (Java 7+)

AutoCloseable resources ke liye. `finally` mein manually close karne ki zaroorat nahi.

```java
try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
    String line = br.readLine();
} catch (IOException e) {
    e.printStackTrace();
}
// br automatically close ho jayega
```

## 7.4 throw vs throws

- `throw`: explicitly exception throw karna (method body mein)
- `throws`: method declaration mein batana ki ye method kya-kya exceptions throw kar sakti hai

```java
public void validateAge(int age) throws IllegalArgumentException {
    if (age < 0) {
        throw new IllegalArgumentException("Age cannot be negative");
    }
}
```

## 7.5 Custom Exceptions

```java
public class InsufficientFundsException extends Exception {
    public InsufficientFundsException(String message) {
        super(message);
    }
}
```

---

## Interview Q&A

**Q: Checked vs Unchecked Exception mein kya farq hai?**

Checked exceptions compile-time pe check hote hain. Tumhe ya to `try-catch` se handle karna padta hai ya method signature mein `throws` declare karna padta hai. Unchecked exceptions (RuntimeException) runtime pe aate hain, compiler force nahi karta. Checked = recoverable (IOException), Unchecked = programming bugs (NullPointerException).

**Q: `finally` block kab execute nahi hota?**

1. `System.exit()` call hone pe
2. JVM crash hone pe
3. `finally` block se pehle infinite loop ya deadlock ho to
4. Power failure / OS kill signal

**Q: `try` ke bina `catch` ya `finally` chalega?**

Nahi. `catch` ya `finally` hamesha `try` ke saath chahiye. Lekin `try` sirf `finally` ke saath bhi ho sakta hai (bina `catch` ke).

**Q: Can we catch `Error`?**

Haan, technically possible hai (`catch (Error e)`), lekin recommended nahi. Errors serious problems indicate karte hain (OutOfMemory, StackOverflow) jo generally recover nahi ho sakte. Unhe catch karne se application unstable state mein chal sakti hai.

**Q: `Exception` catch karne ke baad specific exception catch kar sakte hain?**

Nahi, compile error aayega. Specific exceptions hamesha general exception se pehle catch karne chahiye. `catch (Exception e)` ke baad `catch (IOException e)` unreachable ho jayega.

**Q: `try-with-resources` mein multiple resources kaise use karein?**

```java
try (BufferedReader br = new BufferedReader(new FileReader("in.txt"));
     BufferedWriter bw = new BufferedWriter(new FileWriter("out.txt"))) {
    // code
}
```

Resources semicolon (`;`) se separate hote hain. Closing order reverse order mein hota hai (bw pehle close, phir br).

---

# 8. equals() & hashCode() — Contract & Pitfalls

## 8.1 The Contract

Java mein `equals()` aur `hashCode()` ka ek strict contract hai:

1. **Reflexive**: `x.equals(x)` → `true`
2. **Symmetric**: `x.equals(y)` ↔ `y.equals(x)`
3. **Transitive**: `x.equals(y)` && `y.equals(z)` → `x.equals(z)`
4. **Consistent**: Multiple calls same result
5. **Null**: `x.equals(null)` → `false`

**hashCode Contract:**
- Equal objects → **must** have same hashCode
- Unequal objects → **can** have same hashCode (collision)

## 8.2 Why Override Together?

Agar tum `equals()` override karo lekin `hashCode()` nahi, to `HashMap`/`HashSet` mein objects galat behave karenge.

```java
public class Person {
    private String name;
    private int age;

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Person person = (Person) o;
        return age == person.age && Objects.equals(name, person.name);
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, age);  // Java 7+ utility
    }
}
```

## 8.3 What Happens If Only equals() is Overridden?

```java
// Without hashCode():
Person p1 = new Person("Alice", 25);
Person p2 = new Person("Alice", 25);

Set<Person> set = new HashSet<>();
set.add(p1);
set.add(p2);

System.out.println(set.size());  // 2 (should be 1!) — different hashCodes
```

`HashSet` pehle `hashCode()` check karta hai. Different hashCodes → different buckets → dono store ho jate hain. `equals()` kabhi call hi nahi hota!

---

## Interview Q&A

**Q: `==` vs `equals()` mein kya farq hai?**

`==` reference/memory address compare karta hai. `equals()` content/value compare karta hai (unless overridden). `Object` class mein `equals()` internally `==` hi use karta hai. `String`, `Integer` etc. ne `equals()` override kiya hai.

**Q: `hashCode()` kyun override karna chahiye jab `equals()` override kiya?**

Kyunki hash-based collections (`HashMap`, `HashSet`, `HashTable`) pehle `hashCode()` se bucket decide karte hain, phir `equals()` se equality check. Agar `equals()` true lekin `hashCode()` different, to same object different buckets mein jayega — duplicate entries, lost lookups.

**Q: Two different objects can have same hashCode?**

Haan, ye "hash collision" kehlata hai. Different objects same bucket mein jate hain, phir `equals()` se distinguish hote hain (linked list ya tree se). Isliye hashCode distribution achha hona chahiye.

**Q: `Objects.equals()` vs `==` for null-safe comparison?**

```java
Objects.equals(a, b);  // null-safe — dono null ho to true, ek null ho to false
```

**Q: Can we make `hashCode()` always return 1?**

Haan, lekin ye worst practice hai. Saare objects same bucket mein jayenge, `HashMap` O(1) se O(n) ban jayega. HashCode should be well-distributed.

---

# 9. Comparable vs Comparator

## 9.1 Comparable

Natural ordering define karta hai. Class khud implement karta hai.

```java
public class Student implements Comparable<Student> {
    private int marks;

    @Override
    public int compareTo(Student other) {
        return this.marks - other.marks;  // ascending
        // return other.marks - this.marks;  // descending
    }
}

Collections.sort(students);  // uses compareTo()
```

## 9.2 Comparator

External ordering. Multiple sorting criteria ke liye. Class modify nahi karni padti.

```java
// Lambda syntax (Java 8+)
Comparator<Student> byName = (s1, s2) -> s1.getName().compareTo(s2.getName());
Comparator<Student> byMarksDesc = Comparator.comparingInt(Student::getMarks).reversed();

Collections.sort(students, byName);
// or
students.sort(byMarksDesc);
```

**Comparator methods:**
```java
Comparator.comparing(Student::getName)
    .thenComparingInt(Student::getMarks)
    .reversed();
```

---

## Interview Q&A

**Q: `Comparable` aur `Comparator` mein kya farq hai?**

`Comparable` = natural ordering, class implement karti hai (`compareTo()`). `Comparator` = external/custom ordering, alag class/object define karta hai (`compare()`). `Comparable` ek hi ho sakta hai per class, `Comparator` multiple ho sakte hain.

**Q: `Collections.sort()` ka time complexity kya hai?**

Timsort algorithm use karta hai (Java 7+): O(n log n). Stable sort hai — equal elements ka relative order preserve hota hai.

**Q: `Comparable` ke bina `TreeSet` mein objects daal sakte hain?**

Nahi, `ClassCastException` aayega. `TreeSet` sorted order maintain karta hai, isliye elements comparable hone chahiye (ya `TreeSet` constructor mein `Comparator` pass karo).

---

# 10. Collections Framework — Deep Dive

## 10.1 Hierarchy

```
Iterable
├── Collection
│   ├── List (ordered, duplicates allowed)
│   │   ├── ArrayList
│   │   ├── LinkedList
│   │   └── Vector (legacy, synchronized)
│   ├── Set (no duplicates)
│   │   ├── HashSet (unordered)
│   │   ├── LinkedHashSet (insertion order)
│   │   └── TreeSet (sorted)
│   └── Queue
│       ├── PriorityQueue
│       └── Deque (ArrayDeque, LinkedList)
└── Map (key-value pairs)
    ├── HashMap
    ├── LinkedHashMap
    ├── TreeMap
    └── Hashtable (legacy, synchronized)
```

## 10.2 List Implementations

| Feature | ArrayList | LinkedList | Vector |
|---------|-----------|------------|--------|
| Internal | Dynamic Array | Doubly Linked List | Dynamic Array |
| Access | O(1) | O(n) | O(1) |
| Insert/Delete | O(n) | O(1) at ends | O(n) |
| Memory | Less overhead | More (pointers) | Less |
| Thread-Safe | No | No | Yes (synchronized) |
| Use Case | Random access | Frequent add/remove | Legacy code |

**ArrayList Internals:**
```java
// Default capacity: 10
// Growth: oldCapacity + (oldCapacity >> 1) = 1.5x
// Array full hone pe: new array (1.5x) → copy elements → old array GC
```

## 10.3 Set Implementations

| Feature | HashSet | LinkedHashSet | TreeSet |
|---------|---------|---------------|---------|
| Ordering | None | Insertion order | Sorted (natural/custom) |
| Internal | HashMap | LinkedHashMap | TreeMap (Red-Black Tree) |
| Null | One null | One null | No null |
| Complexity | O(1) | O(1) | O(log n) |

## 10.4 Map Implementations

| Feature | HashMap | LinkedHashMap | TreeMap | Hashtable |
|---------|---------|---------------|---------|-----------|
| Ordering | None | Insertion/Access | Sorted | None |
| Null key/value | 1 null key, many null values | Same | No null | No null |
| Thread-Safe | No | No | No | Yes |
| Performance | O(1) | O(1) | O(log n) | O(1) |
| Introduced | Java 2 | Java 4 | Java 2 | Java 1 (legacy) |

**HashMap Internals (Java 8+):**
- Array of buckets (Node[] table)
- Hash collision: Linked List (≤8 entries) → Red-Black Tree (>8 entries)
- Load factor: 0.75 (default). Resize jab 75% full.
- Capacity: powers of 2 (16, 32, 64, ...)

```java
// HashMap put() flow:
// 1. key ka hashCode() → hash function → bucket index
// 2. Bucket empty? → new Node
// 3. Bucket occupied? → equals() se check → replace if equal
// 4. Collision? → Linked List / Tree mein add
```

## 10.5 Queue & Deque

```java
Queue<String> queue = new LinkedList<>();
queue.offer("A");      // add (throws exception nahi)
queue.poll();          // remove & return head
queue.peek();          // return head without removing

Deque<String> deque = new ArrayDeque<>();
deque.addFirst("A");   // stack push
deque.removeFirst();   // stack pop
deque.addLast("B");    // queue enqueue
deque.removeFirst();   // queue dequeue
```

---

## Interview Q&A

**Q: `ArrayList` vs `LinkedList` — kab kya use karein?**

`ArrayList` jab random access (get by index) zyada ho. `LinkedList` jab frequent insertions/deletions (especially middle mein) ho. `LinkedList` mein memory overhead zyada hai (next/prev pointers). Most cases mein `ArrayList` better hai.

**Q: `HashMap` ka internal working batao.**

`HashMap` array of buckets (Node[]) use karta hai. Key ka `hashCode()` hash function se process hota hai aur bucket index decide hota hai. Collision pe linked list (Java 8+ mein tree jab size > 8) use hota hai. Load factor 0.75 pe resize (double capacity + rehash).

**Q: `HashMap` mein `null` key kaise kaam karta hai?**

`HashMap` null key ko bucket 0 mein store karta hai (hash = 0). Sirf ek null key allowed hai. `HashTable` aur `ConcurrentHashMap` mein null key allowed nahi hai.

**Q: `HashMap` vs `ConcurrentHashMap` mein kya farq hai?**

`HashMap` thread-safe nahi hai. `ConcurrentHashMap` thread-safe hai bina global lock ke — segment-level (Java 7) ya bucket-level (Java 8+) locking use karta hai. `ConcurrentHashMap` mein null key/value nahi allowed.

**Q: `fail-fast` vs `fail-safe` iterators mein kya farq hai?**

`fail-fast` (ArrayList, HashMap): Concurrent modification pe `ConcurrentModificationException` throw karta hai. `fail-safe` (CopyOnWriteArrayList, ConcurrentHashMap): Collection ka snapshot banata hai, modification se unaffected rehta hai. `fail-fast` immediate error deta hai, `fail-safe` stale data de sakta hai.

**Q: Why `HashMap` capacity is always power of 2?**

Hash index calculate karne ke liye `hash % capacity` ki jagah `hash & (capacity - 1)` use hota hai (bitwise AND). Ye modulo se fast hai. Power of 2 hone se ye optimization possible hai.

**Q: `TreeMap` ka underlying data structure kya hai?**

Red-Black Tree (self-balancing BST). Isliye operations O(log n) hain. Natural ordering ya `Comparator` chahiye.

---

# 11. Generics in Java

## 11.1 Basics

Type safety compile time pe ensure karta hai. Runtime pe type erasure hoti hai.

```java
List<String> list = new ArrayList<>();  // type-safe
list.add("hello");
// list.add(123);  // Compile error!

String s = list.get(0);  // No cast needed
```

## 11.2 Type Parameters

```java
// Generic class
public class Box<T> {
    private T item;
    public void set(T item) { this.item = item; }
    public T get() { return item; }
}

Box<String> stringBox = new Box<>();
Box<Integer> intBox = new Box<>();
```

## 11.3 Wildcards

```java
// Unbounded: any type
List<?> list;

// Upper bounded: T or subclass of T
List<? extends Number> numbers;  // Number, Integer, Double, etc.

// Lower bounded: T or superclass of T
List<? super Integer> ints;    // Integer, Number, Object
```

**PECS Principle:**
- **P**roducer → **E**xtends (read from)
- **C**onsumer → **S**uper (write to)

```java
// Producer: we read from it
void printNumbers(List<? extends Number> list) {
    for (Number n : list) System.out.println(n);
}

// Consumer: we write to it
void addIntegers(List<? super Integer> list) {
    list.add(1); list.add(2);
}
```

## 11.4 Type Erasure

Generics sirf compile-time construct hain. Runtime pe type information erase ho jati hai.

```java
List<String> strings = new ArrayList<>();
List<Integer> integers = new ArrayList<>();

System.out.println(strings.getClass() == integers.getClass());  // true!
// Both are just ArrayList at runtime
```

---

## Interview Q&A

**Q: Generics kyun use karte hain?**

Type safety (compile-time type checking), no explicit casting, code reusability. `List<String>` ensure karta hai ki sirf Strings store ho, bina runtime `ClassCastException` ke risk ke.

**Q: `List<Object>` aur `List<?>` mein kya farq hai?**

`List<Object>` mein tum `Object` type ka kuch bhi add kar sakte ho. `List<?>` mein tum sirf `null` add kar sakte ho (unknown type). `List<?>` read-only-ish hota hai.

**Q: Can we create a generic array?**

Nahi, `new T[10]` compile error hai. Type erasure ki wajah se JVM ko actual type pata nahi hota. Workaround: `Object[]` array bana kar cast karo, ya `ArrayList<T>` use karo.

**Q: `<? extends T>` vs `<? super T>` — PECS principle?**

Producer Extends, Consumer Super. Agar tum list se read karte ho (producer), use `extends`. Agar tum list mein write karte ho (consumer), use `super`. `extends` se write nahi kar sakte, `super` se specific type read nahi kar sakte (sirf Object).

**Q: Can generic type be primitive?**

Nahi. `List<int>` invalid hai. `List<Integer>` use karo. Autoboxing/unboxing handle kar leta hai.

---

# 12. Java 8 Features — Lambda, Stream, Optional, Date/Time

## 12.1 Lambda Expressions

Anonymous functions. Functional interfaces implement karne ka concise way.

```java
// Before Java 8
Runnable r = new Runnable() {
    public void run() { System.out.println("Hello"); }
};

// Java 8 Lambda
Runnable r = () -> System.out.println("Hello");

// With parameters
Comparator<String> c = (a, b) -> a.compareTo(b);

// Method reference
list.forEach(System.out::println);
```

## 12.2 Functional Interfaces

Sirf ek abstract method wala interface. `@FunctionalInterface` annotation optional.

| Interface | Method | Use |
|-----------|--------|-----|
| Runnable | `void run()` | No input, no output |
| Consumer<T> | `void accept(T)` | Input, no output |
| Supplier<T> | `T get()` | No input, output |
| Function<T,R> | `R apply(T)` | Input → Output |
| Predicate<T> | `boolean test(T)` | Input → boolean |
| BiFunction<T,U,R> | `R apply(T,U)` | 2 inputs → Output |

## 12.3 Stream API

Collection/data processing ke liye functional-style operations.

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);

List<Integer> result = numbers.stream()
    .filter(n -> n % 2 == 0)      // intermediate
    .map(n -> n * n)                // intermediate
    .sorted()                       // intermediate
    .collect(Collectors.toList());  // terminal

// Parallel stream
numbers.parallelStream()
    .map(n -> heavyComputation(n))
    .collect(Collectors.toList());
```

**Stream Operations:**

| Intermediate (lazy) | Terminal (eager) |
|---------------------|------------------|
| filter, map, flatMap | collect, forEach |
| sorted, distinct | reduce, count |
| peek, limit, skip | anyMatch, allMatch |
| | findFirst, findAny |

**Collectors:**
```java
Collectors.toList();
Collectors.toSet();
Collectors.toMap(keyMapper, valueMapper);
Collectors.groupingBy(Class::getDepartment);  // Map<Dept, List<Employee>>
Collectors.partitioningBy(e -> e.getSalary() > 50000);  // Map<Boolean, List>
Collectors.joining(", ");
```

## 12.4 Optional

NullPointerException avoid karne ke liye.

```java
Optional<String> opt = Optional.ofNullable(getString());

String result = opt
    .filter(s -> s.length() > 5)
    .map(String::toUpperCase)
    .orElse("DEFAULT");

// or
opt.ifPresent(System.out::println);
```

**Never do this:**
```java
Optional<String> opt = ...;
if (opt.isPresent()) {  // anti-pattern
    return opt.get();
}
```

## 12.5 Date/Time API (java.time)

Old `java.util.Date`/`Calendar` ki jagah. Immutable aur thread-safe.

```java
LocalDate today = LocalDate.now();
LocalTime now = LocalTime.now();
LocalDateTime dateTime = LocalDateTime.now();

ZonedDateTime zdt = ZonedDateTime.now(ZoneId.of("Asia/Kolkata"));

Period period = Period.between(startDate, endDate);
Duration duration = Duration.between(startTime, endTime);

DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd-MM-yyyy");
String formatted = today.format(formatter);
```

---

## Interview Q&A

**Q: Lambda expression ka syntax batao.**

`(parameters) -> { body }`. Single parameter mein parentheses optional. Single statement mein braces aur return optional. `(x) -> x * x` ya `x -> x * x`.

**Q: Stream intermediate aur terminal operations mein kya farq hai?**

Intermediate operations (filter, map) lazy hain — execute nahi hote jab tak terminal operation (collect, forEach) call nahi hota. Intermediate operations new Stream return karte hain (chaining possible). Terminal operations void ya non-stream value return karte hain.

**Q: `map()` vs `flatMap()` mein kya farq hai?**

`map()` har element ko transform karta hai (1-to-1). `flatMap()` har element ko stream mein flatten karta hai (1-to-many). `flatMap` nested streams ko single level stream mein convert karta hai.

```java
List<List<Integer>> nested = Arrays.asList(Arrays.asList(1, 2), Arrays.asList(3, 4));
List<Integer> flat = nested.stream().flatMap(List::stream).collect(Collectors.toList());
// [1, 2, 3, 4]
```

**Q: `Optional` ka use kyun karte hain?**

NullPointerException explicitly handle karne ke liye. `Optional` force karta hai ki caller soch ke deal kare missing value ke saath. Method return type mein use karo jab value absent ho sakti hai. **Never use Optional as field or method parameter** — sirah return type ke liye.

**Q: `findFirst()` vs `findAny()` mein kya farq hai?**

`findFirst()` deterministic hai — pehla element jo condition match kare. `findAny()` non-deterministic — koi bhi matching element. Sequential streams mein dono same behave karte hain. Parallel streams mein `findAny()` faster ho sakta hai.

**Q: `java.time` API purane `Date`/`Calendar` se better kyun hai?**

Immutable (thread-safe), fluent API, timezone support, clear separation (Date vs Time vs DateTime), no month indexing confusion (January = 1, not 0).

**Q: `Collectors.groupingBy()` ka use batao.**

```java
Map<String, List<Employee>> byDept = employees.stream()
    .collect(Collectors.groupingBy(Employee::getDepartment));
```

Employees ko department ke hisaab se group karta hai. `groupingBy` ke saath downstream collector bhi pass kar sakte hain (jaise counting, averaging).

---

# 13. File I/O & Serialization

## 13.1 Reading/Writing Files

```java
// Java 7+ — Files utility class
List<String> lines = Files.readAllLines(Path.of("file.txt"));
Files.writeString(Path.of("out.txt"), "Hello World");

// Stream API ke saath
Files.lines(Path.of("file.txt"))
    .filter(line -> line.contains("ERROR"))
    .forEach(System.out::println);
```

## 13.2 Serialization

Object ko byte stream mein convert karna (file mein save karne ya network pe bhejne ke liye).

```java
// Serialize
ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("obj.ser"));
oos.writeObject(myObject);

// Deserialize
ObjectInputStream ois = new ObjectInputStream(new FileInputStream("obj.ser"));
MyObject obj = (MyObject) ois.readObject();
```

**Requirements:**
- Class must implement `Serializable` (marker interface)
- `serialVersionUID` define karna chahiye (version compatibility)
- `transient` fields serialize nahi hote
- Static fields serialize nahi hote

```java
public class Employee implements Serializable {
    private static final long serialVersionUID = 1L;
    private String name;
    private transient String password;  // won't be serialized
    private static String company;     // won't be serialized
}
```

---

## Interview Q&A

**Q: `transient` keyword kya karta hai?**

`transient` fields serialization mein skip ho jate hain. Sensitive data (passwords, keys) ya computed values ke liye use hota hai.

**Q: `serialVersionUID` kyun important hai?**

Class version ka unique identifier. Agar class modify ho (fields add/remove) aur `serialVersionUID` same nahi rakha, to deserialization pe `InvalidClassException` aata hai. Explicitly define karne se version control possible hai.

**Q: Can we serialize static fields?**

Nahi. Static fields class level pe hote hain, object level pe nahi. Serialization object state ko save karti hai, class state nahi.

**Q: Custom serialization kaise karein?**

`writeObject()` aur `readObject()` methods define karo:

```java
private void writeObject(ObjectOutputStream out) throws IOException {
    out.defaultWriteObject();
    // custom logic
}

private void readObject(ObjectInputStream in) throws IOException, ClassNotFoundException {
    in.defaultReadObject();
    // custom logic
}
```

---

# 14. Reflection & Annotations

## 14.1 Reflection

Runtime pe class ki information inspect aur modify karna.

```java
Class<?> clazz = Class.forName("com.example.MyClass");

// Methods
Method[] methods = clazz.getDeclaredMethods();
Method method = clazz.getMethod("doSomething", String.class);
method.invoke(object, "arg");

// Fields
Field field = clazz.getDeclaredField("privateField");
field.setAccessible(true);  // bypass private
field.set(object, "newValue");

// Constructors
Constructor<?> ctor = clazz.getConstructor();
Object obj = ctor.newInstance();
```

## 14.2 Custom Annotations

```java
@Retention(RetentionPolicy.RUNTIME)  // compile, class, or runtime
@Target(ElementType.METHOD)          // where annotation can be applied
public @interface MyAnnotation {
    String value() default "";
    int priority() default 0;
}

// Usage
@MyAnnotation(value = "test", priority = 1)
public void myMethod() { }
```

---

## Interview Q&A

**Q: Reflection kya hai aur kab use karte hain?**

Runtime pe classes, methods, fields inspect aur modify karne ki capability. Frameworks (Spring, Hibernate) heavily use karte hain. Dependency injection, ORM mapping, serialization mein use hota hai. Slow hota hai (bypasses compile-time optimizations), isliye production code mein avoid karo unless necessary.

**Q: Annotation ka retention policy kya hota hai?**

`SOURCE` — sirf compile time (e.g., `@Override`). `CLASS` — class file mein rehta hai, runtime pe nahi (default). `RUNTIME` — runtime pe accessible via reflection (e.g., `@Entity`, `@Autowired`).

**Q: Can we make our own annotations?**

Haan, `@interface` keyword se. `@Retention` aur `@Target` meta-annotations define karte hain ki annotation kab aur kahan applicable hai.

---

# 15. Garbage Collection — How It Works

## 15.1 What is GC?

Automatic memory management. JVM heap mein unused objects ko identify karke memory free karta hai.

## 15.2 How Objects Become Eligible

1. **Null reference**: `obj = null;`
2. **Reassign reference**: `obj = new Object();` (old object eligible)
3. **Local variable**: method end hone pe
4. **Island of isolation**: objects referencing each other but no external reference

## 15.3 GC Algorithms

| Collector | Best For | Characteristics |
|-----------|----------|----------------|
| Serial | Single CPU, small heap | Single thread, stop-the-world |
| Parallel | Multi-CPU, throughput | Multiple threads, stop-the-world |
| CMS | Low latency | Concurrent, deprecated Java 14+ |
| G1 (default Java 9+) | Balanced | Regions, predictable pause times |
| ZGC | Large heap, ultra-low latency | Concurrent, scalable |
| Shenandoah | Low latency | Concurrent compaction |

## 15.4 G1 GC

Heap ko regions mein divide karta hai (Eden, Survivor, Old). Humongous objects ke liye dedicated regions. Mixed collections (young + some old). Target pause time configurable (`-XX:MaxGCPauseMillis=200`).

## 15.5 Memory Regions

```
Heap
├── Young Generation
│   ├── Eden (new objects)
│   └── Survivor 0 & 1 (minor GC survivors)
└── Old Generation (long-lived objects)

Method Area (Metaspace in Java 8+)
```

**Minor GC**: Young generation. Fast, frequent.
**Major GC**: Old generation. Slow, less frequent.
**Full GC**: Entire heap. Stop-the-world, expensive.

---

## Interview Q&A

**Q: `System.gc()` call karna chahiye?**

Nahi. Ye sirf JVM ko hint deta hai, force nahi karta. JVM ignore kar sakta hai. Manual GC calls generally anti-pattern hai — JVM ka GC algorithm already optimized hai.

**Q: `finalize()` method kya karti hai?**

Object destroy hone se pehle JVM call karta hai. Resource cleanup ke liye. Lekin unreliable hai — kabhi bhi call ho sakta hai, ya kabhi nahi. Java 9+ mein deprecated. `try-with-resources` ya `Cleaner` class use karo.

**Q: Heap aur Stack mein kya farq hai?**

Heap: objects, dynamic allocation, GC manage karta hai, shared across threads. Stack: method frames, local variables, per-thread, automatic allocation/deallocation.

**Q: Java 8 mein PermGen kyun hata diya?**

PermGen (Permanent Generation) fixed size hota tha, `OutOfMemoryError: PermGen` common tha. Java 8 mein **Metaspace** aaya — native memory use karta hai, dynamically resize hota hai. Class metadata ab native memory mein rehta hai.

**Q: Strong, Soft, Weak, Phantom references mein kya farq hai?**

- **Strong**: Normal reference. GC nahi karta jab tak reachable hai.
- **Soft**: Memory pressure pe GC karta hai. Caching ke liye use hota hai.
- **Weak**: Next GC cycle pe collect ho jata hai. `WeakHashMap` mein use hota hai.
- **Phantom**: Object collect hone ke baad reference. Cleanup notification ke liye.

---

# 16. Java Memory Model (JMM) — Brief

Already covered in detail in the concurrency document. Quick recap:

- **Happens-before**: Actions ka visibility guarantee
- **volatile**: Visibility + ordering (no atomicity)
- **synchronized**: Visibility + atomicity + ordering
- **final**: Safe publication guarantee

See the concurrency document for deep dive.

---

# PART 2: ADVANCED JAVA / FRAMEWORKS

---

# 17. JDBC — Java Database Connectivity

## 17.1 JDBC Steps

```java
// 1. Load Driver (Java 6+ mein optional — auto-loaded)
Class.forName("com.mysql.cj.jdbc.Driver");

// 2. Create Connection
Connection conn = DriverManager.getConnection(
    "jdbc:mysql://localhost:3306/mydb", "user", "password");

// 3. Create Statement
Statement stmt = conn.createStatement();  // NOT recommended — SQL Injection
PreparedStatement pstmt = conn.prepareStatement(
    "SELECT * FROM users WHERE id = ?");  // Use this!
pstmt.setInt(1, 101);

// 4. Execute Query
ResultSet rs = pstmt.executeQuery();

// 5. Process Results
while (rs.next()) {
    System.out.println(rs.getString("name"));
}

// 6. Close Resources
rs.close(); pstmt.close(); conn.close();
```

## 17.2 Statement Types

| Type | Use | Safe? |
|------|-----|-------|
| Statement | Static queries | No SQL Injection protection |
| PreparedStatement | Dynamic queries with parameters | Yes (pre-compiled) |
| CallableStatement | Stored procedures | Yes |

**PreparedStatement benefits:**
- Pre-compiled (faster for repeated execution)
- SQL Injection protection (parameters escaped)
- Type safety

---

## Interview Q&A

**Q: `Statement` vs `PreparedStatement` mein kya farq hai?**

`Statement` static SQL execute karta hai. `PreparedStatement` parameterized queries pre-compile karta hai. `PreparedStatement` SQL Injection se protect karta hai aur repeated execution mein faster hai.

**Q: SQL Injection kya hai?**

Malicious SQL code user input ke through inject karna. Example: `username = "admin' OR '1'='1"` — ye condition hamesha true ban jati hai. `PreparedStatement` use karne se ye prevent hota hai kyunki parameters escaped hote hain.

**Q: Connection pooling kya hai?**

Database connections banana expensive hai. Connection pool (HikariCP, C3P0) pre-created connections maintain karta hai. Application pool se connection borrow karta hai aur use karke return karta hai. Spring Boot mein HikariCP default hai.

---

# 18. Servlet & JSP Basics

## 18.1 Servlet Lifecycle

```
1. load() → Class load
2. init() → Initialization (once)
3. service() → Request handle (har request pe)
   └── doGet(), doPost(), doPut(), doDelete()
4. destroy() → Cleanup (once)
```

## 18.2 Servlet vs JSP

| Servlet | JSP |
|---------|-----|
| Java code with HTML | HTML with Java code |
| Controller logic | View logic |
| `out.println()` for HTML | Direct HTML tags |
| Compiled to Java class first | Compiled to Servlet first |

**JSP Implicit Objects:** `request`, `response`, `session`, `application`, `out`, `config`, `pageContext`, `page`, `exception`

---

## Interview Q&A

**Q: Servlet lifecycle batao.**

`init()` (once) → `service()` (har request) → `destroy()` (once). `service()` method HTTP method ke hisaab se `doGet()`, `doPost()`, etc. call karta hai.

**Q: `forward()` vs `sendRedirect()` mein kya farq hai?**

`forward()` server-side hota hai — same request object forward hota hai, URL change nahi hota. `sendRedirect()` client-side hota hai — browser ko new URL pe bheja jata hai, new request create hoti hai.

**Q: Servlet container kya hai?**

Web server jo Servlet API implement karta hai. Examples: Tomcat, Jetty, WildFly. HTTP requests ko Servlet instances ko delegate karta hai.

---

# 19. Design Patterns — Most Asked

## 19.1 Creational Patterns

**Singleton:**
```java
public class Singleton {
    private static volatile Singleton instance;

    private Singleton() {}

    public static Singleton getInstance() {
        if (instance == null) {
            synchronized (Singleton.class) {
                if (instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}
```

**Factory:**
```java
interface Shape { void draw(); }
class Circle implements Shape { public void draw() {} }
class Square implements Shape { public void draw() {} }

class ShapeFactory {
    public Shape getShape(String type) {
        return switch (type) {
            case "CIRCLE" -> new Circle();
            case "SQUARE" -> new Square();
            default -> throw new IllegalArgumentException();
        };
    }
}
```

**Builder:**
```java
public class Computer {
    private String cpu;
    private int ram;

    public static class Builder {
        private Computer computer = new Computer();
        public Builder cpu(String cpu) { computer.cpu = cpu; return this; }
        public Builder ram(int ram) { computer.ram = ram; return this; }
        public Computer build() { return computer; }
    }
}

Computer c = new Computer.Builder().cpu("i7").ram(16).build();
```

## 19.2 Structural Patterns

**Adapter:** Incompatible interfaces ko compatible banana.
**Decorator:** Behavior dynamically add karna bina subclassing ke.
**Facade:** Complex subsystem ko simple interface provide karna.

## 19.3 Behavioral Patterns

**Strategy:** Family of algorithms, interchangeably use karna.
**Observer:** One-to-many dependency — state change pe saare observers notify hote hain.
**Template Method:** Algorithm skeleton define karna, steps subclasses implement karti hain.

---

## Interview Q&A

**Q: Singleton pattern ka real-world use case?**

Database connection pool, configuration manager, logger, cache manager. Jahan ek hi instance control karna zaroori ho.

**Q: Builder pattern kab use karein?**

Jab constructor parameters zyada ho (telescoping constructor problem). Immutable objects banane ke liye. Optional parameters ke saath.

**Q: Strategy vs Template Method pattern mein kya farq hai?**

Strategy mein complete algorithm replace hota hai. Template Method mein algorithm ka skeleton fixed hai, sirf specific steps override hote hain.

---

# 20. Maven & Gradle Basics

## 20.1 Maven

```xml
<!-- pom.xml -->
<project>
    <groupId>com.example</groupId>
    <artifactId>my-app</artifactId>
    <version>1.0.0</version>
    <packaging>jar</packaging>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
            <version>3.2.0</version>
        </dependency>
    </dependencies>
</project>
```

**Maven Lifecycle:**
1. `validate` → `compile` → `test` → `package` → `verify` → `install` → `deploy`

## 20.2 Gradle

```groovy
// build.gradle
plugins {
    id 'java'
    id 'org.springframework.boot' version '3.2.0'
}

dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-web'
    testImplementation 'org.springframework.boot:spring-boot-starter-test'
}
```

---

## Interview Q&A

**Q: Maven aur Gradle mein kya farq hai?**

Maven XML-based hai, convention over configuration. Gradle Groovy/Kotlin DSL use karta hai, zyada flexible aur fast hai (incremental builds). Gradle mein tasks define karte hain, Maven mein phases.

**Q: `compile` vs `provided` vs `runtime` scope mein kya farq hai?**

`compile`: Sab phases mein available. `provided`: Compile time pe chahiye, runtime pe container provide karta hai (e.g., servlet-api). `runtime`: Runtime pe chahiye, compile time pe nahi (e.g., JDBC driver). `test`: Sirf test phase mein.

**Q: Transitive dependency kya hai?**

Agar tum A dependency add karte ho, aur A ko B chahiye, to B automatically include ho jata hai. Maven/Gradle dependency tree resolve karte hain.

---

# 21. JUnit & Mockito — Unit Testing

## 21.1 JUnit 5 Basics

```java
import org.junit.jupiter.api.*;
import static org.junit.jupiter.api.Assertions.*;

class CalculatorTest {

    @BeforeAll
    static void init() { /* once before all tests */ }

    @BeforeEach
    void setUp() { /* before each test */ }

    @Test
    void testAdd() {
        Calculator calc = new Calculator();
        assertEquals(5, calc.add(2, 3));
        assertThrows(IllegalArgumentException.class, () -> calc.divide(1, 0));
    }

    @AfterEach
    void tearDown() { /* after each test */ }

    @AfterAll
    static void cleanUp() { /* once after all tests */ }
}
```

## 21.2 Mockito

```java
import static org.mockito.Mockito.*;

@Test
void testUserService() {
    UserRepository mockRepo = mock(UserRepository.class);
    when(mockRepo.findById(1L)).thenReturn(Optional.of(new User("Alice")));

    UserService service = new UserService(mockRepo);
    User user = service.getUser(1L);

    assertEquals("Alice", user.getName());
    verify(mockRepo, times(1)).findById(1L);
}
```

**Mockito Annotations:**
```java
@ExtendWith(MockitoExtension.class)
class MyTest {
    @Mock UserRepository repo;
    @InjectMocks UserService service;

    @Test
    void test() {
        when(repo.findById(any())).thenReturn(Optional.empty());
        // ...
    }
}
```

---

## Interview Q&A

**Q: `mock()` vs `spy()` vs `@Mock` mein kya farq hai?**

`mock()` = fake object, saare methods stubbed. `spy()` = real object ka wrapper, real methods call hote hain unless stubbed. `@Mock` = annotation se mock inject karna (MockitoExtension ke saath).

**Q: `when()` vs `doReturn()`/`doThrow()` mein kya farq hai?**

`when()` normal stubbing ke liye. `doReturn()`/`doThrow()` void methods, spies, ya consecutive calls ke liye. `when(mock.voidMethod()).thenThrow()` compile nahi hota, isliye `doThrow().when(mock).voidMethod()` use karte hain.

**Q: Code coverage kya hoti hai?**

Percentage of code jo tests execute karte hain. Tools: JaCoCo, Cobertura. Aim for 70-80%+ coverage. 100% coverage guarantee nahi deta ki code bug-free hai.

---

# PART 3: SPRING ECOSYSTEM

---

# 22. Spring Core — IOC, DI, Bean Lifecycle

## 22.1 IOC (Inversion of Control)

Traditional: Object apni dependencies khud create karta hai.
```java
class Service {
    private Repository repo = new Repository();  // tight coupling
}
```

IOC: Container dependencies inject karta hai.
```java
class Service {
    private Repository repo;

    @Autowired  // Spring inject karega
    public Service(Repository repo) {
        this.repo = repo;
    }
}
```

## 22.2 DI (Dependency Injection) Types

1. **Constructor Injection** (Recommended)
```java
@Service
public class UserService {
    private final UserRepository repo;

    public UserService(UserRepository repo) {  // Spring injects
        this.repo = repo;
    }
}
```

2. **Setter Injection**
```java
@Autowired
public void setRepo(UserRepository repo) {
    this.repo = repo;
}
```

3. **Field Injection** (Avoid)
```java
@Autowired
private UserRepository repo;  // Hard to test, hidden dependencies
```

**Why Constructor Injection is best:**
- Immutable dependencies (final fields)
- Required dependencies — object without them nahi ban sakta
- Easy unit testing (no reflection needed)
- Circular dependencies detect ho jati hain

## 22.3 Bean Scopes

| Scope | Description |
|-------|-------------|
| singleton | Ek instance per Spring container (default) |
| prototype | Har request pe naya instance |
| request | Ek instance per HTTP request |
| session | Ek instance per HTTP session |
| application | Ek instance per ServletContext |

## 22.4 Bean Lifecycle

```
1. Instantiate → new Object()
2. Populate Properties → Dependencies inject
3. setBeanName() → BeanNameAware
4. setBeanFactory() → BeanFactoryAware
5. setApplicationContext() → ApplicationContextAware
6. @PostConstruct → Custom initialization
7. InitializingBean.afterPropertiesSet()
8. Custom init-method
9. Bean Ready → Use
10. @PreDestroy → Custom cleanup
11. DisposableBean.destroy()
12. Custom destroy-method
```

---

## Interview Q&A

**Q: IOC aur DI mein kya farq hai?**

IOC ek design principle hai — control ka inversion. DI IOC ka ek implementation hai — dependencies externally provide ki jati hain. IOC ke aur bhi implementations hain: Factory Pattern, Service Locator, etc.

**Q: `@Component`, `@Service`, `@Repository`, `@Controller` mein kya farq hai?**

Functionally same hain — sab `@Component` ke specialization hain. Semantic meaning aur potential AOP behavior alag hai:
- `@Component`: Generic stereotype
- `@Service`: Business logic layer
- `@Repository`: Data access layer (exception translation)
- `@Controller`: Web layer (request handling)

**Q: `@Autowired` vs `@Inject` vs `@Resource` mein kya farq hai?**

`@Autowired`: Spring-specific. Type-based injection. `@Inject`: JSR-330 standard. Type-based. `@Resource`: JSR-250 standard. Name-based injection (pehle name match, phir type). Spring projects mein `@Autowired` most common.

**Q: Circular dependency kaise solve karein?**

Constructor injection mein Spring circular dependency detect karke `BeanCurrentlyInCreationException` throw karta hai. Solutions:
1. Setter injection use karo (lazy resolution)
2. `@Lazy` use karo ek bean pe
3. Design refactor karo — single responsibility violation indicate karti hai

**Q: `@PostConstruct` aur `@PreDestroy` kab use karte hain?**

`@PostConstruct`: Bean create aur dependencies inject hone ke baad initialization logic (database connection, cache warm-up). `@PreDestroy`: Container destroy hone pe cleanup (connections close, resources release).

---

# 23. Spring AOP — Aspect-Oriented Programming

## 23.1 What is AOP?

Cross-cutting concerns (logging, transaction, security) ko business logic se alag karna. Without AOP, har method mein same boilerplate code.

```java
@Aspect
@Component
public class LoggingAspect {

    @Before("execution(* com.example.service.*.*(..))")
    public void logBefore(JoinPoint jp) {
        System.out.println("Method called: " + jp.getSignature().getName());
    }

    @AfterReturning(pointcut = "execution(* com.example.service.*.*(..))", 
                    returning = "result")
    public void logAfter(JoinPoint jp, Object result) {
        System.out.println("Method returned: " + result);
    }

    @Around("execution(* com.example.service.*.*(..))")
    public Object logAround(ProceedingJoinPoint pjp) throws Throwable {
        long start = System.currentTimeMillis();
        Object result = pjp.proceed();  // actual method call
        long duration = System.currentTimeMillis() - start;
        System.out.println("Duration: " + duration + "ms");
        return result;
    }
}
```

## 23.2 Advice Types

| Advice | When It Runs |
|--------|--------------|
| @Before | Method execution se pehle |
| @After | Method execution ke baad (chahe exception aaye ya na) |
| @AfterReturning | Method successfully return hone ke baad |
| @AfterThrowing | Exception throw hone ke baad |
| @Around | Method execution ke around (pehle + baad) |

## 23.3 Pointcut Expressions

```java
execution(* com.example.service.*.*(..))        // any method in service package
execution(public * *(..))                         // any public method
@annotation(com.example.Loggable)                 // methods with @Loggable
within(com.example.service..*)                    // any class in service or sub-packages
```

---

## Interview Q&A

**Q: Spring AOP kaise kaam karta hai?**

Spring AOP **proxy-based** hai. Runtime pe JDK Dynamic Proxy (interfaces) ya CGLIB Proxy (classes) create hota hai. Proxy method call intercept karta hai, advice execute karta hai, phir actual method call karta hai.

**Q: `@Transactional` AOP ka example hai. Explain karo.**

`@Transactional` Spring AOP use karta hai. Method call pe proxy intercept karta hai, transaction start karta hai, method execute karta hai, success pe commit, exception pe rollback. Ye declarative transaction management hai.

**Q: AOP mein `this` vs `target` mein kya farq hai?**

`this`: proxy object refer karta hai. `target`: actual target object refer karta hai. `this` ke through proxy methods call honge (advice re-apply), `target` ke through direct methods (advice re-apply nahi honge).

**Q: Can AOP be applied to private methods?**

Spring AOP mein nahi — proxy sirf public methods intercept kar sakta hai. AspectJ (compile-time weaving) private methods pe bhi kaam karta hai.

---

# 24. Spring Boot — Auto-Configuration, Starters, Actuator

## 24.1 What is Spring Boot?

Opinionated framework Spring applications quickly build karne ke liye. Auto-configuration, embedded servers, production-ready features provide karta hai.

**Key Features:**
- Auto-configuration: Classpath pe dependencies dekh kar beans automatically configure
- Standalone: Embedded Tomcat/Jetty — `java -jar` se run
- Production-ready: Metrics, health checks, externalized config

## 24.2 Auto-Configuration

```java
// @SpringBootApplication = @Configuration + @EnableAutoConfiguration + @ComponentScan
@SpringBootApplication
public class MyApp {
    public static void main(String[] args) {
        SpringApplication.run(MyApp.class, args);
    }
}
```

Auto-configuration `META-INF/spring.factories` mein defined hoti hai. Conditional annotations:
- `@ConditionalOnClass` — class present ho
- `@ConditionalOnMissingBean` — bean missing ho
- `@ConditionalOnProperty` — property set ho

## 24.3 Spring Boot Starters

Pre-defined dependency descriptors. Version conflicts handle kar lete hain.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

## 24.4 Actuator

Production monitoring endpoints.

```yaml
management:
  endpoints:
    web:
      exposure:
        include: health,info,metrics,env
  endpoint:
    health:
      show-details: always
```

Endpoints: `/actuator/health`, `/actuator/metrics`, `/actuator/env`, `/actuator/beans`

## 24.5 Configuration Priority

1. Command line arguments
2. `SPRING_APPLICATION_JSON` properties
3. ServletConfig init parameters
4. ServletContext init parameters
5. JNDI attributes
6. OS environment variables
7. `application-{profile}.properties` (profile-specific)
8. `application.properties` / `application.yml`
9. `@PropertySource`
10. Default properties

---

## Interview Q&A

**Q: Spring Boot ka main advantage kya hai?**

Convention over configuration — minimal setup mein production-ready app. Auto-configuration, embedded server, starter dependencies, actuator monitoring. Developer productivity significantly improve hoti hai.

**Q: `@SpringBootApplication` mein kya kya included hai?**

`@Configuration` + `@EnableAutoConfiguration` + `@ComponentScan`. Ye teen annotations ek mein combine ho gayi hain convenience ke liye.

**Q: Auto-configuration ko disable kaise karein?**

`@SpringBootApplication(exclude = {DataSourceAutoConfiguration.class})` ya `spring.autoconfigure.exclude` property. Ya `@EnableAutoConfiguration(exclude = ...)`.

**Q: `application.properties` vs `application.yml` mein kya farq hai?**

`.properties` flat key-value format. `.yml` hierarchical, more readable. Same functionality, different syntax. Spring Boot dono support karta hai. `.yml` complex nested configs ke liye better.

**Q: Spring Boot profiles kya hain?**

Environment-specific configurations. `application-dev.properties`, `application-prod.properties`. Activate via `spring.profiles.active=dev`. Beans bhi profile-specific ho sakte hain: `@Profile("dev")`.

**Q: `@ConfigurationProperties` ka use karo.**

Type-safe configuration binding. POJO mein properties bind karta hai.

```java
@ConfigurationProperties(prefix = "app")
public class AppProperties {
    private String name;
    private int timeout;
    // getters/setters
}
```

---

# 25. Spring Data JPA & Hibernate

## 25.1 JPA vs Hibernate vs Spring Data JPA

| Technology | What It Is |
|-----------|------------|
| JPA | Specification (API) for ORM |
| Hibernate | JPA Implementation (most popular) |
| Spring Data JPA | Abstraction layer on top of JPA/Hibernate |

## 25.2 Entity Mapping

```java
@Entity
@Table(name = "employees")
public class Employee {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "full_name", nullable = false, length = 100)
    private String name;

    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "dept_id")
    private Department department;

    @OneToMany(mappedBy = "employee", cascade = CascadeType.ALL, orphanRemoval = true)
    private List<Address> addresses = new ArrayList<>();
}
```

## 25.3 Fetch Types

| Type | Behavior | Use Case |
|------|----------|----------|
| EAGER | Data immediately load | Small, always needed data |
| LAZY | Data on-demand load | Large/collections, avoid N+1 |

**N+1 Problem:**
```java
// 1 query for employees
List<Employee> emps = repo.findAll();  // SELECT * FROM employees

// N queries for departments (LAZY fetch)
for (Employee e : emps) {
    e.getDepartment().getName();  // SELECT * FROM departments WHERE id = ?
}
// Total: N+1 queries!
```

**Solution:** `JOIN FETCH` or Entity Graph
```java
@Query("SELECT e FROM Employee e JOIN FETCH e.department")
List<Employee> findAllWithDepartment();
```

## 25.4 Cascade Types

| Type | Effect |
|------|--------|
| PERSIST | Save child with parent |
| MERGE | Update child with parent |
| REMOVE | Delete child with parent |
| REFRESH | Refresh child with parent |
| DETACH | Detach child with parent |
| ALL | All of the above |

## 25.5 Spring Data JPA Repositories

```java
public interface EmployeeRepository extends JpaRepository<Employee, Long> {
    // Derived query methods
    List<Employee> findByNameContainingIgnoreCase(String name);
    List<Employee> findByDepartmentNameAndSalaryGreaterThan(String dept, Double salary);

    // Custom JPQL
    @Query("SELECT e FROM Employee e WHERE e.salary > :minSalary")
    List<Employee> findHighEarners(@Param("minSalary") Double minSalary);

    // Native SQL
    @Query(value = "SELECT * FROM employees WHERE salary > ?1", nativeQuery = true)
    List<Employee> findHighEarnersNative(Double minSalary);

    // Modifying query
    @Modifying
    @Query("UPDATE Employee e SET e.salary = e.salary * 1.1 WHERE e.department.name = :dept")
    int giveRaise(@Param("dept") String department);
}
```

---

## Interview Q&A

**Q: JPA vs Hibernate mein kya farq hai?**

JPA ek specification hai (interfaces). Hibernate JPA ka ek implementation hai. Tum JPA APIs use karte ho, Hibernate unka implementation provide karta hai. Spring Data JPA Hibernate ke upar ek aur abstraction layer hai.

**Q: `LazyInitializationException` kya hai aur kaise solve karein?**

Session closed hone ke baad LAZY entity access karne pe aata hai. Solutions:
1. `JOIN FETCH` query mein use karo
2. `@Transactional` method pe rakho (session open rakhta hai)
3. `OpenEntityManagerInViewFilter` (web requests ke liye)
4. DTO projections use karo

**Q: `merge()` vs `persist()` vs `save()` mein kya farq hai?**

`persist()`: New entity ko managed banata hai. Detached entity pe `IllegalArgumentException`. `merge()`: Detached entity ko managed state mein merge karta hai, copy return karta hai. `save()`: Spring Data JPA method — new entity pe `persist()`, existing pe `merge()`.

**Q: `@Transactional` read-only kyun mark karein?**

`@Transactional(readOnly = true)` Hibernate ko hint deta hai ki no dirty checking, no flush needed. Performance improve hoti hai. Read operations pe hamesha use karo.

**Q: `orphanRemoval = true` kya karta hai?**

Parent se child remove karne pe child database se bhi delete ho jata hai. `CascadeType.REMOVE` sirf parent delete pe child delete karta hai. `orphanRemoval` parent se relationship break pe bhi delete karta hai.

**Q: Pagination kaise implement karein Spring Data JPA mein?**

```java
Page<Employee> page = repo.findByDepartmentName("IT", 
    PageRequest.of(0, 10, Sort.by("name").ascending()));

List<Employee> content = page.getContent();
int totalPages = page.getTotalPages();
long totalElements = page.getTotalElements();
```

---

# 26. Spring Transactions — @Transactional Deep Dive

## 26.1 Transaction Basics

ACID properties:
- **Atomicity**: All or nothing
- **Consistency**: Valid state to valid state
- **Isolation**: Concurrent transactions don't interfere
- **Durability**: Committed data survives crashes

## 26.2 @Transactional

```java
@Service
@Transactional
public class OrderService {

    public void placeOrder(Order order) {
        // All DB operations in this method are in one transaction
        orderRepo.save(order);
        paymentRepo.save(order.getPayment());
        inventoryRepo.decreaseStock(order.getItems());
    }

    @Transactional(readOnly = true)
    public Order getOrder(Long id) {
        return orderRepo.findById(id).orElseThrow();
    }

    @Transactional(propagation = Propagation.REQUIRES_NEW)
    public void auditLog(String action) {
        // Independent transaction — parent rollback se unaffected
        auditRepo.save(new AuditLog(action));
    }
}
```

## 26.3 Propagation Types

| Propagation | Behavior |
|-------------|----------|
| REQUIRED | Default. Existing join, else new. |
| REQUIRES_NEW | Always new. Suspend existing. |
| SUPPORTS | Join if exists, else non-transactional. |
| NOT_SUPPORTED | Suspend existing, run without tx. |
| MANDATORY | Must join existing, else exception. |
| NEVER | Must not run in tx, else exception. |
| NESTED | Savepoint-based nested tx. |

## 26.4 Isolation Levels

| Level | Dirty Read | Non-Repeatable | Phantom |
|-------|-----------|----------------|---------|
| READ_UNCOMMITTED | Yes | Yes | Yes |
| READ_COMMITTED | No | Yes | Yes |
| REPEATABLE_READ | No | No | Yes |
| SERIALIZABLE | No | No | No |

**Problems:**
- **Dirty Read**: Uncommitted data read
- **Non-Repeatable Read**: Same query, different results (update)
- **Phantom Read**: Same query, different rows (insert/delete)

## 26.5 Rollback Behavior

Default: Runtime exceptions (`RuntimeException`) pe rollback. Checked exceptions pe nahi.

```java
@Transactional(rollbackFor = Exception.class)  // checked bhi rollback
@Transactional(noRollbackFor = IllegalStateException.class)  // specific exclude
```

---

## Interview Q&A

**Q: `@Transactional` method ko same class se call karne pe kaam kyun nahi karta?**

Spring AOP proxy-based hai. Same class se method call proxy bypass karta hai — Spring intercept nahi kar paata. `self-injection` (bean ko inject karna) ya `AopContext` use karo, ya better design karo.

**Q: `REQUIRES_NEW` vs `NESTED` mein kya farq hai?**

`REQUIRES_NEW`: Completely independent transaction. Parent suspend ho jata hai. Child commit/rollback independent. `NESTED`: Same physical transaction, savepoint-based. Parent rollback se child bhi rollback. Child rollback se parent unaffected.

**Q: Transaction timeout kaise set karein?**

`@Transactional(timeout = 30)` — seconds mein. Default: underlying transaction manager ka timeout.

**Q: `@Transactional` private method pe kaam karega?**

Nahi. Spring AOP proxy sirf public methods pe kaam karta hai. Private method pe `@Transactional` ignore ho jayega.

---

# 27. Spring Security — JWT, OAuth2 Basics

## 27.1 Spring Security Architecture

```
HTTP Request
    │
    ▼
Filter Chain (SecurityFilterChain)
    ├── UsernamePasswordAuthenticationFilter
    ├── JwtAuthenticationFilter (custom)
    ├── AuthorizationFilter
    └── ...
    │
    ▼
AuthenticationManager
    │
    ▼
AuthenticationProvider
    │
    ▼
UserDetailsService → UserDetails
```

## 27.2 JWT (JSON Web Token)

```
header.payload.signature

header: { "alg": "HS256", "typ": "JWT" }
payload: { "sub": "user123", "roles": ["USER"], "exp": 1234567890 }
signature: HMACSHA256(base64(header) + "." + base64(payload), secret)
```

```java
@Component
public class JwtUtil {
    private String secret = "mySecretKey";

    public String generateToken(String username) {
        return Jwts.builder()
            .setSubject(username)
            .setIssuedAt(new Date())
            .setExpiration(new Date(System.currentTimeMillis() + 86400000))
            .signWith(SignatureAlgorithm.HS256, secret)
            .compact();
    }

    public String extractUsername(String token) {
        return Jwts.parser().setSigningKey(secret)
            .parseClaimsJws(token).getBody().getSubject();
    }
}
```

## 27.3 OAuth2 Basics

**Roles:**
- Resource Owner: User
- Client: Application
- Authorization Server: Token issue karta hai
- Resource Server: API protect karta hai

**Flows:**
- Authorization Code (most secure, web apps)
- Implicit (SPA, deprecated)
- Password (trusted apps, deprecated)
- Client Credentials (server-to-server)

---

## Interview Q&A

**Q: JWT vs Session-based authentication mein kya farq hai?**

Session: Server-side session store karta hai, session ID cookie mein bhejta hai. Stateful. JWT: Self-contained token, server pe storage nahi chahiye. Stateless. JWT scale karta hai better (no session storage), lekin revoke karna mushkil hai (token expiry tak valid).

**Q: JWT token ko kaise invalidate karein?**

JWT stateless hai — server pe store nahi hota. Options:
1. Short expiry + refresh token
2. Blacklist (Redis mein revoked tokens store karo)
3. Token version/rotation

**Q: Spring Security filter chain kaise kaam karta hai?**

`DelegatingFilterProxy` → `FilterChainProxy` → multiple `SecurityFilterChain`. Har request filters se guzarti hai. Authentication filter token validate karta hai, `AuthenticationManager` authenticate karta hai, `SecurityContext` mein store karta hai.

**Q: `@PreAuthorize` vs `@Secured` mein kya farq hai?**

`@Secured`: Simple role-based (`@Secured("ROLE_ADMIN")`). `@PreAuthorize`: Expression-based, zyada powerful (`@PreAuthorize("hasRole('ADMIN') and #id < 100")`). `@PreAuthorize` modern aur flexible hai.

---

# 28. REST API Design — Best Practices

## 28.1 HTTP Methods

| Method | Idempotent | Safe | Use Case |
|--------|-----------|------|----------|
| GET | Yes | Yes | Read |
| POST | No | No | Create |
| PUT | Yes | No | Full update / Replace |
| PATCH | No | No | Partial update |
| DELETE | Yes | No | Remove |

## 28.2 Status Codes

| Code | Meaning |
|------|---------|
| 200 OK | Success |
| 201 Created | Resource created |
| 204 No Content | Success, no body |
| 400 Bad Request | Invalid input |
| 401 Unauthorized | Authentication required |
| 403 Forbidden | No permission |
| 404 Not Found | Resource doesn't exist |
| 409 Conflict | Resource conflict |
| 500 Internal Server Error | Server error |

## 28.3 URL Design

```
GET    /api/v1/users           → List users
GET    /api/v1/users/{id}      → Get user
POST   /api/v1/users           → Create user
PUT    /api/v1/users/{id}      → Update user (full)
PATCH  /api/v1/users/{id}      → Update user (partial)
DELETE /api/v1/users/{id}      → Delete user
GET    /api/v1/users/{id}/orders → Get user's orders
```

**Rules:**
- Nouns use karo, verbs nahi (`/getUsers` ❌, `/users` ✅)
- Plural nouns (`/users` not `/user`)
- Versioning (`/v1/`, `/v2/`)
- Pagination: `?page=0&size=10&sort=name,asc`
- Filtering: `?status=ACTIVE&role=ADMIN`

## 28.4 HATEOAS (optional)

```json
{
    "id": 1,
    "name": "Alice",
    "_links": {
        "self": { "href": "/api/v1/users/1" },
        "orders": { "href": "/api/v1/users/1/orders" }
    }
}
```

---

## Interview Q&A

**Q: Idempotent kya hota hai?**

Same request multiple times karne pe same result. GET, PUT, DELETE idempotent hain. POST nahi (har baar naya resource). Payment APIs mein idempotency keys use hote hain.

**Q: `PUT` vs `PATCH` mein kya farq hai?**

`PUT` full resource replace karta hai — missing fields null/default ho jate hain. `PATCH` partial update karta hai — sirf provided fields update hote hain.

**Q: API versioning ka best tareeka kya hai?**

URL path (`/v1/`, `/v2/`) — most common and explicit. Alternatives: Header (`Accept: application/vnd.api.v1+json`), Query param (`?version=1`). URL path easiest to understand and cache.

**Q: Pagination mein offset vs cursor-based mein kya farq hai?**

Offset (`?page=0&size=10`): Simple, lekin large offsets slow hote hain (deep pagination problem). Cursor-based (`?after=xyz`): Fast for large datasets, real-time data ke liye better, lekin random access nahi possible.

---

# 29. Microservices Architecture

## 29.1 Monolith vs Microservices

| Monolith | Microservices |
|----------|---------------|
| Single deployable unit | Multiple independent services |
| Shared database | Database per service |
| Tight coupling | Loose coupling |
| Simple to develop | Complex to develop |
| Hard to scale individual parts | Scale specific services |
| Single tech stack | Polyglot (different tech per service) |

## 29.2 Key Patterns

**API Gateway:**
- Single entry point for clients
- Authentication, rate limiting, routing
- Examples: Spring Cloud Gateway, Netflix Zuul

**Service Discovery:**
- Services dynamically register and discover each other
- Examples: Eureka, Consul, Zookeeper

**Circuit Breaker:**
- Failing service ko temporarily bypass karna
- States: CLOSED → OPEN (after threshold) → HALF-OPEN (retry)
- Examples: Resilience4j, Hystrix (deprecated)

```java
@CircuitBreaker(name = "orderService", fallbackMethod = "fallback")
public Order getOrder(Long id) {
    return orderClient.getOrder(id);
}

public Order fallback(Long id, Exception ex) {
    return new Order(id, "DEFAULT");  // cached/default response
}
```

**Config Server:**
- Centralized configuration management
- Spring Cloud Config Server

## 29.3 Inter-Service Communication

| Type | Use Case | Examples |
|------|----------|----------|
| Synchronous (REST) | Real-time, simple | HTTP/REST, gRPC |
| Asynchronous (Messaging) | Decoupled, scalable | Kafka, RabbitMQ |

## 29.4 Data Management

**Database per Service:**
- Har service apna database own karta hai
- Data consistency via Saga pattern

**Saga Patterns:**
- **Orchestration**: Central coordinator manages transactions
- **Choreography**: Services events publish/subscribe karte hain

---

## Interview Q&A

**Q: Microservices ke challenges kya hain?**

Distributed system complexity: network failures, data consistency, debugging, deployment overhead, inter-service communication latency, testing complexity. "Microservices nahi, Distributed Monolith" ban sakta hai agar services tightly coupled hain.

**Q: API Gateway kya karta hai?**

Single entry point, request routing, load balancing, authentication, SSL termination, rate limiting, request/response transformation. Client ko har service ka endpoint nahi pata chahiye.

**Q: Circuit Breaker pattern kyun zaroori hai?**

Cascading failures prevent karta hai. Agar downstream service slow/failing hai, to upstream service bhi resource exhaust kar sakti hai waiting mein. Circuit breaker fail fast karta hai aur fallback deta hai.

**Q: Saga pattern kya hai?**

Distributed transactions manage karne ka pattern. Local transactions + compensating transactions. Orchestration: central saga manager. Choreography: services events se communicate karte hain.

**Q: When NOT to use microservices?**

Small team, simple domain, no scaling needs, tight deadlines. Monolith se shuru karo, jab pain points aayein tab extract karo (Strangler Fig pattern).

---

# 30. Caching — Redis Basics

## 30.1 Why Caching?

Database calls slow hain. Frequently accessed data ko memory mein store karo for fast retrieval.

**Cache Aside Pattern:**
```
1. Check cache → hit? return
2. Cache miss → fetch from DB
3. Store in cache → return
```

## 30.2 Spring Cache Abstraction

```java
@Configuration
@EnableCaching
public class CacheConfig {
    @Bean
    public CacheManager cacheManager() {
        return new ConcurrentMapCacheManager("users", "products");
    }
}

@Service
public class UserService {
    @Cacheable(value = "users", key = "#id")
    public User getUser(Long id) {
        return userRepo.findById(id).orElseThrow();
    }

    @CacheEvict(value = "users", key = "#user.id")
    public void updateUser(User user) {
        userRepo.save(user);
    }

    @CachePut(value = "users", key = "#user.id")
    public User updateAndCache(User user) {
        return userRepo.save(user);
    }
}
```

## 30.3 Redis

In-memory data structure store. Used as cache, message broker, database.

```java
// Spring Data Redis
@Autowired
private StringRedisTemplate redisTemplate;

public void cacheUser(String key, User user) {
    redisTemplate.opsForValue().set(key, json, Duration.ofMinutes(10));
}

public User getCachedUser(String key) {
    String json = redisTemplate.opsForValue().get(key);
    return json != null ? objectMapper.readValue(json, User.class) : null;
}
```

**Redis Data Types:**
- String, Hash, List, Set, Sorted Set, Bitmap, HyperLogLog, Stream

---

## Interview Q&A

**Q: Cache stampede / thundering herd kya hai?**

Cache expire hone pe multiple requests simultaneously DB hit karte hain. Solutions: staggered TTL, cache warming, singleflight pattern (sirf ek request DB jaye, baaki wait karein).

**Q: Cache eviction policies kya hain?**

LRU (Least Recently Used), LFU (Least Frequently Used), FIFO, Random. Redis mein `volatile-lru`, `allkeys-lru`, etc.

**Q: Cache-Aside vs Read-Through vs Write-Through mein kya farq hai?**

Cache-Aside: Application cache manage karta hai. Read-Through: Cache library DB fetch karta hai miss pe. Write-Through: Write simultaneously DB aur cache dono mein hota hai.

**Q: `@Cacheable` vs `@CachePut` mein kya farq hai?**

`@Cacheable`: Pehle cache check karta hai, miss pe method execute aur cache karta hai. `@CachePut`: Hamesha method execute karta hai aur result cache mein daalta hai (update ke liye).

---

# 31. Message Queues — Kafka/RabbitMQ Basics

## 31.1 Why Message Queues?

- Decoupling: Producer aur consumer independent
- Async processing: Request immediately return, processing background mein
- Load leveling: Spikes handle karta hai
- Reliability: Message persist hota hai

## 31.2 Kafka Basics

**Architecture:**
- **Producer**: Messages bhejta hai
- **Consumer**: Messages padhta hai
- **Broker**: Kafka server
- **Topic**: Message category
- **Partition**: Topic ka shard, ordered log
- **Offset**: Message position in partition
- **Consumer Group**: Multiple consumers load share karte hain

```java
// Producer
KafkaProducer<String, String> producer = new KafkaProducer<>(props);
producer.send(new ProducerRecord<>("orders", orderId, orderJson));

// Consumer
KafkaConsumer<String, String> consumer = new KafkaConsumer<>(props);
consumer.subscribe(Arrays.asList("orders"));
ConsumerRecords<String, String> records = consumer.poll(Duration.ofMillis(100));
```

**Kafka Guarantees:**
- At-most-once: Message lost ho sakta hai
- At-least-once: Message duplicate ho sakta hai (default)
- Exactly-once: Idempotent producer + transactions

## 31.3 RabbitMQ Basics

**Architecture:**
- **Exchange**: Message routing (direct, topic, fanout, headers)
- **Queue**: Message storage
- **Binding**: Exchange to Queue connection
- **Routing Key**: Message routing identifier

```java
// Spring AMQP
@RabbitListener(queues = "order-queue")
public void handleOrder(OrderMessage order) {
    processOrder(order);
}

@Autowired
private RabbitTemplate rabbitTemplate;

public void sendOrder(Order order) {
    rabbitTemplate.convertAndSend("exchange", "routing.key", order);
}
```

## 31.4 Kafka vs RabbitMQ

| Feature | Kafka | RabbitMQ |
|---------|-------|----------|
| Architecture | Distributed log | Message broker |
| Throughput | Very high (millions/sec) | High (thousands/sec) |
| Message Retention | Configurable (days) | Consumed = removed |
| Replay | Yes | No |
| Use Case | Event streaming, logs | Task queues, RPC |
| Ordering | Per partition | Per queue |

---

## Interview Q&A

**Q: Kafka mein partition kyun important hai?**

Parallelism aur ordering. Same partition mein messages ordered hain. Different partitions parallel consume ho sakte hain. Producer key se partition decide hota hai.

**Q: Consumer group ka concept batao.**

Ek consumer group mein saare consumers topic ke partitions ko share karte hain. Har partition exactly ek consumer ko assign hota hai. New consumer add karne pe rebalancing hoti hai. Multiple groups independently same messages consume kar sakte hain.

**Q: Dead Letter Queue (DLQ) kya hai?**

Messages jo process nahi ho sakte (after retries) unko DLQ mein bhejna. Baad mein analysis aur reprocessing ke liye. Error handling aur monitoring ke liye important.

**Q: Message queue mein message ordering kaise ensure karein?**

Single partition/queue mein ordering guaranteed. Multiple partitions mein ordering nahi guaranteed. Agar ordering zaroori hai, to same key use karo (same partition jayega) ya single partition use karo (throughput trade-off).

**Q: Idempotent consumer kyun zaroori hai?**

At-least-once delivery mein messages duplicate ho sakte hain. Consumer ko idempotent banana chahiye — same message do baar process karne pe same result. Unique message IDs se deduplication karo.

---

<div align="center">

# 🎯 Quick Reference — Sabse Zyada Puche Jane Wale Questions

## Core Java
- OOPs: Encapsulation vs Abstraction, Overloading vs Overriding
- String: Pool, Immutability, Builder vs Buffer
- Collections: HashMap internals, ArrayList vs LinkedList, fail-fast vs fail-safe
- Java 8: Lambda, Stream (map vs flatMap), Optional, Date/Time API
- Exception: Checked vs Unchecked, try-with-resources
- equals/hashCode contract, Comparable vs Comparator

## Advanced
- JDBC: PreparedStatement vs Statement, SQL Injection
- Design Patterns: Singleton, Factory, Builder, Strategy
- Testing: JUnit lifecycle, Mockito mock vs spy

## Spring
- IOC/DI: Constructor injection, @Autowired vs @Inject
- AOP: Proxy-based, Advice types
- Boot: Auto-configuration, Starters, Actuator
- JPA: Lazy vs Eager, N+1, Cascade, @Transactional
- Security: JWT vs Session, Filter chain
- REST: HTTP methods, Status codes, Idempotency
- Microservices: API Gateway, Circuit Breaker, Service Discovery

## Data
- Redis: Cache patterns, eviction
- Kafka: Partitions, Consumer groups, Exactly-once

---

**☕ Best of Luck for Your Interview!**

*Ye guide regularly update hoti rahegi. Feedback welcome.*

</div>
