---
layout: topic
title: "Data Structures"
level: "A2 Level"
level_url: "/a2/"
unit_name: "Unit 3: Programming & System Development"
unit_url: "/a2/unit3/"
subtopics:
  - "Arrays (up to three dimensions), stacks, queues, trees, linked lists, hash tables"
  - "Manipulation of arrays (up to three dimensions)"
  - "Stacks and queues using pointers and arrays"
  - "Linked lists and trees using pointers and arrays"
---

At A2 level you are expected to understand, implement, and manipulate a range of abstract data structures using array-based representations with pointers. This topic extends the AS understanding of simple data types into more complex structures that underpin real-world software systems.

## Arrays (Up to Three Dimensions)

<div class="key-term" markdown="1">

**Array** -- a fixed-size, ordered collection of elements of the same data type, stored in contiguous memory locations. Elements are accessed directly using one or more index values, giving O(1) random access.

</div>

### One-Dimensional Arrays

A 1D array is a simple linear sequence. Each element is accessed by a single index.

```python
# Python — 1D array
scores = [0] * 5  # creates [0, 0, 0, 0, 0]

# Assigning values
scores[0] = 85
scores[1] = 92
scores[2] = 78
scores[3] = 90
scores[4] = 88

# Accessing a value
print(scores[2])  # outputs 78

# Iterating
for i in range(len(scores)):
    print(f"scores[{i}] = {scores[i]}")
```

```vb
' VB.NET — 1D array
Dim scores(4) As Integer  ' indices 0 to 4

scores(0) = 85
scores(1) = 92
scores(2) = 78
scores(3) = 90
scores(4) = 88

' Accessing a value
Console.WriteLine(scores(2))  ' outputs 78

' Iterating
For i As Integer = 0 To scores.Length - 1
    Console.WriteLine($"scores({i}) = {scores(i)}")
Next
```

### Two-Dimensional Arrays

A 2D array is a table of rows and columns. Elements are accessed with two indices: `array[row][col]`.

| Index | Col 0 | Col 1 | Col 2 |
|-------|-------|-------|-------|
| Row 0 | 1 | 2 | 3 |
| Row 1 | 4 | 5 | 6 |
| Row 2 | 7 | 8 | 9 |

```python
# Python — 2D array (3 rows x 3 columns)
grid = [[0] * 3 for _ in range(3)]

# Assigning values
grid[0][0] = 1
grid[0][1] = 2
grid[0][2] = 3
grid[1][0] = 4
grid[1][1] = 5
grid[1][2] = 6
grid[2][0] = 7
grid[2][1] = 8
grid[2][2] = 9

# Accessing a value
print(grid[1][2])  # row 1, col 2 → outputs 6

# Iterating through all elements
for row in range(3):
    for col in range(3):
        print(grid[row][col], end=" ")
    print()
```

```vb
' VB.NET — 2D array (3 rows x 3 columns)
Dim grid(2, 2) As Integer  ' indices 0..2, 0..2

grid(0, 0) = 1 : grid(0, 1) = 2 : grid(0, 2) = 3
grid(1, 0) = 4 : grid(1, 1) = 5 : grid(1, 2) = 6
grid(2, 0) = 7 : grid(2, 1) = 8 : grid(2, 2) = 9

' Accessing a value
Console.WriteLine(grid(1, 2))  ' row 1, col 2 → outputs 6

' Iterating through all elements
For row As Integer = 0 To 2
    For col As Integer = 0 To 2
        Console.Write(grid(row, col) & " ")
    Next
    Console.WriteLine()
Next
```

### Three-Dimensional Arrays

A 3D array adds a third dimension -- think of it as multiple 2D tables (layers). Elements are accessed as `array[layer][row][col]`.

A practical example is storing the timetable for multiple classrooms across multiple days: `timetable[classroom][day][period]`.

```python
# Python — 3D array (2 layers x 3 rows x 4 columns)
# e.g. 2 classrooms, 3 days, 4 periods per day
LAYERS = 2
ROWS = 3
COLS = 4

timetable = [[['' for _ in range(COLS)] for _ in range(ROWS)] for _ in range(LAYERS)]

# Assigning: classroom 0, day 1, period 2
timetable[0][1][2] = "Maths"

# Assigning: classroom 1, day 2, period 0
timetable[1][2][0] = "Physics"

# Accessing a value
print(timetable[0][1][2])  # outputs "Maths"

# Iterating through all elements
for layer in range(LAYERS):
    print(f"Classroom {layer}:")
    for row in range(ROWS):
        for col in range(COLS):
            subject = timetable[layer][row][col]
            print(f"  Day {row}, Period {col}: {subject if subject else 'Free'}")
```

```vb
' VB.NET — 3D array (2 layers x 3 rows x 4 columns)
Dim timetable(1, 2, 3) As String  ' 0..1, 0..2, 0..3

' Assigning: classroom 0, day 1, period 2
timetable(0, 1, 2) = "Maths"

' Assigning: classroom 1, day 2, period 0
timetable(1, 2, 0) = "Physics"

' Accessing a value
Console.WriteLine(timetable(0, 1, 2))  ' outputs "Maths"

' Iterating through all elements
For layer As Integer = 0 To 1
    Console.WriteLine($"Classroom {layer}:")
    For row As Integer = 0 To 2
        For col As Integer = 0 To 3
            Dim subject As String = timetable(layer, row, col)
            If subject Is Nothing Then subject = "Free"
            Console.WriteLine($"  Day {row}, Period {col}: {subject}")
        Next
    Next
Next
```

### Manipulation of Arrays

Common operations on arrays that you must be able to implement include:

| Operation | Description |
|-----------|-------------|
| Linear search | Sequentially check each element |
| Summing / averaging | Accumulate values across elements |
| Finding max / min | Track the largest or smallest value |
| Copying | Duplicate contents into a new array |
| Merging | Combine two arrays into one |
| Transposing (2D) | Swap rows and columns |

