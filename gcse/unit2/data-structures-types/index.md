---
layout: topic
title: "Data Structures & Data Types"
level: "GCSE"
level_url: "/gcse/"
unit_name: "Unit 2: Computational Thinking & Programming"
unit_url: "/gcse/unit2/"
prev_topic: "/gcse/unit2/programming-languages/"
next_topic: "/gcse/unit2/security-authentication/"
---

## Implementing: 1D and 2D Arrays, Files and Records

Programs need ways to store and organise data. This section covers three important data structures you must know: **arrays**, **files** and **records**.

### 1D Arrays

A 1D (one-dimensional) array is a list of items stored under a single name. Each item has an **index** (position number) so you can access it directly.

<div class="key-term" markdown="1">
**Array** -- A data structure that stores a fixed collection of elements of the same data type, accessed by index.
</div>

**Python**

```python
# Creating a 1D array (list in Python)
scores = [45, 78, 92, 61, 85]

# Accessing an element by index (starts at 0)
print(scores[0])   # Output: 45
print(scores[3])   # Output: 61

# Changing an element
scores[2] = 99

# Looping through the array
for i in range(len(scores)):
    print("Index", i, "=", scores[i])
```

**VB.NET**

```vb
' Creating a 1D array
Dim scores(4) As Integer  ' 5 elements, index 0 to 4
scores(0) = 45
scores(1) = 78
scores(2) = 92
scores(3) = 61
scores(4) = 85

' Accessing an element by index (starts at 0)
Console.WriteLine(scores(0))   ' Output: 45
Console.WriteLine(scores(3))   ' Output: 61

' Changing an element
scores(2) = 99

' Looping through the array
For i As Integer = 0 To scores.Length - 1
    Console.WriteLine("Index " & i & " = " & scores(i))
Next
```

### 2D Arrays

A 2D (two-dimensional) array is like a table with rows and columns. You need **two indices** to access an element -- one for the row and one for the column.

**Python**

```python
# Creating a 2D array (list of lists)
# 3 rows, 4 columns -- e.g. marks for 3 students across 4 tests
marks = [
    [56, 78, 45, 90],
    [88, 64, 72, 81],
    [43, 91, 67, 55]
]

# Accessing row 1, column 2
print(marks[1][2])   # Output: 72

# Changing a value
marks[0][3] = 95

# Looping through every element
for row in range(len(marks)):
    for col in range(len(marks[row])):
        print(marks[row][col], end=" ")
    print()
```

**VB.NET**

```vb
' Creating a 2D array -- 3 rows, 4 columns
Dim marks(2, 3) As Integer
marks(0, 0) = 56
marks(0, 1) = 78
marks(0, 2) = 45
marks(0, 3) = 90
marks(1, 0) = 88
marks(1, 1) = 64
marks(1, 2) = 72
marks(1, 3) = 81
marks(2, 0) = 43
marks(2, 1) = 91
marks(2, 2) = 67
marks(2, 3) = 55

' Accessing row 1, column 2
Console.WriteLine(marks(1, 2))   ' Output: 72

' Changing a value
marks(0, 3) = 95

' Looping through every element
For row As Integer = 0 To 2
    For col As Integer = 0 To 3
        Console.Write(marks(row, col) & " ")
    Next
    Console.WriteLine()
Next
```

<div class="exam-tip" markdown="1">
Remember that array indices usually start at **0**, not 1. An array with 5 elements has indices 0 to 4. In VB.NET, `Dim arr(4)` creates an array with indices 0 to 4 (5 elements).
</div>

### Files

Programs use **files** to store data permanently. When a program ends, variables in memory are lost, but data written to a file remains on disk. You need to know how to **read from** and **write to** text files.

<div class="key-term" markdown="1">
**Text file** -- A file that stores data as plain text, with each line typically representing one piece or row of data.
</div>

**Python**

```python
# Writing to a file
file = open("scores.txt", "w")
file.write("Alice,85\n")
file.write("Bob,72\n")
file.write("Charlie,91\n")
file.close()

# Reading from a file
file = open("scores.txt", "r")
for line in file:
    print(line.strip())
file.close()

# Appending to a file (adds to the end)
file = open("scores.txt", "a")
file.write("Diana,68\n")
file.close()
```

**VB.NET**

```vb
Imports System.IO

' Writing to a file
Dim writer As New StreamWriter("scores.txt")
writer.WriteLine("Alice,85")
writer.WriteLine("Bob,72")
writer.WriteLine("Charlie,91")
writer.Close()

' Reading from a file
Dim reader As New StreamReader("scores.txt")
While Not reader.EndOfStream
    Dim line As String = reader.ReadLine()
    Console.WriteLine(line)
End While
reader.Close()

' Appending to a file (adds to the end)
Dim appender As New StreamWriter("scores.txt", True)
appender.WriteLine("Diana,68")
appender.Close()
```

