---
layout: topic
title: "Code Quality"
level: "AS"
level_url: "/as/"
unit_name: "Unit 2: Practical Programming to Solve Problems"
unit_url: "/as/unit2/"
prev_topic: "/as/unit2/programming-skills/"
---

## Introduction

Writing code that works is not enough. At AS level, you are expected to write code that is **readable, maintainable, and efficient**. This topic covers the techniques and practices that make the difference between code that merely functions and code that demonstrates professional quality. Examiners and moderators look for these qualities in your coursework.

---

## Self-Documenting Identifiers

<div class="key-term" markdown="1">
**Self-documenting code** -- Code that is written in such a way that its purpose can be understood from reading the code itself, without needing additional comments. Meaningful identifier names are the most important aspect of self-documenting code.
</div>

### Naming Conventions

Good identifier names clearly describe what the variable, function, or constant represents.

| Bad Name | Good Name | Why It Is Better |
|---|---|---|
| `x` | `student_age` | Describes what the data represents |
| `a` | `total_marks` | No ambiguity about what is being stored |
| `temp` | `celsius_temperature` | Specific and descriptive |
| `flag` | `is_logged_in` | Boolean naming convention (is/has prefix) |
| `data` | `customer_records` | Tells you what kind of data |
| `fn` | `calculate_average` | Describes what the function does |
| `n` | `num_students` | Clear that it is a count of students |

### Python Naming Conventions

```python
# Variables and functions: snake_case
student_name = "Alice"
total_score = 85
is_valid = True

def calculate_average(marks):
    total = sum(marks)
    return total / len(marks)

def get_student_by_id(student_id):
    # ...
    pass

# Constants: UPPER_SNAKE_CASE
MAX_ATTEMPTS = 3
VAT_RATE = 0.2
DEFAULT_PASSWORD_LENGTH = 8

# Booleans: use is_, has_, can_ prefixes
is_active = True
has_permission = False
can_edit = True
```

### VB.NET Naming Conventions

```vb
' Variables: camelCase
Dim studentName As String = "Alice"
Dim totalScore As Integer = 85
Dim isValid As Boolean = True

' Functions and Subs: PascalCase
Function CalculateAverage(marks() As Integer) As Double
    Dim total As Integer = 0
    For Each mark As Integer In marks
        total += mark
    Next
    Return total / marks.Length
End Function

Function GetStudentById(studentId As Integer) As String
    ' ...
    Return ""
End Function

' Constants: PascalCase or UPPER_CASE
Const MaxAttempts As Integer = 3
Const VatRate As Double = 0.2
Const DEFAULT_PASSWORD_LENGTH As Integer = 8

' Booleans: use is, has, can prefixes
Dim isActive As Boolean = True
Dim hasPermission As Boolean = False
Dim canEdit As Boolean = True
```

### Comparison: Poor vs Good Naming

```python
# POOR: What does this code do?
def calc(a, b, c):
    d = (a + b + c) / 3
    if d >= 50:
        return True
    return False

x = calc(65, 72, 58)
```

```python
# GOOD: Immediately understandable
def has_passed_course(exam_mark, coursework_mark, practical_mark):
    average_mark = (exam_mark + coursework_mark + practical_mark) / 3
    if average_mark >= 50:
        return True
    return False

student_passed = has_passed_course(65, 72, 58)
```

```vb
' POOR: What does this code do?
Function Calc(a As Integer, b As Integer, c As Integer) As Boolean
    Dim d As Double = (a + b + c) / 3
    If d >= 50 Then
        Return True
    End If
    Return False
End Function

Dim x As Boolean = Calc(65, 72, 58)
```

```vb
' GOOD: Immediately understandable
Function HasPassedCourse(examMark As Integer, courseworkMark As Integer, practicalMark As Integer) As Boolean
    Dim averageMark As Double = (examMark + courseworkMark + practicalMark) / 3
    If averageMark >= 50 Then
        Return True
    End If
    Return False
End Function

Dim studentPassed As Boolean = HasPassedCourse(65, 72, 58)
```

<div class="exam-tip" markdown="1">
The use of meaningful identifiers is one of the easiest marks to gain in the coursework. Never use single-letter variable names (except for loop counters like `i` and `j`) or generic names like `data`, `temp`, or `stuff`. Every identifier should make its purpose obvious.
</div>

---

## Program Annotation and Comments

Comments explain the **why** behind your code, not the **what**. Good comments add value by explaining intent, reasoning, or complex logic that is not immediately obvious.

### When to Comment

| Do Comment | Do Not Comment |
|---|---|
| Why a decision was made | What an obvious line of code does |
| Complex algorithms or formulas | Every single line |
| Assumptions made | Things that are clear from good naming |
| Known limitations or workarounds | Restating the code in English |
| The purpose of each subroutine | Obvious variable assignments |

