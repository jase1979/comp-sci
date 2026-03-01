---
layout: topic
title: "Algorithms & Programming Constructs"
level: "GCSE"
level_url: "/gcse/"
unit_name: "Unit 2: Computational Thinking & Programming"
unit_url: "/gcse/unit2/"
prev_topic: "/gcse/unit2/problem-solving/"
next_topic: "/gcse/unit2/programming-languages/"
---

An **algorithm** is a step-by-step set of instructions used to solve a problem or complete a task. In this topic you will learn how to represent algorithms, use the three main programming constructs, handle data with variables and operators, and analyse searching and sorting techniques.

---

## Algorithms: Pseudo-code and flowcharts

Algorithms can be represented in two main ways before you write actual code: **pseudo-code** and **flowcharts**.

<div class="key-term" markdown="1">
**Pseudo-code** is a structured way of writing an algorithm using short English statements. It is not a real programming language, so there is no single correct syntax, but it should be clear and unambiguous.
</div>

<div class="key-term" markdown="1">
**Flowchart** is a diagram that uses standard shapes to represent the steps in an algorithm. Each shape has a specific meaning.
</div>

### Common flowchart symbols

| Shape | Name | Purpose |
|-------|------|---------|
| Rounded rectangle | Terminal | Start or end of the algorithm |
| Parallelogram | Input / Output | Reading data in or displaying data out |
| Rectangle | Process | A calculation or assignment |
| Diamond | Decision | A yes/no or true/false question |
| Arrow | Flow line | Shows the order of steps |

### Pseudo-code example

```
OUTPUT "Enter your name"
INPUT name
IF name = "Admin" THEN
    OUTPUT "Welcome, administrator"
ELSE
    OUTPUT "Hello, " + name
ENDIF
```

### Flowchart tips

- Always include a **Start** and **Stop** terminal.
- A decision diamond must have exactly **two** branches (Yes / No).
- Arrows should flow in a clear direction -- normally top to bottom and left to right.

<div class="exam-tip" markdown="1">
In your exam you may be asked to write pseudo-code or complete a flowchart. Make sure you practise converting between the two representations -- they describe the same logic in different forms.
</div>

---

## Sub routines in algorithms and programs

A **sub routine** (also called a subroutine) is a named block of code that performs a specific task. Sub routines help you break large problems into smaller, manageable parts. There are two types:

| Type | Description | Returns a value? |
|------|-------------|-----------------|
| **Procedure** | Carries out a task | No |
| **Function** | Carries out a task and returns a value | Yes |

### Why use sub routines?

- **Reusability** -- write the code once, call it many times.
- **Readability** -- the main program is shorter and easier to follow.
- **Testing** -- each sub routine can be tested on its own.
- **Maintenance** -- fixing a bug in one place fixes it everywhere the sub routine is used.

### Examples

```python
# Function -- returns a value
def calculate_area(length, width):
    area = length * width
    return area

# Procedure -- does not return a value
def display_result(area):
    print("The area is", area)

# Main program
a = calculate_area(5, 3)
display_result(a)
```

```vb
' Function -- returns a value
Function CalculateArea(length As Integer, width As Integer) As Integer
    Dim area As Integer = length * width
    Return area
End Function

' Procedure -- does not return a value
Sub DisplayResult(area As Integer)
    Console.WriteLine("The area is " & area)
End Sub

' Main program
Dim a As Integer = CalculateArea(5, 3)
DisplayResult(a)
```

<div class="exam-tip" markdown="1">
Remember that a **function** always returns a value using a `return` statement, while a **procedure** simply performs an action. If the exam asks for the difference, focus on whether a value is sent back to the calling code.
</div>

---

## Sequence, selection and iteration

These are the **three basic programming constructs**. Every algorithm can be built from these three building blocks.

<div class="key-term" markdown="1">
**Sequence** -- instructions are carried out one after another, in the order they are written.
</div>

<div class="key-term" markdown="1">
**Selection** -- a decision is made and the program follows one path or another depending on a condition. Common selection statements are `IF...ELSE` and `CASE` / `SELECT`.
</div>