**Example -- summing columns and finding the maximum in a 2D array:**

```python
# Python — column sums and row maximum in a 2D array
sales = [
    [120, 200, 150],
    [180, 160, 210],
    [90,  220, 170]
]

ROWS = 3
COLS = 3

# Sum each column
for col in range(COLS):
    col_total = 0
    for row in range(ROWS):
        col_total += sales[row][col]
    print(f"Column {col} total: {col_total}")

# Find the maximum value in the entire array
max_val = sales[0][0]
for row in range(ROWS):
    for col in range(COLS):
        if sales[row][col] > max_val:
            max_val = sales[row][col]
print(f"Maximum value: {max_val}")
```

```vb
' VB.NET — column sums and maximum in a 2D array
Dim sales(,) As Integer = {
    {120, 200, 150},
    {180, 160, 210},
    {90, 220, 170}
}

Dim rows As Integer = 3
Dim cols As Integer = 3

' Sum each column
For col As Integer = 0 To cols - 1
    Dim colTotal As Integer = 0
    For row As Integer = 0 To rows - 1
        colTotal += sales(row, col)
    Next
    Console.WriteLine($"Column {col} total: {colTotal}")
Next

' Find the maximum value in the entire array
Dim maxVal As Integer = sales(0, 0)
For row As Integer = 0 To rows - 1
    For col As Integer = 0 To cols - 1
        If sales(row, col) > maxVal Then
            maxVal = sales(row, col)
        End If
    Next
Next
Console.WriteLine($"Maximum value: {maxVal}")
```

<div class="exam-tip" markdown="1">

**Exam tip** -- when writing pseudocode for 2D or 3D array operations, always state the meaning of each dimension (e.g. "rows represent students, columns represent test scores"). Examiners award marks for demonstrating understanding of the structure, not just syntax.

</div>

---

## Stacks

<div class="key-term" markdown="1">

**Stack** -- a Last-In-First-Out (LIFO) data structure. The last item added (pushed) is the first item removed (popped). A stack can be visualised as a pile of plates -- you can only add or remove from the top.

</div>

### Stack Operations

| Operation | Description |
|-----------|-------------|
| **push(item)** | Add an item to the top of the stack |
| **pop()** | Remove and return the item from the top |
| **peek()** | Return the top item without removing it |
| **isEmpty()** | Return True if the stack contains no items |
| **isFull()** | Return True if the stack has reached capacity |

### Array-Based Stack Implementation

The stack is stored in a fixed-size array. A `top` pointer keeps track of the index of the topmost element. When the stack is empty, `top` is set to -1.

```
Index:  [0]  [1]  [2]  [3]  [4]
Data:    10   20   30    _    _
                    ↑
                   top = 2
```

```python
# Python — full array-based stack implementation

class Stack:
    def __init__(self, capacity):
        self.capacity = capacity
        self.data = [None] * capacity
        self.top = -1  # -1 indicates an empty stack

    def is_empty(self):
        return self.top == -1

    def is_full(self):
        return self.top == self.capacity - 1

    def push(self, item):
        if self.is_full():
            print("Stack overflow — stack is full")
            return
        self.top += 1
        self.data[self.top] = item

    def pop(self):
        if self.is_empty():
            print("Stack underflow — stack is empty")
            return None
        item = self.data[self.top]
        self.data[self.top] = None
        self.top -= 1
        return item

    def peek(self):
        if self.is_empty():
            print("Stack is empty — nothing to peek")
            return None
        return self.data[self.top]

    def display(self):
        if self.is_empty():
            print("Stack is empty")
        else:
            for i in range(self.top, -1, -1):
                marker = " ← top" if i == self.top else ""
                print(f"  [{i}] {self.data[i]}{marker}")


# --- Demonstration ---
s = Stack(5)
s.push(10)
s.push(20)
s.push(30)
s.display()
# Output:
#   [2] 30 ← top
#   [1] 20
#   [0] 10

print("Peek:", s.peek())    # 30
print("Pop:", s.pop())      # 30
print("Pop:", s.pop())      # 20
print("isEmpty:", s.is_empty())  # False
s.pop()
print("isEmpty:", s.is_empty())  # True
s.pop()                     # Stack underflow
```

```vb
' VB.NET — full array-based stack implementation

Module StackModule

    Const CAPACITY As Integer = 5
    Dim data(CAPACITY - 1) As String
    Dim top As Integer = -1  ' -1 indicates an empty stack

    Function IsEmpty() As Boolean
        Return top = -1
    End Function

    Function IsFull() As Boolean
        Return top = CAPACITY - 1
    End Function

    Sub Push(item As String)
        If IsFull() Then
            Console.WriteLine("Stack overflow — stack is full")
            Return
        End If
        top += 1
        data(top) = item
    End Sub

    Function Pop() As String
        If IsEmpty() Then
            Console.WriteLine("Stack underflow — stack is empty")
            Return Nothing
        End If
        Dim item As String = data(top)
        data(top) = Nothing
        top -= 1
        Return item
    End Function

    Function Peek() As String
        If IsEmpty() Then
            Console.WriteLine("Stack is empty — nothing to peek")
            Return Nothing
        End If
        Return data(top)
    End Function

    Sub Display()
        If IsEmpty() Then
            Console.WriteLine("Stack is empty")
        Else
            For i As Integer = top To 0 Step -1
                Dim marker As String = If(i = top, " ← top", "")
                Console.WriteLine($"  [{i}] {data(i)}{marker}")
            Next
        End If
    End Sub

    Sub Main()
        Push("10")
        Push("20")
        Push("30")
        Display()

        Console.WriteLine("Peek: " & Peek())
        Console.WriteLine("Pop: " & Pop())
        Console.WriteLine("Pop: " & Pop())
        Console.WriteLine("isEmpty: " & IsEmpty())
        Pop()
        Console.WriteLine("isEmpty: " & IsEmpty())
        Pop()  ' Stack underflow
    End Sub

End Module
```

