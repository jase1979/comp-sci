---
layout: topic
title: "Principles of Programming"
level: "A2 Level"
level_url: "/a2/"
unit_name: "Unit 3: Programming & System Development"
unit_url: "/a2/unit3/"
subtopics:
  - "Different programming paradigms and their advantages"
  - "Situations where each paradigm may be used"
  - "Object-oriented approach: Object, class, method"
  - "Standardisation of computer languages"
  - "Difficulties in agreeing and implementing standards"
  - "Ambiguities in natural language"
  - "Need for unambiguous syntax in computer languages"
  - "Syntax diagrams and Backus-Naur Form (BNF)"
---

## Programming Paradigms

A **programming paradigm** is a fundamental style or approach to programming that dictates how problems are structured, broken down, and solved. Different paradigms suit different types of problem, and understanding when to apply each one is essential at A2 level.

### Procedural Programming

Procedural programming organises code as a sequence of instructions grouped into procedures (also called subroutines or functions). The program executes statements in order, calling procedures as needed.

<div class="key-term" markdown="1">
**Procedural programming** is a paradigm based on the concept of procedure calls, where programs are built from one or more procedures (sequences of instructions) that operate on data.
</div>

**Key features:**
- Programs follow a top-down, step-by-step approach
- Code is organised into reusable procedures/functions
- Data and functions are kept separate
- Uses sequence, selection, and iteration as control structures
- Variables may be local or global in scope

```python
# Procedural approach: calculating average of marks
def get_marks():
    marks = []
    for i in range(5):
        mark = int(input("Enter mark: "))
        marks.append(mark)
    return marks

def calculate_average(marks):
    total = sum(marks)
    return total / len(marks)

def display_result(average):
    print(f"The average mark is: {average:.1f}")

# Main program flow
marks = get_marks()
avg = calculate_average(marks)
display_result(avg)
```

```vb
' Procedural approach: calculating average of marks
Sub Main()
    Dim marks(4) As Integer
    GetMarks(marks)
    Dim avg As Double = CalculateAverage(marks)
    DisplayResult(avg)
End Sub

Sub GetMarks(ByRef marks() As Integer)
    For i As Integer = 0 To 4
        Console.Write("Enter mark: ")
        marks(i) = CInt(Console.ReadLine())
    Next
End Sub

Function CalculateAverage(marks() As Integer) As Double
    Dim total As Integer = 0
    For Each mark As Integer In marks
        total += mark
    Next
    Return total / marks.Length
End Function

Sub DisplayResult(average As Double)
    Console.WriteLine($"The average mark is: {average:F1}")
End Sub
```

**Advantages:**
- Simple and straightforward to understand
- Easy to trace the flow of execution
- Well suited for small to medium-sized programs
- Good for scripting and automation tasks

**When to use:**
- Simple sequential tasks such as batch processing or scripts
- Mathematical or scientific calculations
- Problems where data structures are straightforward
- When the development team is more familiar with procedural approaches

### Object-Oriented Programming (OOP)

Object-oriented programming organises code around **objects** that combine data (attributes) and behaviour (methods) together. Programs are built by defining classes and creating objects that interact with one another.

**Key features:**
- Encapsulation of data and methods within objects
- Inheritance allows code reuse through class hierarchies
- Polymorphism enables a single interface for different underlying forms
- Abstraction hides complex details behind simple interfaces

**Advantages:**
- Models real-world entities naturally
- Promotes code reuse through inheritance
- Easier to maintain and modify large codebases
- Encapsulation protects data integrity
- Supports modular development by teams

**When to use:**
- Large, complex systems such as enterprise applications
- GUI-based applications and games
- Projects requiring long-term maintenance
- Simulations that model real-world entities
- When multiple developers work on different components

### Functional Programming

Functional programming treats computation as the evaluation of mathematical functions. It avoids changing state and mutable data, relying instead on pure functions and immutable values.

<div class="key-term" markdown="1">
**Functional programming** is a paradigm where programs are constructed by applying and composing **pure functions** -- functions that always produce the same output for the same input and have no side effects.
</div>

