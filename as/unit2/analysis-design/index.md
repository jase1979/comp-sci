---
layout: topic
title: "Analysis & Design Skills"
level: "AS"
level_url: "/as/"
unit_name: "Unit 2: Practical Programming to Solve Problems"
unit_url: "/as/unit2/"
next_topic: "/as/unit2/programming-skills/"
---

## Introduction

Before writing a single line of code, a programmer must analyse the problem and design a solution. This topic covers the key analysis and design techniques you need for the WJEC AS Unit 2 coursework and examination, including entity relationship diagrams, data structure tables, flowcharts, and system design considerations.

---

## Entity Relationship Diagrams (ERDs)

An Entity Relationship Diagram (ERD) is a visual representation of the data entities in a system and the relationships between them. At AS level you need to be able to create ERDs for given scenarios.

<div class="key-term" markdown="1">
**Entity** -- A thing or object in the real world that we want to store data about (e.g. Student, Course, Teacher). Entities are drawn as rectangles.
</div>

<div class="key-term" markdown="1">
**Relationship** -- A link or association between two entities (e.g. a Student *enrols on* a Course). Relationships are drawn as lines connecting entities, with a diamond or label on the line.
</div>

### Types of Relationship

| Relationship | Notation | Example |
|---|---|---|
| One-to-One (1:1) | 1 --- 1 | A headteacher *manages* one school |
| One-to-Many (1:M) | 1 --- M | A teacher *teaches* many students |
| Many-to-Many (M:M) | M --- M | Students *enrol on* many courses; courses have many students |

### Drawing an ERD -- Worked Example

**Scenario:** A school library system. Members borrow books. Each book has one author. A member can borrow many books, but each copy of a book is only loaned to one member at a time. An author can write many books.

**Step 1 -- Identify entities:** Member, Book, Author, Loan

**Step 2 -- Identify relationships:**
- A Member *takes out* many Loans (1:M)
- A Loan *is for* one Book (M:1)
- An Author *writes* many Books (1:M)

**Step 3 -- Draw the diagram:**

```
Author  1----M  Book  1----M  Loan  M----1  Member
```

In a more formal notation:

```
[Author] ---1:M--- [Book] ---1:M--- [Loan] ---M:1--- [Member]
```

<div class="exam-tip" markdown="1">
When a scenario has a many-to-many relationship, you should resolve it by introducing a **link entity** (sometimes called a junction table). For example, if Students enrol on Courses (M:M), introduce an Enrolment entity so you get: Student 1:M Enrolment M:1 Course.
</div>

### Practice Scenario

**A veterinary surgery tracks pets and their owners. Each pet belongs to one owner. An owner can have many pets. Vets carry out appointments. Each appointment is for one pet and is handled by one vet. A vet handles many appointments.**

Entities: Owner, Pet, Appointment, Vet

Relationships:
- Owner 1:M Pet
- Pet 1:M Appointment
- Vet 1:M Appointment

---

## Data Structure Tables

A data structure table defines the fields (columns) that each entity requires, along with data types, sizes, and validation rules. This is an essential part of the design phase.

### Example -- Member Entity

| Field Name | Data Type | Size | Validation | Example |
|---|---|---|---|---|
| MemberID | Integer | -- | Auto-generated, unique, primary key | 1042 |
| FirstName | String | 30 | Presence check, max length 30 | "Megan" |
| Surname | String | 40 | Presence check, max length 40 | "Jones" |
| DateOfBirth | Date | -- | Format check (DD/MM/YYYY), range check (reasonable date) | 15/03/2008 |
| Email | String | 100 | Format check (must contain @ and .), presence check | "megan@example.com" |
| MembershipType | String | 10 | Lookup check (must be "Adult", "Child", or "Senior") | "Child" |

### Example -- Book Entity

| Field Name | Data Type | Size | Validation | Example |
|---|---|---|---|---|
| BookID | Integer | -- | Primary key, unique | 5671 |
| Title | String | 100 | Presence check | "Great Expectations" |
| AuthorID | Integer | -- | Foreign key referencing Author, existence check | 23 |
| ISBN | String | 13 | Length check (exactly 13 digits), format check | "9780141439563" |
| Available | Boolean | -- | Must be True or False | True |

<div class="key-term" markdown="1">
**Primary Key** -- A field (or combination of fields) that uniquely identifies each record in an entity. For example, MemberID.
</div>

<div class="key-term" markdown="1">
**Foreign Key** -- A field in one entity that references the primary key of another entity, establishing a link between them. For example, AuthorID in the Book table references AuthorID in the Author table.
</div>

