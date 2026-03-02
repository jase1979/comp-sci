---
layout: topic
title: "Software Design"
level: "AS"
level_url: "/as/"
unit_name: "Unit 1: Fundamentals of Computer Science"
unit_url: "/as/unit1/"
prev_topic: "/as/unit1/systems-analysis/"
next_topic: "/as/unit1/program-design/"
---

## Top-Down Design and Stepwise Refinement

<div class="key-term" markdown="1">
**Top-down design** is a problem-solving approach where a complex problem is broken down into a series of smaller, more manageable sub-problems. Each sub-problem is then further broken down until each part is simple enough to be solved directly. This repeated decomposition is called **stepwise refinement**.
</div>

Top-down design is one of the most fundamental techniques in software engineering. Rather than trying to solve an entire problem at once, you start with a high-level overview and progressively add detail.

### How Stepwise Refinement Works

1. **Identify the overall problem** -- state what the system must do at the highest level.
2. **Decompose** the problem into major sub-tasks (typically 3--6 at each level).
3. **Refine** each sub-task by breaking it down further into smaller steps.
4. **Repeat** until every step is simple enough to be implemented directly in code (i.e. it cannot meaningfully be broken down any further).

### Example -- Library Book Loan System

- **Level 0:** Library Book Loan System
- **Level 1:** Search for Book | Issue Book | Return Book | Generate Reports
- **Level 2 (Issue Book):** Validate Member | Check Availability | Record Loan | Print Receipt

### Advantages of Top-Down Design

- Makes large problems manageable by dividing them into small, well-defined tasks.
- Enables team working -- different programmers can work on different modules.
- Each module can be tested independently (unit testing).
- Produces a clear structure that is easy to understand and maintain.
- Naturally leads to modular, well-organised code.

<div class="exam-tip" markdown="1">
In an exam, if asked to produce a top-down design, start with a single box at the top representing the whole system, then break it into 3--5 sub-tasks, then break at least one of those sub-tasks down further. Always use verbs for task names (e.g. "Validate Input", "Calculate Total") to show they are actions the system performs.
</div>

---

## Structure Diagrams

A **structure diagram** (also called a hierarchy chart) is a graphical representation of a top-down design. It shows the system broken down into modules arranged in a tree-like hierarchy.

### Rules for Structure Diagrams

- The **root node** at the top represents the entire system.
- Each level below shows the sub-tasks that make up the level above.
- Lines connect parent modules to their children, showing which module calls which.
- Modules at the same level are read left to right in the order they would typically execute.
- The lowest-level modules are simple enough to be coded directly.

### Example: Student Report System

```
                +---------------------------+
                |  Student Report System    |
                +---------------------------+
                       |          |
          +------------+          +-------------+
          |                                     |
+-------------------+               +---------------------+
|   Input Data      |               |   Output Reports    |
+-------------------+               +---------------------+
    |         |                        |            |
+--------+ +----------+        +-----------+ +-----------+
| Read   | | Validate |        | Calculate | | Display   |
| Marks  | | Marks    |        | Averages  | | Results   |
+--------+ +----------+        +-----------+ +-----------+
```

### Example: ATM System

```
                    +-------------+
                    |   ATM       |
                    +-------------+
                         |
       +-----------------+-----------------+
       |                 |                 |
+------------+    +-------------+   +-------------+
| Authenticate|   | Transaction |   | Print       |
| User       |    | Menu        |   | Receipt     |
+------------+    +-------------+   +-------------+
                        |
          +-------------+-------------+
          |             |             |
   +------------+ +-----------+ +-----------+
   | Withdraw   | | Deposit   | | Check     |
   | Cash       | | Funds     | | Balance   |
   +------------+ +-----------+ +-----------+
```

<div class="key-term" markdown="1">
A **structure diagram** visually represents the hierarchical decomposition of a system into modules. It shows which modules call which other modules and provides a clear overview of the system architecture.
</div>

<div class="exam-tip" markdown="1">
Structure diagrams do not show the order of execution, loops, or decisions. They only show the hierarchy of modules. If asked to draw one, keep boxes neat, use clear labels, and ensure every line connects a parent to a child.
</div>

---

## Data Flow Diagrams (DFDs)

A **Data Flow Diagram (DFD)** models how data moves through a system. It shows where data originates, what processes transform it, where it is stored, and where it ends up. DFDs focus entirely on data -- they do not show control flow, timing, or decision logic.

### DFD Symbols

