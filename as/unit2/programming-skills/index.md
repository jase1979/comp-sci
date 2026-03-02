---
layout: topic
title: "Programming Skills"
level: "AS"
level_url: "/as/"
unit_name: "Unit 2: Practical Programming to Solve Problems"
unit_url: "/as/unit2/"
prev_topic: "/as/unit2/analysis-design/"
next_topic: "/as/unit2/code-quality/"
---

## Introduction

This topic covers the core programming skills required for WJEC AS Unit 2. You must be able to write, trace, and explain code using these fundamental constructs. All examples are provided in both Python and VB.NET.

---

## User Interface Design

The user interface (UI) is how the user interacts with your program. At AS level, you should understand two main types.

### Command Line Interface (CLI)

A CLI uses text-based input and output. The user types commands or data and the program responds with text on the screen.

```python
# CLI menu system
def display_menu():
    print("===== Student Records =====")
    print("1. Add student")
    print("2. View all students")
    print("3. Search for student")
    print("4. Quit")
    print("===========================")

def main():
    while True:
        display_menu()
        choice = input("Enter your choice (1-4): ")

        if choice == "1":
            add_student()
        elif choice == "2":
            view_students()
        elif choice == "3":
            search_student()
        elif choice == "4":
            print("Goodbye!")
            break
        else:
            print("Invalid choice. Please try again.")

main()
```

```vb
' CLI menu system
Sub DisplayMenu()
    Console.WriteLine("===== Student Records =====")
    Console.WriteLine("1. Add student")
    Console.WriteLine("2. View all students")
    Console.WriteLine("3. Search for student")
    Console.WriteLine("4. Quit")
    Console.WriteLine("===========================")
End Sub

Sub Main()
    Dim choice As String = ""

    While choice <> "4"
        DisplayMenu()
        Console.Write("Enter your choice (1-4): ")
        choice = Console.ReadLine()

        Select Case choice
            Case "1"
                AddStudent()
            Case "2"
                ViewStudents()
            Case "3"
                SearchStudent()
            Case "4"
                Console.WriteLine("Goodbye!")
            Case Else
                Console.WriteLine("Invalid choice. Please try again.")
        End Select
    End While
End Sub
```

### Graphical User Interface (GUI)

A GUI uses visual elements such as windows, buttons, text boxes, and labels. Users interact using a mouse and keyboard.

```python
# Basic GUI with tkinter
import tkinter as tk

def greet_user():
    name = entry_name.get()
    label_output.config(text=f"Hello, {name}!")

window = tk.Tk()
window.title("Greeting App")

label_prompt = tk.Label(window, text="Enter your name:")
label_prompt.pack()

entry_name = tk.Entry(window)
entry_name.pack()

button_greet = tk.Button(window, text="Greet", command=greet_user)
button_greet.pack()

label_output = tk.Label(window, text="")
label_output.pack()

window.mainloop()
```

```vb
' Basic GUI in VB.NET (Windows Forms)
' In a Form with TextBox (txtName), Button (btnGreet), Label (lblOutput)
Public Class Form1
    Private Sub btnGreet_Click(sender As Object, e As EventArgs) Handles btnGreet.Click
        Dim name As String = txtName.Text
        lblOutput.Text = "Hello, " & name & "!"
    End Sub
End Class
```

<div class="exam-tip" markdown="1">
For your coursework, a CLI is perfectly acceptable and often simpler to implement. If you choose a GUI, make sure it is functional and well-organised. The marks are for the programming, not the visual design.
</div>

| Feature | CLI | GUI |
|---|---|---|
| Input method | Keyboard only | Mouse and keyboard |
| Ease of use | Requires knowledge of commands | Intuitive, visual |
| Development time | Faster to code | Slower to code |
| Resource usage | Low | Higher |

---

## Data Types

You must understand and use the following data types correctly.

<div class="key-term" markdown="1">
**Data type** -- Defines what kind of data a variable can hold and what operations can be performed on it.
</div>

| Data Type | Description | Python Example | VB.NET Example |
|---|---|---|---|
| String | Text / sequence of characters | `"Hello"` | `"Hello"` |
| Integer | Whole number | `42` | `42` |
| Real / Float | Decimal number | `3.14` | `3.14` |
| Boolean | True or False | `True` | `True` |
| Char | Single character | `'A'` (Python uses strings) | `"A"c` |

### Declaring and Using Data Types

```python
# Python is dynamically typed - types are inferred
name = "Alice"          # string
age = 17                # integer
height = 1.65           # float (real)
is_student = True       # boolean
initial = "A"           # Python has no separate char type

# You can check the type of a variable
print(type(name))       # <class 'str'>
print(type(age))        # <class 'int'>
print(type(height))     # <class 'float'>
print(type(is_student)) # <class 'bool'>

# Type casting (converting between types)
age_as_string = str(age)         # "17"
height_as_int = int(height)      # 1 (truncates decimal)
text_number = "25"
number = int(text_number)        # 25
decimal = float(text_number)     # 25.0
```

