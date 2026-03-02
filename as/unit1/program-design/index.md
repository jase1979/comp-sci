---
layout: topic
title: "Program Design"
level: "AS"
level_url: "/as/"
unit_name: "Unit 1: Fundamentals of Computer Science"
unit_url: "/as/unit1/"
prev_topic: "/as/unit1/software-design/"
next_topic: "/as/unit1/software-testing/"
---

## Structure of a Typical Program

A well-structured program follows a logical layout that makes it easy to read, debug, and maintain. Although the exact syntax differs between programming languages, most programs share common structural elements.

### Common Structural Elements

1. **Import/library statements** -- bring in external modules or libraries at the top of the file.
2. **Constant declarations** -- values that do not change throughout execution are declared early.
3. **Global variable declarations** -- variables accessible throughout the entire program (used sparingly).
4. **Subroutine definitions** -- functions and procedures that contain the main logic, defined before they are called.
5. **Main program / entry point** -- the block of code that runs when the program starts, typically calling subroutines to carry out tasks.
6. **Comments** -- annotations explaining the purpose of code, placed throughout to aid readability.

```python
# Import statements
import math

# Constants
PI = 3.14159
MAX_ATTEMPTS = 3

# Function definitions
def calculate_area(radius):
    return PI * radius ** 2

def get_radius():
    radius = float(input("Enter radius: "))
    return radius

# Main program
def main():
    r = get_radius()
    area = calculate_area(r)
    print(f"The area is {area:.2f}")

main()
```

```vb
' Import statements
Imports System.Math

Module Program
    ' Constants
    Const PI As Double = 3.14159
    Const MAX_ATTEMPTS As Integer = 3

    ' Function definitions
    Function CalculateArea(radius As Double) As Double
        Return PI * radius ^ 2
    End Function

    Function GetRadius() As Double
        Console.Write("Enter radius: ")
        Dim radius As Double = Convert.ToDouble(Console.ReadLine())
        Return radius
    End Function

    ' Main program
    Sub Main()
        Dim r As Double = GetRadius()
        Dim area As Double = CalculateArea(r)
        Console.WriteLine($"The area is {area:F2}")
    End Sub
End Module
```

<div class="key-term" markdown="1">
A **subroutine** is a named block of code that performs a specific task. Subroutines include both **functions** (which return a value) and **procedures** (which do not return a value). Using subroutines is fundamental to writing structured, modular programs.
</div>

---

## Modular Design and Decomposition

**Modular design** is the practice of breaking a large program into smaller, independent, self-contained modules. Each module handles one specific aspect of the program's functionality. This is the practical application of top-down design during the coding phase.

### Benefits of Modular Design

| Benefit | Explanation |
|---------|-------------|
| **Readability** | Smaller modules are easier to read and understand than one monolithic block of code |
| **Reusability** | A well-written module can be reused in other programs without modification |
| **Ease of debugging** | Bugs are isolated within specific modules, making them easier to locate and fix |
| **Team working** | Different programmers can develop and test different modules simultaneously |
| **Maintainability** | Individual modules can be updated or replaced without affecting the rest of the program |
| **Testing** | Each module can be tested independently (unit testing) before being integrated |

### Decomposition in Practice

Decomposition means dividing a problem into sub-problems, each of which becomes a module. For example, a student records system might be decomposed into:

- A module to add new students
- A module to search for student records
- A module to update student details
- A module to generate reports
- A module to handle file input/output

Each module would be implemented as one or more subroutines.

<div class="exam-tip" markdown="1">
When asked about the benefits of a modular approach, always relate your answer to practical programming scenarios. For example: "Modular design allows team working because programmer A can write the input validation module while programmer B works on the report generation module, reducing overall development time."
</div>

---

## Functions and Procedures

Subroutines come in two forms: **functions** and **procedures**. The key difference is that a function returns a value, while a procedure does not.

### Procedures

A **procedure** performs a task but does not return a value to the calling code. It is called for its side effects (e.g. displaying output, writing to a file).

```python
# Procedure - does not return a value
def display_welcome(name):
    print(f"Welcome, {name}!")
    print("Please select an option from the menu.")

# Calling the procedure
display_welcome("Alice")
```

```vb
' Procedure - does not return a value
Sub DisplayWelcome(name As String)
    Console.WriteLine($"Welcome, {name}!")
    Console.WriteLine("Please select an option from the menu.")
End Sub

' Calling the procedure
DisplayWelcome("Alice")
```

### Functions

A **function** performs a task and returns a value to the calling code. The returned value can be stored in a variable or used directly in an expression.