<div class="key-term" markdown="1">
**Iteration** -- a section of code is repeated. This can be a fixed number of times (count-controlled) or until a condition is met (condition-controlled).
</div>

### Sequence

```python
name = input("Enter your name: ")
print("Hello, " + name)
print("Welcome to the system")
```

```vb
Dim name As String = Console.ReadLine()
Console.WriteLine("Hello, " & name)
Console.WriteLine("Welcome to the system")
```

### Selection (IF...ELSE)

```python
age = int(input("Enter your age: "))
if age >= 18:
    print("You are an adult")
else:
    print("You are a minor")
```

```vb
Dim age As Integer = CInt(Console.ReadLine())
If age >= 18 Then
    Console.WriteLine("You are an adult")
Else
    Console.WriteLine("You are a minor")
End If
```

### Iteration -- FOR loop (count-controlled)

```python
for i in range(1, 6):
    print(i)
```

```vb
For i As Integer = 1 To 5
    Console.WriteLine(i)
Next
```

### Iteration -- WHILE loop (condition-controlled)

```python
password = ""
while password != "secret":
    password = input("Enter password: ")
print("Access granted")
```

```vb
Dim password As String = ""
While password <> "secret"
    password = Console.ReadLine()
End While
Console.WriteLine("Access granted")
```

---

## Counts and rogue values

When reading data from a user or a file, you often need to know how many items have been entered or when to stop reading. Two important concepts help with this: **counts** and **rogue values**.

<div class="key-term" markdown="1">
**Count** -- a variable used to keep track of how many times something has happened, such as how many numbers have been entered.
</div>

<div class="key-term" markdown="1">
**Rogue value** (also called a sentinel value) -- a special value that signals the end of data entry. It is not part of the actual data. For example, entering `-1` to indicate there are no more marks to add.
</div>

### Example: using a count and a rogue value

```python
total = 0
count = 0
mark = int(input("Enter a mark (-1 to stop): "))

while mark != -1:
    total = total + mark
    count = count + 1
    mark = int(input("Enter a mark (-1 to stop): "))

if count > 0:
    average = total / count
    print("Average mark:", average)
else:
    print("No marks entered")
```

```vb
Dim total As Integer = 0
Dim count As Integer = 0
Dim mark As Integer = CInt(Console.ReadLine())

While mark <> -1
    total = total + mark
    count = count + 1
    mark = CInt(Console.ReadLine())
End While

If count > 0 Then
    Dim average As Double = total / count
    Console.WriteLine("Average mark: " & average)
Else
    Console.WriteLine("No marks entered")
End If
```

<div class="exam-tip" markdown="1">
A common mistake is to include the rogue value in the total or the count. Always check the condition **before** processing the value.
</div>

---

## Constructs in object oriented programs

Object oriented programming (OOP) organises code around **objects** rather than actions. At GCSE level you need to understand the key ideas behind OOP.

<div class="key-term" markdown="1">
**Class** -- a blueprint or template that defines the attributes (data) and methods (actions) that an object will have.
</div>

<div class="key-term" markdown="1">
**Object** -- an instance of a class. You can create many objects from one class.
</div>

<div class="key-term" markdown="1">
**Attribute** -- a variable that belongs to an object, describing its properties (for example, `name`, `age`).
</div>

<div class="key-term" markdown="1">
**Method** -- a sub routine that belongs to a class. It defines the behaviour of the object.
</div>

### Key OOP concepts

| Concept | Meaning |
|---------|---------|
| **Encapsulation** | Bundling data and methods together inside a class, hiding internal details from outside code |
| **Inheritance** | A new class (child) can inherit attributes and methods from an existing class (parent) |
| **Polymorphism** | Different classes can have methods with the same name that behave differently |

### Example: a simple class

```python
class Dog:
    def __init__(self, name, breed):
        self.name = name
        self.breed = breed

    def bark(self):
        print(self.name + " says Woof!")

my_dog = Dog("Rex", "Labrador")
my_dog.bark()
```