```vb
' VB.NET is statically typed - you must declare types
Dim name As String = "Alice"
Dim age As Integer = 17
Dim height As Double = 1.65       ' Double is the real/float type
Dim isStudent As Boolean = True
Dim initial As Char = "A"c        ' Note the 'c' suffix for Char

' Type casting (converting between types)
Dim ageAsString As String = CStr(age)         ' "17"
Dim heightAsInt As Integer = CInt(height)     ' 2 (rounds)
Dim textNumber As String = "25"
Dim number As Integer = CInt(textNumber)      ' 25
Dim decimalNum As Double = CDbl(textNumber)   ' 25.0
```

<div class="exam-tip" markdown="1">
Remember that Python is **dynamically typed** (you do not declare the type) while VB.NET is **statically typed** (you must declare the type with `Dim ... As`). The exam may ask you about the consequences of this difference.
</div>

---

## Variables and Constants

<div class="key-term" markdown="1">
**Variable** -- A named storage location in memory whose value can change during program execution.
</div>

<div class="key-term" markdown="1">
**Constant** -- A named storage location whose value is set once and cannot be changed during program execution.
</div>

```python
# Variables - values can change
score = 0
score = score + 10
player_name = "Player 1"

# Constants - Python uses UPPER_CASE by convention (not enforced)
VAT_RATE = 0.2
MAX_ATTEMPTS = 3
PI = 3.14159

# Using constants in calculations
price = 50.00
tax = price * VAT_RATE
total = price + tax
print(f"Price: {price}, Tax: {tax}, Total: {total}")
```

```vb
' Variables - values can change
Dim score As Integer = 0
score = score + 10
Dim playerName As String = "Player 1"

' Constants - enforced by the language
Const VAT_RATE As Double = 0.2
Const MAX_ATTEMPTS As Integer = 3
Const PI As Double = 3.14159

' Using constants in calculations
Dim price As Double = 50.0
Dim tax As Double = price * VAT_RATE
Dim total As Double = price + tax
Console.WriteLine("Price: " & price & ", Tax: " & tax & ", Total: " & total)
```

<div class="exam-tip" markdown="1">
Always use **constants** for values that do not change (e.g. VAT rate, maximum retries, pi). This makes code easier to maintain -- if the value needs updating, you change it in one place. Using a constant also makes the code more readable than using a "magic number".
</div>

---

## Arrays (1D and 2D)

<div class="key-term" markdown="1">
**Array** -- An ordered, fixed-size collection of elements of the same data type, accessed by index.
</div>

### 1D Arrays

A one-dimensional array is a simple list of values.

```python
# Python uses lists (which act like dynamic arrays)
# 1D array of student names
students = ["Alice", "Bob", "Charlie", "Diana", "Eve"]

# Accessing elements (0-indexed)
print(students[0])        # Alice
print(students[3])        # Diana

# Modifying an element
students[1] = "Benjamin"

# Length of the array
print(len(students))      # 5

# Iterating through the array
for i in range(len(students)):
    print(f"Index {i}: {students[i]}")

# Alternative: iterate directly
for student in students:
    print(student)

# Initialise an array of 10 zeros
scores = [0] * 10
```

```vb
' VB.NET arrays
' 1D array of student names (index 0 to 4)
Dim students(4) As String
students(0) = "Alice"
students(1) = "Bob"
students(2) = "Charlie"
students(3) = "Diana"
students(4) = "Eve"

' Or initialise with values
Dim names() As String = {"Alice", "Bob", "Charlie", "Diana", "Eve"}

' Accessing elements (0-indexed)
Console.WriteLine(students(0))    ' Alice
Console.WriteLine(students(3))    ' Diana

' Modifying an element
students(1) = "Benjamin"

' Length of the array
Console.WriteLine(students.Length) ' 5

' Iterating through the array
For i As Integer = 0 To students.Length - 1
    Console.WriteLine("Index " & i & ": " & students(i))
Next

' Initialise an array of 10 zeros
Dim scores(9) As Integer   ' indices 0 to 9, default value 0
```

### 2D Arrays

A two-dimensional array is like a table with rows and columns.

```python
# 2D array: 3 students, 4 test scores each
scores = [
    [78, 85, 92, 88],   # Student 0
    [65, 72, 80, 75],   # Student 1
    [90, 95, 88, 92]    # Student 2
]

# Accessing elements: scores[row][column]
print(scores[0][2])   # 92 (Student 0, Test 2)
print(scores[2][1])   # 95 (Student 2, Test 1)

# Iterating through a 2D array
for row in range(len(scores)):
    total = 0
    for col in range(len(scores[row])):
        total += scores[row][col]
    average = total / len(scores[row])
    print(f"Student {row}: Average = {average:.1f}")

# Modifying an element
scores[1][3] = 78
```