### Examples of Good and Bad Comments

```python
# BAD COMMENTS - restating the obvious
x = 0          # Set x to 0
x = x + 1      # Add 1 to x
name = input("Enter name: ")   # Get the user's name

# GOOD COMMENTS - explaining why
# Using binary search as the list is sorted and may contain thousands of records
def search_student(student_list, target_id):
    low = 0
    high = len(student_list) - 1

    while low <= high:
        mid = (low + high) // 2
        if student_list[mid]["id"] == target_id:
            return student_list[mid]
        elif student_list[mid]["id"] < target_id:
            low = mid + 1
        else:
            high = mid - 1
    return None
```

```vb
' BAD COMMENTS - restating the obvious
Dim x As Integer = 0          ' Set x to 0
x = x + 1                     ' Add 1 to x

' GOOD COMMENTS - explaining why
' Using binary search as the list is sorted and may contain thousands of records
Function SearchStudent(studentList() As Student, targetId As Integer) As Student
    Dim low As Integer = 0
    Dim high As Integer = studentList.Length - 1

    While low <= high
        Dim mid As Integer = (low + high) \ 2
        If studentList(mid).Id = targetId Then
            Return studentList(mid)
        ElseIf studentList(mid).Id < targetId Then
            low = mid + 1
        Else
            high = mid - 1
        End If
    End While
    Return Nothing
End Function
```

### Subroutine Header Comments

Every subroutine should have a brief comment explaining its purpose, parameters, and return value.

```python
def calculate_discount(price, membership_type):
    """
    Calculates the discounted price based on the customer's membership type.

    Parameters:
        price (float): The original price of the item
        membership_type (str): "gold", "silver", or "bronze"

    Returns:
        float: The price after the discount has been applied
    """
    if membership_type == "gold":
        discount = 0.20
    elif membership_type == "silver":
        discount = 0.10
    elif membership_type == "bronze":
        discount = 0.05
    else:
        discount = 0.0

    return price * (1 - discount)
```

```vb
' Calculates the discounted price based on the customer's membership type.
' Parameters:
'   price (Double) - The original price of the item
'   membershipType (String) - "Gold", "Silver", or "Bronze"
' Returns:
'   Double - The price after the discount has been applied
Function CalculateDiscount(price As Double, membershipType As String) As Double
    Dim discount As Double

    Select Case membershipType.ToLower()
        Case "gold"
            discount = 0.2
        Case "silver"
            discount = 0.1
        Case "bronze"
            discount = 0.05
        Case Else
            discount = 0.0
    End Select

    Return price * (1 - discount)
End Function
```

### Section Comments

Use comments to divide your code into logical sections.

```python
# ===== CONSTANTS =====
MAX_STUDENTS = 30
PASS_MARK = 50

# ===== FILE OPERATIONS =====
def load_students(filename):
    # ...
    pass

def save_students(filename, students):
    # ...
    pass

# ===== VALIDATION =====
def validate_mark(mark):
    # ...
    pass

# ===== MAIN PROGRAM =====
def main():
    students = load_students("students.csv")
    # ...
```

```vb
' ===== CONSTANTS =====
Const MAX_STUDENTS As Integer = 30
Const PASS_MARK As Integer = 50

' ===== FILE OPERATIONS =====
Function LoadStudents(filename As String) As List(Of String)
    ' ...
    Return New List(Of String)
End Function

Sub SaveStudents(filename As String, students As List(Of String))
    ' ...
End Sub

' ===== VALIDATION =====
Function ValidateMark(mark As Integer) As Boolean
    ' ...
    Return True
End Function

' ===== MAIN PROGRAM =====
Sub Main()
    Dim students As List(Of String) = LoadStudents("students.csv")
    ' ...
End Sub
```

<div class="exam-tip" markdown="1">
In your coursework, aim for a balance. Too few comments and the examiner may struggle to follow your logic. Too many comments (especially obvious ones) clutter the code and show a lack of understanding. Comment the **purpose** of subroutines and explain any **non-obvious** logic.
</div>

---

## Program Layout and Structure

Well-structured code is easier to read, debug, and maintain. Good layout includes consistent indentation, appropriate use of whitespace, and logical grouping of related code.

### Indentation

Indentation shows the structure of your code -- which statements belong inside loops, conditionals, and subroutines.

```python
# GOOD indentation - clear structure
def process_students(students):
    for student in students:
        if student["mark"] >= 50:
            print(f"{student['name']} - PASS")
            if student["mark"] >= 70:
                print("  Distinction!")
        else:
            print(f"{student['name']} - FAIL")
            send_resit_notification(student)

# BAD indentation - confusing and error-prone
def process_students(students):
  for student in students:
        if student["mark"] >= 50:
           print(f"{student['name']} - PASS")
            if student["mark"] >= 70:    # Inconsistent indent
              print("  Distinction!")
        else:
           print(f"{student['name']} - FAIL")
```

