---
layout: topic
title: "Data Structures"
level: "AS"
level_url: "/as/"
unit_name: "Unit 1: Fundamentals of Computer Science"
unit_url: "/as/unit1/"
prev_topic: "/as/unit1/data-transmission/"
next_topic: "/as/unit1/organisation-of-data/"
---

## Arrays (One-Dimensional and Two-Dimensional)

An **array** is a **static data structure** that stores a fixed number of elements of the **same data type** under a single identifier. Elements are stored in **contiguous memory locations**, meaning they sit next to each other in memory. Each element is accessed using an **index** (position number).

<div class="key-term" markdown="1">
An **array** is an ordered, fixed-size collection of elements of the same data type, stored in contiguous memory locations. Each element is accessed by its index.
</div>

### One-Dimensional Arrays

A 1D array is a linear sequence of elements — essentially a single list. Most languages use **zero-based indexing**, where the first element has index 0.

```python
# Python — declaring and using a 1D array (list)
scores = [95, 82, 89, 74, 91]

# Accessing elements
print(scores[0])    # Output: 95 (first element)
print(scores[4])    # Output: 91 (last element)

# Modifying an element
scores[2] = 100
print(scores)       # Output: [95, 82, 100, 74, 91]

# Iterating through the array
for i in range(len(scores)):
    print(f"Index {i}: {scores[i]}")
```

```vb
' VB.NET — declaring and using a 1D array
Dim scores(4) As Integer  ' Declares an array with 5 elements (index 0 to 4)
scores(0) = 95
scores(1) = 82
scores(2) = 89
scores(3) = 74
scores(4) = 91

' Accessing elements
Console.WriteLine(scores(0))    ' Output: 95
Console.WriteLine(scores(4))    ' Output: 91

' Modifying an element
scores(2) = 100

' Iterating through the array
For i As Integer = 0 To scores.Length - 1
    Console.WriteLine("Index " & i & ": " & scores(i))
Next
```

### Two-Dimensional Arrays

A 2D array is a "table" or "grid" of elements organised into rows and columns. It can be thought of as an **array of arrays**. To access an element you need two indices: the **row index** and the **column index**.

```python
# Python — 2D array (list of lists)
# A 3x4 grid representing student marks for 3 students across 4 tests
marks = [
    [72, 85, 90, 68],   # Student 0
    [55, 60, 75, 80],   # Student 1
    [91, 88, 95, 79]    # Student 2
]

# Access element at row 1, column 2
print(marks[1][2])   # Output: 75

# Iterate through all elements using nested loops
for row in range(len(marks)):
    for col in range(len(marks[row])):
        print(f"marks[{row}][{col}] = {marks[row][col]}", end="  ")
    print()  # New line after each row
```

```vb
' VB.NET — 2D array
Dim marks(2, 3) As Integer  ' 3 rows (0-2), 4 columns (0-3)
marks(0, 0) = 72 : marks(0, 1) = 85 : marks(0, 2) = 90 : marks(0, 3) = 68
marks(1, 0) = 55 : marks(1, 1) = 60 : marks(1, 2) = 75 : marks(1, 3) = 80
marks(2, 0) = 91 : marks(2, 1) = 88 : marks(2, 2) = 95 : marks(2, 3) = 79

' Access element at row 1, column 2
Console.WriteLine(marks(1, 2))   ' Output: 75

' Iterate through all elements using nested loops
For row As Integer = 0 To 2
    For col As Integer = 0 To 3
        Console.Write("marks(" & row & "," & col & ") = " & marks(row, col) & "  ")
    Next
    Console.WriteLine()
Next
```

### Key Properties of Arrays

| Property | Detail |
|---|---|
| **Size** | Fixed at declaration (static) |
| **Data type** | All elements must be the same type |
| **Access** | Direct access via index — O(1) time |
| **Memory** | Contiguous allocation |
| **Searching** | Linear search O(n); binary search O(log n) if sorted |
| **Insertion/Deletion** | Expensive — elements must be shifted |

<div class="exam-tip" markdown="1">
When working with 2D arrays, always remember the convention: **first index = row, second index = column**. Nested loops are required to traverse all elements — the outer loop iterates over rows and the inner loop iterates over columns.
</div>