```vb
Class Dog
    Public name As String
    Public breed As String

    Sub New(n As String, b As String)
        name = n
        breed = b
    End Sub

    Sub Bark()
        Console.WriteLine(name & " says Woof!")
    End Sub
End Class

' Creating an object
Dim myDog As New Dog("Rex", "Labrador")
myDog.Bark()
```

<div class="exam-tip" markdown="1">
You do not need to write full OOP programs in your exam, but you should be able to read and understand class diagrams, identify classes, objects, attributes, and methods, and explain how inheritance works.
</div>

---

## Follow and alter algorithms using sequence, selection, iteration

You will often be asked to **trace through** (follow) an algorithm or **modify** (alter) an existing one. This means reading the code line by line and tracking what happens to each variable.

### How to trace an algorithm

1. Create a **trace table** with a column for each variable and one for any output.
2. Work through the algorithm line by line.
3. Update the table each time a variable changes or output is produced.

### Example: trace this algorithm

```python
x = 3
y = 5
for i in range(1, 4):
    x = x + y
    y = y - 1
print(x, y)
```

```vb
Dim x As Integer = 3
Dim y As Integer = 5
For i As Integer = 1 To 3
    x = x + y
    y = y - 1
Next
Console.WriteLine(x & " " & y)
```

### Trace table

| i | x | y | Output |
|---|---|---|--------|
| -- | 3 | 5 | |
| 1 | 8 | 4 | |
| 2 | 12 | 3 | |
| 3 | 15 | 2 | |
| -- | -- | -- | 15 2 |

### Altering an algorithm

When asked to alter an algorithm, common tasks include:

- Changing a condition in a selection statement.
- Adjusting the range or condition of a loop.
- Adding an extra variable or output.

Always re-trace the algorithm after making changes to check your answer.

---

## Follow and alter algorithms using input, processing, output

Every algorithm follows the **input -- process -- output** (IPO) model:

| Stage | What happens | Example |
|-------|-------------|---------|
| **Input** | Data is received from the user or a file | `number = int(input())` |
| **Processing** | Calculations or decisions are made | `result = number * 2` |
| **Output** | Results are displayed or stored | `print(result)` |

### Example

```python
# Input
length = float(input("Enter length: "))
width = float(input("Enter width: "))

# Processing
area = length * width
perimeter = 2 * (length + width)

# Output
print("Area:", area)
print("Perimeter:", perimeter)
```

```vb
' Input
Dim length As Double = CDbl(Console.ReadLine())
Dim width As Double = CDbl(Console.ReadLine())

' Processing
Dim area As Double = length * width
Dim perimeter As Double = 2 * (length + width)

' Output
Console.WriteLine("Area: " & area)
Console.WriteLine("Perimeter: " & perimeter)
```

When following this type of algorithm in an exam, clearly identify which lines handle input, which perform processing, and which produce output. When altering the algorithm, you might be asked to add validation on the input, change the processing formula, or format the output differently.

---

## Write algorithms solving problems with sequence, selection, iteration

Exam questions will ask you to **write your own** algorithm from a problem description. Follow these steps:

1. **Identify inputs** -- what data does the user provide?
2. **Identify processing** -- what calculations or decisions are needed?
3. **Identify outputs** -- what should the algorithm display?
4. **Choose constructs** -- decide where you need sequence, selection, or iteration.
5. **Write the algorithm** in pseudo-code or a programming language.

### Worked example

**Problem:** Ask the user to enter 10 test scores. Display the highest score and whether it is a pass (50 or above) or fail.

```python
highest = 0
for i in range(10):
    score = int(input("Enter score: "))
    if score > highest:
        highest = score

print("Highest score:", highest)
if highest >= 50:
    print("Pass")
else:
    print("Fail")
```

```vb
Dim highest As Integer = 0
For i As Integer = 1 To 10
    Dim score As Integer = CInt(Console.ReadLine())
    If score > highest Then
        highest = score
    End If
Next

Console.WriteLine("Highest score: " & highest)
If highest >= 50 Then
    Console.WriteLine("Pass")
Else
    Console.WriteLine("Fail")
End If
```

<div class="exam-tip" markdown="1">
When writing algorithms in an exam, always consider **edge cases**. What happens if all scores are zero? What if the user enters invalid data? Even if you are not asked to handle them, mentioning edge cases can earn extra marks.
</div>

