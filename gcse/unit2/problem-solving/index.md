---
layout: topic
title: "Problem Solving"
level: "GCSE"
level_url: "/gcse/"
unit_name: "Unit 2: Computational Thinking & Programming"
unit_url: "/gcse/unit2/"
next_topic: "/gcse/unit2/algorithms-and-constructs/"
---

## Systematic Approach: Decomposition and Abstraction

When faced with a large or complex problem, trying to solve it all at once is overwhelming. In computer science, we use a **systematic approach** that breaks the problem into smaller, more manageable pieces. The two key techniques are **decomposition** and **abstraction**.

<div class="key-term" markdown="1">
**Decomposition** is the process of breaking a large problem down into smaller sub-problems that are easier to understand, solve, and test individually.
</div>

<div class="key-term" markdown="1">
**Abstraction** is the process of removing unnecessary detail from a problem so you can focus on the important parts.
</div>

### Decomposition in Practice

Imagine you need to build a quiz program. Rather than writing all the code in one go, you could decompose it into sub-problems:

1. Load the questions from a file
2. Display a question to the user
3. Get the user's answer
4. Check whether the answer is correct
5. Keep track of the score
6. Display the final result

Each of these sub-problems can be solved separately, tested on its own, and then combined into the full solution.

```python
# Python - Decomposed quiz program
def load_questions(filename):
    questions = []
    with open(filename, "r") as file:
        for line in file:
            parts = line.strip().split(",")
            questions.append({"question": parts[0], "answer": parts[1]})
    return questions

def ask_question(question):
    print(question["question"])
    return input("Your answer: ")

def check_answer(user_answer, correct_answer):
    return user_answer.strip().lower() == correct_answer.strip().lower()

def run_quiz(filename):
    questions = load_questions(filename)
    score = 0
    for q in questions:
        response = ask_question(q)
        if check_answer(response, q["answer"]):
            print("Correct!")
            score += 1
        else:
            print("Incorrect. The answer was: " + q["answer"])
    print("You scored " + str(score) + " out of " + str(len(questions)))

run_quiz("questions.txt")
```

```vb
' VB.NET - Decomposed quiz program
Module QuizProgram
    Function LoadQuestions(filename As String) As List(Of Dictionary(Of String, String))
        Dim questions As New List(Of Dictionary(Of String, String))
        For Each line As String In IO.File.ReadAllLines(filename)
            Dim parts() As String = line.Split(",")
            Dim q As New Dictionary(Of String, String)
            q.Add("question", parts(0))
            q.Add("answer", parts(1))
            questions.Add(q)
        Next
        Return questions
    End Function

    Sub AskQuestion(question As Dictionary(Of String, String), ByRef userAnswer As String)
        Console.WriteLine(question("question"))
        Console.Write("Your answer: ")
        userAnswer = Console.ReadLine()
    End Sub

    Function CheckAnswer(userAnswer As String, correctAnswer As String) As Boolean
        Return userAnswer.Trim().ToLower() = correctAnswer.Trim().ToLower()
    End Function

    Sub RunQuiz(filename As String)
        Dim questions = LoadQuestions(filename)
        Dim score As Integer = 0
        For Each q In questions
            Dim response As String = ""
            AskQuestion(q, response)
            If CheckAnswer(response, q("answer")) Then
                Console.WriteLine("Correct!")
                score += 1
            Else
                Console.WriteLine("Incorrect. The answer was: " & q("answer"))
            End If
        Next
        Console.WriteLine("You scored " & score & " out of " & questions.Count)
    End Sub

    Sub Main()
        RunQuiz("questions.txt")
    End Sub
End Module
```

### Benefits of Decomposition

| Benefit | Explanation |
|---|---|
| Easier to solve | Smaller problems are simpler to understand and code |
| Easier to test | Each part can be tested independently before combining |
| Teamwork | Different people can work on different sub-problems at the same time |
| Reusability | Sub-solutions can be reused in other programs |

<div class="exam-tip" markdown="1">
When an exam question asks you to "decompose" a problem, list the individual sub-problems as clear, separate steps. Think about what inputs, processes, and outputs each step needs.
</div>

---

## Abstraction to Model Aspects of the External World

Abstraction is used to create simplified models of real-world things inside a computer program. We keep only the details that matter for the problem we are solving and leave out everything else.

### How Abstraction Works