---

## Records (Structs)

A **record** (sometimes called a **struct**) is a data structure that groups together related items of **different data types** under a single identifier. Unlike arrays, where all elements share the same type, a record can hold a mix of strings, integers, booleans, and other types.

<div class="key-term" markdown="1">
A **record** is a data structure that stores a collection of related fields, each of which can be a different data type. Each field is accessed by its **field name** rather than an index.
</div>

### Defining and Using Records

```python
# Python — using a class to represent a record
class Student:
    def __init__(self, student_id, name, date_of_birth, mark):
        self.student_id = student_id
        self.name = name
        self.date_of_birth = date_of_birth
        self.mark = mark

# Creating record instances
student1 = Student("S101", "Alice Smith", "2007-03-15", 85)
student2 = Student("S102", "Bob Jones", "2006-11-22", 72)

# Accessing fields
print(student1.name)          # Output: Alice Smith
print(student2.mark)          # Output: 72

# Modifying a field
student1.mark = 90

# An array of records
students = [student1, student2]
for s in students:
    print(f"{s.student_id}: {s.name} scored {s.mark}")
```

```vb
' VB.NET — using a Structure to represent a record
Structure Student
    Dim StudentID As String
    Dim Name As String
    Dim DateOfBirth As Date
    Dim Mark As Integer
End Structure

' Creating and using records
Dim student1 As Student
student1.StudentID = "S101"
student1.Name = "Alice Smith"
student1.DateOfBirth = #03/15/2007#
student1.Mark = 85

Dim student2 As Student
student2.StudentID = "S102"
student2.Name = "Bob Jones"
student2.DateOfBirth = #11/22/2006#
student2.Mark = 72

' Accessing fields
Console.WriteLine(student1.Name)     ' Output: Alice Smith
Console.WriteLine(student2.Mark)     ' Output: 72

' An array of records
Dim students(1) As Student
students(0) = student1
students(1) = student2
For Each s As Student In students
    Console.WriteLine(s.StudentID & ": " & s.Name & " scored " & s.Mark)
Next
```

### Arrays vs Records

| Feature | Array | Record |
|---|---|---|
| **Data types** | All elements same type | Fields can be different types |
| **Access method** | By index (e.g., `arr[0]`) | By field name (e.g., `student.name`) |
| **Purpose** | Store list of similar items | Group related but different attributes |
| **Size** | Fixed number of elements | Fixed number of fields |

---

## Stacks (LIFO)

A **stack** is a **linear data structure** that follows the **LIFO (Last-In, First-Out)** principle. The last item added (pushed) to the stack is the first item to be removed (popped). Think of a stack of plates — you always add to and remove from the top.

<div class="key-term" markdown="1">
A **stack** is a LIFO data structure where items are added (pushed) and removed (popped) from the **top** only. A **stack pointer** keeps track of the position of the top element.
</div>

### Stack Operations

| Operation | Description |
|---|---|
| **Push** | Add an item to the top of the stack |
| **Pop** | Remove and return the item from the top |
| **Peek / Top** | View the top item without removing it |
| **isEmpty** | Check if the stack contains no items |
| **isFull** | Check if the stack has reached its maximum capacity |

### Stack Trace Example

Starting with an empty stack (max size 4):

| Step | Operation | Stack (bottom to top) | Top Pointer |
|---|---|---|---|
| 1 | Push(10) | [10] | 0 |
| 2 | Push(20) | [10, 20] | 1 |
| 3 | Push(30) | [10, 20, 30] | 2 |
| 4 | Pop() → returns 30 | [10, 20] | 1 |
| 5 | Push(40) | [10, 20, 40] | 2 |
| 6 | Peek() → returns 40 | [10, 20, 40] | 2 |
| 7 | Pop() → returns 40 | [10, 20] | 1 |
| 8 | Pop() → returns 20 | [10] | 0 |

### Stack Implementation