| Symbol | Shape | Description |
|--------|-------|-------------|
| **External Entity** | Rectangle (square) | A source or destination of data that is outside the system boundary (e.g. a customer, another system) |
| **Process** | Circle (or rounded rectangle) | A task or action that transforms data. Must have at least one data flow in and one data flow out. Labelled with a verb phrase (e.g. "Validate Order") |
| **Data Store** | Open-ended rectangle (two parallel lines) | A place where data is held for later use (e.g. a database table, a file). Labelled with "D1", "D2", etc. and a name |
| **Data Flow** | Arrow (labelled) | Shows the direction data travels. The label describes what data is flowing (e.g. "Order Details", "Invoice") |

### What DFDs Do NOT Show

- The order or sequence of processes.
- Decision logic (IF/ELSE).
- Loops or repetition.
- How data is processed internally within a process.

### Levels of DFDs

DFDs can be drawn at different levels of detail:

**Context Diagram (Level 0):**
- Shows the entire system as a single process.
- Shows all external entities and the data flows between them and the system.
- Provides a high-level overview of the system boundary.
- Contains no data stores.

**Level 1 DFD:**
- Expands the single process from the context diagram into its main sub-processes.
- Shows data stores used by the system.
- Shows data flows between processes, data stores, and external entities.
- Every data flow in the context diagram must appear in the Level 1 DFD.

**Level 2 DFD (and beyond):**
- Further decomposes individual processes from Level 1 into more detailed sub-processes.
- Used when a Level 1 process is still too complex.

### Example: Online Ordering System

**Context Diagram (Level 0):**
- External entities: Customer, Warehouse
- Single process: Online Ordering System
- Data flows: Customer sends "Order Details" to the system; system sends "Order Confirmation" to Customer; system sends "Dispatch Request" to Warehouse; Warehouse sends "Dispatch Confirmation" to system.

**Level 1 DFD might include:**
- Process 1: Validate Order
- Process 2: Process Payment
- Process 3: Arrange Dispatch
- Data Store D1: Customer Database
- Data Store D2: Product Database
- Data Store D3: Order Database

### Rules for Drawing DFDs

- Every process must have at least one input and one output data flow.
- Data cannot flow directly between two external entities (it must pass through a process).
- Data cannot flow directly between two data stores (it must pass through a process).
- Data cannot flow directly from an external entity to a data store (it must pass through a process).
- All data flows must be labelled.
- Processes should be labelled with verb phrases (e.g. "Calculate Total", not "Totals").

<div class="exam-tip" markdown="1">
When drawing DFDs in an exam, the most common errors are: (1) missing labels on data flows, (2) data flowing directly between two data stores or two external entities without passing through a process, and (3) a process with no output. Always check these rules before finishing your diagram.
</div>

<div class="key-term" markdown="1">
A **Data Flow Diagram (DFD)** is a graphical tool that shows the flow of data through a system, including its sources, destinations, processes, and storage. A **context diagram** is the highest-level DFD showing the whole system as one process.
</div>

---

## State-Transition Diagrams

A **state-transition diagram** (STD) models the behaviour of a system by showing the different **states** it can be in and the **events** (or conditions) that cause it to change from one state to another.

### Components

| Component | Representation | Description |
|-----------|---------------|-------------|
| **State** | Rounded rectangle or circle | A condition or situation the system is in at a particular time (e.g. "Idle", "Processing", "Error") |
| **Transition** | Arrow between states | A change from one state to another, triggered by an event |
| **Event/Condition** | Label on the transition arrow | What causes the transition (e.g. "Button Pressed", "Timer Expires") |
| **Action** | Label on the transition arrow (after /) | What happens as a result of the transition (e.g. "/ Display Error Message") |
| **Start state** | Filled black circle | The initial state when the system begins |
| **End state** | Filled black circle inside a larger circle | A terminal state (the system stops) |

### Notation for Transition Labels

Transitions are typically labelled in the form: **event [condition] / action**

- **event** -- what triggers the transition (e.g. "Insert Card")
- **[condition]** -- optional guard condition that must be true (e.g. "[PIN correct]")
- **/action** -- optional action that occurs during the transition (e.g. "/ Dispense Cash")

### Example: ATM Machine

```
(Start) --> [Idle]
[Idle] --Insert Card--> [Reading Card]
[Reading Card] --Card Valid--> [Awaiting PIN]
[Reading Card] --Card Invalid / Eject Card--> [Idle]
[Awaiting PIN] --PIN Correct--> [Main Menu]
[Awaiting PIN] --PIN Incorrect [attempts < 3]--> [Awaiting PIN]
[Awaiting PIN] --PIN Incorrect [attempts = 3] / Retain Card--> [Idle]
[Main Menu] --Select Withdraw--> [Processing Withdrawal]
[Processing Withdrawal] --Sufficient Funds / Dispense Cash--> [Idle]
[Processing Withdrawal] --Insufficient Funds / Display Message--> [Main Menu]
[Main Menu] --Select Cancel / Eject Card--> [Idle]
```