**Key features:**
- First-class functions (functions can be passed as arguments and returned as values)
- Pure functions with no side effects
- Immutable data (values cannot be changed once created)
- Recursion used instead of iterative loops
- Higher-order functions such as `map`, `filter`, and `reduce`

```python
# Functional approach: filtering and transforming a list
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Use map, filter, and lambda (higher-order functions)
evens = list(filter(lambda x: x % 2 == 0, numbers))
squared_evens = list(map(lambda x: x ** 2, evens))

print(squared_evens)  # Output: [4, 16, 36, 64, 100]

# Using recursion instead of a loop
def factorial(n):
    if n <= 1:
        return 1
    return n * factorial(n - 1)

print(factorial(5))  # Output: 120
```

```vb
' Functional-style approach in VB.NET using LINQ and lambda
Imports System.Linq

Module FunctionalExample
    Sub Main()
        Dim numbers() As Integer = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10}

        ' Filter and map using LINQ with lambda expressions
        Dim squaredEvens = numbers.
            Where(Function(x) x Mod 2 = 0).
            Select(Function(x) x * x).
            ToList()

        For Each value In squaredEvens
            Console.Write(value & " ")  ' Output: 4 16 36 64 100
        Next
    End Sub

    ' Recursive factorial
    Function Factorial(n As Integer) As Integer
        If n <= 1 Then Return 1
        Return n * Factorial(n - 1)
    End Function
End Module
```

**Advantages:**
- Easier to test and debug because pure functions have predictable outputs
- Well suited to parallel and concurrent processing (no shared mutable state)
- Produces concise, mathematically elegant code
- Fewer bugs related to unintended side effects

**When to use:**
- Data processing and transformation pipelines
- Concurrent or parallel programming
- Mathematical and statistical computation
- Problems that can be expressed as transformations on data

### Declarative / Logic Programming

Declarative programming describes **what** the program should accomplish rather than **how** to accomplish it. Logic programming (e.g. Prolog) is a subset where programs are expressed as a set of facts and rules, and the system uses logical inference to derive answers.

<div class="key-term" markdown="1">
**Declarative programming** specifies the desired result without explicitly listing the step-by-step commands needed to achieve it. **Logic programming** uses facts and rules to answer queries through logical inference.
</div>

**Key features:**
- Programs state facts and rules rather than procedures
- A query engine derives solutions automatically
- Backtracking is used to explore possible solutions
- No explicit control flow (the runtime determines execution order)

**Example in Prolog (logic programming):**
```
% Facts
parent(tom, bob).
parent(tom, liz).
parent(bob, ann).
parent(bob, pat).

% Rule
grandparent(X, Z) :- parent(X, Y), parent(Y, Z).

% Query: Who are Tom's grandchildren?
?- grandparent(tom, Who).
% Result: Who = ann ; Who = pat
```

**Advantages:**
- Very concise for problems involving relationships and rules
- The programmer focuses on the problem domain, not the algorithm
- Well suited to artificial intelligence and expert systems
- Easy to add new facts and rules without restructuring code

**When to use:**
- Database queries (SQL is declarative)
- Artificial intelligence and expert systems
- Natural language processing
- Scheduling and constraint-satisfaction problems
- Rule-based systems

### Paradigm Comparison

| Feature | Procedural | Object-Oriented | Functional | Declarative/Logic |
|---|---|---|---|---|
| **Focus** | Steps/procedures | Objects and interactions | Functions and transformations | Facts and rules |
| **Data handling** | Separate from functions | Encapsulated in objects | Immutable values | Facts in a knowledge base |
| **Code reuse** | Procedures/functions | Inheritance and polymorphism | Higher-order functions | Reusable rules |
| **Best for** | Simple scripts, calculations | Large systems, GUIs | Data processing, concurrency | AI, databases, expert systems |
| **Example languages** | C, Pascal, early BASIC | Java, Python, C#, VB.NET | Haskell, Erlang, Lisp | Prolog, SQL |