### Common Uses of Stacks

- **Function call management** -- the call stack stores return addresses and local variables.
- **Expression evaluation** -- converting infix to postfix notation and evaluating postfix expressions.
- **Undo functionality** -- each action is pushed; undoing pops the most recent action.
- **Backtracking algorithms** -- depth-first search uses a stack (explicitly or via recursion).

<div class="exam-tip" markdown="1">

**Exam tip** -- in stack questions, always check for overflow before pushing and underflow before popping. Examiners specifically look for these boundary checks. Remember that `top = -1` means empty, and `top = capacity - 1` means full.

</div>

---

## Queues

<div class="key-term" markdown="1">

**Queue** -- a First-In-First-Out (FIFO) data structure. The first item added (enqueued) is the first item removed (dequeued). A queue can be visualised as a line of people waiting -- people join at the rear and leave from the front.

</div>

### Queue Operations

| Operation | Description |
|-----------|-------------|
| **enqueue(item)** | Add an item to the rear of the queue |
| **dequeue()** | Remove and return the item from the front |
| **peek()** | Return the front item without removing it |
| **isEmpty()** | Return True if the queue contains no items |
| **isFull()** | Return True if the queue has reached capacity |

### Circular Queue Array Implementation

A linear queue wastes space because dequeued slots at the front can never be reused. A **circular queue** solves this by wrapping the `front` and `rear` pointers around the array using the modulus operator.

```
Circular queue with capacity 5, containing items A, B, C:

Index:  [0]  [1]  [2]  [3]  [4]
Data:    _    A    B    C    _
              ↑              ↑
            front=1        rear=3

After enqueue("D") and enqueue("E"):
Index:  [0]  [1]  [2]  [3]  [4]
Data:    _    A    B    C    D
              ↑              ↑
            front=1        rear=4

After dequeue() removes A, then enqueue("E"):
Index:  [0]  [1]  [2]  [3]  [4]
Data:    E    _    B    C    D
         ↑         ↑
       rear=0   front=2
(The rear has wrapped around to index 0)
```

A `size` counter tracks how many items are in the queue, making it straightforward to distinguish between full and empty states.

```python
# Python — full circular queue implementation

class CircularQueue:
    def __init__(self, capacity):
        self.capacity = capacity
        self.data = [None] * capacity
        self.front = 0
        self.rear = -1
        self.size = 0

    def is_empty(self):
        return self.size == 0

    def is_full(self):
        return self.size == self.capacity

    def enqueue(self, item):
        if self.is_full():
            print("Queue overflow — queue is full")
            return
        self.rear = (self.rear + 1) % self.capacity
        self.data[self.rear] = item
        self.size += 1

    def dequeue(self):
        if self.is_empty():
            print("Queue underflow — queue is empty")
            return None
        item = self.data[self.front]
        self.data[self.front] = None
        self.front = (self.front + 1) % self.capacity
        self.size -= 1
        return item

    def peek(self):
        if self.is_empty():
            print("Queue is empty — nothing to peek")
            return None
        return self.data[self.front]

    def display(self):
        if self.is_empty():
            print("Queue is empty")
            return
        print("Queue contents (front to rear):")
        index = self.front
        for i in range(self.size):
            marker = ""
            if index == self.front and index == self.rear:
                marker = " ← front/rear"
            elif index == self.front:
                marker = " ← front"
            elif index == self.rear:
                marker = " ← rear"
            print(f"  [{index}] {self.data[index]}{marker}")
            index = (index + 1) % self.capacity


# --- Demonstration ---
q = CircularQueue(5)
q.enqueue("A")
q.enqueue("B")
q.enqueue("C")
q.display()
# Output:
#   [0] A ← front
#   [1] B
#   [2] C ← rear

print("Peek:", q.peek())       # A
print("Dequeue:", q.dequeue())  # A
print("Dequeue:", q.dequeue())  # B

q.enqueue("D")
q.enqueue("E")
q.enqueue("F")
q.display()
# Now the rear has wrapped around

print("Size:", q.size)          # 3
q.enqueue("G")
q.enqueue("H")
q.enqueue("I")                  # Queue overflow
```

```vb
' VB.NET — full circular queue implementation

Module CircularQueueModule

    Const CAPACITY As Integer = 5
    Dim data(CAPACITY - 1) As String
    Dim front As Integer = 0
    Dim rear As Integer = -1
    Dim size As Integer = 0

    Function IsEmpty() As Boolean
        Return size = 0
    End Function

    Function IsFull() As Boolean
        Return size = CAPACITY
    End Function

    Sub Enqueue(item As String)
        If IsFull() Then
            Console.WriteLine("Queue overflow — queue is full")
            Return
        End If
        rear = (rear + 1) Mod CAPACITY
        data(rear) = item
        size += 1
    End Sub

    Function Dequeue() As String
        If IsEmpty() Then
            Console.WriteLine("Queue underflow — queue is empty")
            Return Nothing
        End If
        Dim item As String = data(front)
        data(front) = Nothing
        front = (front + 1) Mod CAPACITY
        size -= 1
        Return item
    End Function

    Function Peek() As String
        If IsEmpty() Then
            Console.WriteLine("Queue is empty — nothing to peek")
            Return Nothing
        End If
        Return data(front)
    End Function

    Sub Display()
        If IsEmpty() Then
            Console.WriteLine("Queue is empty")
            Return
        End If
        Console.WriteLine("Queue contents (front to rear):")
        Dim index As Integer = front
        For i As Integer = 0 To size - 1
            Dim marker As String = ""
            If index = front AndAlso index = rear Then
                marker = " ← front/rear"
            ElseIf index = front Then
                marker = " ← front"
            ElseIf index = rear Then
                marker = " ← rear"
            End If
            Console.WriteLine($"  [{index}] {data(index)}{marker}")
            index = (index + 1) Mod CAPACITY
        Next
    End Sub

    Sub Main()
        Enqueue("A")
        Enqueue("B")
        Enqueue("C")
        Display()

        Console.WriteLine("Peek: " & Peek())
        Console.WriteLine("Dequeue: " & Dequeue())
        Console.WriteLine("Dequeue: " & Dequeue())

        Enqueue("D")
        Enqueue("E")
        Enqueue("F")
        Display()
    End Sub

End Module
```