### Example: Simple Traffic Light

```
(Start) --> [Red]
[Red] --Timer expires--> [Red and Amber]
[Red and Amber] --Timer expires--> [Green]
[Green] --Timer expires--> [Amber]
[Amber] --Timer expires--> [Red]
```

### When to Use State-Transition Diagrams

- Modelling systems that have clearly defined states (e.g. vending machines, login systems, games).
- Showing how a system responds to different events or inputs.
- Designing user interfaces where the screen changes based on user actions.
- Modelling communication protocols.

<div class="key-term" markdown="1">
A **state-transition diagram** models the behaviour of a system by showing its possible states and the events that cause transitions between those states. Each transition may have an associated condition and/or action.
</div>

<div class="exam-tip" markdown="1">
When drawing state-transition diagrams, always include a start state (filled circle) and label every transition arrow with the event that triggers it. If you forget to label transitions, you will lose marks. Remember: states are nouns/adjectives (e.g. "Locked"), transitions are events (e.g. "Enter Correct Code").
</div>

---

## Entity-Relationship Diagrams (ERDs)

An **Entity-Relationship Diagram (ERD)** is used to model the data that a system stores and the relationships between different data entities. ERDs are a key tool in database design.

### Components of an ERD

| Component | Representation | Description |
|-----------|---------------|-------------|
| **Entity** | Rectangle | A thing about which data is stored (e.g. Student, Course, Order). Represents a table in a database. |
| **Attribute** | Listed inside or beside the entity (sometimes in ovals) | A data item stored about an entity (e.g. StudentID, Name, DateOfBirth) |
| **Relationship** | Diamond or labelled line between entities | How two entities are related (e.g. "enrols on", "places") |
| **Primary Key** | Underlined attribute | The attribute that uniquely identifies each record in the entity |

### Types of Relationship

| Relationship | Notation | Meaning | Example |
|-------------|----------|---------|---------|
| **One-to-One (1:1)** | 1 ---- 1 | One instance of entity A relates to exactly one instance of entity B | One person has one passport |
| **One-to-Many (1:M)** | 1 ---- M | One instance of entity A relates to many instances of entity B | One teacher teaches many students |
| **Many-to-Many (M:M)** | M ---- M | Many instances of entity A relate to many instances of entity B | Many students take many courses |

### Example: School Database

```
+-------------+         +----------------+         +------------+
|  TEACHER    | 1     M |    CLASS       | M     M |  STUDENT   |
|-------------|---------|----------------|---------|------------|
| TeacherID   |teaches  | ClassID        |attends  | StudentID  |
| Name        |         | Subject        |         | Name       |
| Department  |         | Room           |         | DateOfBirth|
+-------------+         +----------------+         +------------+
```

- One TEACHER teaches many CLASSes (1:M).
- Many STUDENTs attend many CLASSes (M:M).

### Resolving Many-to-Many Relationships

Many-to-many relationships cannot be directly implemented in a relational database. They are resolved by introducing a **link entity** (also called a junction table or associative entity) that sits between the two entities, converting the M:M into two 1:M relationships.

**Example:** STUDENT M:M CLASS becomes:

```
STUDENT 1----M ENROLMENT M----1 CLASS
```

The ENROLMENT entity would contain: EnrolmentID, StudentID (foreign key), ClassID (foreign key), EnrolmentDate.

<div class="key-term" markdown="1">
An **Entity-Relationship Diagram (ERD)** models the data entities in a system and the relationships between them. A **primary key** uniquely identifies each record in an entity. A **foreign key** is an attribute in one entity that references the primary key of another entity.
</div>

<div class="exam-tip" markdown="1">
In the exam, always label both ends of a relationship line with "1" or "M". Always underline primary keys. If you have a many-to-many relationship, show that you understand it must be decomposed using a link entity. Name your relationships with verbs (e.g. "places", "enrols on", "teaches").
</div>

---

## Pseudocode Conventions

**Pseudocode** is a structured, informal way of writing algorithms that uses natural language mixed with programming-like constructs. It is not tied to any specific programming language and is used to plan and communicate algorithms clearly.

### Why Use Pseudocode?

- It allows you to focus on the logic of an algorithm without worrying about syntax.
- It is language-independent, so anyone can understand it regardless of their programming background.
- It is quicker to write than actual code during the design phase.
- It can be easily translated into any programming language.

### Common Pseudocode Conventions

**Variable assignment:**
```
SET total TO 0
SET name TO "Alice"
```

**Input and output:**
```
INPUT age
OUTPUT "Your age is: ", age
```

**Selection (IF/ELSE):**
```
IF age >= 18 THEN
    OUTPUT "Adult"
ELSE IF age >= 13 THEN
    OUTPUT "Teenager"
ELSE
    OUTPUT "Child"
END IF
```