```vb
' 2D array: 3 students (rows 0-2), 4 test scores each (columns 0-3)
Dim scores(2, 3) As Integer
scores(0, 0) = 78 : scores(0, 1) = 85 : scores(0, 2) = 92 : scores(0, 3) = 88
scores(1, 0) = 65 : scores(1, 1) = 72 : scores(1, 2) = 80 : scores(1, 3) = 75
scores(2, 0) = 90 : scores(2, 1) = 95 : scores(2, 2) = 88 : scores(2, 3) = 92

' Accessing elements: scores(row, column)
Console.WriteLine(scores(0, 2))   ' 92 (Student 0, Test 2)
Console.WriteLine(scores(2, 1))   ' 95 (Student 2, Test 1)

' Iterating through a 2D array
For row As Integer = 0 To 2
    Dim total As Integer = 0
    For col As Integer = 0 To 3
        total += scores(row, col)
    Next
    Dim average As Double = total / 4
    Console.WriteLine("Student " & row & ": Average = " & average.ToString("F1"))
Next

' Modifying an element
scores(1, 3) = 78
```

<div class="exam-tip" markdown="1">
Note that in VB.NET, `Dim scores(2, 3)` creates an array with indices 0 to 2 and 0 to 3 (i.e. 3 rows and 4 columns). The number in the declaration is the **upper bound**, not the size. In Python, 2D arrays are lists of lists and use two separate sets of square brackets: `scores[row][col]`.
</div>

---

## File Handling -- Reading and Writing Files

File handling is essential for storing data permanently. At AS level, you need to work with text files and CSV files.

### Writing to a Text File

```python
# Writing to a text file
with open("students.txt", "w") as file:
    file.write("Alice\n")
    file.write("Bob\n")
    file.write("Charlie\n")

# Appending to a text file (adds to end, does not overwrite)
with open("students.txt", "a") as file:
    file.write("Diana\n")
```

```vb
' Writing to a text file
Using writer As New System.IO.StreamWriter("students.txt", False) ' False = overwrite
    writer.WriteLine("Alice")
    writer.WriteLine("Bob")
    writer.WriteLine("Charlie")
End Using

' Appending to a text file
Using writer As New System.IO.StreamWriter("students.txt", True) ' True = append
    writer.WriteLine("Diana")
End Using
```

### Reading from a Text File

```python
# Reading all lines from a text file
with open("students.txt", "r") as file:
    lines = file.readlines()
    for line in lines:
        print(line.strip())  # strip() removes the trailing newline

# Reading line by line
with open("students.txt", "r") as file:
    for line in file:
        print(line.strip())

# Reading the entire file as one string
with open("students.txt", "r") as file:
    content = file.read()
    print(content)
```

```vb
' Reading all lines from a text file
Dim lines() As String = System.IO.File.ReadAllLines("students.txt")
For Each line As String In lines
    Console.WriteLine(line)
Next

' Reading line by line
Using reader As New System.IO.StreamReader("students.txt")
    While Not reader.EndOfStream
        Dim line As String = reader.ReadLine()
        Console.WriteLine(line)
    End While
End Using
```

### Working with CSV Files

CSV (Comma-Separated Values) files store tabular data as plain text, with each field separated by a comma.

```python
# Writing CSV data
with open("students.csv", "w") as file:
    file.write("Name,Age,Grade\n")
    file.write("Alice,17,A\n")
    file.write("Bob,16,B\n")
    file.write("Charlie,17,C\n")

# Reading and parsing CSV data
with open("students.csv", "r") as file:
    header = file.readline().strip()  # Read and skip header
    print(f"{'Name':<15}{'Age':<5}{'Grade':<5}")
    print("-" * 25)
    for line in file:
        parts = line.strip().split(",")
        name = parts[0]
        age = parts[1]
        grade = parts[2]
        print(f"{name:<15}{age:<5}{grade:<5}")

# Using the csv module (recommended)
import csv

with open("students.csv", "r") as file:
    reader = csv.reader(file)
    header = next(reader)  # Skip header row
    for row in reader:
        print(f"Name: {row[0]}, Age: {row[1]}, Grade: {row[2]}")
```

```vb
' Writing CSV data
Using writer As New System.IO.StreamWriter("students.csv", False)
    writer.WriteLine("Name,Age,Grade")
    writer.WriteLine("Alice,17,A")
    writer.WriteLine("Bob,16,B")
    writer.WriteLine("Charlie,17,C")
End Using

' Reading and parsing CSV data
Dim lines() As String = System.IO.File.ReadAllLines("students.csv")
Console.WriteLine(String.Format("{0,-15}{1,-5}{2,-5}", "Name", "Age", "Grade"))
Console.WriteLine(New String("-"c, 25))

For i As Integer = 1 To lines.Length - 1  ' Start at 1 to skip header
    Dim parts() As String = lines(i).Split(","c)
    Dim name As String = parts(0)
    Dim age As String = parts(1)
    Dim grade As String = parts(2)
    Console.WriteLine(String.Format("{0,-15}{1,-5}{2,-5}", name, age, grade))
Next
```

### Searching a File

```python
# Searching for a student in a CSV file
def search_student(filename, search_name):
    with open(filename, "r") as file:
        file.readline()  # Skip header
        for line in file:
            parts = line.strip().split(",")
            if parts[0].lower() == search_name.lower():
                return {"name": parts[0], "age": parts[1], "grade": parts[2]}
    return None

result = search_student("students.csv", "Bob")
if result:
    print(f"Found: {result['name']}, Age: {result['age']}, Grade: {result['grade']}")
else:
    print("Student not found.")
```

