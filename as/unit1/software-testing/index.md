---
layout: topic
title: "Software Testing"
level: "AS"
level_url: "/as/"
unit_name: "Unit 1: Fundamentals of Computer Science"
unit_url: "/as/unit1/"
prev_topic: "/as/unit1/program-design/"
next_topic: "/as/unit1/software-maintenance/"
---

## Purpose of Testing

**Software testing** is the process of executing a program with the deliberate intention of finding errors. Testing is a critical stage in the software development life cycle and is essential for producing reliable, high-quality software.

### Why Testing is Important

- **Identify defects** before the software is released to users, reducing the cost of fixing errors later.
- **Verify** that the software meets the functional requirements specified during analysis and design.
- **Validate** that the software is fit for purpose and meets the needs of the end user.
- **Improve quality** and reliability, giving stakeholders confidence in the system.
- **Prevent failures** in live environments that could cause data loss, financial loss, or safety hazards.
- **Ensure robustness** -- the software should handle unexpected inputs and situations gracefully without crashing.

<div class="key-term" markdown="1">
**Verification** checks whether the software has been built correctly according to the specification ("Are we building the product right?"). **Validation** checks whether the software meets the actual needs of the user ("Are we building the right product?").
</div>

---

## Types of Testing

There are two main approaches to testing, distinguished by whether the tester can see the internal code.

### Black-Box Testing

- The tester does **not** have access to the internal code or structure of the program.
- Testing is based entirely on the **inputs and expected outputs** defined in the specification.
- The program is treated as a "black box" -- the tester only sees what goes in and what comes out.
- Also called **functional testing** because it tests whether the program functions correctly according to its specification.

**When it is used:**
- During acceptance testing by end users who do not know the code.
- When testing against the requirements specification.
- When testing external interfaces or APIs.

**Advantages:**
- No programming knowledge is required.
- Tests are based on user requirements, so they validate the system from the user's perspective.
- Tester is unbiased -- they do not know the code, so they are less likely to make assumptions.

**Disadvantages:**
- May miss errors in code paths that are not covered by the test cases.
- Cannot test internal logic or code quality.
- Difficult to design comprehensive test cases without knowing the code structure.

### White-Box Testing

- The tester **has full access** to the internal code and structure of the program.
- Test cases are designed to exercise specific **code paths**, branches, and logic within the program.
- Also called **structural testing** or **glass-box testing**.

**When it is used:**
- During unit testing by the programmer who wrote the code.
- When trying to ensure all branches and paths through the code are tested.
- When looking for specific types of defects such as logic errors.

**Advantages:**
- Can ensure all code paths are tested (path coverage).
- Can identify dead code (code that is never executed).
- Can test internal logic and boundary conditions within the code.

**Disadvantages:**
- Requires programming knowledge and access to the source code.
- Tester may be biased -- they may test the code the way they think it should work.
- Does not check whether the program meets user requirements (only that the code works as written).

### Comparison

| Feature | Black-Box Testing | White-Box Testing |
|---------|-------------------|-------------------|
| Code access | No | Yes |
| Based on | Specification/requirements | Internal code structure |
| Performed by | Testers / end users | Programmers / developers |
| Also known as | Functional testing | Structural / glass-box testing |
| Focus | What the program does | How the program does it |
| Tests paths through code | No | Yes |

<div class="exam-tip" markdown="1">
Remember: **Black box** = can't see inside = testing based on specification. **White box** = can see inside = testing based on code. A thorough testing strategy uses both approaches.
</div>

---

## Levels of Testing

Testing is not a single activity but a series of tests performed at different stages of development. Each level builds on the previous one.

### Unit Testing

- Tests **individual components or modules** of a program in isolation.
- Usually performed by the **programmer** who wrote the code.
- Each function, procedure, or module is tested independently with its own test data.
- Uses white-box testing techniques because the developer has access to the code.
- **Goal:** Verify that each unit of the software performs as designed.