<div class="exam-tip" markdown="1">
Exam questions often ask you to **justify** which paradigm is most appropriate for a given scenario. Always link your answer to the specific features of the paradigm (e.g. "OOP is appropriate because the system models real-world entities such as customers and orders, which naturally map to objects with attributes and methods").
</div>

---

## Object-Oriented Programming Concepts

OOP is built on several core concepts. You must be able to define each concept, explain its purpose, and provide code examples.

### Classes and Objects

<div class="key-term" markdown="1">
A **class** is a blueprint or template that defines the attributes (data) and methods (behaviour) that objects of that type will have. An **object** is a specific instance of a class, with its own values for the attributes defined by the class.
</div>

```python
class Dog:
    def __init__(self, name, breed, age):
        self.__name = name      # private attribute
        self.__breed = breed    # private attribute
        self.__age = age        # private attribute

    def bark(self):
        return f"{self.__name} says Woof!"

    def get_name(self):
        return self.__name

    def get_info(self):
        return f"{self.__name} is a {self.__age}-year-old {self.__breed}"

# Creating objects (instances of the Dog class)
dog1 = Dog("Rex", "German Shepherd", 5)
dog2 = Dog("Bella", "Labrador", 3)

print(dog1.bark())       # Rex says Woof!
print(dog2.get_info())   # Bella is a 3-year-old Labrador
```

```vb
Public Class Dog
    Private _name As String
    Private _breed As String
    Private _age As Integer

    Public Sub New(name As String, breed As String, age As Integer)
        _name = name
        _breed = breed
        _age = age
    End Sub

    Public Function Bark() As String
        Return $"{_name} says Woof!"
    End Function

    Public Function GetName() As String
        Return _name
    End Function

    Public Function GetInfo() As String
        Return $"{_name} is a {_age}-year-old {_breed}"
    End Function
End Class

' Creating objects
Dim dog1 As New Dog("Rex", "German Shepherd", 5)
Dim dog2 As New Dog("Bella", "Labrador", 3)

Console.WriteLine(dog1.Bark())       ' Rex says Woof!
Console.WriteLine(dog2.GetInfo())    ' Bella is a 3-year-old Labrador
```

### Methods and Attributes

<div class="key-term" markdown="1">
**Attributes** (also called properties or fields) are the data items stored within an object. **Methods** are the functions defined within a class that operate on the object's attributes and define its behaviour.
</div>

Methods typically fall into several categories:

| Method Type | Purpose | Example |
|---|---|---|
| **Constructor** | Initialises a new object | `__init__` in Python, `Sub New` in VB.NET |
| **Accessor (getter)** | Returns the value of a private attribute | `get_name()` |
| **Mutator (setter)** | Changes the value of a private attribute | `set_name(new_name)` |
| **General method** | Performs an action or calculation | `bark()`, `calculate_area()` |

### Encapsulation

<div class="key-term" markdown="1">
**Encapsulation** is the bundling of data (attributes) and the methods that operate on that data into a single unit (class), while restricting direct access to the internal state. External code interacts with the object only through its public methods.
</div>

Encapsulation is achieved by making attributes **private** and providing **public getter and setter methods** to control access. This protects the data from being set to invalid values.

```python
class BankAccount:
    def __init__(self, account_holder, balance=0):
        self.__account_holder = account_holder
        self.__balance = balance  # private attribute

    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount
            return True
        return False

    def withdraw(self, amount):
        if 0 < amount <= self.__balance:
            self.__balance -= amount
            return True
        return False

    def get_balance(self):
        return self.__balance

account = BankAccount("Alice", 1000)
account.deposit(500)
account.withdraw(200)
print(account.get_balance())  # 1300
# account.__balance = -999   # This would NOT work (name mangling)
```