```vb
' Searching for a student in a CSV file
Function SearchStudent(filename As String, searchName As String) As String
    Dim lines() As String = System.IO.File.ReadAllLines(filename)
    For i As Integer = 1 To lines.Length - 1
        Dim parts() As String = lines(i).Split(","c)
        If parts(0).ToLower() = searchName.ToLower() Then
            Return "Found: " & parts(0) & ", Age: " & parts(1) & ", Grade: " & parts(2)
        End If
    Next
    Return "Student not found."
End Function

Console.WriteLine(SearchStudent("students.csv", "Bob"))
```

<div class="exam-tip" markdown="1">
Always use the `with` statement in Python (or `Using` in VB.NET) when working with files. This ensures the file is properly closed even if an error occurs. Forgetting to close a file can cause data loss or file corruption.
</div>

---

## Validation Techniques

<div class="key-term" markdown="1">
**Validation** -- The process of checking that data meets specified rules or criteria before it is accepted by the program. Validation checks that data is **reasonable and sensible**, but it cannot guarantee data is **correct**.
</div>

### Range Check

Ensures a value falls within an acceptable range.

```python
def get_age():
    while True:
        age = int(input("Enter age (0-120): "))
        if 0 <= age <= 120:
            return age
        print("Error: Age must be between 0 and 120.")
```

```vb
Function GetAge() As Integer
    Dim age As Integer
    Do
        Console.Write("Enter age (0-120): ")
        age = CInt(Console.ReadLine())
        If age < 0 Or age > 120 Then
            Console.WriteLine("Error: Age must be between 0 and 120.")
        End If
    Loop Until age >= 0 And age <= 120
    Return age
End Function
```

### Format Check

Ensures data matches an expected pattern or format.

```python
import re

def get_email():
    while True:
        email = input("Enter email address: ")
        # Simple email format check
        if re.match(r"^[^@]+@[^@]+\.[^@]+$", email):
            return email
        print("Error: Invalid email format. Must contain @ and a domain.")

def get_postcode():
    while True:
        postcode = input("Enter UK postcode (e.g. CF10 3AT): ")
        if re.match(r"^[A-Z]{1,2}\d{1,2}\s?\d[A-Z]{2}$", postcode.upper()):
            return postcode.upper()
        print("Error: Invalid postcode format.")
```

```vb
Function GetEmail() As String
    Dim email As String
    Do
        Console.Write("Enter email address: ")
        email = Console.ReadLine()
        If Not email.Contains("@") Or Not email.Contains(".") Then
            Console.WriteLine("Error: Invalid email format. Must contain @ and a domain.")
        End If
    Loop Until email.Contains("@") And email.Contains(".")
    Return email
End Function
```

### Presence Check

Ensures a field is not left empty.

```python
def get_name():
    while True:
        name = input("Enter your name: ")
        if name.strip() != "":
            return name.strip()
        print("Error: Name cannot be empty.")
```

```vb
Function GetName() As String
    Dim name As String
    Do
        Console.Write("Enter your name: ")
        name = Console.ReadLine().Trim()
        If name = "" Then
            Console.WriteLine("Error: Name cannot be empty.")
        End If
    Loop Until name <> ""
    Return name
End Function
```

### Length Check

Ensures data has an acceptable number of characters.

```python
def get_password():
    while True:
        password = input("Enter password (8-20 characters): ")
        if 8 <= len(password) <= 20:
            return password
        print(f"Error: Password must be 8-20 characters. You entered {len(password)}.")
```

```vb
Function GetPassword() As String
    Dim password As String
    Do
        Console.Write("Enter password (8-20 characters): ")
        password = Console.ReadLine()
        If password.Length < 8 Or password.Length > 20 Then
            Console.WriteLine("Error: Password must be 8-20 characters. You entered " & password.Length & ".")
        End If
    Loop Until password.Length >= 8 And password.Length <= 20
    Return password
End Function
```

### Type Check

Ensures the data entered is of the correct data type.

```python
def get_integer(prompt):
    while True:
        try:
            value = int(input(prompt))
            return value
        except ValueError:
            print("Error: Please enter a whole number.")

def get_float(prompt):
    while True:
        try:
            value = float(input(prompt))
            return value
        except ValueError:
            print("Error: Please enter a number.")
```

```vb
Function GetInteger(prompt As String) As Integer
    Dim value As Integer
    Dim valid As Boolean = False
    Do
        Console.Write(prompt)
        Dim userInput As String = Console.ReadLine()
        If Integer.TryParse(userInput, value) Then
            valid = True
        Else
            Console.WriteLine("Error: Please enter a whole number.")
        End If
    Loop Until valid
    Return value
End Function
```

### Lookup Check

Ensures the data matches one of a predefined set of acceptable values.

```python
def get_membership_type():
    valid_types = ["adult", "child", "senior"]
    while True:
        membership = input("Enter membership type (Adult/Child/Senior): ")
        if membership.lower() in valid_types:
            return membership.capitalize()
        print(f"Error: Must be one of: {', '.join(valid_types)}")
```