| File mode | Python | VB.NET | Purpose |
|---|---|---|---|
| Write | `"w"` | `New StreamWriter(path)` | Creates or overwrites a file |
| Read | `"r"` | `New StreamReader(path)` | Opens a file for reading |
| Append | `"a"` | `New StreamWriter(path, True)` | Adds data to the end of a file |

### Records

A **record** is a data structure that groups together related fields of different data types under one name. For example, a student record might hold a name (string), age (integer) and grade (character).

<div class="key-term" markdown="1">
**Record** -- A data structure made up of a fixed number of related fields, where each field can be a different data type.
</div>

**Python**

```python
# Using a dictionary to represent a record
student = {
    "name": "Alice",
    "age": 16,
    "grade": "A"
}

# Accessing fields
print(student["name"])    # Output: Alice
print(student["age"])     # Output: 16

# A list of records
students = [
    {"name": "Alice", "age": 16, "grade": "A"},
    {"name": "Bob", "age": 15, "grade": "B"},
    {"name": "Charlie", "age": 16, "grade": "C"}
]

# Looping through records
for s in students:
    print(s["name"], "is", s["age"], "years old")
```

**VB.NET**

```vb
' Defining a record using a Structure
Structure Student
    Dim Name As String
    Dim Age As Integer
    Dim Grade As Char
End Structure

' Creating and using a record
Dim pupil As Student
pupil.Name = "Alice"
pupil.Age = 16
pupil.Grade = "A"c

' Accessing fields
Console.WriteLine(pupil.Name)    ' Output: Alice
Console.WriteLine(pupil.Age)     ' Output: 16

' An array of records
Dim students(2) As Student
students(0).Name = "Alice"
students(0).Age = 16
students(0).Grade = "A"c
students(1).Name = "Bob"
students(1).Age = 15
students(1).Grade = "B"c
students(2).Name = "Charlie"
students(2).Age = 16
students(2).Grade = "C"c

' Looping through records
For i As Integer = 0 To 2
    Console.WriteLine(students(i).Name & " is " & students(i).Age & " years old")
Next
```

<div class="exam-tip" markdown="1">
In exam questions, records are often shown as tables. Each **row** is a single record and each **column** is a field. Be ready to write pseudocode that creates a record structure and accesses its fields.
</div>

---

## Data Types: Integer, Boolean, Real, Character, String

Every piece of data in a program has a **data type**. The data type tells the computer what kind of value it is and what operations can be performed on it.

| Data type | Description | Example values |
|---|---|---|
| **Integer** | A whole number (no decimal point) | `5`, `-12`, `0` |
| **Real** (float) | A number with a decimal point | `3.14`, `-0.5`, `99.0` |
| **Boolean** | A value that is either True or False | `True`, `False` |
| **Character** | A single letter, digit or symbol | `'A'`, `'7'`, `'!'` |
| **String** | A sequence of characters (text) | `"Hello"`, `"GCSE"` |

<div class="key-term" markdown="1">
**Data type** -- Defines what kind of value a variable holds and determines what operations can be performed on it.
</div>

**Python**

```python
# Integer
age = 16
print(type(age))         # <class 'int'>

# Real (float)
price = 9.99
print(type(price))       # <class 'float'>

# Boolean
is_student = True
print(type(is_student))  # <class 'bool'>

# Character (Python uses a string of length 1)
initial = "J"
print(type(initial))     # <class 'str'>

# String
name = "Alice"
print(type(name))        # <class 'str'>

# Casting between types
number_text = "42"
number = int(number_text)       # String to integer
decimal = float(number_text)    # String to real
back_to_text = str(number)      # Integer to string
```

**VB.NET**

```vb
' Integer
Dim age As Integer = 16

' Real (single or double precision)
Dim price As Single = 9.99

' Boolean
Dim isStudent As Boolean = True

' Character
Dim initial As Char = "J"c

' String
Dim name As String = "Alice"

' Casting between types
Dim numberText As String = "42"
Dim number As Integer = CInt(numberText)        ' String to integer
Dim decimal As Single = CSng(numberText)        ' String to real
Dim backToText As String = CStr(number)         ' Integer to string
```

<div class="exam-tip" markdown="1">
**Casting** (type conversion) is a common exam topic. You must know how to convert between strings and numbers. In Python, use `int()`, `float()` and `str()`. In VB.NET, use `CInt()`, `CSng()` / `CDbl()` and `CStr()`.
</div>

---

## Constants and Variables: Assignment, Identification, Use

### Variables

A **variable** is a named location in memory whose value can change while the program runs. You create a variable by **assigning** a value to it.

<div class="key-term" markdown="1">
**Variable** -- A named storage location in memory whose value can be changed during program execution.
</div>

**Python**

```python
# Assigning variables
score = 0
player_name = "Alice"

# Changing (reassigning) a variable
score = score + 10
print(score)        # Output: 10

# Using variables in expressions
bonus = 5
total = score + bonus
print(total)        # Output: 15
```