**Example:** Testing a `calculateVAT()` function on its own with various input values to check it returns the correct results.

### Integration Testing

- Tests how individual **modules work together** when they are combined.
- Checks that data is passed correctly between modules and that interfaces work as expected.
- May reveal issues with parameter passing, data formats, or timing.
- **Goal:** Expose faults in the interaction between integrated units.

**Example:** Testing that the `calculateVAT()` function works correctly when called by the `generateInvoice()` module and that the returned value is used correctly.

### System Testing

- Tests the **complete, integrated software system** as a whole.
- Checks that the entire system meets all the specified requirements (functional and non-functional).
- Includes testing performance, security, usability, and compatibility.
- **Goal:** Evaluate the system's compliance with its specified requirements.

**Example:** Testing the entire invoicing system end-to-end -- from entering order details to generating and printing the final invoice.

### Acceptance Testing

- The **final level** of testing, performed to determine whether the system is ready for release.
- Usually carried out by the **end users or client**, not the developers.
- Tests the system against the original user requirements and business needs.
- If the system passes acceptance testing, it is approved for deployment.
- **Goal:** Confirm that the system meets the business requirements and is acceptable for delivery.

**Example:** The client uses the invoicing system with real data for a trial period and confirms that it meets their needs.

### Summary of Testing Levels

| Level | Who performs it | What is tested | When |
|-------|----------------|---------------|------|
| **Unit** | Programmer | Individual modules/functions | During development |
| **Integration** | Development team | Modules working together | After unit testing |
| **System** | Testing team | Complete system | After integration testing |
| **Acceptance** | End user / client | System against user requirements | Before deployment |

<div class="exam-tip" markdown="1">
Remember the order: **Unit -> Integration -> System -> Acceptance**. Think of it as building up from the smallest part (a single function) to the entire system being signed off by the client. Each level of testing can only begin once the previous level is complete.
</div>

---

## Alpha and Beta Testing

These are two stages of testing that occur before a product is released to the general public.

### Alpha Testing