---

## Local and global variables

<div class="key-term" markdown="1">
**Local variable** -- a variable declared inside a sub routine. It can only be used within that sub routine and is destroyed when the sub routine ends.
</div>

<div class="key-term" markdown="1">
**Global variable** -- a variable declared outside all sub routines, usually at the top of the program. It can be accessed from anywhere in the program.
</div>

| Feature | Local variable | Global variable |
|---------|---------------|----------------|
| **Scope** | Only inside the sub routine where it is declared | Everywhere in the program |
| **Lifetime** | Created when the sub routine runs, destroyed when it ends | Exists for the whole program |
| **Risk** | Low -- cannot be accidentally changed elsewhere | Higher -- any part of the program can change it |
| **Best practice** | Preferred in most situations | Use sparingly |

### Example

```python
total = 0  # global variable

def add_to_total(value):
    global total
    result = value * 2  # local variable
    total = total + result

add_to_total(5)
print(total)  # Output: 10
```

```vb
Dim total As Integer = 0  ' global variable

Sub AddToTotal(value As Integer)
    Dim result As Integer = value * 2  ' local variable
    total = total + result
End Sub

AddToTotal(5)
Console.WriteLine(total)  ' Output: 10
```

<div class="exam-tip" markdown="1">
Using **local variables** is generally better practice because it reduces the chance of unexpected side effects. Only use global variables when data genuinely needs to be shared across multiple sub routines.
</div>

---

## Self-documenting identifiers and annotation

Good code should be easy to read and understand. Two techniques help with this: **meaningful identifiers** and **annotation** (comments).

<div class="key-term" markdown="1">
**Self-documenting identifier** -- a variable, function, or sub routine name that clearly describes its purpose. For example, `totalScore` is better than `ts`.
</div>

<div class="key-term" markdown="1">
**Annotation** -- comments added to the code to explain what it does. Comments are ignored by the computer when the program runs.
</div>

### Bad vs good identifiers

| Bad | Good | Why? |
|-----|------|------|
| `x` | `numberOfStudents` | Describes what the variable holds |
| `fn` | `calculateAverage` | Describes what the function does |
| `t` | `totalMarks` | Clear and unambiguous |

### Adding comments

```python
# Calculate the average of all marks entered
total_marks = 0  # running total of marks
num_students = 5  # fixed number of students

for i in range(num_students):
    mark = int(input("Enter mark: "))  # get mark from user
    total_marks = total_marks + mark

average = total_marks / num_students
print("Average:", average)
```

```vb
' Calculate the average of all marks entered
Dim totalMarks As Integer = 0  ' running total of marks
Dim numStudents As Integer = 5  ' fixed number of students

For i As Integer = 1 To numStudents
    Dim mark As Integer = CInt(Console.ReadLine())  ' get mark from user
    totalMarks = totalMarks + mark
Next

Dim average As Double = totalMarks / numStudents
Console.WriteLine("Average: " & average)
```

<div class="exam-tip" markdown="1">
Using self-documenting identifiers makes your code easier to read and maintain. In the exam, if you name your variables well you may need fewer comments -- but always add a brief comment at the start of each sub routine explaining its purpose.
</div>

---

## String handling routines

Strings are sequences of characters. Programming languages provide built-in routines for working with strings.

### Common string operations

| Operation | Python | VB.NET |
|-----------|--------|--------|
| Length | `len(s)` | `s.Length` |
| Upper case | `s.upper()` | `s.ToUpper()` |
| Lower case | `s.lower()` | `s.ToLower()` |
| Extract substring | `s[1:4]` | `s.Substring(1, 3)` |
| Find character | `s.find("a")` | `s.IndexOf("a")` |
| Concatenation | `s1 + s2` | `s1 & s2` |
| Access a character | `s[0]` | `s(0)` |

### Examples