**VB.NET**

```vb
' Assigning variables
Dim score As Integer = 0
Dim playerName As String = "Alice"

' Changing (reassigning) a variable
score = score + 10
Console.WriteLine(score)        ' Output: 10

' Using variables in expressions
Dim bonus As Integer = 5
Dim total As Integer = score + bonus
Console.WriteLine(total)        ' Output: 15
```

### Constants

A **constant** is a named value that is set once and **cannot be changed** while the program runs. Constants are used for values that should stay the same, such as VAT rate or pi.

<div class="key-term" markdown="1">
**Constant** -- A named storage location in memory whose value is fixed at the start and cannot change during program execution.
</div>

**Python**

```python
# Python does not enforce constants, but UPPERCASE names
# signal to other programmers that the value should not change
VAT_RATE = 0.2
MAX_LIVES = 3
PI = 3.14159

# Using a constant in a calculation
item_price = 50.00
total_price = item_price + (item_price * VAT_RATE)
print(total_price)   # Output: 60.0
```

**VB.NET**

```vb
' VB.NET enforces constants with the Const keyword
Const VAT_RATE As Double = 0.2
Const MAX_LIVES As Integer = 3
Const PI As Double = 3.14159

' Using a constant in a calculation
Dim itemPrice As Double = 50.0
Dim totalPrice As Double = itemPrice + (itemPrice * VAT_RATE)
Console.WriteLine(totalPrice)   ' Output: 60.0

' Trying to change a constant causes an error:
' VAT_RATE = 0.25   <-- This would NOT compile
```

| Feature | Variable | Constant |
|---|---|---|
| Value can change? | Yes | No |
| When is the value set? | Any time during the program | Once, when it is declared |
| Naming convention | `camelCase` or `snake_case` | `UPPER_CASE` |
| Use case | Scores, user input, counters | Tax rates, maximum values, pi |

<div class="exam-tip" markdown="1">
Using constants instead of hard-coded numbers makes your code easier to read and maintain. If the value needs to change, you only update it in one place. Examiners reward the use of **meaningful constant names**.
</div>

---

## Scope and Lifetime of Variables

### Scope

The **scope** of a variable is the part of the program where that variable can be accessed.

- A **local variable** is declared inside a function or subroutine. It can only be used within that function.
- A **global variable** is declared outside all functions. It can be accessed from anywhere in the program.

<div class="key-term" markdown="1">
**Scope** -- The region of a program in which a variable is visible and can be used. Local scope means inside one function; global scope means the entire program.
</div>

**Python**

```python
# Global variable
total_score = 0

def add_points(points):
    # Local variable -- only exists inside this function
    bonus = 2
    result = points + bonus

    # Accessing the global variable requires the global keyword
    global total_score
    total_score = total_score + result

add_points(10)
print(total_score)   # Output: 12

# print(bonus)  <-- This would cause an error because
#                    bonus is local to add_points
```

**VB.NET**

```vb
' Global variable (declared at module level)
Dim totalScore As Integer = 0

Sub AddPoints(points As Integer)
    ' Local variable -- only exists inside this subroutine
    Dim bonus As Integer = 2
    Dim result As Integer = points + bonus

    ' Accessing the global variable
    totalScore = totalScore + result
End Sub

Sub Main()
    AddPoints(10)
    Console.WriteLine(totalScore)   ' Output: 12

    ' Console.WriteLine(bonus)  <-- This would cause an error
    '                               because bonus is local to AddPoints
End Sub
```

### Lifetime

The **lifetime** of a variable is how long it exists in memory.

| Type | Scope | Lifetime |
|---|---|---|
| **Local variable** | Inside the function where it is declared | Created when the function is called; destroyed when the function ends |
| **Global variable** | The entire program | Created when the program starts; destroyed when the program ends |

**Python**

```python
def roll_dice():
    # This local variable is created each time roll_dice is called
    import random
    result = random.randint(1, 6)
    print("You rolled:", result)
    # When the function ends, result is destroyed

roll_dice()
roll_dice()
# Each call creates a fresh 'result' variable
```

**VB.NET**

```vb
Sub RollDice()
    ' This local variable is created each time RollDice is called
    Dim rng As New Random()
    Dim result As Integer = rng.Next(1, 7)
    Console.WriteLine("You rolled: " & result)
    ' When the subroutine ends, result is destroyed
End Sub

Sub Main()
    RollDice()
    RollDice()
    ' Each call creates a fresh 'result' variable
End Sub
```

<div class="exam-tip" markdown="1">
Examiners often ask **why local variables are preferred** over global variables. Key reasons: (1) they prevent accidental changes from other parts of the program, (2) they use memory only while the function runs, and (3) they make code easier to debug and test. Only use global variables when data genuinely needs to be shared across the whole program.
</div>