```python
# Function - returns a value
def calculate_vat(price, rate=0.20):
    vat = price * rate
    return vat

# Calling the function and using the returned value
item_price = 50.00
tax = calculate_vat(item_price)
total = item_price + tax
print(f"Total including VAT: £{total:.2f}")
```

```vb
' Function - returns a value
Function CalculateVAT(price As Double, Optional rate As Double = 0.2) As Double
    Dim vat As Double = price * rate
    Return vat
End Function

' Calling the function and using the returned value
Dim itemPrice As Double = 50.0
Dim tax As Double = CalculateVAT(itemPrice)
Dim total As Double = itemPrice + tax
Console.WriteLine($"Total including VAT: £{total:F2}")
```

### Key Differences

| Feature | Function | Procedure |
|---------|----------|-----------|
| Returns a value | Yes | No |
| Can be used in expressions | Yes (e.g. `x = myFunc()`) | No |
| Keyword in Python | `def` (with `return`) | `def` (without `return`) |
| Keyword in VB.NET | `Function ... End Function` | `Sub ... End Sub` |
| Typical use | Calculations, lookups, conversions | Displaying output, modifying data structures |

<div class="key-term" markdown="1">
A **function** is a subroutine that returns a value. A **procedure** (called a `Sub` in VB.NET) is a subroutine that performs an action but does not return a value.
</div>

---

## Parameter Passing

**Parameters** are the values passed into a subroutine when it is called. There are two main mechanisms for passing parameters: **by value** and **by reference**.

### Passing by Value

- A **copy** of the data is passed to the subroutine.
- Any changes made to the parameter inside the subroutine have **no effect** on the original variable in the calling code.
- This is the default in most languages (including Python for immutable types and VB.NET with `ByVal`).
- Safer because the original data is protected from accidental modification.

```python
# Pass by value (Python passes immutable types like int by value effectively)
def double_value(num):
    num = num * 2
    print(f"Inside function: {num}")

original = 5
double_value(original)
print(f"Outside function: {original}")
# Output:
# Inside function: 10
# Outside function: 5   <-- original is unchanged
```

```vb
' Pass by value (ByVal is the default in VB.NET)
Sub DoubleValue(ByVal num As Integer)
    num = num * 2
    Console.WriteLine($"Inside sub: {num}")
End Sub

Dim original As Integer = 5
DoubleValue(original)
Console.WriteLine($"Outside sub: {original}")
' Output:
' Inside sub: 10
' Outside sub: 5   <-- original is unchanged
```

### Passing by Reference

- A **reference** (memory address) to the original data is passed to the subroutine.
- Any changes made to the parameter inside the subroutine **directly affect** the original variable in the calling code.
- Used when you need the subroutine to modify the original variable.
- Must be used carefully as it can lead to unexpected side effects.

```python
# Pass by reference (Python passes mutable types like lists by reference)
def add_item(shopping_list, item):
    shopping_list.append(item)

my_list = ["bread", "milk"]
add_item(my_list, "eggs")
print(my_list)
# Output: ['bread', 'milk', 'eggs']  <-- original list is modified
```

```vb
' Pass by reference (ByRef keyword in VB.NET)
Sub DoubleValue(ByRef num As Integer)
    num = num * 2
    Console.WriteLine($"Inside sub: {num}")
End Sub

Dim original As Integer = 5
DoubleValue(original)
Console.WriteLine($"Outside sub: {original}")
' Output:
' Inside sub: 10
' Outside sub: 10   <-- original IS changed
```

### Comparison

| Feature | By Value | By Reference |
|---------|----------|--------------|
| What is passed | A copy of the data | A reference to the original data |
| Effect on original | Original is unchanged | Original can be changed |
| Safety | Safer -- protects original data | Riskier -- can cause side effects |
| Memory | Uses more memory (creates a copy) | Uses less memory (no copy made) |
| VB.NET keyword | `ByVal` (default) | `ByRef` |
| When to use | When the subroutine only needs to read the value | When the subroutine needs to modify the original variable |

<div class="exam-tip" markdown="1">
A common exam question is to trace through code that uses `ByVal` and `ByRef` and predict the output. Remember: with `ByVal`, changes inside the subroutine are discarded when the subroutine ends. With `ByRef`, changes persist because the subroutine operates on the original variable.
</div>

---

## Local and Global Variables

### Local Variables

A **local variable** is declared inside a subroutine and can only be accessed from within that subroutine. It is created when the subroutine starts and destroyed when the subroutine ends.