Consider modelling a **student** in a school database. A real student has thousands of characteristics, but we only store the ones relevant to the system:

| Kept (relevant) | Removed (irrelevant) |
|---|---|
| Name | Favourite colour |
| Date of birth | Shoe size |
| Student ID | Hobbies |
| Form group | Hair colour |
| Exam results | Height |

This is abstraction: we have created a simplified model that captures only what the school system needs.

### Abstraction in Code

We can represent the abstracted model of a student in code using data structures:

```python
# Python - Abstraction of a student
class Student:
    def __init__(self, name, student_id, form_group):
        self.name = name
        self.student_id = student_id
        self.form_group = form_group
        self.results = {}

    def add_result(self, subject, grade):
        self.results[subject] = grade

    def get_average(self):
        if len(self.results) == 0:
            return 0
        total = sum(self.results.values())
        return total / len(self.results)

# Using the abstraction
pupil = Student("Alice Smith", "S1042", "10B")
pupil.add_result("Maths", 78)
pupil.add_result("English", 85)
print(pupil.name + " average: " + str(pupil.get_average()))
```

```vb
' VB.NET - Abstraction of a student
Public Class Student
    Public Property Name As String
    Public Property StudentID As String
    Public Property FormGroup As String
    Public Property Results As New Dictionary(Of String, Integer)

    Public Sub New(name As String, studentID As String, formGroup As String)
        Me.Name = name
        Me.StudentID = studentID
        Me.FormGroup = formGroup
    End Sub

    Public Sub AddResult(subject As String, grade As Integer)
        Results.Add(subject, grade)
    End Sub

    Public Function GetAverage() As Double
        If Results.Count = 0 Then
            Return 0
        End If
        Dim total As Integer = 0
        For Each grade In Results.Values
            total += grade
        Next
        Return total / Results.Count
    End Function
End Class

' Using the abstraction
Module Program
    Sub Main()
        Dim pupil As New Student("Alice Smith", "S1042", "10B")
        pupil.AddResult("Maths", 78)
        pupil.AddResult("English", 85)
        Console.WriteLine(pupil.Name & " average: " & pupil.GetAverage())
    End Sub
End Module
```

### Other Examples of Abstraction

- **Maps** are abstractions of the real world -- they show roads and landmarks but leave out individual trees and people.
- **Weather forecasts** abstract real atmospheric data into simplified temperature and rain predictions.
- **A game character** might have health, speed, and strength, but not blood type or a favourite food.

<div class="key-term" markdown="1">
**Abstraction** in programming means representing real-world entities using only the attributes and behaviours that are relevant to the problem being solved.
</div>

<div class="exam-tip" markdown="1">
If asked to "identify the abstraction" in an exam, look for what details have been **included** and what has been **left out**. Explain *why* the removed details are not needed for the particular system.
</div>

---

## Structuring Programs into Modular Parts with Clear Interfaces

As programs grow, keeping all the code in one place becomes difficult to read, debug, and maintain. **Modular programming** means splitting a program into separate, self-contained modules (such as functions or procedures), each responsible for one specific task.

<div class="key-term" markdown="1">
**Modular programming** is a design approach where a program is divided into independent, interchangeable modules, each handling a specific piece of functionality.
</div>

<div class="key-term" markdown="1">
An **interface** is the way that different modules communicate with each other. In practice, this means the **parameters** a function accepts and the **value** it returns.
</div>

### Why Use Modules?

| Advantage | Explanation |
|---|---|
| Readability | Shorter blocks of code with clear names are easier to understand |
| Debugging | Errors can be traced to a specific module rather than searching the entire program |
| Reusability | A well-written module can be used in other programs without changes |
| Teamwork | Different programmers can build and test different modules independently |
| Maintenance | Updating one module does not require changing the rest of the program |

### Clear Interfaces: Parameters and Return Values

A module communicates with the rest of the program through its **interface** -- the parameters it takes in and the values it sends back. A clear interface means other parts of the program do not need to know *how* the module works internally, only *what* it expects and *what* it returns.

```python
# Python - Modules with clear interfaces
def calculate_area(length, width):
    """Takes length and width, returns the area."""
    return length * width

def calculate_perimeter(length, width):
    """Takes length and width, returns the perimeter."""
    return 2 * (length + width)

def display_results(length, width):
    """Uses the other modules to display results."""
    area = calculate_area(length, width)
    perimeter = calculate_perimeter(length, width)
    print("Length: " + str(length))
    print("Width: " + str(width))
    print("Area: " + str(area))
    print("Perimeter: " + str(perimeter))

# Main program
l = float(input("Enter length: "))
w = float(input("Enter width: "))
display_results(l, w)
```

