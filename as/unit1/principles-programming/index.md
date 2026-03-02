---
layout: topic
title: "Principles of Programming"
level: "AS"
level_url: "/as/"
unit_name: "Unit 1: Fundamentals of Computer Science"
unit_url: "/as/unit1/"
prev_topic: "/as/unit1/algorithms-programs/"
next_topic: "/as/unit1/systems-analysis/"
---

## Programming Paradigms

<div class="key-term" markdown="1">
A **programming paradigm** is a fundamental style or approach to programming that defines how we structure and organise code to solve problems.
</div>

There are several major paradigms, and many modern languages support more than one (these are called **multi-paradigm** languages). The WJEC AS specification requires knowledge of four paradigms: procedural, object-oriented, declarative, and functional.

### Procedural Programming

Procedural programming organises code as a sequence of instructions (statements) that are executed in order. The program is broken down into **procedures** (also called subroutines, functions, or methods) that perform specific tasks.

Key features:
- Programs follow a **top-down** design -- the problem is broken into smaller sub-problems, each solved by a procedure.
- Data and procedures are **separate** -- data is passed to procedures via parameters or accessed through global variables.
- Uses **sequence**, **selection** (if/else), and **iteration** (loops) as control structures.
- Variables have defined **scope** (local or global).

```python
# Procedural example: calculating average of a list
def calculate_total(numbers):
    total = 0
    for num in numbers:
        total += num
    return total

def calculate_average(numbers):
    total = calculate_total(numbers)
    return total / len(numbers)

marks = [72, 85, 64, 91, 78]
avg = calculate_average(marks)
print(f"Average: {avg}")
```

```vb
' Procedural example: calculating average of a list
Function CalculateTotal(numbers() As Double) As Double
    Dim total As Double = 0
    For Each num As Double In numbers
        total += num
    Next
    Return total
End Function

Function CalculateAverage(numbers() As Double) As Double
    Dim total As Double = CalculateTotal(numbers)
    Return total / numbers.Length
End Function

Dim marks() As Double = {72, 85, 64, 91, 78}
Dim avg As Double = CalculateAverage(marks)
Console.WriteLine("Average: " & avg)
```

Examples of procedural languages: C, Pascal, BASIC, COBOL.

### Object-Oriented Programming (OOP)

Object-oriented programming organises code around **objects** -- self-contained entities that combine data (**attributes**) and behaviour (**methods**) into a single unit. Objects are created from **classes**, which serve as blueprints.

Key features:
- **Encapsulation** -- data and methods are bundled together; internal details are hidden.
- **Inheritance** -- a class can inherit attributes and methods from a parent class.
- **Polymorphism** -- objects of different classes can respond to the same method call in different ways.
- **Abstraction** -- complex details are hidden behind a simple interface.

Examples of OOP languages: Java, Python, C#, C++, VB.NET.

### Declarative Programming

Declarative programming focuses on **what** the program should accomplish rather than **how** to accomplish it. The programmer describes the desired result, and the language implementation determines how to produce it.

```
-- SQL example (declarative)
SELECT name, grade FROM students WHERE grade > 70 ORDER BY grade DESC;
```

The programmer does not specify how to loop through records, compare values, or sort results. The database engine handles all of that.

Other examples: Prolog (logic programming), HTML/CSS (markup/styling).

### Functional Programming

Functional programming treats computation as the evaluation of **mathematical functions**. It avoids changing state and mutable data.

Key features:
- **First-class functions** -- functions can be assigned to variables, passed as arguments, and returned from other functions.
- **Pure functions** -- a function always produces the same output for the same input and has no side effects.
- **Immutability** -- data is not modified after creation; new data structures are created instead.
- **Higher-order functions** -- functions that take other functions as parameters or return functions.

```python
# Functional style in Python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Using map and filter (higher-order functions)
evens = list(filter(lambda x: x % 2 == 0, numbers))
doubled = list(map(lambda x: x * 2, evens))
print(doubled)  # Output: [4, 8, 12, 16, 20]
```