```vb
' GOOD indentation - clear structure
Sub ProcessStudents(students As List(Of Student))
    For Each student As Student In students
        If student.Mark >= 50 Then
            Console.WriteLine(student.Name & " - PASS")
            If student.Mark >= 70 Then
                Console.WriteLine("  Distinction!")
            End If
        Else
            Console.WriteLine(student.Name & " - FAIL")
            SendResitNotification(student)
        End If
    Next
End Sub
```

### Whitespace and Blank Lines

Use blank lines to separate logical blocks of code within a subroutine.

```python
def register_student():
    # Get student details
    name = get_validated_name()
    age = get_validated_age()
    email = get_validated_email()

    # Create student record
    student_id = generate_next_id()
    student = {
        "id": student_id,
        "name": name,
        "age": age,
        "email": email
    }

    # Save to file
    save_student(student)

    # Confirm to user
    print(f"Student {name} registered with ID {student_id}.")
```

```vb
Sub RegisterStudent()
    ' Get student details
    Dim name As String = GetValidatedName()
    Dim age As Integer = GetValidatedAge()
    Dim email As String = GetValidatedEmail()

    ' Create student record
    Dim studentId As Integer = GenerateNextId()

    ' Save to file
    SaveStudent(studentId, name, age, email)

    ' Confirm to user
    Console.WriteLine("Student " & name & " registered with ID " & studentId & ".")
End Sub
```

### Logical Grouping

Organise your program so that related subroutines are grouped together, and the main program flow is easy to follow.

```python
# ===== CONSTANTS =====
FILENAME = "inventory.csv"
LOW_STOCK_THRESHOLD = 5

# ===== DATA ACCESS FUNCTIONS =====
def load_inventory():
    items = []
    try:
        with open(FILENAME, "r") as file:
            file.readline()  # Skip header
            for line in file:
                parts = line.strip().split(",")
                items.append({
                    "name": parts[0],
                    "quantity": int(parts[1]),
                    "price": float(parts[2])
                })
    except FileNotFoundError:
        print("No inventory file found. Starting fresh.")
    return items

def save_inventory(items):
    with open(FILENAME, "w") as file:
        file.write("Name,Quantity,Price\n")
        for item in items:
            file.write(f"{item['name']},{item['quantity']},{item['price']:.2f}\n")

# ===== BUSINESS LOGIC =====
def find_item(items, search_name):
    for item in items:
        if item["name"].lower() == search_name.lower():
            return item
    return None

def get_low_stock_items(items):
    low_stock = []
    for item in items:
        if item["quantity"] < LOW_STOCK_THRESHOLD:
            low_stock.append(item)
    return low_stock

# ===== USER INTERFACE =====
def display_menu():
    print("\n===== Inventory System =====")
    print("1. View all items")
    print("2. Search for item")
    print("3. Add item")
    print("4. Low stock report")
    print("5. Quit")
    print("============================")

def display_items(items):
    print(f"{'Name':<20}{'Qty':<10}{'Price':<10}")
    print("-" * 40)
    for item in items:
        print(f"{item['name']:<20}{item['quantity']:<10}{item['price']:<10.2f}")

# ===== MAIN PROGRAM =====
def main():
    items = load_inventory()

    while True:
        display_menu()
        choice = input("Enter choice: ")

        if choice == "1":
            display_items(items)
        elif choice == "2":
            name = input("Enter item name: ")
            result = find_item(items, name)
            if result:
                print(f"Found: {result['name']}, Qty: {result['quantity']}, Price: {result['price']:.2f}")
            else:
                print("Item not found.")
        elif choice == "4":
            low = get_low_stock_items(items)
            if low:
                print("Low stock items:")
                display_items(low)
            else:
                print("No items are low on stock.")
        elif choice == "5":
            save_inventory(items)
            print("Goodbye!")
            break

main()
```