```python
name = "Computer Science"

# Length
print(len(name))  # 16

# Upper and lower case
print(name.upper())  # COMPUTER SCIENCE
print(name.lower())  # computer science

# Substring (characters at index 0 to 7)
print(name[0:8])  # Computer

# Find a character
print(name.find("S"))  # 9

# Concatenation
greeting = "Hello, " + name
print(greeting)  # Hello, Computer Science

# Loop through each character
for char in name:
    print(char, end=" ")
```

```vb
Dim name As String = "Computer Science"

' Length
Console.WriteLine(name.Length)  ' 16

' Upper and lower case
Console.WriteLine(name.ToUpper())  ' COMPUTER SCIENCE
Console.WriteLine(name.ToLower())  ' computer science

' Substring (3 characters starting at index 0)
Console.WriteLine(name.Substring(0, 8))  ' Computer

' Find a character
Console.WriteLine(name.IndexOf("S"))  ' 9

' Concatenation
Dim greeting As String = "Hello, " & name
Console.WriteLine(greeting)  ' Hello, Computer Science

' Loop through each character
For i As Integer = 0 To name.Length - 1
    Console.Write(name(i) & " ")
Next
```

<div class="exam-tip" markdown="1">
Remember that string indexing starts at **0** in both Python and VB.NET. The first character of `"Hello"` is at index 0, not 1. Watch out for **off-by-one errors** when extracting substrings.
</div>

---

## Mathematical operations in algorithms

Algorithms frequently use mathematical operations. You need to know the standard arithmetic operators and two special ones: **integer division** and **modulus**.

### Arithmetic operators

| Operation | Symbol (Python) | Symbol (VB.NET) | Example | Result |
|-----------|----------------|-----------------|---------|--------|
| Addition | `+` | `+` | `7 + 3` | `10` |
| Subtraction | `-` | `-` | `7 - 3` | `4` |
| Multiplication | `*` | `*` | `7 * 3` | `21` |
| Division | `/` | `/` | `7 / 2` | `3.5` |
| Integer division | `//` | `\` | `7 // 2` | `3` |
| Modulus (remainder) | `%` | `Mod` | `7 % 2` | `1` |
| Exponent (power) | `**` | `^` | `2 ** 3` | `8` |

### Practical uses of integer division and modulus

```python
# Modulus: check if a number is even or odd
number = 15
if number % 2 == 0:
    print("Even")
else:
    print("Odd")

# Integer division: convert seconds to minutes and seconds
total_seconds = 200
minutes = total_seconds // 60
seconds = total_seconds % 60
print(minutes, "minutes and", seconds, "seconds")  # 3 minutes and 20 seconds
```

```vb
' Modulus: check if a number is even or odd
Dim number As Integer = 15
If number Mod 2 = 0 Then
    Console.WriteLine("Even")
Else
    Console.WriteLine("Odd")
End If

' Integer division: convert seconds to minutes and seconds
Dim totalSeconds As Integer = 200
Dim minutes As Integer = totalSeconds \ 60
Dim seconds As Integer = totalSeconds Mod 60
Console.WriteLine(minutes & " minutes and " & seconds & " seconds")
```

<div class="exam-tip" markdown="1">
The **modulus** operator is very commonly tested. Typical uses include checking if a number is even/odd, extracting individual digits from a number, and working with time conversions. Make sure you are confident using both `%` (Python) and `Mod` (VB.NET).
</div>

---

## Logical operators: AND, OR, NOT, XOR in programs

Logical operators are used to combine or invert Boolean conditions in selection and iteration statements.

| Operator | Meaning | Result is True when... |
|----------|---------|----------------------|
| `AND` | Both conditions must be true | A is True **and** B is True |
| `OR` | At least one condition must be true | A is True **or** B is True (or both) |
| `NOT` | Inverts the condition | The condition is False |
| `XOR` | Exactly one condition must be true | A is True **or** B is True, but **not both** |

### Truth tables

**AND**

| A | B | A AND B |
|---|---|---------|
| True | True | True |
| True | False | False |
| False | True | False |
| False | False | False |

**OR**

| A | B | A OR B |
|---|---|--------|
| True | True | True |
| True | False | True |
| False | True | True |
| False | False | False |

**XOR**

| A | B | A XOR B |
|---|---|---------|
| True | True | False |
| True | False | True |
| False | True | True |
| False | False | False |