```python
# Python — Stack implementation using a list
class Stack:
    def __init__(self, max_size):
        self.stack = []
        self.max_size = max_size

    def push(self, item):
        if self.is_full():
            print("Stack Overflow - stack is full")
        else:
            self.stack.append(item)

    def pop(self):
        if self.is_empty():
            print("Stack Underflow - stack is empty")
            return None
        else:
            return self.stack.pop()

    def peek(self):
        if self.is_empty():
            print("Stack is empty")
            return None
        else:
            return self.stack[-1]

    def is_empty(self):
        return len(self.stack) == 0

    def is_full(self):
        return len(self.stack) == self.max_size

    def size(self):
        return len(self.stack)

# Using the stack
my_stack = Stack(5)
my_stack.push(10)
my_stack.push(20)
my_stack.push(30)
print(my_stack.peek())   # Output: 30
print(my_stack.pop())    # Output: 30
print(my_stack.pop())    # Output: 20
print(my_stack.size())   # Output: 1
```

```vb
' VB.NET — Stack implementation using an array
Module StackModule
    Const MAX_SIZE As Integer = 5
    Dim stack(MAX_SIZE - 1) As Integer
    Dim top As Integer = -1   ' -1 indicates empty stack

    Sub Push(item As Integer)
        If top = MAX_SIZE - 1 Then
            Console.WriteLine("Stack Overflow - stack is full")
        Else
            top += 1
            stack(top) = item
        End If
    End Sub

    Function Pop() As Integer
        If top = -1 Then
            Console.WriteLine("Stack Underflow - stack is empty")
            Return -1
        Else
            Dim item As Integer = stack(top)
            top -= 1
            Return item
        End If
    End Function

    Function Peek() As Integer
        If top = -1 Then
            Console.WriteLine("Stack is empty")
            Return -1
        Else
            Return stack(top)
        End If
    End Function

    Function IsEmpty() As Boolean
        Return top = -1
    End Function

    Function IsFull() As Boolean
        Return top = MAX_SIZE - 1
    End Function

    Sub Main()
        Push(10)
        Push(20)
        Push(30)
        Console.WriteLine(Peek())   ' Output: 30
        Console.WriteLine(Pop())    ' Output: 30
        Console.WriteLine(Pop())    ' Output: 20
    End Sub
End Module
```

### Common Uses of Stacks

- **Function call stack** — stores return addresses and local variables when subroutines are called
- **Undo/Redo operations** — each action is pushed; undo pops the last action
- **Expression evaluation** — converting and evaluating infix, prefix, and postfix expressions
- **Reversing data** — push all items then pop them off in reverse order
- **Backtracking algorithms** — e.g., navigating a maze or depth-first search in a graph

<div class="exam-tip" markdown="1">
**Stack overflow** occurs when you try to push onto a full stack. **Stack underflow** occurs when you try to pop from an empty stack. Be ready to trace push and pop operations step by step in an exam.
</div>

---

## Queues (FIFO)

A **queue** is a **linear data structure** that follows the **FIFO (First-In, First-Out)** principle. Items are added (enqueued) at the **rear** and removed (dequeued) from the **front**. Think of a queue of people at a checkout — the first person to join is the first to be served.

<div class="key-term" markdown="1">
A **queue** is a FIFO data structure. Items are added at the **rear** and removed from the **front**. A **front pointer** tracks the first item and a **rear pointer** tracks the last item.
</div>

### Queue Operations

| Operation | Description |
|---|---|
| **Enqueue** | Add an item to the rear of the queue |
| **Dequeue** | Remove and return the item from the front |
| **Peek / Front** | View the front item without removing it |
| **isEmpty** | Check if the queue contains no items |
| **isFull** | Check if the queue has reached its maximum capacity |

### Queue Trace Example (Linear Queue)

Starting with an empty queue (max size 4):

| Step | Operation | Queue (front to rear) | Front | Rear |
|---|---|---|---|---|
| 1 | Enqueue(A) | [A] | 0 | 0 |
| 2 | Enqueue(B) | [A, B] | 0 | 1 |
| 3 | Enqueue(C) | [A, B, C] | 0 | 2 |
| 4 | Dequeue() → returns A | [B, C] | 1 | 2 |
| 5 | Enqueue(D) | [B, C, D] | 1 | 3 |
| 6 | Dequeue() → returns B | [C, D] | 2 | 3 |