<div class="exam-tip" markdown="1">
Always include a primary key for each entity. If the exam asks you to create a data structure table, include field name, data type, size (where applicable), and at least one appropriate validation rule per field.
</div>

### Common Data Types for Data Structure Tables

| Data Type | Use | Example Values |
|---|---|---|
| String / Text | Names, addresses, descriptions | "John Smith" |
| Integer | Whole numbers, IDs, quantities | 42 |
| Real / Float | Decimal numbers, prices, measurements | 19.99 |
| Boolean | True/False flags | True |
| Date | Calendar dates | 01/09/2025 |
| Char | Single characters | 'M' |

---

## Selecting and Justifying a Programming Approach

At AS level, you may be asked to select a programming method and justify your choice. The main approaches are:

### Procedural Programming

Code is organised as a sequence of instructions, using subroutines (procedures and functions) to break the problem into manageable parts.

**When to use:** Most AS-level problems are best solved with a procedural approach. It is suitable for problems that follow a clear step-by-step process such as data processing, file handling, and menu-driven applications.

**Justification points:**
- Straightforward to plan and implement
- Easy to trace and debug
- Suitable for problems with a clear sequence of operations
- Well-suited to small to medium programs

### Event-Driven Programming

Code responds to events (e.g. button clicks, key presses, mouse movements). This is the basis of GUI applications.

**When to use:** When the program requires a graphical user interface or when the flow of execution depends on user actions rather than a fixed sequence.

**Justification points:**
- Natural fit for GUI-based applications
- User controls the flow of the program
- Responsive to user input

### Justifying Your Choice -- Example Answer

> "I have chosen a procedural approach because the system processes student records in a clear sequence: input data, validate, store to file, and generate reports. The program follows a logical step-by-step flow which maps well to procedural subroutines. A procedural approach also makes the code easier to test by allowing each subroutine to be tested independently."

<div class="exam-tip" markdown="1">
When justifying your choice of programming approach, always link your reasoning to the **specific problem** you are solving. Do not just list generic advantages -- explain why those advantages matter for this particular scenario.
</div>

---

## Designing Flowcharts for Processes

A flowchart is a diagrammatic representation of an algorithm or process. You must be able to design flowcharts for processes in your programs.

### Standard Flowchart Symbols

| Symbol | Shape | Purpose |
|---|---|---|
| Terminal | Rounded rectangle (oval) | Start / End of the process |
| Process | Rectangle | An action or instruction |
| Decision | Diamond | A question with Yes/No (or True/False) outcomes |
| Input/Output | Parallelogram | Data input or output |
| Flow line | Arrow | Direction of flow |
| Subroutine | Rectangle with double side lines | Call to a defined subroutine |

### Example -- Flowchart for Login Validation

```
[Start]
   |
   v
[Input username and password]  (parallelogram)
   |
   v
<Do credentials match?>  (diamond)
  / \
Yes   No
 |     |
 v     v
[Grant access]   [Increment attempt counter]
 |                    |
 v                    v
[End]            <Attempts >= 3?>  (diamond)
                   / \
                 Yes   No
                  |     |
                  v     v
            [Lock account]  [Return to input]
                  |
                  v
                [End]
```

### Example -- Flowchart for Calculating Average

```
[Start]
   |
   v
[Set total = 0, count = 0]
   |
   v
[Input number]
   |
   v
<Is number = -1?>
  / \
Yes   No
 |     |
 v     v
<count > 0?>   [total = total + number]
  / \            |
Yes   No        [count = count + 1]
 |     |         |
 v     v         v
[average = total / count]  [Output "No data"]  [Loop back to Input]
 |                          |
 v                          v
[Output average]          [End]
 |
 v
[End]
```

<div class="exam-tip" markdown="1">
In the exam, always use the correct standard symbols. Marks are awarded for correct symbol usage as well as correct logic. Every flowchart must have a clear Start and End terminal.
</div>

---

## Modes of Operation

A mode of operation describes how a computer system processes its data. You need to understand three modes:

### Batch Processing

<div class="key-term" markdown="1">
**Batch Processing** -- Data is collected over a period of time and processed all at once as a single batch, without user interaction during processing.
</div>

**Characteristics:**
- Jobs are queued and processed together
- No user interaction during processing
- Often scheduled to run at off-peak times (e.g. overnight)

**Examples:**
- Payroll processing (employee hours collected weekly, then all wages calculated at once)
- Electricity bill generation (meter readings collected, bills produced in a batch)
- End-of-day bank transaction processing