### Examples in code

```python
age = 20
has_ticket = True

# AND -- both must be true
if age >= 18 and has_ticket:
    print("Entry allowed")

# OR -- at least one must be true
if age < 12 or age > 65:
    print("Discount applies")

# NOT -- inverts the condition
logged_in = False
if not logged_in:
    print("Please log in")

# XOR -- Python uses the ^ operator for XOR on booleans
a = True
b = False
if a ^ b:
    print("Exactly one is true")
```

```vb
Dim age As Integer = 20
Dim hasTicket As Boolean = True

' AND -- both must be true
If age >= 18 And hasTicket Then
    Console.WriteLine("Entry allowed")
End If

' OR -- at least one must be true
If age < 12 Or age > 65 Then
    Console.WriteLine("Discount applies")
End If

' NOT -- inverts the condition
Dim loggedIn As Boolean = False
If Not loggedIn Then
    Console.WriteLine("Please log in")
End If

' XOR -- exactly one must be true
Dim a As Boolean = True
Dim b As Boolean = False
If a Xor b Then
    Console.WriteLine("Exactly one is true")
End If
```

<div class="exam-tip" markdown="1">
**XOR** is the one students most often forget. Think of it as "one or the other, but not both". A handy way to remember: XOR returns True when the two inputs are **different**.
</div>

---

## Sorting: Merge sort and bubble sort characteristics

Sorting means arranging data into a specific order (usually ascending or descending). You need to know two algorithms: **bubble sort** and **merge sort**.

### Bubble sort

Bubble sort works by repeatedly comparing **adjacent** items and swapping them if they are in the wrong order. It keeps passing through the list until no swaps are needed.

**How it works:**
1. Start at the beginning of the list.
2. Compare each pair of adjacent items.
3. If they are in the wrong order, swap them.
4. Repeat until a full pass is made with no swaps.

```python
def bubble_sort(data):
    n = len(data)
    for i in range(n - 1):
        swapped = False
        for j in range(n - 1 - i):
            if data[j] > data[j + 1]:
                data[j], data[j + 1] = data[j + 1], data[j]
                swapped = True
        if not swapped:
            break
    return data

numbers = [5, 3, 8, 1, 2]
print(bubble_sort(numbers))  # [1, 2, 3, 5, 8]
```

```vb
Sub BubbleSort(data() As Integer)
    Dim n As Integer = data.Length
    For i As Integer = 0 To n - 2
        Dim swapped As Boolean = False
        For j As Integer = 0 To n - 2 - i
            If data(j) > data(j + 1) Then
                Dim temp As Integer = data(j)
                data(j) = data(j + 1)
                data(j + 1) = temp
                swapped = True
            End If
        Next
        If Not swapped Then Exit For
    Next
End Sub

Dim numbers() As Integer = {5, 3, 8, 1, 2}
BubbleSort(numbers)
' numbers is now {1, 2, 3, 5, 8}
```

### Merge sort

Merge sort uses a **divide and conquer** approach. It splits the list in half repeatedly until each sub-list has one item, then merges the sub-lists back together in order.

**How it works:**
1. Split the list into two halves.
2. Recursively sort each half.
3. Merge the two sorted halves into one sorted list.

```python
def merge_sort(data):
    if len(data) <= 1:
        return data
    mid = len(data) // 2
    left = merge_sort(data[:mid])
    right = merge_sort(data[mid:])
    return merge(left, right)

def merge(left, right):
    result = []
    i = 0
    j = 0
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
    result.extend(left[i:])
    result.extend(right[j:])
    return result

numbers = [5, 3, 8, 1, 2]
print(merge_sort(numbers))  # [1, 2, 3, 5, 8]
```