```vb
Public Class BankAccount
    Private _accountHolder As String
    Private _balance As Decimal

    Public Sub New(accountHolder As String, Optional balance As Decimal = 0)
        _accountHolder = accountHolder
        _balance = balance
    End Sub

    Public Function Deposit(amount As Decimal) As Boolean
        If amount > 0 Then
            _balance += amount
            Return True
        End If
        Return False
    End Function

    Public Function Withdraw(amount As Decimal) As Boolean
        If amount > 0 AndAlso amount <= _balance Then
            _balance -= amount
            Return True
        End If
        Return False
    End Function

    Public ReadOnly Property Balance As Decimal
        Get
            Return _balance
        End Get
    End Property
End Class

Dim account As New BankAccount("Alice", 1000)
account.Deposit(500)
account.Withdraw(200)
Console.WriteLine(account.Balance)  ' 1300
```

### Inheritance

<div class="key-term" markdown="1">
**Inheritance** allows a new class (subclass or child class) to be based on an existing class (superclass or parent class), inheriting its attributes and methods. The subclass can add new attributes/methods or override existing ones.
</div>

```python
class Animal:
    def __init__(self, name, species):
        self.__name = name
        self.__species = species

    def get_name(self):
        return self.__name

    def speak(self):
        return "..."

class Dog(Animal):  # Dog inherits from Animal
    def __init__(self, name, breed):
        super().__init__(name, "Dog")
        self.__breed = breed

    def speak(self):          # overriding the parent method
        return "Woof!"

    def get_breed(self):      # new method specific to Dog
        return self.__breed

class Cat(Animal):  # Cat also inherits from Animal
    def speak(self):          # overriding the parent method
        return "Meow!"

dog = Dog("Rex", "Labrador")
cat = Cat("Whiskers", "Cat")
print(f"{dog.get_name()} says {dog.speak()}")  # Rex says Woof!
print(f"{cat.get_name()} says {cat.speak()}")  # Whiskers says Meow!
```

```vb
Public Class Animal
    Private _name As String
    Private _species As String

    Public Sub New(name As String, species As String)
        _name = name
        _species = species
    End Sub

    Public Function GetName() As String
        Return _name
    End Function

    Public Overridable Function Speak() As String
        Return "..."
    End Function
End Class

Public Class Dog
    Inherits Animal

    Private _breed As String

    Public Sub New(name As String, breed As String)
        MyBase.New(name, "Dog")
        _breed = breed
    End Sub

    Public Overrides Function Speak() As String
        Return "Woof!"
    End Function

    Public Function GetBreed() As String
        Return _breed
    End Function
End Class

Public Class Cat
    Inherits Animal

    Public Sub New(name As String)
        MyBase.New(name, "Cat")
    End Sub

    Public Overrides Function Speak() As String
        Return "Meow!"
    End Function
End Class

Dim dog As New Dog("Rex", "Labrador")
Dim cat As New Cat("Whiskers")
Console.WriteLine($"{dog.GetName()} says {dog.Speak()}")  ' Rex says Woof!
Console.WriteLine($"{cat.GetName()} says {cat.Speak()}")  ' Whiskers says Meow!
```

### Polymorphism

<div class="key-term" markdown="1">
**Polymorphism** (meaning "many forms") allows objects of different classes to be treated through the same interface. A method call on a variable can produce different behaviour depending on the actual type of the object at runtime.
</div>

In the inheritance example above, both `Dog` and `Cat` override the `speak()` method. We can treat them polymorphically:

```python
# Polymorphism in action
animals = [Dog("Rex", "Labrador"), Cat("Whiskers", "Cat")]

for animal in animals:
    # The same method call produces different output
    print(f"{animal.get_name()} says {animal.speak()}")

# Output:
# Rex says Woof!
# Whiskers says Meow!
```

```vb
' Polymorphism in action
Dim animals As New List(Of Animal)
animals.Add(New Dog("Rex", "Labrador"))
animals.Add(New Cat("Whiskers"))

For Each animal As Animal In animals
    ' The same method call produces different output
    Console.WriteLine($"{animal.GetName()} says {animal.Speak()}")
Next

' Output:
' Rex says Woof!
' Whiskers says Meow!
```

### Abstraction