**Code Example -- Simulating Batch Processing:**

```python
# Batch processing: process all orders at end of day
def process_batch(order_file):
    with open(order_file, "r") as f:
        orders = f.readlines()

    results = []
    for order in orders:
        parts = order.strip().split(",")
        customer = parts[0]
        amount = float(parts[1])
        tax = amount * 0.2
        total = amount + tax
        results.append(f"{customer},{total:.2f}")

    with open("processed_orders.csv", "w") as f:
        for result in results:
            f.write(result + "\n")

    print(f"Batch complete: {len(results)} orders processed.")

# Run the batch at end of day
process_batch("daily_orders.csv")
```

```vb
' Batch processing: process all orders at end of day
Sub ProcessBatch(orderFile As String)
    Dim orders As New List(Of String)
    Dim results As New List(Of String)

    Using reader As New System.IO.StreamReader(orderFile)
        While Not reader.EndOfStream
            orders.Add(reader.ReadLine())
        End While
    End Using

    For Each order As String In orders
        Dim parts() As String = order.Split(","c)
        Dim customer As String = parts(0)
        Dim amount As Double = CDbl(parts(1))
        Dim tax As Double = amount * 0.2
        Dim total As Double = amount + tax
        results.Add(customer & "," & total.ToString("F2"))
    Next

    Using writer As New System.IO.StreamWriter("processed_orders.csv")
        For Each result As String In results
            writer.WriteLine(result)
        Next
    End Using

    Console.WriteLine("Batch complete: " & results.Count & " orders processed.")
End Sub
```

### Real-Time Processing

<div class="key-term" markdown="1">
**Real-Time Processing** -- Data is processed immediately as it is received, with results produced fast enough to influence the current process or environment.
</div>

**Characteristics:**
- Instant or near-instant response required
- Continuous monitoring of inputs
- Often used in safety-critical systems

**Examples:**
- Air traffic control systems
- Anti-lock braking systems (ABS) in cars
- Medical patient monitoring systems
- Autopilot systems

### Interactive Processing

<div class="key-term" markdown="1">
**Interactive Processing** -- The user interacts with the system and receives immediate responses. Processing occurs in direct response to user input.
</div>

**Characteristics:**
- Two-way communication between user and system
- User provides input and gets immediate feedback
- Processing happens on demand

**Examples:**
- Online shopping (browsing, adding to basket, checking out)
- ATM machines (user inserts card, selects options, receives cash)
- Booking systems (searching availability, making reservations)

### Comparison of Modes

| Feature | Batch | Real-Time | Interactive |
|---|---|---|---|
| User interaction | None during processing | Minimal / automated | Continuous |
| Response time | Hours / scheduled | Milliseconds | Seconds |
| When processed | Collected then processed together | Immediately and continuously | On user demand |
| Example | Payroll | ABS braking | ATM |

<div class="exam-tip" markdown="1">
The exam may give you a scenario and ask which mode of operation is most appropriate. Always justify your answer by linking to the scenario's requirements -- for example, if lives depend on immediate responses, it must be real-time processing.
</div>

---

## Changeover Methods

When a new system replaces an old one, the method of transition is called the changeover method. There are four main methods:

### Direct Changeover

The old system is switched off and the new system is switched on immediately.

| Advantages | Disadvantages |
|---|---|
| Quick and simple | High risk -- if new system fails, no fallback |
| No duplication of effort | Users must adapt immediately |
| Lower cost (no parallel running) | Data could be lost if problems occur |

**Best for:** Low-risk systems, or when the old system is completely unusable.

### Parallel Running

Both old and new systems run simultaneously for a period. Outputs are compared.

| Advantages | Disadvantages |
|---|---|
| Low risk -- old system is a safety net | Expensive (running two systems) |
| Outputs can be compared for accuracy | Staff workload doubles temporarily |
| Gradual transition | Takes longer to complete |

**Best for:** Critical systems where accuracy is essential (e.g. payroll, financial systems).

### Phased Changeover

The new system is introduced in stages -- one module or feature at a time.

| Advantages | Disadvantages |
|---|---|
| Problems are isolated to one phase | Takes a long time overall |
| Staff can learn gradually | Some modules depend on others |
| Lower risk than direct changeover | Complex to manage |

**Best for:** Large, modular systems where components can be independently introduced.

### Pilot Changeover

The new system is trialled by a small group of users or at one location before full rollout.