```python
def calculate_total():
    # 'subtotal' and 'tax' are local variables
    subtotal = 100.00
    tax = subtotal * 0.20
    total = subtotal + tax
    return total

result = calculate_total()
print(result)        # Works: prints 120.0
# print(subtotal)    # Error! 'subtotal' is not defined here
```

```vb
Function CalculateTotal() As Double
    ' subtotal and tax are local variables
    Dim subtotal As Double = 100.0
    Dim tax As Double = subtotal * 0.2
    Dim total As Double = subtotal + tax
    Return total
End Function

Dim result As Double = CalculateTotal()
Console.WriteLine(result)     ' Works: prints 120
' Console.WriteLine(subtotal) ' Error! subtotal is not accessible here
```

### Global Variables

A **global variable** is declared outside any subroutine and can be accessed from anywhere in the program.

```python
# Global variable
score = 0

def add_points(points):
    global score    # Must use 'global' keyword in Python to modify a global variable
    score = score + points

def display_score():
    print(f"Current score: {score}")

add_points(10)
add_points(5)
display_score()   # Output: Current score: 15
```

```vb
Module Program
    ' Global variable
    Dim score As Integer = 0

    Sub AddPoints(points As Integer)
        score = score + points
    End Sub

    Sub DisplayScore()
        Console.WriteLine($"Current score: {score}")
    End Sub

    Sub Main()
        AddPoints(10)
        AddPoints(5)
        DisplayScore()   ' Output: Current score: 15
    End Sub
End Module
```

### Why Local Variables Are Preferred

| Reason | Explanation |
|--------|-------------|
| **Avoids naming conflicts** | Two subroutines can use the same variable name without conflict |
| **Reduces side effects** | Changes in one subroutine cannot accidentally affect another |
| **Easier debugging** | You only need to look at the subroutine to understand the variable's behaviour |
| **Memory efficient** | Local variables are destroyed when the subroutine ends, freeing memory |
| **Portability** | Subroutines with local variables are self-contained and can be reused elsewhere |

<div class="key-term" markdown="1">
A **local variable** is declared inside a subroutine and is only accessible within that subroutine. A **global variable** is declared outside all subroutines and is accessible throughout the entire program. Best practice is to use local variables wherever possible and pass data between subroutines using parameters.
</div>

---

## Scope and Lifetime

### Scope

The **scope** of a variable refers to the region of the program where it can be accessed. A variable can only be used within its scope.

- **Local scope**: the variable is accessible only within the subroutine where it is declared.
- **Global scope**: the variable is accessible from anywhere in the program.

If a local variable has the same name as a global variable, the local variable takes precedence within its subroutine (this is called **shadowing**).

```python
name = "Global"    # Global scope

def greet():
    name = "Local"  # Local scope - shadows the global variable
    print(name)     # Prints "Local"

greet()
print(name)         # Prints "Global" - global variable is unaffected
```

```vb
Module Program
    Dim name As String = "Global"  ' Global scope

    Sub Greet()
        Dim name As String = "Local"  ' Local scope - shadows the global variable
        Console.WriteLine(name)        ' Prints "Local"
    End Sub

    Sub Main()
        Greet()
        Console.WriteLine(name)        ' Prints "Global"
    End Sub
End Module
```

### Lifetime

The **lifetime** of a variable is the period during which it exists in memory.

- **Local variables** exist from the moment the subroutine is called until the subroutine finishes. They are created and destroyed each time the subroutine runs.
- **Global variables** exist for the entire duration of the program's execution.

| Concept | Local Variable | Global Variable |
|---------|---------------|-----------------|
| **Scope** | Within the subroutine only | Entire program |
| **Lifetime** | Created when subroutine starts; destroyed when it ends | Created when program starts; destroyed when it ends |
| **Initialisation** | Reinitialised each time the subroutine is called | Initialised once when the program starts |

<div class="exam-tip" markdown="1">
Be careful not to confuse scope and lifetime. **Scope** is about where a variable can be accessed. **Lifetime** is about how long the variable exists in memory. A local variable's scope is its subroutine; its lifetime is the duration of that subroutine's execution.
</div>

---

## Constants and Their Importance

A **constant** is a named value that is set once and cannot be changed during program execution. Constants are declared in a similar way to variables but their value is fixed.

```python
# Constants (Python convention: use UPPER_CASE names)
VAT_RATE = 0.20
MAX_STUDENTS = 30
SCHOOL_NAME = "Greenfield Academy"
PI = 3.14159265

def calculate_price(base_price):
    return base_price * (1 + VAT_RATE)
```