```vb
Function GetMembershipType() As String
    Dim validTypes() As String = {"Adult", "Child", "Senior"}
    Dim membership As String
    Dim valid As Boolean = False
    Do
        Console.Write("Enter membership type (Adult/Child/Senior): ")
        membership = Console.ReadLine()
        For Each validType As String In validTypes
            If membership.ToLower() = validType.ToLower() Then
                valid = True
                membership = validType
                Exit For
            End If
        Next
        If Not valid Then
            Console.WriteLine("Error: Must be one of: Adult, Child, Senior")
        End If
    Loop Until valid
    Return membership
End Function
```

### Summary of Validation Techniques

| Technique | Purpose | Example |
|---|---|---|
| Range check | Value within min/max bounds | Age between 0 and 120 |
| Format check | Matches expected pattern | Email contains @ and . |
| Presence check | Field is not empty | Name must not be blank |
| Length check | Correct number of characters | Password 8-20 chars |
| Type check | Correct data type entered | Must be a whole number |
| Lookup check | Matches allowed values | Must be Adult, Child, or Senior |

<div class="exam-tip" markdown="1">
**Validation is not the same as verification.** Validation checks data is reasonable; verification checks data has been entered correctly (e.g. "enter your email twice"). A common exam question asks you to distinguish between the two.
</div>

---

## Local and Global Variables

<div class="key-term" markdown="1">
**Local variable** -- A variable declared inside a subroutine. It can only be accessed within that subroutine and exists only while the subroutine is executing.
</div>

<div class="key-term" markdown="1">
**Global variable** -- A variable declared outside all subroutines, at the top level of the program. It can be accessed from anywhere in the program.
</div>

```python
# Global variable
total_score = 0

def add_score(points):
    global total_score          # Needed to modify a global in Python
    local_message = "Adding score"   # Local variable
    print(local_message)
    total_score += points

def display_score():
    # Can read global variable
    print(f"Total score: {total_score}")
    # print(local_message)  # ERROR: local_message is not accessible here

add_score(10)
add_score(25)
display_score()      # Output: Total score: 35
```

```vb
' Global variable (declared at module level)
Module Program
    Dim totalScore As Integer = 0

    Sub AddScore(points As Integer)
        Dim localMessage As String = "Adding score"   ' Local variable
        Console.WriteLine(localMessage)
        totalScore += points
    End Sub

    Sub DisplayScore()
        ' Can access global variable
        Console.WriteLine("Total score: " & totalScore)
        ' Console.WriteLine(localMessage)  ' ERROR: not accessible here
    End Sub

    Sub Main()
        AddScore(10)
        AddScore(25)
        DisplayScore()   ' Output: Total score: 35
    End Sub
End Module
```

### Why Prefer Local Variables?

| Reason | Explanation |
|---|---|
| Avoids side effects | Changes inside a subroutine do not accidentally affect other parts of the program |
| Easier to debug | You only need to look at the subroutine to find problems |
| Reusability | Subroutines with local variables are self-contained and can be reused |
| Memory efficiency | Local variables are destroyed when the subroutine ends |

<div class="exam-tip" markdown="1">
In general, **avoid global variables** wherever possible. Use parameters to pass data into subroutines and return values to get data out. Global variables make programs harder to debug and maintain because any part of the code could change them unexpectedly.
</div>

---

## Subroutines -- Functions and Procedures

<div class="key-term" markdown="1">
**Subroutine** -- A named block of code that performs a specific task. Subroutines are either **procedures** (which do not return a value) or **functions** (which return a value).
</div>

### Procedures

A procedure performs an action but does not return a value.

```python
# Procedure (no return value)
def print_header(title):
    print("=" * 40)
    print(f"  {title}")
    print("=" * 40)

def print_student(name, age, grade):
    print(f"Name: {name}, Age: {age}, Grade: {grade}")

print_header("Student Report")
print_student("Alice", 17, "A")
```

```vb
' Procedure (Sub - no return value)
Sub PrintHeader(title As String)
    Console.WriteLine(New String("="c, 40))
    Console.WriteLine("  " & title)
    Console.WriteLine(New String("="c, 40))
End Sub

Sub PrintStudent(name As String, age As Integer, grade As String)
    Console.WriteLine("Name: " & name & ", Age: " & age & ", Grade: " & grade)
End Sub

Sub Main()
    PrintHeader("Student Report")
    PrintStudent("Alice", 17, "A")
End Sub
```

### Functions

A function performs an action and returns a value to the caller.

```python
# Function (returns a value)
def calculate_average(marks):
    total = sum(marks)
    return total / len(marks)

def get_grade(average):
    if average >= 70:
        return "A"
    elif average >= 60:
        return "B"
    elif average >= 50:
        return "C"
    elif average >= 40:
        return "D"
    else:
        return "U"

def calculate_area(length, width):
    return length * width

# Using functions
marks = [78, 85, 92, 88]
avg = calculate_average(marks)
grade = get_grade(avg)
print(f"Average: {avg:.1f}, Grade: {grade}")

area = calculate_area(5.0, 3.2)
print(f"Area: {area}")
```