| Advantages | Disadvantages |
|---|---|
| Problems found before full deployment | Pilot group may not be representative |
| Lessons learned improve the rollout | Two systems running at different sites |
| Lower risk than direct changeover | Takes longer than direct changeover |

**Best for:** Organisations with multiple branches or departments (e.g. rolling out a new till system at one shop first).

<div class="exam-tip" markdown="1">
In the exam, you will often be given a scenario and asked to recommend a changeover method. Always justify your recommendation by explaining why the chosen method suits the scenario's **risk level, budget, and operational needs**. For example: "Parallel running is appropriate for the hospital's patient records system because any errors could endanger patients. Running both systems simultaneously allows staff to verify the new system's accuracy before relying on it entirely."
</div>

---

## Input-Process-Output (IPO) Diagrams

An IPO diagram is a simple design tool that shows what data goes into a process, what processing occurs, and what output is produced.

### Structure

```
+------------+     +-------------------+     +-------------+
|   INPUT    | --> |     PROCESS       | --> |   OUTPUT    |
+------------+     +-------------------+     +-------------+
```

### Example 1 -- Calculating a Student's Grade

| Input | Process | Output |
|---|---|---|
| Student name | Calculate average mark | Student name |
| Test mark 1 | Compare average to grade boundaries | Average mark |
| Test mark 2 | Determine grade | Grade (A, B, C, D, E, U) |
| Test mark 3 | | |

### Example 2 -- Library Book Loan

| Input | Process | Output |
|---|---|---|
| Member ID | Validate member ID exists | Confirmation message |
| Book ID | Check book is available | Updated loan record |
| Loan date | Create loan record | Due date |
| | Calculate due date (loan date + 21 days) | Receipt |
| | Update book availability to False | |

### Example 3 -- Online Shopping Checkout

| Input | Process | Output |
|---|---|---|
| Basket items | Calculate subtotal | Order summary |
| Delivery address | Apply discount code if valid | Delivery cost |
| Payment details | Calculate delivery cost | Total cost |
| Discount code | Calculate total | Confirmation email |
| | Validate payment | Dispatch notification |
| | Generate order reference | Order reference number |

### Using IPO in Code Design

An IPO diagram maps directly to how you structure your code:

```python
# IPO: Calculate student grade
# INPUT
name = input("Enter student name: ")
mark1 = int(input("Enter mark 1: "))
mark2 = int(input("Enter mark 2: "))
mark3 = int(input("Enter mark 3: "))

# PROCESS
average = (mark1 + mark2 + mark3) / 3

if average >= 70:
    grade = "A"
elif average >= 60:
    grade = "B"
elif average >= 50:
    grade = "C"
elif average >= 40:
    grade = "D"
else:
    grade = "U"

# OUTPUT
print(f"{name} - Average: {average:.1f}, Grade: {grade}")
```

```vb
' IPO: Calculate student grade
' INPUT
Console.Write("Enter student name: ")
Dim name As String = Console.ReadLine()
Console.Write("Enter mark 1: ")
Dim mark1 As Integer = CInt(Console.ReadLine())
Console.Write("Enter mark 2: ")
Dim mark2 As Integer = CInt(Console.ReadLine())
Console.Write("Enter mark 3: ")
Dim mark3 As Integer = CInt(Console.ReadLine())

' PROCESS
Dim average As Double = (mark1 + mark2 + mark3) / 3
Dim grade As String

If average >= 70 Then
    grade = "A"
ElseIf average >= 60 Then
    grade = "B"
ElseIf average >= 50 Then
    grade = "C"
ElseIf average >= 40 Then
    grade = "D"
Else
    grade = "U"
End If

' OUTPUT
Console.WriteLine(name & " - Average: " & average.ToString("F1") & ", Grade: " & grade)
```

<div class="exam-tip" markdown="1">
IPO diagrams are useful for planning your code before you write it. They help you identify what data you need, what operations you must perform, and what results you must produce. In the coursework, using an IPO table in your design section demonstrates a clear, methodical approach.
</div>

---

## Summary

| Design Tool | Purpose |
|---|---|
| Entity Relationship Diagram | Shows entities and the relationships between them |
| Data Structure Table | Defines fields, data types, sizes, and validation for each entity |
| Flowchart | Visualises the step-by-step logic of a process or algorithm |
| IPO Diagram | Identifies inputs, processing steps, and outputs for a process |
| Mode of Operation | Determines how and when data is processed (batch, real-time, interactive) |
| Changeover Method | Plans how to transition from an old system to a new system |