### Linear Queue vs Circular Queue

A **linear queue** has a problem: as items are dequeued, the front pointer moves forward, leaving unused space at the beginning of the array. Eventually the queue reports "full" even though there are empty spaces at the front.

A **circular queue** solves this by wrapping around to the beginning of the array when the rear reaches the end. Pointers are advanced using **modular arithmetic**: `rear = (rear + 1) MOD maxSize`.

| Feature | Linear Queue | Circular Queue |
|---|---|---|
| **Space usage** | Wastes space as front advances | Reuses freed space at the front |
| **Implementation** | Simpler | Slightly more complex (uses MOD) |
| **Full condition** | `rear == maxSize - 1` | `(rear + 1) MOD maxSize == front` |
| **Empty condition** | `front > rear` | `front == rear` (with a count or flag) |

### Queue Implementation (Linear)

```python
# Python — Linear Queue implementation
class Queue:
    def __init__(self, max_size):
        self.queue = [None] * max_size
        self.front = 0
        self.rear = -1
        self.size = 0
        self.max_size = max_size

    def enqueue(self, item):
        if self.is_full():
            print("Queue is full")
        else:
            self.rear += 1
            self.queue[self.rear] = item
            self.size += 1

    def dequeue(self):
        if self.is_empty():
            print("Queue is empty")
            return None
        else:
            item = self.queue[self.front]
            self.queue[self.front] = None
            self.front += 1
            self.size -= 1
            return item

    def peek(self):
        if self.is_empty():
            return None
        return self.queue[self.front]

    def is_empty(self):
        return self.size == 0

    def is_full(self):
        return self.rear == self.max_size - 1

# Using the queue
q = Queue(5)
q.enqueue("A")
q.enqueue("B")
q.enqueue("C")
print(q.dequeue())   # Output: A
print(q.peek())      # Output: B
q.enqueue("D")
print(q.dequeue())   # Output: B
```

```vb
' VB.NET — Linear Queue implementation
Module QueueModule
    Const MAX_SIZE As Integer = 5
    Dim queue(MAX_SIZE - 1) As String
    Dim front As Integer = 0
    Dim rear As Integer = -1
    Dim count As Integer = 0

    Sub Enqueue(item As String)
        If count = MAX_SIZE Then
            Console.WriteLine("Queue is full")
        Else
            rear += 1
            queue(rear) = item
            count += 1
        End If
    End Sub

    Function Dequeue() As String
        If count = 0 Then
            Console.WriteLine("Queue is empty")
            Return Nothing
        Else
            Dim item As String = queue(front)
            queue(front) = Nothing
            front += 1
            count -= 1
            Return item
        End If
    End Function

    Function Peek() As String
        If count = 0 Then
            Return Nothing
        End If
        Return queue(front)
    End Function

    Sub Main()
        Enqueue("A")
        Enqueue("B")
        Enqueue("C")
        Console.WriteLine(Dequeue())   ' Output: A
        Console.WriteLine(Peek())      ' Output: B
        Enqueue("D")
        Console.WriteLine(Dequeue())   ' Output: B
    End Sub
End Module
```

### Common Uses of Queues

- **Print spooler** — documents queued in order for printing
- **CPU process scheduling** — processes waiting for CPU time (e.g., Round Robin)
- **Keyboard buffer** — keystrokes stored in order as they are typed
- **Web server request handling** — requests served in order of arrival
- **Breadth-first search** in graph/tree traversal

---

## Stacks vs Queues — Comparison

| Feature | Stack | Queue |
|---|---|---|
| **Principle** | LIFO (Last-In, First-Out) | FIFO (First-In, First-Out) |
| **Add operation** | Push (to top) | Enqueue (to rear) |
| **Remove operation** | Pop (from top) | Dequeue (from front) |
| **Pointers** | Top pointer only | Front and rear pointers |
| **Analogy** | Stack of plates | Queue of people |
| **Overflow** | Push to a full stack | Enqueue to a full queue |
| **Underflow** | Pop from an empty stack | Dequeue from an empty queue |
| **Use case** | Undo operations, call stack | Print queue, scheduling |