<div class="exam-tip" markdown="1">

**Exam tip** -- the modulus operator (`%` in Python, `Mod` in VB.NET) is essential for circular queues. The expression `(rear + 1) % capacity` wraps the pointer back to index 0 after it reaches the end of the array. Make sure you can trace through a circular queue on paper, including the wrap-around case.

</div>

---

## Linked Lists

<div class="key-term" markdown="1">

**Linked list** -- a dynamic data structure made up of nodes, where each node contains a data field and a pointer (link) to the next node in the sequence. Unlike arrays, linked list elements are not stored contiguously -- they are connected logically through pointers.

</div>

### Singly Linked List Concepts

In a singly linked list, each node has:
- **Data** -- the value stored in the node.
- **Next pointer** -- the index (or reference) of the next node in the list.

A special **head** pointer indicates the first node. The last node has a next pointer of `-1` (or `null`/`None`) to indicate the end of the list.

```
Head → [0] Data: "Cat" | Next: 2 → [2] Data: "Dog" | Next: 4 → [4] Data: "Fox" | Next: -1
```

### Array-Based Linked List with a Free List

At A2 level, you must be able to implement a linked list using parallel arrays (one for data, one for next pointers) rather than dynamic memory. A **free list** tracks which array slots are available for reuse.

```
Array-based linked list with free list:

Index:    0       1       2       3       4       5
Data:   "Cat"    ""    "Dog"    ""    "Fox"    ""
Next:     2      3       4      5      -1      -1

head = 0     (start of data list: Cat → Dog → Fox)
free = 1     (start of free list: 1 → 3 → 5)
```

```python
# Python — array-based singly linked list with free list

class LinkedList:
    def __init__(self, capacity):
        self.capacity = capacity
        self.data = [None] * capacity
        self.next = [0] * capacity
        self.head = -1  # -1 means the list is empty
        self.free = 0   # start of the free list

        # Initialise the free list: each slot points to the next
        for i in range(capacity - 1):
            self.next[i] = i + 1
        self.next[capacity - 1] = -1  # last free slot points to -1

    def is_empty(self):
        return self.head == -1

    def is_full(self):
        return self.free == -1

    def _allocate_node(self):
        """Get the next available node from the free list."""
        if self.free == -1:
            return -1  # no free nodes
        node = self.free
        self.free = self.next[self.free]
        return node

    def _release_node(self, index):
        """Return a node to the free list."""
        self.next[index] = self.free
        self.data[index] = None
        self.free = index

    def insert_at_start(self, item):
        if self.is_full():
            print("List is full — cannot insert")
            return
        new_node = self._allocate_node()
        self.data[new_node] = item
        self.next[new_node] = self.head
        self.head = new_node

    def insert_at_end(self, item):
        if self.is_full():
            print("List is full — cannot insert")
            return
        new_node = self._allocate_node()
        self.data[new_node] = item
        self.next[new_node] = -1
        if self.head == -1:
            self.head = new_node
        else:
            current = self.head
            while self.next[current] != -1:
                current = self.next[current]
            self.next[current] = new_node

    def insert_in_order(self, item):
        """Insert into a sorted list, maintaining ascending order."""
        if self.is_full():
            print("List is full — cannot insert")
            return
        new_node = self._allocate_node()
        self.data[new_node] = item

        # Insert at start if list is empty or item is smaller than head
        if self.head == -1 or item < self.data[self.head]:
            self.next[new_node] = self.head
            self.head = new_node
        else:
            current = self.head
            while self.next[current] != -1 and self.data[self.next[current]] < item:
                current = self.next[current]
            self.next[new_node] = self.next[current]
            self.next[current] = new_node

    def delete(self, item):
        if self.is_empty():
            print("List is empty — cannot delete")
            return False
        # Deleting the head node
        if self.data[self.head] == item:
            old_head = self.head
            self.head = self.next[self.head]
            self._release_node(old_head)
            return True
        # Search for the node to delete
        current = self.head
        while self.next[current] != -1:
            if self.data[self.next[current]] == item:
                node_to_delete = self.next[current]
                self.next[current] = self.next[node_to_delete]
                self._release_node(node_to_delete)
                return True
            current = self.next[current]
        print(f"'{item}' not found in list")
        return False

    def traverse(self):
        if self.is_empty():
            print("List is empty")
            return
        current = self.head
        output = []
        while current != -1:
            output.append(str(self.data[current]))
            current = self.next[current]
        print(" → ".join(output))

    def search(self, item):
        current = self.head
        while current != -1:
            if self.data[current] == item:
                return True
            current = self.next[current]
        return False


# --- Demonstration ---
ll = LinkedList(6)
ll.insert_in_order("Dog")
ll.insert_in_order("Cat")
ll.insert_in_order("Fox")
ll.insert_in_order("Eel")
ll.traverse()          # Cat → Dog → Eel → Fox

print("Search 'Eel':", ll.search("Eel"))   # True
print("Search 'Bat':", ll.search("Bat"))   # False

ll.delete("Dog")
ll.traverse()          # Cat → Eel → Fox

ll.insert_at_start("Ant")
ll.traverse()          # Ant → Cat → Eel → Fox
```