```vb
Function MergeSort(data() As Integer) As Integer()
    If data.Length <= 1 Then Return data
    Dim mid As Integer = data.Length \ 2
    Dim left() As Integer = MergeSort(data.Take(mid).ToArray())
    Dim right() As Integer = MergeSort(data.Skip(mid).ToArray())
    Return MergeLists(left, right)
End Function

Function MergeLists(left() As Integer, right() As Integer) As Integer()
    Dim result As New List(Of Integer)
    Dim i As Integer = 0
    Dim j As Integer = 0
    While i < left.Length And j < right.Length
        If left(i) <= right(j) Then
            result.Add(left(i))
            i += 1
        Else
            result.Add(right(j))
            j += 1
        End If
    End While
    While i < left.Length
        result.Add(left(i))
        i += 1
    End While
    While j < right.Length
        result.Add(right(j))
        j += 1
    End While
    Return result.ToArray()
End Function
```

### Comparison

| Feature | Bubble sort | Merge sort |
|---------|------------|------------|
| **How it works** | Compares adjacent items and swaps | Divides list, sorts halves, merges |
| **Best case** | O(n) -- already sorted | O(n log n) |
| **Worst case** | O(n^2) | O(n log n) |
| **Memory use** | Low -- sorts in place | Higher -- needs extra space for sub-lists |
| **Simple to code?** | Yes | More complex |
| **Good for large lists?** | No -- very slow | Yes -- consistently fast |

<div class="exam-tip" markdown="1">
You are unlikely to be asked to write a full merge sort from memory, but you must be able to describe how it works, trace through its steps, and compare it with bubble sort. Focus on the **efficiency** differences for different list sizes.
</div>

---

## Searching: Linear and binary search algorithms

Searching means finding a particular item in a list. You need to know two algorithms: **linear search** and **binary search**.

### Linear search

Linear search checks each item in the list **one by one** from start to finish until the target is found or the end of the list is reached.

- Works on **any** list (sorted or unsorted).
- Simple but slow for large lists.

```python
def linear_search(data, target):
    for i in range(len(data)):
        if data[i] == target:
            return i  # return the index where found
    return -1  # not found

names = ["Alice", "Bob", "Charlie", "Diana"]
result = linear_search(names, "Charlie")
print(result)  # 2
```

```vb
Function LinearSearch(data() As String, target As String) As Integer
    For i As Integer = 0 To data.Length - 1
        If data(i) = target Then
            Return i  ' return the index where found
        End If
    Next
    Return -1  ' not found
End Function

Dim names() As String = {"Alice", "Bob", "Charlie", "Diana"}
Dim result As Integer = LinearSearch(names, "Charlie")
Console.WriteLine(result)  ' 2
```

### Binary search

Binary search works by repeatedly dividing a **sorted** list in half. It compares the target with the middle item and eliminates half the list each time.

- The list **must be sorted** first.
- Much faster than linear search for large lists.

```python
def binary_search(data, target):
    low = 0
    high = len(data) - 1
    while low <= high:
        mid = (low + high) // 2
        if data[mid] == target:
            return mid
        elif data[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    return -1

numbers = [2, 5, 8, 12, 16, 23, 38, 45]
result = binary_search(numbers, 23)
print(result)  # 5
```

```vb
Function BinarySearch(data() As Integer, target As Integer) As Integer
    Dim low As Integer = 0
    Dim high As Integer = data.Length - 1
    While low <= high
        Dim mid As Integer = (low + high) \ 2
        If data(mid) = target Then
            Return mid
        ElseIf data(mid) < target Then
            low = mid + 1
        Else
            high = mid - 1
        End If
    End While
    Return -1
End Function

Dim numbers() As Integer = {2, 5, 8, 12, 16, 23, 38, 45}
Dim result As Integer = BinarySearch(numbers, 23)
Console.WriteLine(result)  ' 5
```

### Comparison

| Feature | Linear search | Binary search |
|---------|--------------|---------------|
| **List must be sorted?** | No | Yes |
| **Best case** | O(1) -- first item | O(1) -- middle item |
| **Worst case** | O(n) -- last item or not found | O(log n) |
| **How it works** | Checks each item in order | Halves the search area each step |
| **Good for large lists?** | Slow | Fast |

<div class="exam-tip" markdown="1">
Binary search is much faster than linear search, but it **only works on sorted data**. If the data is unsorted, you must either sort it first (which takes time) or use linear search. The exam may ask you to justify which search to use in a given scenario.
</div>