```vb
' Functional style in VB.NET using LINQ
Dim numbers() As Integer = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10}

Dim doubled = numbers.Where(Function(x) x Mod 2 = 0).Select(Function(x) x * 2).ToList()
For Each num In doubled
    Console.Write(num & " ")  ' Output: 4 8 12 16 20
Next
```

Examples of functional languages: Haskell, Erlang, Lisp. Many modern languages (Python, JavaScript, C#) support functional features.

### Paradigm Comparison Table

| Feature | Procedural | Object-Oriented | Declarative | Functional |
|---|---|---|---|---|
| **Core idea** | Sequence of instructions | Interacting objects | Describe the result | Evaluate functions |
| **Data & behaviour** | Separate | Bundled (encapsulation) | Implicit | Functions operate on immutable data |
| **State** | Mutable variables | Mutable object state | Managed by system | Avoided (immutability) |
| **Reuse mechanism** | Procedures/functions | Inheritance, composition | Rules/queries | Higher-order functions |
| **Examples** | C, Pascal | Java, Python, C# | SQL, Prolog | Haskell, Erlang |

<div class="exam-tip" markdown="1">
For the exam, you need to be able to **describe** each paradigm, **identify** which paradigm a given piece of code belongs to, and **explain the differences** between them. Remember that many languages are multi-paradigm -- Python supports procedural, OOP, and functional styles.
</div>

---

## Object-Oriented Programming Concepts in Detail

### Classes and Objects

<div class="key-term" markdown="1">
A **class** is a blueprint or template that defines the attributes (data) and methods (behaviour) that objects of that type will have. An **object** is a specific instance of a class, with its own set of attribute values.
</div>

Think of a class as a cookie cutter and objects as the individual cookies made from it. The class defines the shape; each object is a distinct cookie.

```python
class Dog:
    def __init__(self, name, breed, age):
        self.name = name        # Attribute
        self.breed = breed      # Attribute
        self.age = age          # Attribute

    def bark(self):             # Method
        return f"{self.name} says Woof!"

    def get_info(self):         # Method
        return f"{self.name} is a {self.age}-year-old {self.breed}"

# Creating objects (instances)
dog1 = Dog("Rex", "German Shepherd", 5)
dog2 = Dog("Bella", "Labrador", 3)

print(dog1.bark())       # Output: Rex says Woof!
print(dog2.get_info())   # Output: Bella is a 3-year-old Labrador
```

```vb
Class Dog
    Public Property Name As String
    Public Property Breed As String
    Public Property Age As Integer

    ' Constructor
    Sub New(name As String, breed As String, age As Integer)
        Me.Name = name
        Me.Breed = breed
        Me.Age = age
    End Sub

    ' Method
    Function Bark() As String
        Return Name & " says Woof!"
    End Function

    ' Method
    Function GetInfo() As String
        Return Name & " is a " & Age & "-year-old " & Breed
    End Function
End Class

' Creating objects (instances)
Dim dog1 As New Dog("Rex", "German Shepherd", 5)
Dim dog2 As New Dog("Bella", "Labrador", 3)

Console.WriteLine(dog1.Bark())       ' Output: Rex says Woof!
Console.WriteLine(dog2.GetInfo())    ' Output: Bella is a 3-year-old Labrador
```

### Encapsulation

<div class="key-term" markdown="1">
**Encapsulation** is the principle of bundling data (attributes) and the methods that operate on that data into a single unit (a class), and restricting direct access to some of the object's components. This is achieved through **access modifiers** (public, private, protected).
</div>

Encapsulation protects an object's internal state from unintended interference. External code accesses data through **getter** and **setter** methods (or properties) rather than directly modifying attributes.

```python
class BankAccount:
    def __init__(self, owner, balance):
        self.__owner = owner        # Private attribute (name mangling)
        self.__balance = balance    # Private attribute

    def get_balance(self):          # Getter method
        return self.__balance

    def deposit(self, amount):      # Controlled access
        if amount > 0:
            self.__balance += amount
            return True
        return False

    def withdraw(self, amount):     # Controlled access
        if 0 < amount <= self.__balance:
            self.__balance -= amount
            return True
        return False

account = BankAccount("Alice", 1000)
account.deposit(500)
print(account.get_balance())  # Output: 1500
# account.__balance = -999    # This would NOT work as intended (encapsulation)
```

```vb
Class BankAccount
    Private _owner As String        ' Private attribute
    Private _balance As Decimal     ' Private attribute

    Sub New(owner As String, balance As Decimal)
        _owner = owner
        _balance = balance
    End Sub

    ' Property with getter only (read-only)
    ReadOnly Property Balance As Decimal
        Get
            Return _balance
        End Get
    End Property

    Function Deposit(amount As Decimal) As Boolean
        If amount > 0 Then
            _balance += amount
            Return True
        End If
        Return False
    End Function

    Function Withdraw(amount As Decimal) As Boolean
        If amount > 0 AndAlso amount <= _balance Then
            _balance -= amount
            Return True
        End If
        Return False
    End Function
End Class

Dim account As New BankAccount("Alice", 1000)
account.Deposit(500)
Console.WriteLine(account.Balance)  ' Output: 1500
' account._balance = -999           ' This would cause a compiler error (encapsulation)
```

### Inheritance

<div class="key-term" markdown="1">
**Inheritance** allows a new class (the **child** or **subclass**) to inherit attributes and methods from an existing class (the **parent** or **superclass**). The child class can extend or override the inherited behaviour.
</div>

Inheritance promotes code reuse and establishes an "is-a" relationship: a Dog **is an** Animal, a Car **is a** Vehicle.

```python
class Animal:
    def __init__(self, name, species):
        self.name = name
        self.species = species

    def make_sound(self):
        return "Some generic sound"

    def get_info(self):
        return f"{self.name} is a {self.species}"

# Cat inherits from Animal
class Cat(Animal):
    def __init__(self, name, indoor):
        super().__init__(name, "Cat")  # Call parent constructor
        self.indoor = indoor           # Additional attribute

    def make_sound(self):              # Override parent method
        return f"{self.name} says Meow!"

    def is_indoor(self):               # Additional method
        return self.indoor

cat = Cat("Whiskers", True)
print(cat.get_info())      # Inherited method: Whiskers is a Cat
print(cat.make_sound())    # Overridden method: Whiskers says Meow!
print(cat.is_indoor())     # New method: True
```

```vb
Class Animal
    Public Property Name As String
    Public Property Species As String

    Sub New(name As String, species As String)
        Me.Name = name
        Me.Species = species
    End Sub

    Overridable Function MakeSound() As String
        Return "Some generic sound"
    End Function

    Function GetInfo() As String
        Return Name & " is a " & Species
    End Function
End Class

' Cat inherits from Animal
Class Cat
    Inherits Animal

    Public Property Indoor As Boolean

    Sub New(name As String, indoor As Boolean)
        MyBase.New(name, "Cat")    ' Call parent constructor
        Me.Indoor = indoor          ' Additional attribute
    End Sub

    Overrides Function MakeSound() As String  ' Override parent method
        Return Name & " says Meow!"
    End Function

    Function IsIndoor() As Boolean             ' Additional method
        Return Indoor
    End Function
End Class

Dim cat As New Cat("Whiskers", True)
Console.WriteLine(cat.GetInfo())      ' Inherited method: Whiskers is a Cat
Console.WriteLine(cat.MakeSound())    ' Overridden method: Whiskers says Meow!
Console.WriteLine(cat.IsIndoor())     ' New method: True
```

### Polymorphism

<div class="key-term" markdown="1">
**Polymorphism** (meaning "many forms") allows objects of different classes to be treated through the same interface. The same method name can behave differently depending on which class the object belongs to.
</div>

```python
class Shape:
    def area(self):
        return 0

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        import math
        return math.pi * self.radius ** 2

# Polymorphism in action
shapes = [Rectangle(5, 3), Circle(4), Rectangle(2, 7)]
for shape in shapes:
    print(f"Area: {shape.area():.2f}")
# Each object calls its OWN version of area()
# Output:
# Area: 15.00
# Area: 50.27
# Area: 14.00
```

```vb
MustInherit Class Shape
    MustOverride Function Area() As Double
End Class

Class Rectangle
    Inherits Shape
    Public Property Width As Double
    Public Property Height As Double

    Sub New(width As Double, height As Double)
        Me.Width = width
        Me.Height = height
    End Sub

    Overrides Function Area() As Double
        Return Width * Height
    End Function
End Class

Class Circle
    Inherits Shape
    Public Property Radius As Double

    Sub New(radius As Double)
        Me.Radius = radius
    End Sub

    Overrides Function Area() As Double
        Return Math.PI * Radius ^ 2
    End Function
End Class

' Polymorphism in action
Dim shapes() As Shape = {New Rectangle(5, 3), New Circle(4), New Rectangle(2, 7)}
For Each shape As Shape In shapes
    Console.WriteLine("Area: " & shape.Area().ToString("F2"))
Next
' Each object calls its OWN version of Area()
' Output:
' Area: 15.00
' Area: 50.27
' Area: 14.00
```

### Summary of OOP Concepts

| Concept | Description | Benefit |
|---|---|---|
| **Class** | Blueprint for creating objects | Defines structure and behaviour |
| **Object** | An instance of a class | Represents a specific entity |
| **Encapsulation** | Bundling data and methods; hiding internal state | Protects data integrity; reduces complexity |
| **Inheritance** | Child class inherits from parent class | Code reuse; establishes relationships |
| **Polymorphism** | Same method name, different behaviour | Flexibility; extensibility |
| **Abstraction** | Hiding complex details behind simple interfaces | Reduces complexity for the user |

---

## Low-Level vs High-Level Languages

### Low-Level Languages

Low-level languages have very little or no abstraction from the computer's hardware. They deal directly with memory addresses, registers, and machine instructions.

**Machine code:**
- Binary instructions (patterns of 1s and 0s) that the CPU can execute directly.
- Each instruction corresponds to a single operation (e.g., load, store, add).
- Completely hardware-specific -- machine code for one CPU architecture will not work on another.
- Extremely difficult for humans to read or write.

**Assembly language:**
- Uses human-readable **mnemonics** (e.g., `MOV`, `ADD`, `SUB`, `JMP`, `CMP`) to represent machine code instructions.
- Has a (mostly) **one-to-one** mapping to machine code -- each assembly instruction corresponds to one machine code instruction.
- Still hardware-specific -- different CPU architectures have different instruction sets.
- Requires an **assembler** to translate into machine code.

Example assembly code:
```
MOV AX, 5      ; Load the value 5 into register AX
MOV BX, 3      ; Load the value 3 into register BX
ADD AX, BX     ; Add BX to AX (result: 8 in AX)
```

### High-Level Languages

High-level languages provide a high level of abstraction from the hardware. The programmer does not need to manage memory addresses, registers, or CPU-specific instructions.

- Use English-like keywords and familiar mathematical notation.
- One high-level statement may translate to **many** machine code instructions.
- **Portable** -- the same source code can (in principle) run on different hardware platforms.
- Easier to read, write, debug, and maintain.
- Examples: Python, VB.NET, Java, C#, JavaScript.

### Comparison Table

| Feature | Low-Level Languages | High-Level Languages |
|---|---|---|
| **Abstraction** | Little or none | High |
| **Readability** | Difficult for humans | Easy for humans |
| **Portability** | Hardware-specific | Mostly portable |
| **Execution speed** | Very fast (close to hardware) | Slower (needs translation) |
| **Memory control** | Direct access to memory/registers | Managed automatically |
| **Development time** | Slow and error-prone | Faster and more productive |
| **Use cases** | Device drivers, embedded systems, OS kernels | Applications, web development, data processing |
| **Translation needed** | Assembler (assembly) or none (machine code) | Compiler or interpreter |

<div class="exam-tip" markdown="1">
The key trade-off is **control and speed** vs **productivity and portability**. Low-level languages give direct hardware control and faster execution, but high-level languages allow programmers to be far more productive and write more maintainable code.
</div>

---

## Translators

Source code must be translated into machine code before the CPU can execute it. There are three types of translator: assemblers, compilers, and interpreters.

### Assembler

- Translates **assembly language** into **machine code**.
- Performs a (mostly) **one-to-one** translation -- each assembly mnemonic maps to one machine code instruction.
- Resolves labels and symbolic addresses into actual memory addresses.
- The output is an executable machine code file.

### Compiler

- Translates the **entire** high-level source code into machine code (or an intermediate form) **all at once**, before the program is run.
- Produces a standalone **executable file** (e.g., `.exe` on Windows).
- The source code is not needed to run the compiled program.
- Compilation can be slow, but execution of the compiled program is fast.
- Errors are reported after the whole program is analysed, which can make debugging harder.

### Interpreter

- Translates and executes high-level source code **one statement at a time**.
- No executable file is produced -- the interpreter must be present every time the program runs.
- Stops immediately when an error is encountered, reporting the exact line, which aids debugging.
- Slower execution than compiled code, because each statement is translated every time the program runs.

### Comparison Table

| Feature | Assembler | Compiler | Interpreter |
|---|---|---|---|
| **Input** | Assembly language | High-level source code | High-level source code |
| **Output** | Machine code | Executable file | No file (executes directly) |
| **Translation** | One-to-one | Whole program at once | One line at a time |
| **Execution speed** | Fast (native code) | Fast (pre-compiled) | Slow (translated at runtime) |
| **Error reporting** | After assembly | After full compilation | Immediately at the error line |
| **Debugging** | Difficult | Harder (errors after compilation) | Easier (stops at error line) |
| **Distribution** | Machine code only | Executable only (protects source) | Source code required |
| **Portability** | Hardware-specific | Platform-specific executable | Portable (if interpreter available) |

<div class="key-term" markdown="1">
A **compiler** translates the entire source code into an executable before the program runs. An **interpreter** translates and executes one line at a time during runtime. An **assembler** translates assembly language (low-level) into machine code.
</div>

<div class="exam-tip" markdown="1">
A common exam question is to explain why a developer might use an interpreter during development (easier debugging, immediate feedback) but compile the final product for distribution (faster execution, source code protection). Many real-world development workflows use both.
</div>

---

## Stages of Compilation

A compiler does not simply translate code in one step. The compilation process involves several distinct stages, each transforming the source code into a form closer to machine code.

### 1. Lexical Analysis

The **lexical analyser** (or lexer/tokeniser) reads the source code character by character and converts it into a stream of **tokens**. It also:

- Removes whitespace and comments (these are not needed for execution).
- Identifies **keywords** (e.g., `if`, `while`, `for`), **identifiers** (variable and function names), **operators** (e.g., `+`, `=`, `<`), **literals** (e.g., `42`, `"hello"`), and **punctuation** (e.g., `;`, `{`, `}`).
- Builds a **symbol table** that records each identifier, its type, and its scope.
- Reports lexical errors (e.g., illegal characters).

**Example:** The statement `total = price * quantity` would be tokenised as:

| Token | Type |
|---|---|
| `total` | Identifier |
| `=` | Assignment operator |
| `price` | Identifier |
| `*` | Multiplication operator |
| `quantity` | Identifier |

### 2. Syntax Analysis (Parsing)

The **syntax analyser** (or parser) takes the stream of tokens and checks that they follow the grammatical rules of the language. It:

- Builds a **parse tree** (also called an abstract syntax tree or AST) that represents the hierarchical structure of the code.
- Checks that statements are grammatically correct (e.g., every opening bracket has a matching closing bracket, keywords are used correctly).
- Reports **syntax errors** (e.g., missing semicolons, unmatched brackets, incorrect use of keywords).

### 3. Semantic Analysis

The **semantic analyser** checks the meaning of the code to ensure it makes logical sense. It:

- **Type checking** -- ensures operations are performed on compatible types (e.g., you cannot add a string to an integer without conversion).
- **Scope checking** -- ensures variables are declared before use and used within their valid scope.
- **Consistency checking** -- ensures functions are called with the correct number and type of arguments.

### 4. Code Generation

The **code generator** translates the validated parse tree into **machine code** (or an intermediate representation). It:

- Assigns variables to memory locations or CPU registers.
- Translates high-level constructs (loops, conditionals) into sequences of low-level instructions.
- Produces object code that is functionally equivalent to the source code.

### 5. Code Optimisation

The **optimiser** improves the generated code to make it run faster or use less memory, without changing its behaviour. Common optimisations include:

- **Removing redundant code** -- eliminating instructions that have no effect.
- **Constant folding** -- evaluating constant expressions at compile time (e.g., replacing `3 * 4` with `12`).
- **Loop optimisation** -- moving calculations that do not change out of loops.
- **Register allocation** -- making efficient use of CPU registers to reduce memory access.

Optimisation can occur at multiple stages and may significantly improve performance.

### Summary of Compilation Stages

| Stage | Input | Output | Purpose |
|---|---|---|---|
| **Lexical analysis** | Source code (characters) | Token stream + symbol table | Tokenise; remove whitespace/comments |
| **Syntax analysis** | Token stream | Parse tree (AST) | Check grammar; build tree structure |
| **Semantic analysis** | Parse tree | Annotated parse tree | Check types, scope, consistency |
| **Code generation** | Annotated parse tree | Machine code / object code | Produce executable instructions |
| **Code optimisation** | Unoptimised code | Optimised code | Improve efficiency |

---

## Linkers and Loaders

### Linker

<div class="key-term" markdown="1">
A **linker** combines one or more object code files (produced by the compiler) with any required **library** code into a single executable file. It resolves references between separately compiled modules.
</div>

When a program uses external functions (e.g., from a maths library or a standard I/O library), the compiler produces object code that contains unresolved references to those external functions. The linker:

- Combines all object code modules into one file.
- Resolves external references by linking them to the correct library code.
- Produces a complete, standalone executable.

There are two types of linking:
- **Static linking** -- library code is copied into the executable at compile time. The executable is self-contained but larger.
- **Dynamic linking** -- the executable contains references to shared library files (e.g., `.dll` on Windows) that are loaded at runtime. The executable is smaller, but the libraries must be available on the user's machine.

### Loader

<div class="key-term" markdown="1">
A **loader** is a part of the operating system that loads an executable file from secondary storage into **main memory (RAM)** and prepares it for execution by the CPU.
</div>

The loader:
- Allocates memory space for the program.
- Copies the executable code and data from disk into RAM.
- Resolves any remaining dynamic library references.
- Sets the program counter to the starting address of the program so execution can begin.

---

## IDE Features

<div class="key-term" markdown="1">
An **Integrated Development Environment (IDE)** is a software application that provides a comprehensive set of tools for software development within a single interface. Examples include Visual Studio, PyCharm, Eclipse, and VS Code.
</div>

### Key Features of an IDE

| Feature | Description | Benefit |
|---|---|---|
| **Code editor** | A text editor with syntax highlighting, line numbering, and code indentation | Makes code easier to read; highlights language keywords in colour |
| **Auto-complete / IntelliSense** | Suggests variable names, function names, and keywords as you type | Speeds up coding; reduces typos; helps recall syntax |
| **Syntax highlighting** | Displays different code elements (keywords, strings, comments, variables) in different colours | Improves readability; makes errors easier to spot |
| **Compiler / interpreter** | Built-in translator to compile or interpret code directly within the IDE | No need to switch to a separate tool; one-click build and run |
| **Debugger** | Tools for stepping through code line by line, setting breakpoints, and inspecting variable values | Helps find and fix logic errors by observing program behaviour |
| **Error diagnostics** | Highlights syntax errors and warnings in real time, often with suggested fixes | Catches mistakes as you type, before you even try to compile |
| **Version control integration** | Built-in support for Git or other VCS tools | Track changes, collaborate, and revert to previous versions |
| **Project management** | Organises files, resources, and settings for a project | Keeps related files together; simplifies navigation |
| **Run/build tools** | One-click compilation, execution, and testing | Streamlines the development workflow |
| **Console/terminal** | Built-in terminal for running commands | No need to switch to an external terminal |

### Debugging Tools in Detail

Debugging is one of the most important features of an IDE. Key debugging capabilities include:

- **Breakpoints** -- markers placed on specific lines of code where execution will pause. This allows the programmer to examine the state of the program at that point.
- **Stepping** -- executing the program one line at a time (step over, step into, step out) to observe exactly what happens at each stage.
- **Watch window** -- monitors the values of selected variables as the program executes.
- **Call stack** -- shows the sequence of function calls that led to the current point of execution, which is particularly useful for debugging recursive functions.
- **Variable inspection** -- hovering over a variable to see its current value.

<div class="exam-tip" markdown="1">
IDE questions often ask you to **describe** specific features and **explain** how they help the programmer. Always link the feature to a practical benefit. For example: "The debugger allows the programmer to set breakpoints and step through code line by line, which helps identify logic errors by observing the actual values of variables at each stage of execution."
</div>

---

## Constants and Variables

<div class="key-term" markdown="1">
A **variable** is a named storage location in memory whose value can change during program execution. A **constant** is a named value that is set once and **cannot be changed** during execution.
</div>

### Why Use Constants?

- **Maintainability** — if a value needs to change (e.g. VAT rate), you only change it in one place
- **Readability** — `VAT_RATE` is more meaningful than `0.2` scattered through code
- **Safety** — prevents accidental modification of values that should not change
- **Performance** — some compilers can optimise constants more efficiently

```python
# Python — Constants and variables
VAT_RATE = 0.2  # Python has no true constants, but UPPER_CASE convention signals "do not change"
MAX_ATTEMPTS = 3

price = float(input("Enter price: "))
total = price + (price * VAT_RATE)
print(f"Total including VAT: £{total:.2f}")
```

```vb
' VB.NET — Constants and variables
Const VAT_RATE As Double = 0.2
Const MAX_ATTEMPTS As Integer = 3

Dim price As Double
Console.Write("Enter price: ")
price = CDbl(Console.ReadLine())
Dim total As Double = price + (price * VAT_RATE)
Console.WriteLine("Total including VAT: £" & total.ToString("F2"))
```

---

## MOD and DIV Operators

**MOD** (modulus) returns the **remainder** after integer division. **DIV** (integer division) returns the **whole number** result of division, discarding the remainder.

| Expression | Result | Explanation |
|-----------|--------|-------------|
| `17 MOD 5` | 2 | 17 ÷ 5 = 3 remainder **2** |
| `17 DIV 5` | 3 | 17 ÷ 5 = **3** remainder 2 |
| `20 MOD 4` | 0 | 20 ÷ 4 = 5 remainder **0** (exactly divisible) |
| `7 MOD 2` | 1 | 7 ÷ 2 = 3 remainder **1** (odd number check) |
| `100 DIV 7` | 14 | 100 ÷ 7 = **14** remainder 2 |

```python
# Python — MOD and DIV
number = 17
remainder = number % 5     # MOD — result: 2
quotient = number // 5     # DIV (integer division) — result: 3

# Common use: check if a number is even
if number % 2 == 0:
    print("Even")
else:
    print("Odd")

# Common use: extract digits
last_digit = 1234 % 10     # Result: 4
remaining = 1234 // 10     # Result: 123
```

```vb
' VB.NET — MOD and DIV
Dim number As Integer = 17
Dim remainder As Integer = number Mod 5    ' MOD — result: 2
Dim quotient As Integer = number \ 5       ' DIV (integer division) — result: 3

' Common use: check if a number is even
If number Mod 2 = 0 Then
    Console.WriteLine("Even")
Else
    Console.WriteLine("Odd")
End If
```

<div class="exam-tip" markdown="1">
MOD and DIV are commonly used in exam questions for tasks like checking if a number is **even or odd** (`n MOD 2`), extracting individual **digits** from a number, or converting between **units** (e.g. converting minutes to hours and remaining minutes: `hours = minutes DIV 60`, `mins = minutes MOD 60`).
</div>

---

## Self-Documenting Identifiers

**Self-documenting code** is code that can be understood by reading it, without needing additional comments. The most important technique is using **meaningful identifier names**.

### Naming Conventions

| Convention | Style | Example | Typically Used In |
|-----------|-------|---------|-------------------|
| **camelCase** | First word lowercase, subsequent words capitalised | `studentAge`, `totalMarks` | Java, JavaScript, VB.NET variables |
| **PascalCase** | Every word capitalised | `GetStudentName`, `CalculateTotal` | VB.NET methods, C# classes |
| **snake_case** | Words separated by underscores | `student_age`, `total_marks` | Python variables and functions |
| **UPPER_SNAKE_CASE** | All capitals with underscores | `MAX_SIZE`, `VAT_RATE` | Constants in most languages |

### Good vs Bad Naming

| Bad | Good | Why |
|-----|------|-----|
| `x` | `student_count` | Describes what the data represents |
| `calc()` | `calculate_average()` | Describes what the function does |
| `flag` | `is_logged_in` | Boolean names should read as true/false questions |
| `lst` | `exam_results` | Describes the content of the collection |
| `temp` | `previous_total` | Avoids ambiguity |

---

## Rogue Values and Sentinel Values

<div class="key-term" markdown="1">
A **rogue value** (also called a **sentinel value**) is a special value entered by the user to signal the end of data input. It must be a value that could **never be valid data** in the context of the program.
</div>

### Example: Using -1 as a Rogue Value for Positive Marks

```python
# Python — Rogue value to end input
total = 0
count = 0
mark = int(input("Enter a mark (-1 to finish): "))

while mark != -1:
    total += mark
    count += 1
    mark = int(input("Enter a mark (-1 to finish): "))

if count > 0:
    average = total / count
    print(f"Average mark: {average:.1f}")
else:
    print("No marks entered.")
```

```vb
' VB.NET — Rogue value to end input
Dim total As Integer = 0
Dim count As Integer = 0
Console.Write("Enter a mark (-1 to finish): ")
Dim mark As Integer = CInt(Console.ReadLine())

While mark <> -1
    total += mark
    count += 1
    Console.Write("Enter a mark (-1 to finish): ")
    mark = CInt(Console.ReadLine())
End While

If count > 0 Then
    Dim average As Double = total / count
    Console.WriteLine("Average mark: " & average.ToString("F1"))
Else
    Console.WriteLine("No marks entered.")
End If
```

<div class="exam-tip" markdown="1">
When choosing a rogue value, it must be **outside the range of valid data**. For example, -1 works for positive marks but would **not** work for temperature readings (which can be negative). Always state clearly why the rogue value could never be confused with valid data.
</div>

---

## UML Class Diagrams

A **UML (Unified Modelling Language) class diagram** is a visual representation of a class in object-oriented programming. It shows the class name, its attributes (data), and its methods (behaviours).

### Class Diagram Notation

```
┌──────────────────────────┐
│       ClassName          │
├──────────────────────────┤
│ - privateAttribute: Type │
│ # protectedAttribute: Type│
│ + publicAttribute: Type  │
├──────────────────────────┤
│ + publicMethod(): Type   │
│ - privateMethod(): Type  │
└──────────────────────────┘
```

### Access Modifiers

| Symbol | Modifier | Meaning |
|--------|----------|---------|
| `+` | Public | Accessible from anywhere |
| `-` | Private | Only accessible within the class |
| `#` | Protected | Accessible within the class and its subclasses |

### Example: Inheritance Diagram

```
┌──────────────────────┐
│       Person         │
├──────────────────────┤
│ # name: String       │
│ # dateOfBirth: Date  │
├──────────────────────┤
│ + getName(): String  │
│ + getAge(): Integer  │
└──────────┬───────────┘
           │ inherits
     ┌─────┴─────┐
     ▼           ▼
┌─────────────┐ ┌─────────────┐
│    Pupil    │ │    Staff    │
├─────────────┤ ├─────────────┤
│ - form: Str │ │ - role: Str │
│ - year: Int │ │ - salary: Dec│
├─────────────┤ ├─────────────┤
│ + getForm() │ │ + getRole() │
└─────────────┘ └─────────────┘
```

In this diagram, `Pupil` and `Staff` both **inherit** from `Person`, gaining the `name`, `dateOfBirth`, `getName()` and `getAge()` members. Each subclass adds its own specific attributes and methods.

<div class="exam-tip" markdown="1">
In exam questions, you may be asked to read or draw a class diagram. Pay attention to the **access modifiers** (`+`, `-`, `#`) and the **inheritance arrows**. A subclass inherits all public and protected members from the parent class.
</div>