**Iteration (FOR loop):**
```
FOR i FROM 1 TO 10
    OUTPUT i
END FOR
```

**Iteration (WHILE loop):**
```
SET password TO ""
WHILE password != "secret"
    INPUT password
END WHILE
```

**Iteration (REPEAT-UNTIL loop):**
```
REPEAT
    INPUT number
UNTIL number >= 0
```

**Subroutines:**
```
FUNCTION calculateArea(length, width)
    RETURN length * width
END FUNCTION

PROCEDURE displayMessage(message)
    OUTPUT message
END PROCEDURE
```

**Arrays:**
```
SET marks TO [45, 67, 89, 32, 78]
OUTPUT marks[0]
SET marks[2] TO 90
```

### Key Principles of Good Pseudocode

- Use **consistent indentation** to show the structure of loops and selections.
- Use **meaningful variable names** (e.g. `totalScore` not `x`).
- Use **capital letters for keywords** (SET, IF, THEN, ELSE, WHILE, FOR, REPEAT, UNTIL, INPUT, OUTPUT, RETURN, FUNCTION, PROCEDURE, END).
- Keep it simple and readable -- anyone should be able to follow the logic.
- Do not include language-specific syntax (e.g. do not use `:` or `{}` or `Dim`).

<div class="exam-tip" markdown="1">
In the WJEC exam, pseudocode does not need to follow an exact standard, but it must be clear and unambiguous. Always use indentation and keywords consistently. If the examiner cannot follow your logic, you will lose marks. Write pseudocode as if someone else needs to implement it in any language.
</div>

---

## Flowchart Symbols and Examples

A **flowchart** is a diagrammatic representation of an algorithm. It uses standard symbols connected by arrows to show the flow of control through a program.

### Standard Flowchart Symbols

| Symbol | Shape | Purpose |
|--------|-------|---------|
| **Terminator** | Rounded rectangle (oval) | Marks the start or end of the flowchart. Labelled "Start" or "End" (or "Stop"). |
| **Process** | Rectangle | Represents a step or action (e.g. "Set total to 0", "Calculate tax"). |
| **Input/Output** | Parallelogram | Represents input from the user or output to the screen (e.g. "Input name", "Display result"). |
| **Decision** | Diamond | Represents a decision or condition with two outcomes: Yes/No or True/False. Must have exactly two exit paths. |
| **Flow line** | Arrow | Shows the direction of flow from one symbol to the next. |
| **Subroutine** | Rectangle with double vertical lines on sides | Represents a call to a pre-defined subroutine (function or procedure). |

### Rules for Drawing Flowcharts

- Every flowchart must have exactly one **Start** terminator.
- Every flowchart must have at least one **End** terminator.
- Flow lines must have **arrows** showing direction.
- Decision diamonds must have exactly **two labelled exit paths** (Yes/No or True/False).
- All symbols must be connected -- there should be no orphaned symbols.
- Flow should generally go from top to bottom and left to right.

### Example: Check if a Number is Positive, Negative, or Zero

```
[Start]
   |
   v
/Input number/
   |
   v
<number > 0?>---Yes---> /Output "Positive"/---+
   |                                           |
   No                                          |
   |                                           |
   v                                           |
<number < 0?>---Yes---> /Output "Negative"/---+
   |                                           |
   No                                          |
   |                                           |
   v                                           |
/Output "Zero"/                                |
   |                                           |
   +<------------------------------------------+
   |
   v
[End]
```

### Example: Validate Password Entry (Loop)

```
[Start]
   |
   v
/Input password/
   |
   v
<password = "abc123"?>---Yes---> /Output "Access Granted"/
   |                                        |
   No                                       v
   |                                      [End]
   v
/Output "Incorrect, try again"/
   |
   +----> (back to Input password)
```

### Example: Calculate Sum of Numbers 1 to 10

```
[Start]
   |
   v
[Set total = 0]
   |
   v
[Set i = 1]
   |
   v
<i <= 10?>---No---> /Output total/---> [End]
   |
  Yes
   |
   v
[total = total + i]
   |
   v
[i = i + 1]
   |
   +----> (back to i <= 10? decision)
```

<div class="key-term" markdown="1">
A **flowchart** is a visual representation of an algorithm using standard symbols (terminators, processes, decisions, input/output) connected by arrows to show the flow of control.
</div>

<div class="exam-tip" markdown="1">
In the exam, always use the correct shapes for each symbol. The most common mistake is using a rectangle for a decision instead of a diamond, or forgetting to label the Yes/No paths on a decision. Practice drawing flowcharts neatly by hand. Every decision must have exactly two clearly labelled exits.
</div>