<div class="exam-tip" markdown="1">
You must know the terms **LIFO** and **FIFO** and associate them with stacks and queues respectively. Be prepared to **trace** the state of a stack or queue as items are pushed/popped or enqueued/dequeued. Also know the difference between a **linear queue** and a **circular queue**.
</div>

---

## Linked Lists

A **linked list** is a **dynamic data structure** made up of a series of **nodes**. Each node contains two parts: the **data** and a **pointer** (or link) to the next node in the sequence. The list is accessed from a **head pointer** that points to the first node. The last node's pointer is set to **null**, indicating the end of the list.

<div class="key-term" markdown="1">
A **linked list** is a dynamic data structure where each **node** contains a data value and a pointer to the next node. A **head pointer** indicates the start of the list.
</div>

### Structure of a Linked List

```
Head → [Data: 10 | Next: →] → [Data: 20 | Next: →] → [Data: 30 | Next: null]
```

### Operations on Linked Lists

| Operation | Description | Complexity |
|---|---|---|
| **Traversal** | Visit each node from head to end | O(n) |
| **Insertion at head** | Create new node, point it to current head, update head | O(1) |
| **Insertion at position** | Traverse to position, adjust pointers | O(n) |
| **Deletion** | Traverse to find node, adjust predecessor's pointer to skip it | O(n) |
| **Search** | Traverse from head, comparing data at each node | O(n) |

### Advantages and Disadvantages

| Advantage | Disadvantage |
|---|---|
| **Dynamic size** — can grow and shrink at runtime | **No direct access** — must traverse from the head to reach an element |
| **Efficient insertion/deletion** — no need to shift elements | **Extra memory** — each node requires storage for the pointer as well as data |
| **No wasted space** — only uses memory for current elements | **Slower searching** — cannot use binary search, only sequential |

### Arrays vs Linked Lists

| Feature | Array | Linked List |
|---|---|---|
| **Size** | Fixed (static) | Variable (dynamic) |
| **Memory** | Contiguous allocation | Non-contiguous (scattered nodes) |
| **Access** | Direct access O(1) by index | Sequential access O(n) from head |
| **Insertion/Deletion** | Slow — O(n) shifting required | Fast — O(1) once position found |
| **Memory overhead** | None beyond the data | Pointer stored with each node |
| **Use case** | Known, fixed-size data | Frequently changing data |

---

## Trees and Binary Trees

A **tree** is a **hierarchical, non-linear data structure** consisting of **nodes** connected by **edges**. A tree has a single **root node** at the top, and each node can have zero or more **child nodes**. Nodes with no children are called **leaf nodes**.

<div class="key-term" markdown="1">
A **tree** is a hierarchical data structure with a **root** node at the top. Each node may have child nodes. A **binary tree** is a tree where each node has **at most two children** — a left child and a right child.
</div>

### Tree Terminology

| Term | Definition |
|---|---|
| **Root** | The topmost node in the tree (has no parent) |
| **Parent** | A node that has one or more children |
| **Child** | A node connected below another node |
| **Leaf** | A node with no children (also called a terminal node) |
| **Edge** | The connection between a parent and child |
| **Subtree** | A tree formed by a node and all its descendants |
| **Depth/Level** | The number of edges from the root to a node |
| **Height** | The number of edges on the longest path from the root to a leaf |

### Binary Trees

A **binary tree** restricts each node to **at most two children**: a **left child** and a **right child**.

A **Binary Search Tree (BST)** is a binary tree with an additional ordering rule:
- All values in the **left subtree** are **less than** the parent node
- All values in the **right subtree** are **greater than** the parent node

Example BST storing the values 8, 3, 10, 1, 6, 14:

```
        8
       / \
      3   10
     / \    \
    1   6   14
```

### Tree Traversal Methods

There are three standard ways to visit every node in a binary tree:

| Traversal | Order | Result for tree above |
|---|---|---|
| **In-order** | Left, Root, Right | 1, 3, 6, 8, 10, 14 (sorted order for BST) |
| **Pre-order** | Root, Left, Right | 8, 3, 1, 6, 10, 14 |
| **Post-order** | Left, Right, Root | 1, 6, 3, 14, 10, 8 |

### Uses of Trees