---

## Testing: Explain how algorithm/program works

Testing ensures that an algorithm or program works correctly. You should be able to **explain** what an algorithm does by tracing through it and describing each step.

### Types of test data

| Type | Description | Example for "enter a number between 1 and 100" |
|------|-------------|------------------------------------------------|
| **Normal** | Typical, valid data that the program should handle correctly | `50` |
| **Boundary** | Values at the very edge of what is accepted | `1`, `100` |
| **Erroneous** | Invalid data that should be rejected | `-5`, `hello`, `101` |

### Trace tables

A trace table is a powerful tool for explaining how an algorithm works. You fill it in step by step, recording the value of each variable after every instruction.

### Example: explain how this algorithm works

```python
total = 0
for i in range(1, 5):
    if i % 2 == 0:
        total = total + i
print(total)
```

```vb
Dim total As Integer = 0
For i As Integer = 1 To 4
    If i Mod 2 = 0 Then
        total = total + i
    End If
Next
Console.WriteLine(total)
```

**Trace table:**

| i | i % 2 == 0? | total |
|---|-------------|-------|
| 1 | No | 0 |
| 2 | Yes | 2 |
| 3 | No | 2 |
| 4 | Yes | 6 |

**Explanation:** The algorithm loops through the numbers 1 to 4. For each number, it checks whether it is even (divisible by 2). If it is, the number is added to the total. The final output is 6, which is the sum of the even numbers (2 + 4).

<div class="exam-tip" markdown="1">
When explaining how an algorithm works, do not just describe the code line by line. Instead, explain the **purpose** of the algorithm and what it achieves overall, then use a trace table to show how it gets there.
</div>

---

## Evaluate efficiency using logical reasoning and test data

Evaluating efficiency means judging how well an algorithm performs in terms of **time** (how long it takes) and **space** (how much memory it uses).

### How to evaluate efficiency

1. **Count the operations** -- how many comparisons, swaps, or calculations does the algorithm make for a given input size?
2. **Consider best, worst, and average cases** -- does the algorithm perform differently with different inputs?
3. **Use test data** -- run the algorithm with different data sets and observe how long it takes or how many steps it needs.
4. **Compare algorithms** -- if two algorithms solve the same problem, which one requires fewer steps?

### Example: comparing two approaches

**Problem:** Find the largest number in a list of `n` items.

**Approach 1:** Check every item (linear scan).

```python
def find_max(data):
    largest = data[0]
    for i in range(1, len(data)):
        if data[i] > largest:
            largest = data[i]
    return largest
```

```vb
Function FindMax(data() As Integer) As Integer
    Dim largest As Integer = data(0)
    For i As Integer = 1 To data.Length - 1
        If data(i) > largest Then
            largest = data(i)
        End If
    Next
    Return largest
End Function
```

This approach makes **n - 1** comparisons regardless of the data. It is already efficient because you must look at every item at least once to guarantee you have found the largest.

**Approach 2:** Sort the list first, then take the last item.

```python
def find_max_sort(data):
    data.sort()  # sorts the entire list
    return data[-1]
```

```vb
Function FindMaxSort(data() As Integer) As Integer
    Array.Sort(data)  ' sorts the entire list
    Return data(data.Length - 1)
End Function
```

This approach sorts the whole list just to find one value. Sorting takes many more operations (at best O(n log n)), making it far less efficient than Approach 1 for this task.

### Key efficiency points to remember

| Consideration | What to look for |
|---------------|-----------------|
| **Number of comparisons** | Fewer comparisons generally means a faster algorithm |
| **Number of passes** | How many times does the algorithm loop through the data? |
| **Memory usage** | Does the algorithm create extra lists or variables? |
| **Scalability** | How does the algorithm perform as the data set grows from 10 items to 10,000? |

<div class="exam-tip" markdown="1">
When evaluating efficiency in the exam, always relate your answer to specific test data. For example: "With a list of 100 items, a linear search could take up to 100 comparisons, but a binary search would take at most 7 comparisons (since log2(100) is approximately 7). This shows that binary search is much more efficient for large sorted data sets."
</div>