```vb
' Function (returns a value)
Function CalculateAverage(marks() As Integer) As Double
    Dim total As Integer = 0
    For Each mark As Integer In marks
        total += mark
    Next
    Return total / marks.Length
End Function

Function GetGrade(average As Double) As String
    If average >= 70 Then
        Return "A"
    ElseIf average >= 60 Then
        Return "B"
    ElseIf average >= 50 Then
        Return "C"
    ElseIf average >= 40 Then
        Return "D"
    Else
        Return "U"
    End If
End Function

Function CalculateArea(length As Double, width As Double) As Double
    Return length * width
End Function

Sub Main()
    Dim marks() As Integer = {78, 85, 92, 88}
    Dim avg As Double = CalculateAverage(marks)
    Dim grade As String = GetGrade(avg)
    Console.WriteLine("Average: " & avg.ToString("F1") & ", Grade: " & grade)

    Dim area As Double = CalculateArea(5.0, 3.2)
    Console.WriteLine("Area: " & area)
End Sub
```

<div class="exam-tip" markdown="1">
In Python, both procedures and functions use `def`. The difference is whether the subroutine contains a `return` statement. In VB.NET, procedures use `Sub` and functions use `Function`. Always use functions when you need a result back, and procedures when you just need to perform an action.
</div>

---

## Parameter Passing

<div class="key-term" markdown="1">
**Parameter** -- A variable listed in a subroutine's definition that receives a value when the subroutine is called.
</div>

<div class="key-term" markdown="1">
**Argument** -- The actual value passed to a subroutine when it is called.
</div>

### Passing by Value

A copy of the argument is passed. Changes to the parameter inside the subroutine do not affect the original variable.

```python
# Python passes immutable types (int, string, float) by value effectively
def double_value(num):
    num = num * 2
    print(f"Inside function: {num}")

original = 5
double_value(original)
print(f"Outside function: {original}")
# Output:
# Inside function: 10
# Outside function: 5  (unchanged)
```

```vb
' VB.NET: ByVal (pass by value) - this is the default
Sub DoubleValue(ByVal num As Integer)
    num = num * 2
    Console.WriteLine("Inside sub: " & num)
End Sub

Sub Main()
    Dim original As Integer = 5
    DoubleValue(original)
    Console.WriteLine("Outside sub: " & original)
    ' Output:
    ' Inside sub: 10
    ' Outside sub: 5  (unchanged)
End Sub
```

### Passing by Reference

A reference to the original variable is passed. Changes to the parameter inside the subroutine do affect the original variable.

```python
# Python: mutable types (lists) are passed by reference effectively
def add_item(my_list, item):
    my_list.append(item)

names = ["Alice", "Bob"]
add_item(names, "Charlie")
print(names)  # ["Alice", "Bob", "Charlie"] - original list is modified

# To simulate pass by reference for simple types, return the new value
def double_and_return(num):
    return num * 2

value = 5
value = double_and_return(value)
print(value)  # 10
```

```vb
' VB.NET: ByRef (pass by reference)
Sub DoubleValue(ByRef num As Integer)
    num = num * 2
    Console.WriteLine("Inside sub: " & num)
End Sub

Sub Main()
    Dim original As Integer = 5
    DoubleValue(original)
    Console.WriteLine("Outside sub: " & original)
    ' Output:
    ' Inside sub: 10
    ' Outside sub: 10  (changed!)
End Sub
```

### Comparison

| Feature | By Value | By Reference |
|---|---|---|
| What is passed | A copy of the data | A reference to the original |
| Effect on original | Original is unchanged | Original can be changed |
| VB.NET keyword | `ByVal` (default) | `ByRef` |
| Use case | When you do not want side effects | When the subroutine needs to modify the original |

<div class="exam-tip" markdown="1">
In VB.NET, `ByVal` is the default. You must explicitly use `ByRef` to pass by reference. The exam may give you code and ask you to trace the values of variables -- pay close attention to whether parameters are passed by value or by reference.
</div>

---

## String Manipulation

String manipulation is a frequently tested skill. You must be able to extract, search, and modify strings.

```python
# String basics
text = "Hello, World!"

# Length
print(len(text))              # 13

# Accessing characters (0-indexed)
print(text[0])                # H
print(text[7])                # W

# Slicing (substring)
print(text[0:5])              # Hello
print(text[7:12])             # World
print(text[-1])               # !

# Searching
print(text.find("World"))     # 7  (index of first occurrence)
print("World" in text)        # True

# Case conversion
print(text.upper())           # HELLO, WORLD!
print(text.lower())           # hello, world!

# Replacing
print(text.replace("World", "Python"))  # Hello, Python!

# Splitting
sentence = "the cat sat on the mat"
words = sentence.split(" ")
print(words)                  # ['the', 'cat', 'sat', 'on', 'the', 'mat']
print(words[1])               # cat

# Joining
joined = "-".join(words)
print(joined)                 # the-cat-sat-on-the-mat

# Stripping whitespace
padded = "   hello   "
print(padded.strip())         # "hello"

# Checking content
print("123".isdigit())        # True
print("abc".isalpha())        # True
print("abc123".isalnum())     # True

# String concatenation
first = "Hello"
second = "World"
result = first + " " + second
print(result)                 # Hello World
```