```vb
' ===== CONSTANTS =====
Module InventorySystem
    Const FILENAME As String = "inventory.csv"
    Const LOW_STOCK_THRESHOLD As Integer = 5

    ' ===== DATA ACCESS =====
    Function LoadInventory() As List(Of String())
        Dim items As New List(Of String())
        Try
            Dim lines() As String = System.IO.File.ReadAllLines(FILENAME)
            For i As Integer = 1 To lines.Length - 1
                items.Add(lines(i).Split(","c))
            Next
        Catch ex As System.IO.FileNotFoundException
            Console.WriteLine("No inventory file found. Starting fresh.")
        End Try
        Return items
    End Function

    Sub SaveInventory(items As List(Of String()))
        Using writer As New System.IO.StreamWriter(FILENAME, False)
            writer.WriteLine("Name,Quantity,Price")
            For Each item As String() In items
                writer.WriteLine(item(0) & "," & item(1) & "," & item(2))
            Next
        End Using
    End Sub

    ' ===== USER INTERFACE =====
    Sub DisplayMenu()
        Console.WriteLine(vbCrLf & "===== Inventory System =====")
        Console.WriteLine("1. View all items")
        Console.WriteLine("2. Search for item")
        Console.WriteLine("3. Low stock report")
        Console.WriteLine("4. Quit")
        Console.WriteLine("============================")
    End Sub

    ' ===== MAIN PROGRAM =====
    Sub Main()
        Dim items As List(Of String()) = LoadInventory()
        Dim choice As String = ""

        While choice <> "4"
            DisplayMenu()
            Console.Write("Enter choice: ")
            choice = Console.ReadLine()

            Select Case choice
                Case "1"
                    For Each item As String() In items
                        Console.WriteLine(item(0) & " | Qty: " & item(1) & " | Price: " & item(2))
                    Next
                Case "4"
                    SaveInventory(items)
                    Console.WriteLine("Goodbye!")
            End Select
        End While
    End Sub
End Module
```

<div class="exam-tip" markdown="1">
In Python, indentation is not just a style choice -- it is **part of the syntax**. Incorrect indentation will cause errors. In VB.NET, indentation is optional but strongly expected. Consistent indentation is an easy way to gain marks for code quality.
</div>

---

## Efficient Use of Programming Constructs

Efficient code avoids unnecessary repetition, uses appropriate data structures, and chooses the right control structure for the task.

### Choosing the Right Loop

```python
# Use FOR when you know the number of iterations
for i in range(10):
    print(f"Iteration {i}")

# Use WHILE when you do not know how many times to loop
password = ""
while password != "secret123":
    password = input("Enter password: ")

# INEFFICIENT: using a while loop when a for loop is clearer
i = 0
while i < 10:      # A for loop would be better here
    print(i)
    i += 1
```

```vb
' Use FOR when you know the number of iterations
For i As Integer = 0 To 9
    Console.WriteLine("Iteration " & i)
Next

' Use WHILE (Do...Loop) when you do not know how many times to loop
Dim password As String = ""
Do
    Console.Write("Enter password: ")
    password = Console.ReadLine()
Loop Until password = "secret123"
```

### Avoiding Unnecessary Repetition

```python
# INEFFICIENT: repeated code
mark = int(input("Enter mark: "))
if mark >= 70:
    grade = "A"
    print(f"Mark: {mark}")
    print(f"Grade: {grade}")
    print("Well done!")
elif mark >= 60:
    grade = "B"
    print(f"Mark: {mark}")
    print(f"Grade: {grade}")
    print("Well done!")
elif mark >= 50:
    grade = "C"
    print(f"Mark: {mark}")
    print(f"Grade: {grade}")
    print("Well done!")
else:
    grade = "U"
    print(f"Mark: {mark}")
    print(f"Grade: {grade}")
    print("Better luck next time.")

# EFFICIENT: no repeated code
mark = int(input("Enter mark: "))
if mark >= 70:
    grade = "A"
elif mark >= 60:
    grade = "B"
elif mark >= 50:
    grade = "C"
else:
    grade = "U"

print(f"Mark: {mark}")
print(f"Grade: {grade}")
if grade != "U":
    print("Well done!")
else:
    print("Better luck next time.")
```

```vb
' EFFICIENT: no repeated code
Dim mark As Integer = CInt(Console.ReadLine())
Dim grade As String

If mark >= 70 Then
    grade = "A"
ElseIf mark >= 60 Then
    grade = "B"
ElseIf mark >= 50 Then
    grade = "C"
Else
    grade = "U"
End If

Console.WriteLine("Mark: " & mark)
Console.WriteLine("Grade: " & grade)
If grade <> "U" Then
    Console.WriteLine("Well done!")
Else
    Console.WriteLine("Better luck next time.")
End If
```

### Using Data Structures Instead of Multiple Variables

```python
# INEFFICIENT: separate variables
student1_name = "Alice"
student1_mark = 78
student2_name = "Bob"
student2_mark = 65
student3_name = "Charlie"
student3_mark = 82

# EFFICIENT: use a data structure
students = [
    {"name": "Alice", "mark": 78},
    {"name": "Bob", "mark": 65},
    {"name": "Charlie", "mark": 82}
]

# Now you can loop through them
for student in students:
    print(f"{student['name']}: {student['mark']}")
```