```vb
' VB.NET — array-based singly linked list with free list

Module LinkedListModule

    Const CAPACITY As Integer = 6
    Dim nodeData(CAPACITY - 1) As String
    Dim nextPointer(CAPACITY - 1) As Integer
    Dim head As Integer = -1
    Dim free As Integer = 0

    Sub Initialise()
        For i As Integer = 0 To CAPACITY - 2
            nextPointer(i) = i + 1
        Next
        nextPointer(CAPACITY - 1) = -1
    End Sub

    Function IsEmpty() As Boolean
        Return head = -1
    End Function

    Function IsFull() As Boolean
        Return free = -1
    End Function

    Function AllocateNode() As Integer
        If free = -1 Then Return -1
        Dim node As Integer = free
        free = nextPointer(free)
        Return node
    End Function

    Sub ReleaseNode(index As Integer)
        nextPointer(index) = free
        nodeData(index) = Nothing
        free = index
    End Sub

    Sub InsertAtStart(item As String)
        If IsFull() Then
            Console.WriteLine("List is full — cannot insert")
            Return
        End If
        Dim newNode As Integer = AllocateNode()
        nodeData(newNode) = item
        nextPointer(newNode) = head
        head = newNode
    End Sub

    Sub InsertInOrder(item As String)
        If IsFull() Then
            Console.WriteLine("List is full — cannot insert")
            Return
        End If
        Dim newNode As Integer = AllocateNode()
        nodeData(newNode) = item

        If head = -1 OrElse String.Compare(item, nodeData(head)) < 0 Then
            nextPointer(newNode) = head
            head = newNode
        Else
            Dim current As Integer = head
            While nextPointer(current) <> -1 AndAlso
                  String.Compare(nodeData(nextPointer(current)), item) < 0
                current = nextPointer(current)
            End While
            nextPointer(newNode) = nextPointer(current)
            nextPointer(current) = newNode
        End If
    End Sub

    Function Delete(item As String) As Boolean
        If IsEmpty() Then
            Console.WriteLine("List is empty — cannot delete")
            Return False
        End If

        If nodeData(head) = item Then
            Dim oldHead As Integer = head
            head = nextPointer(head)
            ReleaseNode(oldHead)
            Return True
        End If

        Dim current As Integer = head
        While nextPointer(current) <> -1
            If nodeData(nextPointer(current)) = item Then
                Dim nodeToDelete As Integer = nextPointer(current)
                nextPointer(current) = nextPointer(nodeToDelete)
                ReleaseNode(nodeToDelete)
                Return True
            End If
            current = nextPointer(current)
        End While

        Console.WriteLine($"'{item}' not found in list")
        Return False
    End Function

    Sub Traverse()
        If IsEmpty() Then
            Console.WriteLine("List is empty")
            Return
        End If
        Dim current As Integer = head
        Dim output As String = ""
        While current <> -1
            If output <> "" Then output &= " → "
            output &= nodeData(current)
            current = nextPointer(current)
        End While
        Console.WriteLine(output)
    End Sub

    Sub Main()
        Initialise()
        InsertInOrder("Dog")
        InsertInOrder("Cat")
        InsertInOrder("Fox")
        InsertInOrder("Eel")
        Traverse()          ' Cat → Dog → Eel → Fox

        Delete("Dog")
        Traverse()          ' Cat → Eel → Fox

        InsertAtStart("Ant")
        Traverse()          ' Ant → Cat → Eel → Fox
    End Sub

End Module
```

<div class="exam-tip" markdown="1">

**Exam tip** -- the free list is a linked list itself. When a node is deleted from the data list, it is returned to the front of the free list. When a new node is needed, it is taken from the front of the free list. This is how fixed-size arrays simulate dynamic memory allocation. Be prepared to trace through insertion and deletion operations step by step, showing how both the data list and free list change.

</div>

---

## Binary Trees

<div class="key-term" markdown="1">

**Binary tree** -- a hierarchical data structure in which each node has at most two children, referred to as the left child and the right child. In a **binary search tree (BST)**, all values in the left subtree are less than the node, and all values in the right subtree are greater.

</div>

### Node Structure

Each node in a binary tree contains:
- **Data** -- the value stored.
- **Left pointer** -- index of the left child (-1 if no left child).
- **Right pointer** -- index of the right child (-1 if no right child).

A **root** pointer indicates the starting node of the tree.

### Tree Traversals

There are three standard depth-first traversals:

| Traversal | Order | Mnemonic | Common Use |
|-----------|-------|----------|------------|
| **In-order** | Left, Root, Right | LRoR | Outputs BST values in ascending sorted order |
| **Pre-order** | Root, Left, Right | RoLR | Copying or serialising a tree |
| **Post-order** | Left, Right, Root | LRRo | Deleting a tree; evaluating expression trees |

For the following BST:

```
        50
       /  \
     30    70
    / \   / \
   20 40 60  80
```

- **In-order:** 20, 30, 40, 50, 60, 70, 80
- **Pre-order:** 50, 30, 20, 40, 70, 60, 80
- **Post-order:** 20, 40, 30, 60, 80, 70, 50

### Array-Based Binary Search Tree Implementation

```
Index:    0     1     2     3     4     5     6
Data:    50    30    70    20    40    60    80
Left:     1     3     5    -1    -1    -1    -1
Right:    2     4     6    -1    -1    -1    -1

root = 0
free = 7 (next available slot — or -1 if full)
```