- **Binary search trees** — efficient searching, insertion, and deletion of sorted data
- **File systems** — directory/folder hierarchy
- **Decision trees** — representing choices and outcomes
- **Syntax trees** — parsing expressions in compilers
- **Game trees** — representing possible moves in games like chess

<div class="exam-tip" markdown="1">
You should be able to **draw a binary search tree** from a given set of data and perform all three traversal methods (in-order, pre-order, post-order). Remember: **in-order traversal of a BST always produces a sorted sequence**.
</div>

---

## Hash Tables

A **hash table** is a data structure that stores **key-value pairs** and provides very fast access to data. It uses a **hash function** to compute an **index** (hash value) from the key, which determines where the data is stored in an underlying array (called the **hash table** or **bucket array**).

<div class="key-term" markdown="1">
A **hash table** uses a **hash function** to map a key to an index in an array, allowing near-instant data retrieval. A **collision** occurs when two different keys produce the same hash value.
</div>

### How Hash Tables Work

1. A **key** (e.g., a student name) is passed to a **hash function**
2. The hash function calculates an **index** (e.g., using `hash = key MOD tableSize`)
3. The data is stored at that index in the array
4. To retrieve data, the same hash function is applied to the key to find the index

### Collisions

A **collision** occurs when two different keys produce the same hash value. There are two main strategies for handling collisions:

| Strategy | Description |
|---|---|
| **Open addressing (linear probing)** | If the calculated index is occupied, check the next available slot (index + 1, index + 2, etc.) until an empty slot is found |
| **Chaining** | Each index in the array holds a linked list. Colliding items are added to the linked list at that index |

### Example — Hash Function

For a hash table of size 10, using the hash function `index = key MOD 10`:

| Key | Hash (key MOD 10) | Index |
|---|---|---|
| 25 | 25 MOD 10 = 5 | 5 |
| 37 | 37 MOD 10 = 7 | 7 |
| 45 | 45 MOD 10 = 5 | 5 (collision with 25!) |

With **linear probing**, the value 45 would be placed at index 6 (the next free slot).
With **chaining**, index 5 would contain a linked list: 25 → 45.

### Properties of a Good Hash Function

- Distributes keys **uniformly** across the table to minimise collisions
- Is **fast** to compute
- Is **deterministic** — the same key always produces the same hash value
- Minimises **clustering** (groups of occupied slots)

### Advantages and Disadvantages of Hash Tables

| Advantage | Disadvantage |
|---|---|
| Very fast average lookup, insertion, and deletion — O(1) | Performance degrades with many collisions |
| Efficient for large datasets | Wastes memory if table is too large for the data |
| Direct access using key | Does not maintain data in sorted order |
| | Choosing a good hash function can be difficult |

### Uses of Hash Tables

- **Dictionaries / symbol tables** — mapping variable names to memory addresses in compilers
- **Database indexing** — fast record lookup
- **Caching** — quick retrieval of previously computed results
- **Password storage** — storing hashed passwords rather than plaintext

<div class="exam-tip" markdown="1">
You should be able to apply a simple hash function (e.g., `key MOD tableSize`) to a set of keys, identify where collisions occur, and explain how they are resolved using **linear probing** or **chaining**. Understand why a good hash function distributes data evenly.
</div>

---

## Summary Comparison of Data Structures

| Data Structure | Type | Access | Insertion | Deletion | Key Feature |
|---|---|---|---|---|---|
| **Array** | Static, linear | O(1) direct | O(n) | O(n) | Fixed size, same type |
| **Record** | Static | By field name | N/A | N/A | Mixed data types |
| **Stack** | Dynamic, linear | Top only | O(1) push | O(1) pop | LIFO |
| **Queue** | Dynamic, linear | Front only | O(1) enqueue | O(1) dequeue | FIFO |
| **Linked List** | Dynamic, linear | O(n) sequential | O(1) at head | O(n) | Dynamic size, pointer-based |
| **Binary Tree** | Dynamic, hierarchical | O(log n) for BST | O(log n) for BST | O(log n) for BST | Sorted hierarchical data |
| **Hash Table** | Static/Dynamic | O(1) average | O(1) average | O(1) average | Key-value mapping |