```vb
' Constants (VB.NET uses the Const keyword)
Const VAT_RATE As Double = 0.2
Const MAX_STUDENTS As Integer = 30
Const SCHOOL_NAME As String = "Greenfield Academy"
Const PI As Double = 3.14159265

Function CalculatePrice(basePrice As Double) As Double
    Return basePrice * (1 + VAT_RATE)
End Function
```

### Why Use Constants?

| Reason | Explanation |
|--------|-------------|
| **Readability** | `VAT_RATE` is more meaningful than `0.20` scattered through the code |
| **Maintainability** | If the VAT rate changes, you only need to update it in one place |
| **Prevents accidental modification** | The compiler/interpreter will raise an error if you try to change a constant |
| **Self-documenting** | The constant name explains what the value represents |
| **Reduces errors** | Avoids mistyping a value in multiple places (e.g. typing `0.02` instead of `0.20`) |

<div class="key-term" markdown="1">
A **constant** is a named data item whose value is fixed at the time of declaration and cannot be changed during program execution. Constants improve readability, maintainability, and reduce errors.
</div>

---

## Naming Conventions and Self-Documenting Code

### Naming Conventions

Good naming conventions make code easier to read and maintain. Different conventions are used in different languages, but consistency is key.

| Convention | Style | Example | Typically Used In |
|-----------|-------|---------|-------------------|
| **camelCase** | First word lowercase, subsequent words capitalised | `studentName`, `totalScore` | Python variables, JavaScript |
| **PascalCase** | Every word capitalised | `StudentName`, `CalculateTotal` | VB.NET methods and classes |
| **snake_case** | All lowercase, words separated by underscores | `student_name`, `total_score` | Python functions and variables |
| **UPPER_SNAKE_CASE** | All uppercase, words separated by underscores | `MAX_SIZE`, `VAT_RATE` | Constants in most languages |

### Rules for Good Variable Names

- Use **meaningful, descriptive** names: `total_price` not `tp` or `x`.
- Avoid single-letter names except for simple loop counters (e.g. `i`, `j`).
- Do not use reserved words (e.g. `print`, `if`, `for`).
- Start with a letter, not a number or special character.
- Be consistent with your chosen convention throughout the program.

### Self-Documenting Code

**Self-documenting code** is code that is written so clearly that it explains itself without needing extensive comments. This is achieved through:

- Meaningful variable and subroutine names.
- Clear, logical program structure.
- Appropriate use of constants instead of "magic numbers".
- Short subroutines that each do one thing well.

```python
# Poor naming - not self-documenting
def calc(a, b):
    c = a * b * 0.2
    return a * b + c

# Good naming - self-documenting
def calculate_total_with_vat(quantity, unit_price):
    vat = quantity * unit_price * VAT_RATE
    return quantity * unit_price + vat
```

```vb
' Poor naming - not self-documenting
Function Calc(a As Integer, b As Double) As Double
    Dim c As Double = a * b * 0.2
    Return a * b + c
End Function

' Good naming - self-documenting
Function CalculateTotalWithVAT(quantity As Integer, unitPrice As Double) As Double
    Dim vat As Double = quantity * unitPrice * VAT_RATE
    Return quantity * unitPrice + vat
End Function
```

<div class="exam-tip" markdown="1">
In the exam, if you are asked to write code, always use meaningful variable names. Writing `x = a + b` when you mean `total_price = subtotal + delivery_charge` will cost you marks. Similarly, if asked about self-documenting code, explain that it uses meaningful names and clear structure so that the purpose of the code is obvious without needing comments.
</div>

---

## Data Types

A **data type** defines what kind of data a variable can hold and what operations can be performed on it. Choosing the correct data type is essential for writing correct and efficient programs.

### Common Data Types

| Data Type | Description | Example Values | Storage (typical) |
|-----------|-------------|----------------|-------------------|
| **Integer** | Whole numbers (positive, negative, or zero) | `42`, `-7`, `0` | 2 or 4 bytes |
| **Real (Float/Double)** | Numbers with a decimal/fractional part | `3.14`, `-0.5`, `100.0` | 4 or 8 bytes |
| **Boolean** | Logical values -- only two possible values | `True`, `False` | 1 bit (stored as 1 byte) |
| **Character (Char)** | A single character | `'A'`, `'7'`, `'#'` | 1 or 2 bytes |
| **String** | A sequence of characters | `"Hello"`, `"CS101"`, `""` | Varies (1-2 bytes per character) |

### Declaring Variables with Data Types

```python
# Python uses dynamic typing - types are inferred
age = 17                  # Integer
price = 19.99             # Float (real)
is_student = True         # Boolean
initial = 'J'             # String (Python has no separate char type)
full_name = "Jane Smith"  # String
```