```python
# Python — array-based binary search tree implementation

class BinarySearchTree:
    def __init__(self, capacity):
        self.capacity = capacity
        self.data = [None] * capacity
        self.left = [-1] * capacity
        self.right = [-1] * capacity
        self.root = -1
        self.free = 0

        # Initialise free list
        for i in range(capacity - 1):
            self.left[i] = i + 1  # reuse left pointer for free list chain
        self.left[capacity - 1] = -1

    def _allocate_node(self):
        if self.free == -1:
            return -1
        node = self.free
        self.free = self.left[self.free]
        self.left[node] = -1
        self.right[node] = -1
        return node

    def _release_node(self, index):
        self.data[index] = None
        self.right[index] = -1
        self.left[index] = self.free
        self.free = index

    def insert(self, item):
        new_node = self._allocate_node()
        if new_node == -1:
            print("Tree is full — cannot insert")
            return
        self.data[new_node] = item

        if self.root == -1:
            self.root = new_node
            return

        current = self.root
        while True:
            if item < self.data[current]:
                if self.left[current] == -1:
                    self.left[current] = new_node
                    return
                current = self.left[current]
            elif item > self.data[current]:
                if self.right[current] == -1:
                    self.right[current] = new_node
                    return
                current = self.right[current]
            else:
                # Duplicate value — do not insert
                self._release_node(new_node)
                print(f"'{item}' already exists in the tree")
                return

    def search(self, item):
        current = self.root
        while current != -1:
            if item == self.data[current]:
                return True
            elif item < self.data[current]:
                current = self.left[current]
            else:
                current = self.right[current]
        return False

    def in_order(self, node=None, first_call=True):
        """Left, Root, Right — produces sorted output."""
        if first_call:
            node = self.root
        if node == -1:
            return
        self.in_order(self.left[node], False)
        print(self.data[node], end=" ")
        self.in_order(self.right[node], False)

    def pre_order(self, node=None, first_call=True):
        """Root, Left, Right — useful for copying a tree."""
        if first_call:
            node = self.root
        if node == -1:
            return
        print(self.data[node], end=" ")
        self.pre_order(self.left[node], False)
        self.pre_order(self.right[node], False)

    def post_order(self, node=None, first_call=True):
        """Left, Right, Root — useful for deleting a tree."""
        if first_call:
            node = self.root
        if node == -1:
            return
        self.post_order(self.left[node], False)
        self.post_order(self.right[node], False)
        print(self.data[node], end=" ")


# --- Demonstration ---
bst = BinarySearchTree(10)
for value in [50, 30, 70, 20, 40, 60, 80]:
    bst.insert(value)

print("In-order:  ", end="")
bst.in_order()       # 20 30 40 50 60 70 80
print()

print("Pre-order: ", end="")
bst.pre_order()      # 50 30 20 40 70 60 80
print()

print("Post-order:", end="")
bst.post_order()     # 20 40 30 60 80 70 50
print()

print("Search 40:", bst.search(40))  # True
print("Search 55:", bst.search(55))  # False
```

```vb
' VB.NET — array-based binary search tree implementation

Module BSTModule

    Const CAPACITY As Integer = 10
    Dim nodeData(CAPACITY - 1) As Integer
    Dim leftChild(CAPACITY - 1) As Integer
    Dim rightChild(CAPACITY - 1) As Integer
    Dim root As Integer = -1
    Dim free As Integer = 0

    Sub Initialise()
        For i As Integer = 0 To CAPACITY - 2
            leftChild(i) = i + 1
        Next
        leftChild(CAPACITY - 1) = -1
        For i As Integer = 0 To CAPACITY - 1
            rightChild(i) = -1
        Next
    End Sub

    Function AllocateNode() As Integer
        If free = -1 Then Return -1
        Dim node As Integer = free
        free = leftChild(free)
        leftChild(node) = -1
        rightChild(node) = -1
        Return node
    End Function

    Sub ReleaseNode(index As Integer)
        nodeData(index) = 0
        rightChild(index) = -1
        leftChild(index) = free
        free = index
    End Sub

    Sub Insert(item As Integer)
        Dim newNode As Integer = AllocateNode()
        If newNode = -1 Then
            Console.WriteLine("Tree is full — cannot insert")
            Return
        End If
        nodeData(newNode) = item

        If root = -1 Then
            root = newNode
            Return
        End If

        Dim current As Integer = root
        While True
            If item < nodeData(current) Then
                If leftChild(current) = -1 Then
                    leftChild(current) = newNode
                    Return
                End If
                current = leftChild(current)
            ElseIf item > nodeData(current) Then
                If rightChild(current) = -1 Then
                    rightChild(current) = newNode
                    Return
                End If
                current = rightChild(current)
            Else
                ReleaseNode(newNode)
                Console.WriteLine($"'{item}' already exists in the tree")
                Return
            End If
        End While
    End Sub

    Function Search(item As Integer) As Boolean
        Dim current As Integer = root
        While current <> -1
            If item = nodeData(current) Then
                Return True
            ElseIf item < nodeData(current) Then
                current = leftChild(current)
            Else
                current = rightChild(current)
            End If
        End While
        Return False
    End Function

    Sub InOrder(node As Integer)
        If node = -1 Then Return
        InOrder(leftChild(node))
        Console.Write(nodeData(node) & " ")
        InOrder(rightChild(node))
    End Sub

    Sub PreOrder(node As Integer)
        If node = -1 Then Return
        Console.Write(nodeData(node) & " ")
        PreOrder(leftChild(node))
        PreOrder(rightChild(node))
    End Sub

    Sub PostOrder(node As Integer)
        If node = -1 Then Return
        PostOrder(leftChild(node))
        PostOrder(rightChild(node))
        Console.Write(nodeData(node) & " ")
    End Sub

    Sub Main()
        Initialise()
        Dim values() As Integer = {50, 30, 70, 20, 40, 60, 80}
        For Each v As Integer In values
            Insert(v)
        Next

        Console.Write("In-order:   ")
        InOrder(root)       ' 20 30 40 50 60 70 80
        Console.WriteLine()

        Console.Write("Pre-order:  ")
        PreOrder(root)      ' 50 30 20 40 70 60 80
        Console.WriteLine()

        Console.Write("Post-order: ")
        PostOrder(root)     ' 20 40 30 60 80 70 50
        Console.WriteLine()

        Console.WriteLine("Search 40: " & Search(40))  ' True
        Console.WriteLine("Search 55: " & Search(55))  ' False
    End Sub

End Module
```