```vb
' String basics
Dim text As String = "Hello, World!"

' Length
Console.WriteLine(text.Length)              ' 13

' Accessing characters (0-indexed)
Console.WriteLine(text(0))                 ' H
Console.WriteLine(text(7))                 ' W

' Substring (startIndex, length)
Console.WriteLine(text.Substring(0, 5))    ' Hello
Console.WriteLine(text.Substring(7, 5))    ' World

' Searching
Console.WriteLine(text.IndexOf("World"))   ' 7 (index of first occurrence)
Console.WriteLine(text.Contains("World"))  ' True

' Case conversion
Console.WriteLine(text.ToUpper())          ' HELLO, WORLD!
Console.WriteLine(text.ToLower())          ' hello, world!

' Replacing
Console.WriteLine(text.Replace("World", "VB.NET"))  ' Hello, VB.NET!

' Splitting
Dim sentence As String = "the cat sat on the mat"
Dim words() As String = sentence.Split(" "c)
Console.WriteLine(words(1))                ' cat

' Joining
Dim joined As String = String.Join("-", words)
Console.WriteLine(joined)                  ' the-cat-sat-on-the-mat

' Trimming whitespace
Dim padded As String = "   hello   "
Console.WriteLine(padded.Trim())           ' "hello"

' Checking content
Console.WriteLine(IsNumeric("123"))        ' True

' String concatenation
Dim first As String = "Hello"
Dim second As String = "World"
Dim result As String = first & " " & second
Console.WriteLine(result)                  ' Hello World
```

### Practical Example -- Extracting Initials

```python
def get_initials(full_name):
    parts = full_name.strip().split(" ")
    initials = ""
    for part in parts:
        if len(part) > 0:
            initials += part[0].upper()
    return initials

print(get_initials("John Paul Smith"))   # JPS
print(get_initials("alice jones"))       # AJ
```

```vb
Function GetInitials(fullName As String) As String
    Dim parts() As String = fullName.Trim().Split(" "c)
    Dim initials As String = ""
    For Each part As String In parts
        If part.Length > 0 Then
            initials &= part(0).ToString().ToUpper()
        End If
    Next
    Return initials
End Function

Console.WriteLine(GetInitials("John Paul Smith"))   ' JPS
Console.WriteLine(GetInitials("alice jones"))       ' AJ
```

### Practical Example -- Validating a Password

```python
def check_password_strength(password):
    has_upper = False
    has_lower = False
    has_digit = False
    has_special = False
    special_chars = "!@#$%^&*"

    for char in password:
        if char.isupper():
            has_upper = True
        elif char.islower():
            has_lower = True
        elif char.isdigit():
            has_digit = True
        elif char in special_chars:
            has_special = True

    if len(password) >= 8 and has_upper and has_lower and has_digit and has_special:
        return "Strong"
    elif len(password) >= 8 and has_upper and has_lower and has_digit:
        return "Medium"
    else:
        return "Weak"

print(check_password_strength("MyP@ss99"))   # Strong
print(check_password_strength("MyPass99"))   # Medium
print(check_password_strength("pass"))       # Weak
```

```vb
Function CheckPasswordStrength(password As String) As String
    Dim hasUpper As Boolean = False
    Dim hasLower As Boolean = False
    Dim hasDigit As Boolean = False
    Dim hasSpecial As Boolean = False
    Dim specialChars As String = "!@#$%^&*"

    For Each ch As Char In password
        If Char.IsUpper(ch) Then
            hasUpper = True
        ElseIf Char.IsLower(ch) Then
            hasLower = True
        ElseIf Char.IsDigit(ch) Then
            hasDigit = True
        ElseIf specialChars.Contains(ch) Then
            hasSpecial = True
        End If
    Next

    If password.Length >= 8 And hasUpper And hasLower And hasDigit And hasSpecial Then
        Return "Strong"
    ElseIf password.Length >= 8 And hasUpper And hasLower And hasDigit Then
        Return "Medium"
    Else
        Return "Weak"
    End If
End Function
```

---

## Error Handling

<div class="key-term" markdown="1">
**Error handling** -- The process of anticipating, detecting, and responding to errors that occur during program execution, preventing the program from crashing.
</div>

### Try/Except (Python) and Try/Catch (VB.NET)

```python
# Basic error handling
try:
    number = int(input("Enter a number: "))
    result = 100 / number
    print(f"Result: {result}")
except ValueError:
    print("Error: That is not a valid number.")
except ZeroDivisionError:
    print("Error: Cannot divide by zero.")

# Catching multiple exceptions
try:
    file = open("data.txt", "r")
    content = file.read()
    file.close()
except FileNotFoundError:
    print("Error: File not found.")
except PermissionError:
    print("Error: Permission denied.")

# Using a general except with finally
try:
    value = int(input("Enter value: "))
    print(f"You entered: {value}")
except Exception as e:
    print(f"An error occurred: {e}")
finally:
    print("This always runs, whether an error occurred or not.")
```