```vb
' INEFFICIENT: separate variables
Dim student1Name As String = "Alice"
Dim student1Mark As Integer = 78
Dim student2Name As String = "Bob"
Dim student2Mark As Integer = 65

' EFFICIENT: use arrays
Dim names() As String = {"Alice", "Bob", "Charlie"}
Dim marks() As Integer = {78, 65, 82}

For i As Integer = 0 To names.Length - 1
    Console.WriteLine(names(i) & ": " & marks(i))
Next
```

### Using Subroutines to Avoid Duplication

```python
# INEFFICIENT: validation code repeated everywhere
name = input("Enter first name: ")
while name.strip() == "":
    print("Error: Cannot be empty.")
    name = input("Enter first name: ")

surname = input("Enter surname: ")
while surname.strip() == "":
    print("Error: Cannot be empty.")
    surname = input("Enter surname: ")

city = input("Enter city: ")
while city.strip() == "":
    print("Error: Cannot be empty.")
    city = input("Enter city: ")

# EFFICIENT: reusable validation subroutine
def get_non_empty_string(prompt):
    while True:
        value = input(prompt)
        if value.strip() != "":
            return value.strip()
        print("Error: Cannot be empty.")

name = get_non_empty_string("Enter first name: ")
surname = get_non_empty_string("Enter surname: ")
city = get_non_empty_string("Enter city: ")
```

```vb
' EFFICIENT: reusable validation subroutine
Function GetNonEmptyString(prompt As String) As String
    Dim value As String
    Do
        Console.Write(prompt)
        value = Console.ReadLine().Trim()
        If value = "" Then
            Console.WriteLine("Error: Cannot be empty.")
        End If
    Loop Until value <> ""
    Return value
End Function

Dim name As String = GetNonEmptyString("Enter first name: ")
Dim surname As String = GetNonEmptyString("Enter surname: ")
Dim city As String = GetNonEmptyString("Enter city: ")
```

---

## Code Refactoring

<div class="key-term" markdown="1">
**Refactoring** -- The process of restructuring existing code without changing its external behaviour. The goal is to improve readability, reduce duplication, and make the code easier to maintain.
</div>

### Example: Before and After Refactoring

**Before refactoring:**

```python
# Original messy code
f = open("marks.txt", "r")
lines = f.readlines()
f.close()
t = 0
c = 0
for l in lines:
    m = int(l.strip())
    if m >= 0 and m <= 100:
        t = t + m
        c = c + 1
if c > 0:
    a = t / c
    print("Average: " + str(a))
    if a >= 70:
        print("Grade: A")
    elif a >= 60:
        print("Grade: B")
    elif a >= 50:
        print("Grade: C")
    elif a >= 40:
        print("Grade: D")
    else:
        print("Grade: U")
else:
    print("No valid marks found.")
```

**After refactoring:**

```python
GRADE_BOUNDARIES = [(70, "A"), (60, "B"), (50, "C"), (40, "D"), (0, "U")]

def load_marks(filename):
    """Loads marks from a text file, one mark per line."""
    try:
        with open(filename, "r") as file:
            lines = file.readlines()
        return [int(line.strip()) for line in lines]
    except FileNotFoundError:
        print(f"Error: {filename} not found.")
        return []

def filter_valid_marks(marks):
    """Returns only marks within the valid range of 0-100."""
    return [mark for mark in marks if 0 <= mark <= 100]

def calculate_average(marks):
    """Calculates the average of a list of marks."""
    if len(marks) == 0:
        return None
    return sum(marks) / len(marks)

def determine_grade(average):
    """Returns the grade for a given average mark."""
    for boundary, grade in GRADE_BOUNDARIES:
        if average >= boundary:
            return grade
    return "U"

def display_results(average, grade):
    """Displays the average and grade to the user."""
    print(f"Average: {average:.1f}")
    print(f"Grade: {grade}")

def main():
    all_marks = load_marks("marks.txt")
    valid_marks = filter_valid_marks(all_marks)

    average = calculate_average(valid_marks)
    if average is not None:
        grade = determine_grade(average)
        display_results(average, grade)
    else:
        print("No valid marks found.")

main()
```