<div class="exam-tip" markdown="1">

**Exam tip** -- you must be able to draw a BST from a given insertion sequence and then produce the in-order, pre-order, and post-order traversals. Remember: in-order always gives sorted output for a BST. A common exam question gives you a traversal output and asks you to reconstruct the tree -- pre-order output tells you the root (it is always the first element), and in-order output tells you which elements belong to the left and right subtrees.

</div>

---

## Hash Tables

<div class="key-term" markdown="1">

**Hash table** -- a data structure that maps keys to values using a **hash function**. The hash function converts a key into an array index, allowing average-case O(1) insertion, deletion, and lookup. When two different keys produce the same index, a **collision** occurs and must be resolved.

</div>

### Hash Functions

A hash function takes a key and returns an index within the bounds of the array. A good hash function:
- Is fast to compute.
- Distributes keys uniformly across the table.
- Is deterministic -- the same key always produces the same index.

A simple hash function for integer keys:

```
index = key MOD table_size
```

For string keys, a common approach sums the ASCII values of each character:

```
index = (sum of ASCII values) MOD table_size
```

### Collision Resolution

#### Method 1: Linear Probing (Open Addressing)

When a collision occurs, the algorithm checks the next slot sequentially (wrapping around if necessary) until an empty slot is found.

```
Hash table with capacity 7, hash function = key MOD 7

Insert 10: 10 MOD 7 = 3 → slot 3
Insert 17: 17 MOD 7 = 3 → collision at slot 3 → try slot 4 → empty → slot 4
Insert 24: 24 MOD 7 = 3 → collision at 3 → occupied at 4 → try slot 5 → slot 5

Index:  [0]  [1]  [2]  [3]  [4]  [5]  [6]
Data:    _    _    _   10   17   24    _
```

**Disadvantage:** linear probing leads to **clustering** -- groups of consecutive occupied slots that grow over time, reducing performance.

#### Method 2: Chaining (Separate Chaining)

Each slot in the hash table holds a list (or linked list). All items that hash to the same index are stored in that slot's list.

```
Hash table with capacity 7, hash function = key MOD 7

Insert 10: 10 MOD 7 = 3 → slot 3: [10]
Insert 17: 17 MOD 7 = 3 → slot 3: [10, 17]
Insert 24: 24 MOD 7 = 3 → slot 3: [10, 17, 24]

Index:  [0]  [1]  [2]  [3]           [4]  [5]  [6]
Data:    []   []   []  [10, 17, 24]   []   []   []
```

**Advantage:** no clustering; the table never becomes truly "full".
**Disadvantage:** requires additional memory for the lists; performance degrades if many items hash to the same slot.

### Load Factor

<div class="key-term" markdown="1">

**Load factor** -- the ratio of the number of items stored to the total number of slots in the hash table: `load factor = n / table_size`. A higher load factor increases the likelihood of collisions. For open addressing, performance degrades sharply above a load factor of around 0.7. Tables are often resized when the load factor exceeds a threshold.

</div>

### Hash Table Implementation -- Linear Probing

```python
# Python — hash table with linear probing

class HashTableLP:
    def __init__(self, capacity):
        self.capacity = capacity
        self.keys = [None] * capacity
        self.values = [None] * capacity
        self.size = 0

    def _hash(self, key):
        """Simple hash function for string keys."""
        total = 0
        for char in key:
            total += ord(char)
        return total % self.capacity

    def load_factor(self):
        return self.size / self.capacity

    def insert(self, key, value):
        if self.size == self.capacity:
            print("Hash table is full — cannot insert")
            return
        index = self._hash(key)
        start = index
        while self.keys[index] is not None:
            if self.keys[index] == key:
                # Key already exists — update value
                self.values[index] = value
                return
            index = (index + 1) % self.capacity
            if index == start:
                print("Hash table is full — cannot insert")
                return
        self.keys[index] = key
        self.values[index] = value
        self.size += 1

    def search(self, key):
        index = self._hash(key)
        start = index
        while self.keys[index] is not None:
            if self.keys[index] == key:
                return self.values[index]
            index = (index + 1) % self.capacity
            if index == start:
                break
        return None  # key not found

    def delete(self, key):
        index = self._hash(key)
        start = index
        while self.keys[index] is not None:
            if self.keys[index] == key:
                self.keys[index] = None
                self.values[index] = None
                self.size -= 1
                # Rehash subsequent entries to fill the gap
                next_index = (index + 1) % self.capacity
                while self.keys[next_index] is not None:
                    rehash_key = self.keys[next_index]
                    rehash_value = self.values[next_index]
                    self.keys[next_index] = None
                    self.values[next_index] = None
                    self.size -= 1
                    self.insert(rehash_key, rehash_value)
                    next_index = (next_index + 1) % self.capacity
                return True
            index = (index + 1) % self.capacity
            if index == start:
                break
        print(f"'{key}' not found")
        return False

    def display(self):
        print(f"Load factor: {self.load_factor():.2f}")
        for i in range(self.capacity):
            if self.keys[i] is not None:
                print(f"  [{i}] {self.keys[i]}: {self.values[i]}")
            else:
                print(f"  [{i}] ---")


# --- Demonstration ---
ht = HashTableLP(7)
ht.insert("cat", "a small pet")
ht.insert("dog", "a loyal pet")
ht.insert("act", "to perform")  # "act" and "cat" have same ASCII sum → collision
ht.insert("bat", "a flying mammal")
ht.display()

print("Search 'cat':", ht.search("cat"))  # a small pet
print("Search 'fox':", ht.search("fox"))  # None

ht.delete("cat")
ht.display()
```