<div class="key-term" markdown="1">
**Abstraction** is the process of hiding complex implementation details and exposing only the essential features to the user. In OOP, abstract classes and interfaces define what an object can do without specifying how it does it.
</div>

Abstraction allows programmers to work with high-level concepts. For example, a `Shape` abstract class might define that all shapes must have a `calculate_area()` method, but each specific shape implements the calculation differently.

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def calculate_area(self):
        pass

    @abstractmethod
    def describe(self):
        pass

class Circle(Shape):
    def __init__(self, radius):
        self.__radius = radius

    def calculate_area(self):
        return 3.14159 * self.__radius ** 2

    def describe(self):
        return f"Circle with radius {self.__radius}"

class Rectangle(Shape):
    def __init__(self, width, height):
        self.__width = width
        self.__height = height

    def calculate_area(self):
        return self.__width * self.__height

    def describe(self):
        return f"Rectangle {self.__width} x {self.__height}"

shapes = [Circle(5), Rectangle(4, 6)]
for shape in shapes:
    print(f"{shape.describe()}: area = {shape.calculate_area()}")
```

```vb
Public MustInherit Class Shape
    Public MustOverride Function CalculateArea() As Double
    Public MustOverride Function Describe() As String
End Class

Public Class Circle
    Inherits Shape

    Private _radius As Double

    Public Sub New(radius As Double)
        _radius = radius
    End Sub

    Public Overrides Function CalculateArea() As Double
        Return 3.14159 * _radius ^ 2
    End Function

    Public Overrides Function Describe() As String
        Return $"Circle with radius {_radius}"
    End Function
End Class

Public Class Rectangle
    Inherits Shape

    Private _width As Double
    Private _height As Double

    Public Sub New(width As Double, height As Double)
        _width = width
        _height = height
    End Sub

    Public Overrides Function CalculateArea() As Double
        Return _width * _height
    End Function

    Public Overrides Function Describe() As String
        Return $"Rectangle {_width} x {_height}"
    End Function
End Class

Dim shapes As New List(Of Shape)
shapes.Add(New Circle(5))
shapes.Add(New Rectangle(4, 6))
For Each shape As Shape In shapes
    Console.WriteLine($"{shape.Describe()}: area = {shape.CalculateArea()}")