```vb
' BEFORE refactoring
Sub Main()
    Dim lines() As String = System.IO.File.ReadAllLines("marks.txt")
    Dim t As Integer = 0
    Dim c As Integer = 0
    For Each l As String In lines
        Dim m As Integer = CInt(l.Trim())
        If m >= 0 And m <= 100 Then
            t = t + m
            c = c + 1
        End If
    Next
    If c > 0 Then
        Dim a As Double = t / c
        Console.WriteLine("Average: " & a)
    End If
End Sub

' AFTER refactoring
Module MarksProcessor
    Function LoadMarks(filename As String) As List(Of Integer)
        Dim marks As New List(Of Integer)
        Try
            Dim lines() As String = System.IO.File.ReadAllLines(filename)
            For Each line As String In lines
                marks.Add(CInt(line.Trim()))
            Next
        Catch ex As System.IO.FileNotFoundException
            Console.WriteLine("Error: " & filename & " not found.")
        End Try
        Return marks
    End Function

    Function FilterValidMarks(marks As List(Of Integer)) As List(Of Integer)
        Dim validMarks As New List(Of Integer)
        For Each mark As Integer In marks
            If mark >= 0 And mark <= 100 Then
                validMarks.Add(mark)
            End If
        Next
        Return validMarks
    End Function

    Function CalculateAverage(marks As List(Of Integer)) As Double
        If marks.Count = 0 Then Return -1
        Dim total As Integer = 0
        For Each mark As Integer In marks
            total += mark
        Next
        Return total / marks.Count
    End Function

    Function DetermineGrade(average As Double) As String
        If average >= 70 Then Return "A"
        If average >= 60 Then Return "B"
        If average >= 50 Then Return "C"
        If average >= 40 Then Return "D"
        Return "U"
    End Function

    Sub Main()
        Dim allMarks As List(Of Integer) = LoadMarks("marks.txt")
        Dim validMarks As List(Of Integer) = FilterValidMarks(allMarks)
        Dim average As Double = CalculateAverage(validMarks)

        If average >= 0 Then
            Console.WriteLine("Average: " & average.ToString("F1"))
            Console.WriteLine("Grade: " & DetermineGrade(average))
        Else
            Console.WriteLine("No valid marks found.")
        End If
    End Sub
End Module
```

### What Improved?

| Aspect | Before | After |
|---|---|---|
| Variable names | `t`, `c`, `a`, `m`, `l` | `total`, `valid_marks`, `average`, `grade` |
| Structure | One monolithic block | Separate subroutines with clear purposes |
| Error handling | None | FileNotFoundError caught |
| Reusability | None | Each function can be reused or tested independently |
| Readability | Requires careful reading | Purpose is clear at a glance |

---

## The DRY Principle