```vb
' VB.NET - Modules with clear interfaces
Module ShapeCalculator
    Function CalculateArea(length As Double, width As Double) As Double
        Return length * width
    End Function

    Function CalculatePerimeter(length As Double, width As Double) As Double
        Return 2 * (length + width)
    End Function

    Sub DisplayResults(length As Double, width As Double)
        Dim area As Double = CalculateArea(length, width)
        Dim perimeter As Double = CalculatePerimeter(length, width)
        Console.WriteLine("Length: " & length)
        Console.WriteLine("Width: " & width)
        Console.WriteLine("Area: " & area)
        Console.WriteLine("Perimeter: " & perimeter)
    End Sub

    Sub Main()
        Console.Write("Enter length: ")
        Dim l As Double = Convert.ToDouble(Console.ReadLine())
        Console.Write("Enter width: ")
        Dim w As Double = Convert.ToDouble(Console.ReadLine())
        DisplayResults(l, w)
    End Sub
End Module
```

### A Larger Example: Modular Login System

This example shows how a real program might be split into modules, each with a clear interface:

```python
# Python - Modular login system
def get_credentials():
    """Returns a username and password entered by the user."""
    username = input("Enter username: ")
    password = input("Enter password: ")
    return username, password

def load_users(filename):
    """Loads user data from a file and returns it as a dictionary."""
    users = {}
    with open(filename, "r") as file:
        for line in file:
            parts = line.strip().split(",")
            users[parts[0]] = parts[1]
    return users

def authenticate(username, password, users):
    """Checks credentials against stored users. Returns True or False."""
    if username in users and users[username] == password:
        return True
    return False

def login(filename):
    """Main login module that ties the other modules together."""
    users = load_users(filename)
    username, password = get_credentials()
    if authenticate(username, password, users):
        print("Login successful. Welcome, " + username)
    else:
        print("Login failed. Incorrect username or password.")

login("users.txt")
```

```vb
' VB.NET - Modular login system
Module LoginSystem
    Sub GetCredentials(ByRef username As String, ByRef password As String)
        Console.Write("Enter username: ")
        username = Console.ReadLine()
        Console.Write("Enter password: ")
        password = Console.ReadLine()
    End Sub

    Function LoadUsers(filename As String) As Dictionary(Of String, String)
        Dim users As New Dictionary(Of String, String)
        For Each line As String In IO.File.ReadAllLines(filename)
            Dim parts() As String = line.Split(",")
            users.Add(parts(0), parts(1))
        Next
        Return users
    End Function

    Function Authenticate(username As String, password As String,
                          users As Dictionary(Of String, String)) As Boolean
        If users.ContainsKey(username) AndAlso users(username) = password Then
            Return True
        End If
        Return False
    End Function

    Sub Login(filename As String)
        Dim users = LoadUsers(filename)
        Dim username As String = ""
        Dim password As String = ""
        GetCredentials(username, password)
        If Authenticate(username, password, users) Then
            Console.WriteLine("Login successful. Welcome, " & username)
        Else
            Console.WriteLine("Login failed. Incorrect username or password.")
        End If
    End Sub

    Sub Main()
        Login("users.txt")
    End Sub
End Module
```

### How the Modules Connect

Notice how each module has a clear interface:

- `get_credentials` / `GetCredentials` -- takes no input parameters, returns/outputs the username and password
- `load_users` / `LoadUsers` -- takes a filename, returns a collection of usernames and passwords
- `authenticate` / `Authenticate` -- takes a username, password, and user collection, returns True or False
- `login` / `Login` -- ties the modules together using their interfaces

Each module can be understood, tested, and modified independently. If you needed to change how users are stored (for example, moving from a text file to a database), you would only need to update the `load_users` / `LoadUsers` module. The rest of the program would not need to change because the interface stays the same.

<div class="exam-tip" markdown="1">
In exam questions about modular design, always identify the **parameters** (inputs) and **return values** (outputs) of each module. This is what makes up the "clear interface". You may also be asked to explain why modular design makes programs easier to **test**, **debug**, and **maintain**.
</div>