Next
```

<div class="exam-tip" markdown="1">
A common exam question asks you to distinguish between **encapsulation** and **abstraction**. Encapsulation is about **hiding data** behind private access and controlling it through public methods. Abstraction is about **hiding complexity** so that users interact with a simplified interface without needing to know the internal workings.
</div>

---

## Standardisation of Computer Languages

### Why Standards Matter

Standardisation ensures that programming languages behave consistently across different compilers, interpreters, and platforms. Standards are set by recognised bodies including:

| Organisation | Full Name | Role |
|---|---|---|
| **ANSI** | American National Standards Institute | Sets US standards, including for C and SQL |
| **ISO** | International Organization for Standardization | Sets international standards for many languages (C, C++, SQL, etc.) |
| **W3C** | World Wide Web Consortium | Sets standards for web technologies (HTML, CSS, XML, etc.) |
| **IEEE** | Institute of Electrical and Electronics Engineers | Sets standards for floating-point arithmetic, networking, etc. |
| **ECMA** | European Computer Manufacturers Association | Standards for JavaScript (ECMAScript), C#, etc. |

**Benefits of standardisation:**

- **Portability** -- programs written in a standard-compliant language can be compiled and run on different platforms without modification
- **Interoperability** -- different software systems can work together when they follow the same standards
- **Consistency** -- programmers can move between tools and platforms with confidence that the language behaves the same way
- **Education** -- teaching and learning are simplified when there is one agreed version of a language
- **Longevity** -- standardised code is more likely to remain usable as technology changes

### Difficulties in Agreeing Standards

Despite the clear benefits, reaching agreement on language standards is challenging:

- **Competing interests** -- different companies and organisations may favour features that benefit their own products or platforms
- **Pace of change** -- technology evolves faster than standards committees can agree on specifications; by the time a standard is published it may already be outdated
- **Legacy compatibility** -- new standards must remain backward-compatible with existing code, which constrains innovation
- **Complexity** -- modern languages are extremely complex, and specifying every detail precisely is a huge task (the C++ standard is over 1,500 pages)
- **Vendor extensions** -- companies often add proprietary extensions to languages, which fragments the ecosystem (e.g. Microsoft's extensions to C++)
- **International differences** -- representatives from different countries may have different priorities and requirements

<div class="exam-tip" markdown="1">
When asked about difficulties in agreeing standards, focus on the **tension between innovation and stability**. Companies want to innovate quickly with new features, but standards require slow, careful deliberation to ensure reliability and broad agreement.
</div>

---

## Ambiguities in Natural Language

Natural languages (such as English or Welsh) are inherently ambiguous. A single sentence can have multiple valid interpretations. This is in stark contrast to programming languages, which must be completely unambiguous.

### Lexical Ambiguity

<div class="key-term" markdown="1">
**Lexical ambiguity** occurs when a single word has more than one meaning. The correct meaning depends on context.
</div>

**Examples:**
- "I went to the **bank**." -- a financial institution or the side of a river?
- "She could not **bear** the weight." -- to tolerate, or a large animal?
- "The **bat** flew across the garden." -- a flying mammal or a cricket bat?
- "He **left** his keys on the **left** side." -- departed/remaining, or a direction?

### Syntactic Ambiguity

<div class="key-term" markdown="1">
**Syntactic ambiguity** occurs when the grammatical structure of a sentence allows more than one interpretation, even though each individual word is clear.
</div>

**Examples:**
- "I saw the man with the telescope." -- Did I use a telescope to see him, or did he have a telescope?
- "Flying planes can be dangerous." -- The act of flying planes, or planes that are flying?
- "The teacher said on Monday he would set a test." -- Did the teacher make the statement on Monday, or is the test on Monday?
- "Visiting relatives can be boring." -- The act of visiting, or relatives who are visiting?

### Semantic Ambiguity

<div class="key-term" markdown="1">
**Semantic ambiguity** occurs when a sentence is grammatically clear but can still be interpreted in different ways due to the meaning of the words in context.
</div>

**Examples:**
- "The chicken is ready to eat." -- The chicken is cooked and ready to be eaten, or the chicken (animal) is hungry and ready to eat food?
- "Every student read a book." -- Did they all read the same book, or did each read a different one?
- "Time flies like an arrow." -- Time passes quickly, or there is a species of flies called "time flies" that are fond of arrows?

### Why This Matters for Programming

These types of ambiguity illustrate why natural language cannot be used directly as a programming language. A computer must execute instructions with absolute precision and cannot resolve ambiguous statements. This motivates the need for **formal, unambiguous syntax** in programming languages, which is defined using tools such as syntax diagrams and BNF notation.

---

## Need for Unambiguous Syntax

<div class="key-term" markdown="1">
**Syntax** is the set of rules that defines the valid structure of statements in a programming language. Programming language syntax must be completely unambiguous so that every valid program has exactly one interpretation.
</div>

Programming languages require unambiguous syntax because:

- **Compilers and interpreters** must parse source code into a single, definitive structure -- if a statement could be interpreted in two ways, the machine would not know which one the programmer intended
- **Correctness** -- ambiguous syntax could lead to programs producing unexpected results
- **Error detection** -- clear syntax rules allow compilers to identify and report errors precisely
- **Consistency** -- all programmers and all tools agree on what a given piece of code means

Two formal methods are used to define unambiguous syntax: **syntax diagrams** and **Backus-Naur Form (BNF)**.

---

## Syntax Diagrams

<div class="key-term" markdown="1">
A **syntax diagram** (also called a railroad diagram) is a graphical representation of the syntax rules of a language. It uses lines, arrows, and labelled shapes to show the valid sequences of symbols that form a construct.
</div>

### How to Read Syntax Diagrams

Syntax diagrams use the following conventions:

| Element | Meaning |
|---|---|
| **Rounded box / oval** | Terminal symbol -- an actual character or keyword that appears in the code (e.g. `if`, `=`, `;`) |
| **Rectangular box** | Non-terminal symbol -- a named construct defined by another diagram (e.g. `<expression>`, `<identifier>`) |
| **Arrows / lines** | Show the direction of reading; follow the arrows from left to right |
| **Branching paths** | Indicate choices (alternatives) |
| **Loops (paths going backward)** | Indicate repetition |

### Example: Integer Literal

An integer literal consists of an optional sign (`+` or `-`) followed by one or more digits:

```
          +---+
     +--->| + |---+
     |    +---+   |
     |            v