<div class="key-term" markdown="1">
**DRY (Don't Repeat Yourself)** -- A principle of software development that states every piece of knowledge or logic should have a single, unambiguous representation in the code. If you find yourself copying and pasting code, you should probably extract it into a subroutine.
</div>

### Identifying DRY Violations

```python
# VIOLATION OF DRY: same logic repeated three times
print("=== Report for Class A ===")
total_a = 0
for mark in class_a_marks:
    total_a += mark
avg_a = total_a / len(class_a_marks)
print(f"Average: {avg_a:.1f}")

print("=== Report for Class B ===")
total_b = 0
for mark in class_b_marks:
    total_b += mark
avg_b = total_b / len(class_b_marks)
print(f"Average: {avg_b:.1f}")

print("=== Report for Class C ===")
total_c = 0
for mark in class_c_marks:
    total_c += mark
avg_c = total_c / len(class_c_marks)
print(f"Average: {avg_c:.1f}")
```

```python
# FOLLOWING DRY: extracted into a reusable function
def print_class_report(class_name, marks):
    print(f"=== Report for {class_name} ===")
    average = sum(marks) / len(marks)
    print(f"Average: {average:.1f}")

print_class_report("Class A", class_a_marks)
print_class_report("Class B", class_b_marks)
print_class_report("Class C", class_c_marks)
```

```vb
' FOLLOWING DRY: extracted into a reusable subroutine
Sub PrintClassReport(className As String, marks() As Integer)
    Console.WriteLine("=== Report for " & className & " ===")
    Dim total As Integer = 0
    For Each mark As Integer In marks
        total += mark
    Next
    Dim average As Double = total / marks.Length
    Console.WriteLine("Average: " & average.ToString("F1"))
End Sub

PrintClassReport("Class A", classAMarks)
PrintClassReport("Class B", classBMarks)
PrintClassReport("Class C", classCMarks)
```

### Benefits of DRY

- **Easier maintenance:** Fix a bug in one place, not in every copy
- **Less code:** Fewer lines means fewer places for bugs to hide
- **Consistency:** The same logic is guaranteed to work the same way everywhere
- **Readability:** Subroutine names describe what the code does

<div class="exam-tip" markdown="1">
If you notice the same block of code appearing more than once in your program, it is almost always a sign that you should extract it into a subroutine. This is one of the simplest ways to improve your coursework grade for code quality.
</div>

---

## Readability vs Cleverness

At AS level, **readability always wins over cleverness**. Code that is easy to understand is easier to debug, maintain, and mark.

### Examples

```python
# CLEVER but hard to read (Python one-liner)
grades = ["A" if m >= 70 else "B" if m >= 60 else "C" if m >= 50 else "D" if m >= 40 else "U" for m in marks]

# READABLE and clear
grades = []
for mark in marks:
    if mark >= 70:
        grades.append("A")
    elif mark >= 60:
        grades.append("B")
    elif mark >= 50:
        grades.append("C")
    elif mark >= 40:
        grades.append("D")
    else:
        grades.append("U")
```

```python
# CLEVER: using boolean arithmetic
has_passed = not not (mark - 50 + abs(mark - 50))

# READABLE: clear intent
has_passed = mark >= 50
```

```vb
' READABLE: clear intent
Dim hasPassed As Boolean = (mark >= 50)
```

### Guidelines for Readable Code

| Guideline | Explanation |
|---|---|
| Use clear variable names | `student_count` not `sc` |
| One statement per line | Do not chain multiple operations on one line |
| Keep subroutines short | If a subroutine is longer than 20-30 lines, consider splitting it |
| Avoid deeply nested code | More than 3 levels of nesting makes code hard to follow |
| Use early returns | Return from a function early when a condition is met, rather than nesting |

### Reducing Nesting with Early Returns

```python
# DEEPLY NESTED (hard to read)
def process_order(order):
    if order is not None:
        if order["quantity"] > 0:
            if order["item"] in stock:
                if stock[order["item"]] >= order["quantity"]:
                    # Process the order
                    stock[order["item"]] -= order["quantity"]
                    return "Order processed"
                else:
                    return "Insufficient stock"
            else:
                return "Item not found"
        else:
            return "Invalid quantity"
    else:
        return "No order provided"

# FLAT with early returns (easy to read)
def process_order(order):
    if order is None:
        return "No order provided"
    if order["quantity"] <= 0:
        return "Invalid quantity"
    if order["item"] not in stock:
        return "Item not found"
    if stock[order["item"]] < order["quantity"]:
        return "Insufficient stock"

    stock[order["item"]] -= order["quantity"]
    return "Order processed"
```

```vb
' FLAT with early returns (easy to read)
Function ProcessOrder(order As Order) As String
    If order Is Nothing Then
        Return "No order provided"
    End If
    If order.Quantity <= 0 Then
        Return "Invalid quantity"
    End If
    If Not stock.ContainsKey(order.Item) Then
        Return "Item not found"
    End If
    If stock(order.Item) < order.Quantity Then
        Return "Insufficient stock"
    End If

    stock(order.Item) -= order.Quantity
    Return "Order processed"
End Function
```

---

## Testing Your Own Code

Testing is the process of running your program with various inputs to check it produces the correct outputs and handles errors appropriately.

<div class="key-term" markdown="1">
**Test plan** -- A structured document that lists what will be tested, the test data to be used, the expected outcomes, and the actual outcomes.
</div>

### Types of Test Data

| Type | Description | Example (for age 0-120) |
|---|---|---|
| **Normal** | Typical, valid data within the expected range | 25, 45, 67 |
| **Boundary** | Values at the edges of acceptable ranges | 0, 1, 119, 120 |
| **Erroneous** | Invalid data that should be rejected | -1, 121, "abc", "" |

<div class="exam-tip" markdown="1">
Always include **all three types** of test data in your test plan. Boundary data is particularly important -- test the exact boundary values (e.g. 0 and 120) as well as values just inside and just outside the boundary (e.g. -1, 0, 1 and 119, 120, 121).
</div>

### Example Test Plan

**Function being tested:** `get_validated_age()` -- accepts an integer between 0 and 120.

| Test | Type | Input | Expected Outcome | Actual Outcome | Pass/Fail |
|---|---|---|---|---|---|
| 1 | Normal | 25 | Accepted | Accepted | Pass |
| 2 | Normal | 67 | Accepted | Accepted | Pass |
| 3 | Boundary | 0 | Accepted (minimum valid) | Accepted | Pass |
| 4 | Boundary | 120 | Accepted (maximum valid) | Accepted | Pass |
| 5 | Boundary | -1 | Rejected with error message | Rejected | Pass |
| 6 | Boundary | 121 | Rejected with error message | Rejected | Pass |
| 7 | Erroneous | "abc" | Rejected with error message | Rejected | Pass |
| 8 | Erroneous | "" (empty) | Rejected with error message | Rejected | Pass |
| 9 | Erroneous | 25.5 | Rejected with error message | Rejected | Pass |

### Writing Testable Code

Code that is structured into small, focused subroutines is much easier to test.

```python
# This function is easy to test because it takes input and returns output
def calculate_discount(price, discount_percentage):
    if price < 0:
        return -1  # Error indicator
    if discount_percentage < 0 or discount_percentage > 100:
        return -1
    discount_amount = price * (discount_percentage / 100)
    return price - discount_amount

# Testing the function
def test_calculate_discount():
    # Normal tests
    assert calculate_discount(100, 10) == 90.0, "Test 1 failed"
    assert calculate_discount(50, 20) == 40.0, "Test 2 failed"

    # Boundary tests
    assert calculate_discount(100, 0) == 100.0, "Test 3 failed"
    assert calculate_discount(100, 100) == 0.0, "Test 4 failed"

    # Erroneous tests
    assert calculate_discount(-10, 10) == -1, "Test 5 failed"
    assert calculate_discount(100, -5) == -1, "Test 6 failed"
    assert calculate_discount(100, 150) == -1, "Test 7 failed"

    print("All tests passed!")

test_calculate_discount()
```

```vb
' This function is easy to test because it takes input and returns output
Function CalculateDiscount(price As Double, discountPercentage As Double) As Double
    If price < 0 Then Return -1
    If discountPercentage < 0 Or discountPercentage > 100 Then Return -1
    Dim discountAmount As Double = price * (discountPercentage / 100)
    Return price - discountAmount
End Function

' Testing the function
Sub TestCalculateDiscount()
    ' Normal tests
    Console.WriteLine("Test 1: " & If(CalculateDiscount(100, 10) = 90.0, "PASS", "FAIL"))
    Console.WriteLine("Test 2: " & If(CalculateDiscount(50, 20) = 40.0, "PASS", "FAIL"))

    ' Boundary tests
    Console.WriteLine("Test 3: " & If(CalculateDiscount(100, 0) = 100.0, "PASS", "FAIL"))
    Console.WriteLine("Test 4: " & If(CalculateDiscount(100, 100) = 0.0, "PASS", "FAIL"))

    ' Erroneous tests
    Console.WriteLine("Test 5: " & If(CalculateDiscount(-10, 10) = -1, "PASS", "FAIL"))
    Console.WriteLine("Test 6: " & If(CalculateDiscount(100, -5) = -1, "PASS", "FAIL"))
    Console.WriteLine("Test 7: " & If(CalculateDiscount(100, 150) = -1, "PASS", "FAIL"))
End Sub
```

### Testing File Operations

When testing file operations, consider these additional scenarios:

| Test | Purpose |
|---|---|
| File exists with valid data | Normal operation |
| File does not exist | Error handling works correctly |
| File is empty | Program handles gracefully |
| File has malformed data | Program does not crash |
| Write to read-only location | Error handling for permissions |

```python
def test_file_operations():
    # Test writing
    test_data = ["Alice,17,A", "Bob,16,B"]
    save_to_csv("test_output.csv", test_data)

    # Test reading back
    loaded_data = load_from_csv("test_output.csv")
    assert len(loaded_data) == 2, "Should load 2 records"
    assert loaded_data[0] == "Alice,17,A", "First record should match"

    # Test missing file
    result = load_from_csv("nonexistent.csv")
    assert result == [], "Missing file should return empty list"

    # Clean up test file
    import os
    os.remove("test_output.csv")

    print("All file tests passed!")
```

```vb
Sub TestFileOperations()
    ' Test writing
    Dim testData As New List(Of String)
    testData.Add("Alice,17,A")
    testData.Add("Bob,16,B")

    System.IO.File.WriteAllLines("test_output.csv", testData)

    ' Test reading back
    Dim loadedData() As String = System.IO.File.ReadAllLines("test_output.csv")
    Console.WriteLine("Read test: " & If(loadedData.Length = 2, "PASS", "FAIL"))

    ' Clean up
    System.IO.File.Delete("test_output.csv")

    Console.WriteLine("File tests complete.")
End Sub
```

<div class="exam-tip" markdown="1">
In your coursework, you must include evidence of testing. Create a test plan **before** you test, fill in the "Actual Outcome" column as you test, and include screenshots as evidence. If a test fails, document what you did to fix the problem -- this shows the examiner your debugging process.
</div>

---

## Summary

| Quality Aspect | Key Practice |
|---|---|
| Self-documenting identifiers | Use descriptive names; follow naming conventions |
| Comments | Explain the why, not the what; document subroutine purposes |
| Program layout | Consistent indentation; blank lines between sections; logical grouping |
| Efficient constructs | Choose the right loop; avoid repetition; use appropriate data structures |
| Refactoring | Restructure code for clarity without changing behaviour |
| DRY principle | Extract repeated logic into reusable subroutines |
| Readability | Prioritise clarity over cleverness; reduce nesting |
| Testing | Use normal, boundary, and erroneous test data; create a test plan |