```vb
' VB.NET uses static typing - types must be declared
Dim age As Integer = 17
Dim price As Double = 19.99
Dim isStudent As Boolean = True
Dim initial As Char = "J"c
Dim fullName As String = "Jane Smith"
```

### Choosing the Correct Data Type

- Use **Integer** for counting, indexing, or any whole number quantity (e.g. number of students, age in years).
- Use **Real/Double** for measurements, money, or any value that may have a fractional part (e.g. price, temperature, average).
- Use **Boolean** for yes/no, true/false, on/off situations (e.g. is the user logged in, has the file been saved).
- Use **Character** for a single letter, digit, or symbol (e.g. a grade like 'A', a menu choice like '1').
- Use **String** for text made up of multiple characters (e.g. names, addresses, messages).

<div class="key-term" markdown="1">
A **data type** specifies the kind of value a variable can store and the operations that can be performed on it. The five core data types at AS level are: **integer**, **real** (float/double), **Boolean**, **character**, and **string**.
</div>

---

## Type Casting / Type Conversion

**Type casting** (or type conversion) is the process of converting a value from one data type to another. This is often necessary when combining values of different types or when processing user input.

### Why Type Conversion is Needed

- **User input** is typically received as a string and must be converted to a number before performing calculations.
- **Combining types** in expressions (e.g. concatenating a string with a number) often requires explicit conversion.
- **Storing results** may require a different type (e.g. converting a real number to an integer by rounding).

### Common Conversions

```python
# String to Integer
age_str = input("Enter your age: ")   # input() always returns a string
age = int(age_str)                     # Convert string to integer

# String to Float (Real)
price_str = "19.99"
price = float(price_str)

# Integer to String
score = 85
message = "Your score is " + str(score)

# Float to Integer (truncates decimal part)
height = 5.8
whole_height = int(height)   # Result: 5

# Integer to Float
count = 10
average = float(count) / 3   # Result: 3.333...

# Integer to Boolean
flag = bool(1)    # True (any non-zero is True)
flag2 = bool(0)   # False

# Character to ASCII value and back
ascii_val = ord('A')    # Result: 65
character = chr(65)     # Result: 'A'
```

```vb
' String to Integer
Dim ageStr As String = Console.ReadLine()
Dim age As Integer = Convert.ToInt32(ageStr)
' or: Dim age As Integer = CInt(ageStr)

' String to Double (Real)
Dim priceStr As String = "19.99"
Dim price As Double = Convert.ToDouble(priceStr)
' or: Dim price As Double = CDbl(priceStr)

' Integer to String
Dim score As Integer = 85
Dim message As String = "Your score is " & CStr(score)
' or: Dim message As String = "Your score is " & score.ToString()

' Double to Integer (rounds to nearest)
Dim height As Double = 5.8
Dim wholeHeight As Integer = CInt(height)   ' Result: 6 (rounds)

' Integer to Double
Dim count As Integer = 10
Dim average As Double = CDbl(count) / 3   ' Result: 3.333...

' Integer to Boolean
Dim flag As Boolean = CBool(1)    ' True
Dim flag2 As Boolean = CBool(0)   ' False

' Character to ASCII value and back
Dim asciiVal As Integer = Asc("A"c)     ' Result: 65
Dim character As Char = Chr(65)          ' Result: 'A'
```

### Summary of Conversion Functions

| Conversion | Python | VB.NET |
|-----------|--------|--------|
| String to Integer | `int("42")` | `CInt("42")` or `Convert.ToInt32("42")` |
| String to Real | `float("3.14")` | `CDbl("3.14")` or `Convert.ToDouble("3.14")` |
| Number to String | `str(42)` | `CStr(42)` or `42.ToString()` |
| Real to Integer | `int(3.7)` -- truncates to 3 | `CInt(3.7)` -- rounds to 4 |
| Char to ASCII | `ord('A')` -- gives 65 | `Asc("A"c)` -- gives 65 |
| ASCII to Char | `chr(65)` -- gives 'A' | `Chr(65)` -- gives 'A' |

<div class="exam-tip" markdown="1">
A very common source of errors is forgetting to convert user input from a string to a number before performing arithmetic. In Python, `input()` always returns a string. In VB.NET, `Console.ReadLine()` always returns a string. If you try to add `"5" + "3"` you get `"53"` (concatenation) not `8`. Always convert to the correct type first. Note also that Python's `int()` truncates (removes the decimal) while VB.NET's `CInt()` rounds to the nearest integer.
</div>