- Performed **in-house** by the development team or a dedicated testing team within the organisation.
- Takes place in a **controlled environment** (the developer's site).
- Aims to find bugs and issues before the software is given to external users.
- Both white-box and black-box techniques may be used.
- The software may still be incomplete or unstable at this stage.

### Beta Testing

- Performed by a **selected group of external users** (beta testers) outside the development organisation.
- Takes place in the **user's own environment** with real hardware and real usage patterns.
- Users report bugs, provide feedback on usability, and suggest improvements.
- The software is feature-complete but may still contain bugs.
- Feedback from beta testing is used to make final fixes and improvements before the official release.

### Comparison

| Feature | Alpha Testing | Beta Testing |
|---------|--------------|--------------|
| **Who** | Internal staff / developers | External users / public volunteers |
| **Where** | Developer's site (controlled environment) | User's site (real-world environment) |
| **When** | Before beta testing | After alpha testing, before final release |
| **Purpose** | Find bugs in a controlled setting | Find bugs in real-world conditions, gather user feedback |
| **Software state** | May be incomplete | Feature-complete but may have bugs |

<div class="key-term" markdown="1">
**Alpha testing** is testing done in-house before release. **Beta testing** is testing done by external users in a real-world environment before the final release.
</div>

---

## Test Data

To test a program thoroughly, you need to select appropriate **test data**. Test data should be carefully chosen to check all possible paths through the program and to identify potential errors. There are three main categories.

### Normal (Valid) Data

- Data that is **within the expected range and of the correct format**.
- The system should accept this data and process it correctly.
- Tests that the program works under normal operating conditions.

### Boundary (Extreme) Data

- Data that is at the **very edges of the valid range**.
- This is where errors most commonly occur (off-by-one errors).
- You should test values at the boundary itself and values just inside and just outside the boundary.

### Erroneous (Invalid) Data

- Data that is **outside the expected range, of the wrong type, or otherwise invalid**.
- The system should **reject** this data gracefully without crashing.
- Tests the robustness of input validation.

### Example: Age Input (Valid Range 18--65)

| Test Data | Type | Expected Result | Reason |
|-----------|------|-----------------|--------|
| 25 | Normal | Accepted | Within valid range |
| 40 | Normal | Accepted | Within valid range |
| 18 | Boundary | Accepted | At lower boundary (minimum valid) |
| 17 | Boundary | Rejected | Just below lower boundary |
| 65 | Boundary | Accepted | At upper boundary (maximum valid) |
| 66 | Boundary | Rejected | Just above upper boundary |
| -5 | Erroneous | Rejected | Negative number, outside range |
| 200 | Erroneous | Rejected | Far outside valid range |
| "abc" | Erroneous | Rejected | Wrong data type (string, not integer) |
| 18.5 | Erroneous | Rejected | Real number, not integer |
| "" (empty) | Erroneous | Rejected | No data entered |

<div class="exam-tip" markdown="1">
When creating test data in the exam, always include at least one example of each type: normal, boundary, and erroneous. For boundary data, test the value at the boundary AND the values either side of it (e.g. for a range of 1--100, test 0, 1, 100, and 101). Some mark schemes consider boundary data that falls just outside the range as erroneous -- include both to be safe.
</div>

---

## Test Plans and Test Tables

A **test plan** is a document that describes the testing strategy for a piece of software. It includes a **test table** which lists every individual test to be performed.

### Structure of a Test Table

A test table typically includes the following columns:

| Column | Purpose |
|--------|---------|
| **Test Number** | A unique identifier for each test |
| **Description** | What is being tested and why |
| **Test Data** | The specific input data to use |
| **Test Data Type** | Normal, boundary, or erroneous |
| **Expected Result** | What the program should do with this input |
| **Actual Result** | What the program actually did (filled in after testing) |
| **Pass/Fail** | Whether the actual result matched the expected result |

### Example Test Table: Password Validation

The password must be 8--20 characters long and contain at least one digit.

| Test # | Description | Test Data | Type | Expected Result | Actual Result | Pass/Fail |
|--------|-------------|-----------|------|-----------------|---------------|-----------|
| 1 | Valid password with digit | "Hello123" | Normal | Accepted | | |
| 2 | Valid password, exactly 8 chars | "Pass1234" | Boundary | Accepted | | |
| 3 | Valid password, exactly 20 chars | "Abcdefghij1234567890" | Boundary | Accepted | | |
| 4 | Too short (7 chars) | "Pass123" | Boundary | Rejected - "Too short" | | |
| 5 | Too long (21 chars) | "Abcdefghij12345678901" | Boundary | Rejected - "Too long" | | |
| 6 | No digit included | "Password" | Erroneous | Rejected - "Must contain a digit" | | |
| 7 | Empty string | "" | Erroneous | Rejected - "Too short" | | |
| 8 | Only digits | "12345678" | Normal | Accepted | | |

<div class="key-term" markdown="1">
A **test plan** outlines the testing strategy and contains a **test table** that specifies each individual test case, including the test data, expected results, and actual results.
</div>

---

## Debugging Techniques

**Debugging** is the process of finding and fixing errors (bugs) in a program. Several techniques are used to locate and diagnose errors.

### Trace Tables

A **trace table** is a technique for manually tracking the values of variables as a program executes. You create a table with a column for each variable and a row for each step of execution.

**Example program:**

```python
x = 3
y = 5
total = 0
for i in range(1, 4):
    total = total + x
    x = x + y
```

```vb
Dim x As Integer = 3
Dim y As Integer = 5
Dim total As Integer = 0
For i As Integer = 1 To 3
    total = total + x
    x = x + y
Next
```

**Trace table:**

| Step | i | x | y | total |
|------|---|---|---|-------|
| Init | - | 3 | 5 | 0 |
| 1 | 1 | 3 | 5 | 3 |
| 2 | 1 | 8 | 5 | 3 |
| 3 | 2 | 8 | 5 | 11 |
| 4 | 2 | 13 | 5 | 11 |
| 5 | 3 | 13 | 5 | 24 |
| 6 | 3 | 18 | 5 | 24 |

### Breakpoints

- A **breakpoint** is a marker set at a specific line in the code where execution will pause.
- When the program reaches a breakpoint, it stops, allowing the programmer to inspect the current state of all variables.
- The programmer can then **step through** the code line by line to observe how variables change.
- Available in most Integrated Development Environments (IDEs).

### Watch Variables

- A **watch** allows the programmer to monitor the value of a specific variable during execution.
- The programmer selects variables to "watch", and the IDE displays their current values in real-time as the program runs.
- Useful for tracking variables that are expected to change at certain points.
- Can also be set to break execution when a watched variable reaches a particular value.

### Stepping

- **Stepping** means executing the program one line at a time, allowing the programmer to observe the effect of each statement.
- **Step into** -- enters a subroutine call to step through it line by line.
- **Step over** -- executes a subroutine call as a single step without entering it.
- **Step out** -- runs the rest of the current subroutine and pauses at the calling line.

<div class="exam-tip" markdown="1">
In the exam, you may be asked to complete a trace table for a given piece of code. Work through the code line by line, updating the table after each statement. Be especially careful with loops -- make sure you track the loop counter correctly and know when the loop terminates.
</div>

---

## Dry Running / Desk Checking

**Dry running** (also called **desk checking**) is the process of manually working through a program on paper, without using a computer, to check that it produces the correct results.

### How to Dry Run a Program

1. Write out the variable names as column headings in a trace table.
2. Work through the code **line by line**, updating the variable values in the table.
3. For each decision (IF statement), evaluate the condition and follow the correct branch.
4. For each loop, track the loop counter and repeat until the exit condition is met.
5. Compare the final output with the expected output.

### Benefits of Dry Running

- Can identify logic errors before the program is even entered into a computer.
- Helps programmers understand the flow of execution through complex code.
- Useful during exams where you may not have access to a computer.
- Forces careful, systematic analysis of the algorithm.

### Example: Dry Run

```python
numbers = [4, 7, 2, 9, 1]
largest = numbers[0]
for i in range(1, len(numbers)):
    if numbers[i] > largest:
        largest = numbers[i]
print(largest)
```

```vb
Dim numbers() As Integer = {4, 7, 2, 9, 1}
Dim largest As Integer = numbers(0)
For i As Integer = 1 To numbers.Length - 1
    If numbers(i) > largest Then
        largest = numbers(i)
    End If
Next
Console.WriteLine(largest)
```

**Trace table:**

| i | numbers(i) | numbers(i) > largest? | largest |
|---|-----------|----------------------|---------|
| - | - | - | 4 |
| 1 | 7 | 7 > 4? Yes | 7 |
| 2 | 2 | 2 > 7? No | 7 |
| 3 | 9 | 9 > 7? Yes | 9 |
| 4 | 1 | 1 > 9? No | 9 |

**Output:** 9

<div class="key-term" markdown="1">
**Dry running** (desk checking) is manually working through a program on paper, line by line, to verify that it produces the correct output. A **trace table** is a tabular record of variable values at each step of execution.
</div>

---

## Error Types

Errors in programs fall into three main categories. Understanding the differences is essential for effective debugging.

### Syntax Errors

A **syntax error** occurs when the code violates the rules (grammar) of the programming language. The program will **not compile or run** until syntax errors are fixed.

```python
# Syntax errors in Python
print("Hello"          # Missing closing bracket
if x == 5              # Missing colon
    prit("Five")       # Misspelled keyword (not caught as syntax but as NameError)
for i in range(10)     # Missing colon
```

```vb
' Syntax errors in VB.NET
Console.WriteLine("Hello"      ' Missing closing bracket
If x = 5                       ' Missing Then keyword
    Console.WrteLine("Five")   ' Misspelled method name
For i As Integer = 1 To 10     ' Missing Next at the end
```

**Characteristics:**
- Detected by the compiler/interpreter before the program runs.
- Usually easy to find because the error message indicates the line and type of error.
- The program cannot execute until all syntax errors are corrected.

### Logic Errors

A **logic error** occurs when the program runs without crashing but produces **incorrect results**. The code is syntactically valid but the algorithm is wrong.

```python
# Logic error: using + instead of *
def calculate_area(length, width):
    return length + width    # Should be length * width

# Logic error: wrong comparison operator
def is_adult(age):
    return age > 18    # Should be age >= 18 (18-year-olds are adults)

# Logic error: off-by-one error in loop
total = 0
for i in range(1, 10):    # Misses 10; should be range(1, 11)
    total = total + i
```

```vb
' Logic error: using + instead of *
Function CalculateArea(length As Double, width As Double) As Double
    Return length + width    ' Should be length * width
End Function

' Logic error: wrong comparison operator
Function IsAdult(age As Integer) As Boolean
    Return age > 18    ' Should be age >= 18
End Function

' Logic error: off-by-one error in loop
Dim total As Integer = 0
For i As Integer = 1 To 9    ' Misses 10; should be 1 To 10
    total = total + i
Next
```

**Characteristics:**
- NOT detected by the compiler/interpreter -- the program runs without error messages.
- The program produces incorrect or unexpected output.
- The hardest type of error to find because there are no error messages pointing to the problem.
- Found through testing (using test data and comparing actual output to expected output) or dry running.

### Runtime Errors

A **runtime error** occurs during program execution, causing the program to **crash or terminate abnormally**. The code is syntactically correct but encounters a problem that cannot be handled during execution.

```python
# Runtime errors in Python
numbers = [1, 2, 3]
print(numbers[5])        # IndexError: list index out of range

result = 10 / 0           # ZeroDivisionError: division by zero

age = int("hello")         # ValueError: invalid literal for int()

file = open("nonexistent.txt")  # FileNotFoundError
```

```vb
' Runtime errors in VB.NET
Dim numbers() As Integer = {1, 2, 3}
Console.WriteLine(numbers(5))   ' IndexOutOfRangeException

Dim result As Integer = 10 \ 0   ' DivideByZeroException

Dim age As Integer = CInt("hello")  ' InvalidCastException / FormatException

Dim file As String = IO.File.ReadAllText("nonexistent.txt")  ' FileNotFoundException
```

**Characteristics:**
- NOT detected at compile time -- the program starts running but crashes during execution.
- An error message is displayed indicating the type and location of the error.
- Often caused by unexpected input, missing resources, or edge cases.
- Can be prevented using input validation, error handling (try/catch), and defensive programming.

### Comparison of Error Types

| Feature | Syntax Error | Logic Error | Runtime Error |
|---------|-------------|-------------|---------------|
| **When detected** | Compile/interpret time | During testing or use | During execution |
| **Program runs?** | No | Yes | Yes, but crashes |
| **Error message?** | Yes (from compiler) | No | Yes (when it crashes) |
| **Difficulty to find** | Easy | Hard | Medium |
| **Example** | Missing bracket | Wrong formula | Division by zero |
| **How to fix** | Read error message, fix syntax | Test with data, use trace table | Add validation, use try/catch |

<div class="exam-tip" markdown="1">
The exam often gives a piece of code and asks you to identify the type of error. Remember: if the code would not run at all, it is a **syntax error**. If it runs but gives the wrong answer, it is a **logic error**. If it runs but crashes at some point during execution, it is a **runtime error**. Be prepared to identify the specific error and explain how to fix it.
</div>