### Hash Table Implementation -- Chaining

```python
# Python — hash table with chaining

class HashTableChain:
    def __init__(self, capacity):
        self.capacity = capacity
        self.table = [[] for _ in range(capacity)]
        self.size = 0

    def _hash(self, key):
        total = 0
        for char in key:
            total += ord(char)
        return total % self.capacity

    def load_factor(self):
        return self.size / self.capacity

    def insert(self, key, value):
        index = self._hash(key)
        # Check if key already exists — update if so
        for i, (k, v) in enumerate(self.table[index]):
            if k == key:
                self.table[index][i] = (key, value)
                return
        self.table[index].append((key, value))
        self.size += 1

    def search(self, key):
        index = self._hash(key)
        for k, v in self.table[index]:
            if k == key:
                return v
        return None

    def delete(self, key):
        index = self._hash(key)
        for i, (k, v) in enumerate(self.table[index]):
            if k == key:
                self.table[index].pop(i)
                self.size -= 1
                return True
        print(f"'{key}' not found")
        return False

    def display(self):
        print(f"Load factor: {self.load_factor():.2f}")
        for i in range(self.capacity):
            if self.table[i]:
                entries = ", ".join(f"{k}: {v}" for k, v in self.table[i])
                print(f"  [{i}] {entries}")
            else:
                print(f"  [{i}] ---")


# --- Demonstration ---
ht = HashTableChain(7)
ht.insert("cat", "a small pet")
ht.insert("dog", "a loyal pet")
ht.insert("act", "to perform")  # same hash as "cat" — added to the same chain
ht.insert("bat", "a flying mammal")
ht.display()

print("Search 'act':", ht.search("act"))  # to perform
ht.delete("cat")
ht.display()
```

```vb
' VB.NET — hash table with linear probing

Module HashTableModule

    Const CAPACITY As Integer = 7
    Dim keys(CAPACITY - 1) As String
    Dim values(CAPACITY - 1) As String
    Dim size As Integer = 0

    Function Hash(key As String) As Integer
        Dim total As Integer = 0
        For Each c As Char In key
            total += Asc(c)
        Next
        Return total Mod CAPACITY
    End Function

    Function LoadFactor() As Double
        Return size / CAPACITY
    End Function

    Sub Insert(key As String, value As String)
        If size = CAPACITY Then
            Console.WriteLine("Hash table is full — cannot insert")
            Return
        End If
        Dim index As Integer = Hash(key)
        Dim start As Integer = index
        While keys(index) IsNot Nothing
            If keys(index) = key Then
                values(index) = value
                Return
            End If
            index = (index + 1) Mod CAPACITY
            If index = start Then
                Console.WriteLine("Hash table is full — cannot insert")
                Return
            End If
        End While
        keys(index) = key
        values(index) = value
        size += 1
    End Sub

    Function Search(key As String) As String
        Dim index As Integer = Hash(key)
        Dim start As Integer = index
        While keys(index) IsNot Nothing
            If keys(index) = key Then
                Return values(index)
            End If
            index = (index + 1) Mod CAPACITY
            If index = start Then Exit While
        End While
        Return Nothing
    End Function

    Sub Display()
        Console.WriteLine($"Load factor: {LoadFactor():F2}")
        For i As Integer = 0 To CAPACITY - 1
            If keys(i) IsNot Nothing Then
                Console.WriteLine($"  [{i}] {keys(i)}: {values(i)}")
            Else
                Console.WriteLine($"  [{i}] ---")
            End If
        Next
    End Sub

    Sub Main()
        Insert("cat", "a small pet")
        Insert("dog", "a loyal pet")
        Insert("act", "to perform")
        Insert("bat", "a flying mammal")
        Display()

        Console.WriteLine("Search 'cat': " & Search("cat"))
        Console.WriteLine("Search 'fox': " & If(Search("fox"), "Nothing"))
    End Sub

End Module
```

<div class="exam-tip" markdown="1">

**Exam tip** -- hash table questions frequently ask you to trace through a series of insertions, showing where each item is placed and how collisions are resolved. Practise both linear probing and chaining on paper. You should also be able to explain why prime numbers are preferred for the table size (they reduce clustering by distributing keys more evenly) and calculate the load factor after a given number of insertions.

</div>

---

## Comparing Data Structures

| Data Structure | Access | Search | Insert | Delete | Notes |
|----------------|--------|--------|--------|--------|-------|
| **Array** | O(1) | O(n) | O(n) | O(n) | Fast random access; fixed size |
| **Stack** | O(n) | O(n) | O(1) | O(1) | Push/pop at top only |
| **Queue** | O(n) | O(n) | O(1) | O(1) | Enqueue at rear, dequeue at front |
| **Linked List** | O(n) | O(n) | O(1)* | O(1)* | *Once position is found; dynamic size |
| **Binary Search Tree** | O(log n) | O(log n) | O(log n) | O(log n) | Average case; degrades to O(n) if unbalanced |
| **Hash Table** | N/A | O(1) | O(1) | O(1) | Average case; depends on hash function and load factor |

<div class="exam-tip" markdown="1">

**Exam tip** -- questions often ask you to justify which data structure is most appropriate for a given scenario. Always consider: Is the size fixed or dynamic? Is ordering required? Is fast search more important than fast insertion? Does the data have a hierarchical relationship? Linking your answer to Big-O complexity will earn higher marks.

</div>