---->+----------->+----> [digit] ---+--->
     |            ^                 |
     |    +---+   |                 |
     +--->| - |---+                 |
          +---+                     |
                                    |
              +---------------------+
              |
              v
              +----> [digit] ---+---->
              ^                 |
              +-----------------+
```

This diagram shows that an integer may optionally start with `+` or `-`, must have at least one digit, and may have additional digits.

### Example: If Statement

An `if` statement requires the keyword `if`, followed by a condition, then a block, with an optional `else` clause:

```
----> [if] ----> [condition] ----> [block] ---+---->
                                              |
                                              |    +------+
                                              +--->| else |----> [block] ----->
                                                   +------+
```

---

## Backus-Naur Form (BNF)

<div class="key-term" markdown="1">
**Backus-Naur Form (BNF)** is a formal notation for describing the syntax of a language using a set of production rules. Each rule defines how a non-terminal symbol can be replaced by a sequence of terminal and/or non-terminal symbols.
</div>

### BNF Notation

| Symbol | Meaning |
|---|---|
| `<name>` | Non-terminal symbol (a construct to be defined) |
| `::=` | "Is defined as" |
| `\|` | "Or" (separates alternatives) |
| Terminal text | Actual characters/keywords that appear in the code (sometimes in quotes) |

### BNF Examples

**Defining a digit:**
```
<digit> ::= 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9
```

**Defining a letter:**
```
<letter> ::= a | b | c | ... | z | A | B | C | ... | Z
```

**Defining an identifier (a name starting with a letter, followed by zero or more letters or digits):**
```
<identifier> ::= <letter> | <identifier> <letter> | <identifier> <digit>
```

This is a recursive definition: an identifier is either a single letter, or an existing identifier followed by another letter or digit. This allows identifiers of any length.

**Defining an integer:**
```
<digit> ::= 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9
<sign> ::= + | -
<unsigned_integer> ::= <digit> | <unsigned_integer> <digit>
<integer> ::= <unsigned_integer> | <sign> <unsigned_integer>
```

**Defining a simple assignment statement:**
```
<assignment> ::= <identifier> = <expression>
<expression> ::= <identifier> | <integer> | <expression> <operator> <expression>
<operator> ::= + | - | * | /
```

**Defining an if statement:**
```
<if_statement> ::= if <condition> then <block>
                 | if <condition> then <block> else <block>
```

### Relationship Between Syntax Diagrams and BNF

Syntax diagrams and BNF are two different ways of expressing exactly the same information:

| Syntax Diagram Feature | BNF Equivalent |
|---|---|
| Sequence of boxes connected by arrows | Symbols listed in order on the right of `::=` |
| Branching paths (choices) | The `\|` (or) operator |
| Loops (backward arrows) | Recursive rules (a non-terminal refers to itself) |
| Rounded box (terminal) | Terminal text in the rule |
| Rectangular box (non-terminal) | `<name>` in angle brackets |

Any construct that can be represented as a syntax diagram can also be expressed in BNF, and vice versa. BNF is more compact and suited to formal specification, while syntax diagrams are more visual and easier for humans to follow.

<div class="exam-tip" markdown="1">
In the exam you may be asked to **read** a BNF rule and determine whether a given string is valid, or to **write** a BNF rule for a simple construct. Practice by working through examples: take a rule, pick a string, and trace through the rule to see if it can be derived. Remember that recursive rules are what allow repetition in BNF.
</div>