```vb
' Basic error handling
Try
    Console.Write("Enter a number: ")
    Dim number As Integer = CInt(Console.ReadLine())
    Dim result As Double = 100 / number
    Console.WriteLine("Result: " & result)
Catch ex As InvalidCastException
    Console.WriteLine("Error: That is not a valid number.")
Catch ex As DivideByZeroException
    Console.WriteLine("Error: Cannot divide by zero.")
End Try

' Catching file errors
Try
    Dim content As String = System.IO.File.ReadAllText("data.txt")
    Console.WriteLine(content)
Catch ex As System.IO.FileNotFoundException
    Console.WriteLine("Error: File not found.")
Catch ex As UnauthorizedAccessException
    Console.WriteLine("Error: Permission denied.")
End Try

' Using a general Catch with Finally
Try
    Console.Write("Enter value: ")
    Dim value As Integer = CInt(Console.ReadLine())
    Console.WriteLine("You entered: " & value)
Catch ex As Exception
    Console.WriteLine("An error occurred: " & ex.Message)
Finally
    Console.WriteLine("This always runs, whether an error occurred or not.")
End Try
```

### Robust Input with Error Handling

```python
def get_validated_integer(prompt, min_val, max_val):
    while True:
        try:
            value = int(input(prompt))
            if min_val <= value <= max_val:
                return value
            else:
                print(f"Error: Value must be between {min_val} and {max_val}.")
        except ValueError:
            print("Error: Please enter a whole number.")

# Usage
age = get_validated_integer("Enter your age (0-120): ", 0, 120)
print(f"Your age is: {age}")
```

```vb
Function GetValidatedInteger(prompt As String, minVal As Integer, maxVal As Integer) As Integer
    Dim value As Integer
    Dim valid As Boolean = False

    Do
        Console.Write(prompt)
        Dim userInput As String = Console.ReadLine()
        Try
            value = CInt(userInput)
            If value >= minVal And value <= maxVal Then
                valid = True
            Else
                Console.WriteLine("Error: Value must be between " & minVal & " and " & maxVal & ".")
            End If
        Catch ex As Exception
            Console.WriteLine("Error: Please enter a whole number.")
        End Try
    Loop Until valid

    Return value
End Function

' Usage
Dim age As Integer = GetValidatedInteger("Enter your age (0-120): ", 0, 120)
Console.WriteLine("Your age is: " & age)
```

### Error Handling with File Operations

```python
def save_data(filename, data):
    try:
        with open(filename, "w") as file:
            for item in data:
                file.write(item + "\n")
        print(f"Data saved to {filename} successfully.")
        return True
    except PermissionError:
        print(f"Error: Cannot write to {filename}. Permission denied.")
        return False
    except Exception as e:
        print(f"Error saving data: {e}")
        return False

def load_data(filename):
    try:
        with open(filename, "r") as file:
            data = []
            for line in file:
                data.append(line.strip())
        return data
    except FileNotFoundError:
        print(f"Error: {filename} not found. Starting with empty data.")
        return []
```

```vb
Function SaveData(filename As String, data As List(Of String)) As Boolean
    Try
        Using writer As New System.IO.StreamWriter(filename, False)
            For Each item As String In data
                writer.WriteLine(item)
            Next
        End Using
        Console.WriteLine("Data saved to " & filename & " successfully.")
        Return True
    Catch ex As UnauthorizedAccessException
        Console.WriteLine("Error: Cannot write to " & filename & ". Permission denied.")
        Return False
    Catch ex As Exception
        Console.WriteLine("Error saving data: " & ex.Message)
        Return False
    End Try
End Function

Function LoadData(filename As String) As List(Of String)
    Dim data As New List(Of String)
    Try
        Dim lines() As String = System.IO.File.ReadAllLines(filename)
        For Each line As String In lines
            data.Add(line)
        Next
    Catch ex As System.IO.FileNotFoundException
        Console.WriteLine("Error: " & filename & " not found. Starting with empty data.")
    End Try
    Return data
End Function
```

<div class="exam-tip" markdown="1">
Good error handling provides **meaningful feedback** to the user. Instead of letting the program crash with a technical error message, catch the exception and display a clear, user-friendly message explaining what went wrong and what the user should do.
</div>

---

## Summary

| Skill | Key Points |
|---|---|
| User interface | CLI for text-based interaction; GUI for visual interaction |
| Data types | String, Integer, Real/Float, Boolean, Char |
| Variables and constants | Variables change; constants do not. Use constants for fixed values |
| Arrays | 1D for simple lists; 2D for tables. Access by index |
| File handling | Use `with`/`Using` for safe file access. Read, write, and append |
| Validation | Range, format, presence, length, type, and lookup checks |
| Scope | Prefer local variables; avoid globals where possible |
| Subroutines | Procedures perform actions; functions return values |
| Parameters | By value (copy) vs by reference (original) |
| String manipulation | Length, slicing, searching, case conversion, splitting |
| Error handling | Use try/except (Python) or Try/Catch (VB.NET) for robust programs |
