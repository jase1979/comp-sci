---
layout: topic
title: "Algorithms & Programs"
level: "AS"
level_url: "/as/"
unit_name: "Unit 1: Fundamentals of Computer Science"
unit_url: "/as/unit1/"
prev_topic: "/as/unit1/operating-system/"
next_topic: "/as/unit1/principles-programming/"
---

## What Is an Algorithm?

<div class="key-term" markdown="1">
An **algorithm** is a finite, ordered sequence of unambiguous instructions that, given a set of inputs, produces a defined set of outputs and terminates in a finite amount of time.
</div>

An algorithm is essentially a step-by-step recipe for solving a problem. Before any code is written, a programmer designs an algorithm to describe the logic of the solution. Algorithms are **language-independent** -- the same algorithm can be implemented in Python, VB.NET, Java, or any other language.

### Characteristics of an Algorithm

- **Input** -- An algorithm has zero or more inputs taken from a specified set.
- **Output** -- An algorithm produces one or more outputs that have a defined relationship to the inputs.
- **Finiteness** -- An algorithm must always terminate after a finite number of steps.
- **Definiteness** -- Each step must be precisely and unambiguously defined.
- **Effectiveness** -- Every step must be basic enough that it could, in principle, be carried out by a person using pencil and paper.

### Why Algorithms Matter

- They allow us to **plan** a solution before writing code.
- They help us **communicate** solutions to other programmers regardless of programming language.
- They allow us to **analyse** the efficiency of a solution before implementing it.
- They form the basis for **correctness proofs** and testing strategies.

---

## Representing Algorithms

Before implementing an algorithm in code, we represent it using one of three standard methods.

### Pseudocode

Pseudocode is a structured, English-like notation for describing algorithms. It is **not** a real programming language -- there is no single standard syntax -- but it follows logical programming constructs such as sequence, selection, and iteration.

**Example -- Finding the largest value in a list:**

```
BEGIN
    SET max TO list[0]
    FOR i FROM 1 TO LENGTH(list) - 1
        IF list[i] > max THEN
            SET max TO list[i]
        END IF
    END FOR
    OUTPUT max
END
```

Pseudocode advantages:
- Quick to write and easy to read.
- Not tied to any programming language.
- Focuses on logic rather than syntax.

### Flowcharts

A flowchart is a diagrammatic representation of an algorithm using standard symbols:

| Symbol | Shape | Purpose |
|---|---|---|
| **Terminator** | Rounded rectangle (oval) | Start or end of the algorithm |
| **Process** | Rectangle | An instruction or action |
| **Decision** | Diamond | A yes/no or true/false question |
| **Input/Output** | Parallelogram | Data input or output |
| **Flow line** | Arrow | Shows the direction of flow |

Flowchart advantages:
- Visual representation makes logic easy to follow.
- Good for showing branching and looping clearly.
- Useful for non-programmers to understand the logic.

Flowchart disadvantages:
- Can become very large and unwieldy for complex algorithms.
- Harder to modify than pseudocode.

### Structured English

Structured English uses a restricted subset of natural language combined with programming constructs. It avoids technical jargon and is useful for communicating with non-technical stakeholders.

**Example:**

```
1. Start with the first item in the list.
2. Compare it with every other item.
3. If a larger item is found, remember it as the new largest.
4. After checking all items, display the largest item.
```

<div class="exam-tip" markdown="1">
In the exam, you may be asked to write an algorithm in pseudocode or to trace through a flowchart. Make sure you are comfortable with all three representations and can convert between them.
</div>

---

## Linear Search

<div class="key-term" markdown="1">
**Linear search** (also called sequential search) is an algorithm that checks every element in a list, one by one, from the beginning until the target value is found or the end of the list is reached.
</div>

### How It Works

1. Start at the first element of the list.
2. Compare the current element with the target value.
3. If they match, return the position (index) of the element.
4. If they do not match, move to the next element.
5. If the end of the list is reached without finding the target, report that the item was not found.

### Code Examples

```python
def linear_search(data, target):
    for i in range(len(data)):
        if data[i] == target:
            return i  # Return the index where target is found
    return -1  # Target not found

# Example usage
numbers = [4, 7, 2, 9, 1, 5, 8]
result = linear_search(numbers, 9)
if result != -1:
    print(f"Found at index {result}")
else:
    print("Not found")
```

```vb
Function LinearSearch(data() As Integer, target As Integer) As Integer
    For i As Integer = 0 To data.Length - 1
        If data(i) = target Then
            Return i  ' Return the index where target is found
        End If
    Next
    Return -1  ' Target not found
End Function

' Example usage
Dim numbers() As Integer = {4, 7, 2, 9, 1, 5, 8}
Dim result As Integer = LinearSearch(numbers, 9)
If result <> -1 Then
    Console.WriteLine("Found at index " & result)
Else
    Console.WriteLine("Not found")
End If
```

### Performance

- **Best case:** O(1) -- the target is the first element.
- **Worst case:** O(n) -- the target is the last element or not present.
- **Average case:** O(n) -- on average, half the list is searched.

### Advantages and Disadvantages

| Advantages | Disadvantages |
|---|---|
| Simple to understand and implement | Slow for large data sets |
| Works on unsorted data | Checks every element in the worst case |
| Works on any data structure (arrays, linked lists) | Not efficient compared to binary search on sorted data |

---

## Binary Search

<div class="key-term" markdown="1">
**Binary search** is a search algorithm that works on **sorted** data by repeatedly dividing the search interval in half. It compares the target value to the middle element and eliminates half of the remaining elements at each step.
</div>

### How It Works

1. Set `low` to the first index and `high` to the last index.
2. Find the middle index: `mid = (low + high) // 2`.
3. If `data[mid]` equals the target, return `mid`.
4. If the target is less than `data[mid]`, set `high = mid - 1` (search the left half).
5. If the target is greater than `data[mid]`, set `low = mid + 1` (search the right half).
6. Repeat steps 2-5 until the target is found or `low > high` (target not present).

### Code Examples

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

    return -1  # Target not found

# Example usage
numbers = [1, 3, 5, 7, 9, 11, 13, 15]
result = binary_search(numbers, 7)
if result != -1:
    print(f"Found at index {result}")
else:
    print("Not found")
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

    Return -1  ' Target not found
End Function

' Example usage
Dim numbers() As Integer = {1, 3, 5, 7, 9, 11, 13, 15}
Dim result As Integer = BinarySearch(numbers, 7)
If result <> -1 Then
    Console.WriteLine("Found at index " & result)
Else
    Console.WriteLine("Not found")
End If
```

### Performance

- **Best case:** O(1) -- the target is the middle element.
- **Worst case:** O(log n) -- the search space is halved at each step.
- **Average case:** O(log n).

### Why O(log n)?

Each comparison eliminates half the remaining elements. For a list of 1,000,000 items, binary search needs at most about 20 comparisons (since log2(1,000,000) is approximately 20). Linear search would need up to 1,000,000 comparisons.

---

## Comparison of Searching Algorithms

| Feature | Linear Search | Binary Search |
|---|---|---|
| **Data must be sorted?** | No | Yes |
| **Best case** | O(1) | O(1) |
| **Worst case** | O(n) | O(log n) |
| **Average case** | O(n) | O(log n) |
| **Implementation complexity** | Very simple | Slightly more complex |
| **Suitable for** | Small or unsorted data sets | Large, sorted data sets |
| **Works on linked lists?** | Yes (efficiently) | Not efficiently (no random access) |

<div class="exam-tip" markdown="1">
A common exam question asks you to explain **when** you would use each algorithm. If the data is unsorted and small, linear search is appropriate. If the data is sorted and large, binary search is far more efficient. Remember: binary search **requires sorted data** -- if the data is unsorted, the cost of sorting it first must be considered.
</div>

---

## Bubble Sort

<div class="key-term" markdown="1">
**Bubble sort** is a simple sorting algorithm that repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. The largest unsorted value "bubbles up" to the end of the list on each pass.
</div>

### How It Works

1. Start at the beginning of the list.
2. Compare the first two adjacent elements. If the first is greater than the second, swap them.
3. Move to the next pair and repeat the comparison and swap.
4. Continue until the end of the list -- this completes one **pass**. The largest element is now in its correct position.
5. Repeat passes for the remaining unsorted portion of the list.
6. If a complete pass is made with no swaps, the list is sorted and the algorithm terminates early.

### Code Examples

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
            break  # List is already sorted
    return data

# Example usage
numbers = [64, 34, 25, 12, 22, 11, 90]
print(bubble_sort(numbers))
# Output: [11, 12, 22, 25, 34, 64, 90]
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
        If Not swapped Then
            Exit For  ' List is already sorted
        End If
    Next
End Sub

' Example usage
Dim numbers() As Integer = {64, 34, 25, 12, 22, 11, 90}
BubbleSort(numbers)
For Each num As Integer In numbers
    Console.Write(num & " ")
Next
' Output: 11 12 22 25 34 64 90
```

### Performance

- **Best case:** O(n) -- the list is already sorted (only one pass with no swaps needed).
- **Worst case:** O(n^2) -- the list is in reverse order.
- **Average case:** O(n^2).
- **Space complexity:** O(1) -- it sorts in place (no additional memory needed beyond a temporary swap variable).

---

## Insertion Sort

<div class="key-term" markdown="1">
**Insertion sort** builds the sorted list one element at a time. It takes each element from the unsorted portion and inserts it into its correct position within the sorted portion, shifting elements as necessary.
</div>

### How It Works

1. Consider the first element as a sorted sub-list of one element.
2. Take the next element (the "key") from the unsorted portion.
3. Compare the key with each element in the sorted portion, moving from right to left.
4. Shift elements in the sorted portion one position to the right to make space.
5. Insert the key into its correct position.
6. Repeat until all elements have been processed.

### Code Examples

```python
def insertion_sort(data):
    for i in range(1, len(data)):
        key = data[i]
        j = i - 1
        while j >= 0 and data[j] > key:
            data[j + 1] = data[j]  # Shift element to the right
            j -= 1
        data[j + 1] = key  # Insert key in correct position
    return data

# Example usage
numbers = [12, 11, 13, 5, 6]
print(insertion_sort(numbers))
# Output: [5, 6, 11, 12, 13]
```

```vb
Sub InsertionSort(data() As Integer)
    For i As Integer = 1 To data.Length - 1
        Dim key As Integer = data(i)
        Dim j As Integer = i - 1
        While j >= 0 AndAlso data(j) > key
            data(j + 1) = data(j)  ' Shift element to the right
            j -= 1
        End While
        data(j + 1) = key  ' Insert key in correct position
    Next
End Sub

' Example usage
Dim numbers() As Integer = {12, 11, 13, 5, 6}
InsertionSort(numbers)
For Each num As Integer In numbers
    Console.Write(num & " ")
Next
' Output: 5 6 11 12 13
```

### Performance

- **Best case:** O(n) -- the list is already sorted (no shifts needed, just one comparison per element).
- **Worst case:** O(n^2) -- the list is in reverse order.
- **Average case:** O(n^2).
- **Space complexity:** O(1) -- it sorts in place.

### When Is Insertion Sort Useful?

- When the data set is **small**.
- When the data is **nearly sorted** (it performs very well in this case, approaching O(n)).
- It is an **online** algorithm -- it can sort a list as it receives new data.

---

## Merge Sort

<div class="key-term" markdown="1">
**Merge sort** is a **divide and conquer** sorting algorithm. It recursively splits the list into halves until each sub-list contains a single element, then merges the sub-lists back together in sorted order.
</div>

### How It Works

1. **Divide:** Split the list into two halves.
2. **Conquer:** Recursively apply merge sort to each half.
3. **Merge:** Combine the two sorted halves into a single sorted list by comparing elements from each half and placing the smaller one first.

**Worked example with [38, 27, 43, 3]:**

```
Step 1 (Divide):  [38, 27, 43, 3]
                  /                \
             [38, 27]           [43, 3]
             /      \           /      \
           [38]    [27]       [43]    [3]

Step 2 (Merge):
           [38]    [27]       [43]    [3]
             \      /           \      /
             [27, 38]           [3, 43]
                  \                /
              [3, 27, 38, 43]
```

### Code Examples

```python
def merge_sort(data):
    if len(data) <= 1:
        return data

    mid = len(data) // 2
    left_half = merge_sort(data[:mid])
    right_half = merge_sort(data[mid:])

    return merge(left_half, right_half)

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

    # Add any remaining elements
    result.extend(left[i:])
    result.extend(right[j:])
    return result

# Example usage
numbers = [38, 27, 43, 3, 9, 82, 10]
print(merge_sort(numbers))
# Output: [3, 9, 10, 27, 38, 43, 82]
```

```vb
Function MergeSort(data() As Integer) As Integer()
    If data.Length <= 1 Then
        Return data
    End If

    Dim mid As Integer = data.Length \ 2
    Dim leftHalf(mid - 1) As Integer
    Dim rightHalf(data.Length - mid - 1) As Integer

    Array.Copy(data, 0, leftHalf, 0, mid)
    Array.Copy(data, mid, rightHalf, 0, data.Length - mid)

    leftHalf = MergeSort(leftHalf)
    rightHalf = MergeSort(rightHalf)

    Return Merge(leftHalf, rightHalf)
End Function

Function Merge(left() As Integer, right() As Integer) As Integer()
    Dim result(left.Length + right.Length - 1) As Integer
    Dim i As Integer = 0
    Dim j As Integer = 0
    Dim k As Integer = 0

    While i < left.Length AndAlso j < right.Length
        If left(i) <= right(j) Then
            result(k) = left(i)
            i += 1
        Else
            result(k) = right(j)
            j += 1
        End If
        k += 1
    End While

    While i < left.Length
        result(k) = left(i)
        i += 1
        k += 1
    End While

    While j < right.Length
        result(k) = right(j)
        j += 1
        k += 1
    End While

    Return result
End Function

' Example usage
Dim numbers() As Integer = {38, 27, 43, 3, 9, 82, 10}
Dim sorted() As Integer = MergeSort(numbers)
For Each num As Integer In sorted
    Console.Write(num & " ")
Next
' Output: 3 9 10 27 38 43 82
```

### Performance

- **Best case:** O(n log n).
- **Worst case:** O(n log n).
- **Average case:** O(n log n).
- **Space complexity:** O(n) -- it requires additional memory to hold the sub-lists during merging.

### Why O(n log n)?

The list is divided in half at each level of recursion, giving **log n** levels. At each level, all **n** elements must be compared during the merge step. Therefore, the total work is n multiplied by log n.

---

## Comparison of Sorting Algorithms

| Feature | Bubble Sort | Insertion Sort | Merge Sort |
|---|---|---|---|
| **Best case** | O(n) | O(n) | O(n log n) |
| **Worst case** | O(n^2) | O(n^2) | O(n log n) |
| **Average case** | O(n^2) | O(n^2) | O(n log n) |
| **Space complexity** | O(1) -- in place | O(1) -- in place | O(n) -- extra memory needed |
| **Stable?** | Yes | Yes | Yes |
| **Adaptive?** | Yes (with early exit) | Yes (fast on nearly sorted data) | No |
| **Suitable for** | Small or nearly sorted data | Small or nearly sorted data | Large data sets |
| **Approach** | Comparison and swap | Shift and insert | Divide and conquer |

<div class="key-term" markdown="1">
A **stable** sorting algorithm preserves the relative order of elements with equal keys. All three algorithms covered here (bubble, insertion, merge) are stable.
</div>

<div class="exam-tip" markdown="1">
In the exam you may be asked to recommend a sorting algorithm for a specific scenario. For large data sets, merge sort is preferred because its worst case is O(n log n). For small or nearly sorted data, insertion sort is often the best practical choice. Bubble sort is mainly used for educational purposes due to its simplicity.
</div>

---

## Big O Notation

<div class="key-term" markdown="1">
**Big O notation** is a mathematical notation used to describe the **upper bound** of an algorithm's time complexity or space complexity. It describes how the resource usage of an algorithm grows relative to the input size **n**, focusing on the **worst-case** scenario.
</div>

Big O ignores constants and lower-order terms. For example, an algorithm that takes 3n^2 + 5n + 2 steps is described as O(n^2), because the n^2 term dominates as n grows large.

### Common Big O Complexities

| Notation | Name | Description | Example |
|---|---|---|---|
| **O(1)** | Constant | The time taken does not depend on the input size. | Accessing an array element by index; checking if a number is odd/even. |
| **O(log n)** | Logarithmic | The time grows logarithmically. The algorithm halves the problem size at each step. | Binary search. |
| **O(n)** | Linear | The time grows in direct proportion to the input size. | Linear search; summing all elements in a list. |
| **O(n log n)** | Linearithmic | A combination of linear and logarithmic growth. Common in efficient sorting. | Merge sort; the best comparison-based sorts. |
| **O(n^2)** | Quadratic | The time grows as the square of the input size. Typically caused by nested loops. | Bubble sort; insertion sort (worst case). |
| **O(2^n)** | Exponential | The time doubles with each additional input element. Very slow for even moderate n. | Recursive Fibonacci (naive); brute-force subset enumeration. |
| **O(n!)** | Factorial | The time grows factorially. Extremely slow; only practical for very small n. | Travelling Salesman Problem (brute-force); generating all permutations. |

### Growth Rate Comparison

For an input of size n = 1,000:

| Complexity | Approximate Operations |
|---|---|
| O(1) | 1 |
| O(log n) | 10 |
| O(n) | 1,000 |
| O(n log n) | 10,000 |
| O(n^2) | 1,000,000 |
| O(2^n) | Astronomically large (impractical) |

### Time Complexity vs Space Complexity

- **Time complexity** measures how the **running time** of an algorithm grows with input size.
- **Space complexity** measures how the **memory usage** of an algorithm grows with input size.

For example, merge sort has time complexity O(n log n) but space complexity O(n) because it requires additional arrays during merging. Bubble sort has time complexity O(n^2) but space complexity O(1) because it sorts in place.

<div class="exam-tip" markdown="1">
You must be able to identify the Big O complexity of the standard algorithms: linear search is O(n), binary search is O(log n), bubble sort is O(n^2), insertion sort is O(n^2), and merge sort is O(n log n). You should also be able to explain **why** each algorithm has its particular complexity.
</div>

---

## Recursion vs Iteration

<div class="key-term" markdown="1">
**Recursion** is a technique where a function calls itself to solve a smaller instance of the same problem. Each recursive call works towards a **base case** that stops the recursion. **Iteration** uses loops (for, while) to repeat a block of code.
</div>

### Structure of a Recursive Function

Every recursive function must have:
1. A **base case** -- a condition that stops the recursion and returns a value directly.
2. A **recursive case** -- the function calls itself with a modified argument that moves towards the base case.

### Example: Factorial

The factorial of n (written n!) is defined as:
- 0! = 1 (base case)
- n! = n * (n-1)! (recursive case)

**Recursive approach:**

```python
def factorial_recursive(n):
    if n == 0:        # Base case
        return 1
    else:             # Recursive case
        return n * factorial_recursive(n - 1)

print(factorial_recursive(5))  # Output: 120
```

```vb
Function FactorialRecursive(n As Integer) As Integer
    If n = 0 Then        ' Base case
        Return 1
    Else                 ' Recursive case
        Return n * FactorialRecursive(n - 1)
    End If
End Function

Console.WriteLine(FactorialRecursive(5))  ' Output: 120
```

**Iterative approach:**

```python
def factorial_iterative(n):
    result = 1
    for i in range(1, n + 1):
        result = result * i
    return result

print(factorial_iterative(5))  # Output: 120
```

```vb
Function FactorialIterative(n As Integer) As Integer
    Dim result As Integer = 1
    For i As Integer = 1 To n
        result = result * i
    Next
    Return result
End Function

Console.WriteLine(FactorialIterative(5))  ' Output: 120
```

### Example: Fibonacci Sequence

```python
# Recursive Fibonacci
def fibonacci_recursive(n):
    if n <= 1:          # Base case
        return n
    else:               # Recursive case
        return fibonacci_recursive(n - 1) + fibonacci_recursive(n - 2)

# Iterative Fibonacci
def fibonacci_iterative(n):
    if n <= 1:
        return n
    a, b = 0, 1
    for i in range(2, n + 1):
        a, b = b, a + b
    return b

print(fibonacci_recursive(7))   # Output: 13
print(fibonacci_iterative(7))   # Output: 13
```

```vb
' Recursive Fibonacci
Function FibonacciRecursive(n As Integer) As Integer
    If n <= 1 Then          ' Base case
        Return n
    Else                    ' Recursive case
        Return FibonacciRecursive(n - 1) + FibonacciRecursive(n - 2)
    End If
End Function

' Iterative Fibonacci
Function FibonacciIterative(n As Integer) As Integer
    If n <= 1 Then
        Return n
    End If
    Dim a As Integer = 0
    Dim b As Integer = 1
    For i As Integer = 2 To n
        Dim temp As Integer = b
        b = a + b
        a = temp
    Next
    Return b
End Function

Console.WriteLine(FibonacciRecursive(7))   ' Output: 13
Console.WriteLine(FibonacciIterative(7))   ' Output: 13
```

### Comparison Table

| Feature | Recursion | Iteration |
|---|---|---|
| **Uses** | Function calls itself | Loop constructs (for, while) |
| **Termination** | Base case | Loop condition becomes false |
| **Memory usage** | Higher (each call adds to the call stack) | Lower (no call stack overhead) |
| **Risk** | Stack overflow if base case not reached or recursion too deep | Infinite loop if condition never met |
| **Readability** | Often more elegant and closer to mathematical definitions | Can be more straightforward for simple repetition |
| **Speed** | Often slower due to function call overhead | Usually faster |
| **Best for** | Problems with recursive structure (trees, divide and conquer) | Simple repetition and counting |

<div class="exam-tip" markdown="1">
A common exam question asks you to explain the advantages and disadvantages of recursion versus iteration. Always mention the **call stack**: each recursive call adds a new frame to the call stack, which uses memory. If the recursion is too deep, this can cause a **stack overflow** error.
</div>

---

## Trace Tables

<div class="key-term" markdown="1">
A **trace table** is a technique used to **dry-run** an algorithm by recording the values of variables at each step of execution. It is used to check the correctness of an algorithm and to understand its behaviour.
</div>

### How to Create a Trace Table

1. Create a column for each variable in the algorithm.
2. Add a column for any output.
3. Add a column for the condition being tested (optional but helpful).
4. Work through the algorithm step by step, recording the value of each variable after every instruction that changes it.

### Example: Tracing a Linear Search

Algorithm to search for the value 5 in the list [3, 8, 5, 1]:

```
data = [3, 8, 5, 1]
target = 5
FOR i FROM 0 TO 3
    IF data[i] == target THEN
        OUTPUT i
    END IF
END FOR
```

**Trace table:**

| Step | i | data[i] | data[i] == target? | Output |
|---|---|---|---|---|
| 1 | 0 | 3 | No | -- |
| 2 | 1 | 8 | No | -- |
| 3 | 2 | 5 | Yes | 2 |
| 4 | 3 | 1 | No | -- |

### Example: Tracing a Bubble Sort Pass

First pass of bubble sort on [5, 3, 8, 1]:

| Step | j | data[j] | data[j+1] | Swap? | List after step |
|---|---|---|---|---|---|
| 1 | 0 | 5 | 3 | Yes | [3, 5, 8, 1] |
| 2 | 1 | 5 | 8 | No | [3, 5, 8, 1] |
| 3 | 2 | 8 | 1 | Yes | [3, 5, 1, 8] |

After the first pass, the largest value (8) has "bubbled" to the end.

### Example: Tracing Recursion

Tracing `factorial_recursive(4)`:

| Call | n | n == 0? | Returns |
|---|---|---|---|
| factorial_recursive(4) | 4 | No | 4 * factorial_recursive(3) |
| factorial_recursive(3) | 3 | No | 3 * factorial_recursive(2) |
| factorial_recursive(2) | 2 | No | 2 * factorial_recursive(1) |
| factorial_recursive(1) | 1 | No | 1 * factorial_recursive(0) |
| factorial_recursive(0) | 0 | Yes | 1 |

Now the returns unwind: 1 * 1 = 1, then 2 * 1 = 2, then 3 * 2 = 6, then 4 * 6 = **24**.

<div class="exam-tip" markdown="1">
Trace tables are a very common exam question. Practise by tracing through algorithms by hand. Always work **methodically** -- update one variable at a time and do not skip steps. For recursive algorithms, show the chain of calls and the order in which values are returned.
</div>

---

## Data Compression

Compression reduces file size, making data faster to transmit and requiring less storage. At AS level you need to understand both categories and specific algorithms.

### Lossless vs Lossy Compression

| Feature | Lossless | Lossy |
|---------|----------|-------|
| **Data loss** | None — original data perfectly reconstructed | Some data permanently removed |
| **File size** | Larger than lossy | Smaller than lossless |
| **Use cases** | Text, code, spreadsheets, medical images, archives | Photos, music, video, streaming |
| **File formats** | ZIP, PNG, GIF, FLAC, 7Z | JPEG, MP3, MP4/MPEG, AAC |
| **How it works** | Identifies and encodes patterns/redundancy | Removes data humans are unlikely to notice |

<div class="key-term" markdown="1">
**Lossless compression** reduces file size while allowing the original data to be perfectly reconstructed. **Lossy compression** achieves greater size reduction by permanently removing some data, meaning the original cannot be fully restored.
</div>

---

### Run-Length Encoding (RLE)

RLE is a **lossless** algorithm that replaces consecutive runs of the same value with a **count** and the **value**.

#### Worked Example

**Original data:** `AAAAAABBBBCCDDDDDDD`

| Run | Count | Value | Encoded |
|-----|-------|-------|---------|
| AAAAAA | 6 | A | 6A |
| BBBB | 4 | B | 4B |
| CC | 2 | C | 2C |
| DDDDDDD | 7 | D | 7D |

**Encoded:** `6A4B2C7D`

**Space calculation:**
- Original: 19 characters (19 bytes if 1 byte per character)
- Encoded: 8 characters (8 bytes)
- Saving: (19 - 8) / 19 × 100 = **57.9%**

#### When RLE Works Well vs Poorly

- **Works well:** Data with long runs of repeated values — simple graphics, icons, diagrams, fax documents
- **Works poorly:** Data with little repetition — photographs, random data. The encoded version may be **larger** than the original (e.g. `ABCDEF` → `1A1B1C1D1E1F` is longer)

```python
# Python — Simple RLE encoding
def rle_encode(data):
    encoded = ""
    i = 0
    while i < len(data):
        count = 1
        while i + count < len(data) and data[i + count] == data[i]:
            count += 1
        encoded += str(count) + data[i]
        i += count
    return encoded

def rle_decode(encoded):
    decoded = ""
    i = 0
    while i < len(encoded):
        count = ""
        while encoded[i].isdigit():
            count += encoded[i]
            i += 1
        decoded += encoded[i] * int(count)
        i += 1
    return decoded

original = "AAAAAABBBBCCDDDDDDD"
compressed = rle_encode(original)
print(f"Original:    {original} ({len(original)} chars)")
print(f"Compressed:  {compressed} ({len(compressed)} chars)")
print(f"Decompressed: {rle_decode(compressed)}")
```

```vb
' VB.NET — Simple RLE encoding
Function RLEEncode(data As String) As String
    Dim encoded As String = ""
    Dim i As Integer = 0
    While i < data.Length
        Dim count As Integer = 1
        While i + count < data.Length AndAlso data(i + count) = data(i)
            count += 1
        End While
        encoded &= count.ToString() & data(i)
        i += count
    End While
    Return encoded
End Function

Dim original As String = "AAAAAABBBBCCDDDDDDD"
Dim compressed As String = RLEEncode(original)
Console.WriteLine("Original:   " & original & " (" & original.Length & " chars)")
Console.WriteLine("Compressed: " & compressed & " (" & compressed.Length & " chars)")
```

---

### Dictionary-Based (LZ) Compression

Dictionary-based compression (named after Lempel and Ziv — LZ77, LZ78, LZW) builds a **dictionary** of recurring patterns in the data and replaces them with shorter **codes**.

#### How It Works

1. The algorithm scans the data and identifies **repeated sequences**
2. Each unique sequence is added to a **dictionary** with a short index code
3. Subsequent occurrences of the sequence are replaced with the dictionary code
4. The dictionary is stored with the compressed data so it can be decoded

#### Worked Example

**Original text:** `THE CAT SAT ON THE MAT`

| Dictionary Index | Entry |
|-----------------|-------|
| 0 | THE |
| 1 | CAT |
| 2 | SAT |
| 3 | ON |
| 4 | MAT |

**Encoded:** `0 1 2 3 0 4` (plus spaces/structure)

The word "THE" appears twice but is only stored once in the dictionary. The second occurrence is replaced by its index code (0), saving space.

**Key characteristics:**
- **Lossless** — original data is perfectly reconstructed using the dictionary
- More effective than RLE for **text and general-purpose** compression
- Used in **ZIP**, **GIF**, **PNG**, and **PDF** formats
- Effectiveness depends on how much repetition exists in the data

---

### Huffman Encoding

Huffman encoding is a **lossless** algorithm that assigns **variable-length binary codes** to characters based on their **frequency**. More frequent characters get **shorter codes**, less frequent characters get **longer codes**.

#### How It Works

1. **Count the frequency** of each character in the data
2. Build a **binary tree** by repeatedly combining the two lowest-frequency characters
3. Assign binary codes by traversing the tree (left = 0, right = 1)
4. Replace each character with its Huffman code

#### Worked Example

**Text:** `AABBBCCCCDDDD` (14 characters)

**Step 1 — Frequency count:**

| Character | Frequency |
|-----------|-----------|
| A | 2 |
| B | 3 |
| C | 4 |
| D | 5 |

**Step 2 — Build the tree** (combine two smallest repeatedly):
- Combine A(2) + B(3) = AB(5)
- Combine C(4) + AB(5) = CAB(9)
- Combine D(5) + CAB(9) = Root(14)

**Step 3 — Assign codes** (traversing the tree):

| Character | Code | Code Length |
|-----------|------|-------------|
| D | 0 | 1 bit |
| C | 10 | 2 bits |
| A | 111 | 3 bits |
| B | 110 | 3 bits |

**Step 4 — Encode:**
`AABBBCCCCDDDD` → `111 111 110 110 110 10 10 10 10 0 0 0 0 0`

**Space calculation:**
- Using fixed-length codes (e.g. ASCII 7-bit): 14 × 7 = **98 bits**
- Using Huffman codes: (2×3) + (3×3) + (4×2) + (5×1) = 6 + 9 + 8 + 5 = **28 bits**
- Saving: (98 - 28) / 98 × 100 = **71.4%**

(The dictionary must also be stored, adding some overhead, but for large files the savings are substantial.)

<div class="exam-tip" markdown="1">
In exam questions on Huffman coding, you may be asked to: (1) build a frequency table, (2) construct the Huffman tree, (3) determine the codes for each character, or (4) calculate the space saving compared to fixed-length encoding. Always show your working clearly. Remember that more frequent characters get **shorter** codes — this is the key insight that makes Huffman efficient.
</div>

---

### Compression File Formats Summary

| Format | Type | Algorithm | Typical Use |
|--------|------|-----------|-------------|
| **ZIP** | Lossless | LZ + Huffman (DEFLATE) | General file archiving |
| **PNG** | Lossless | LZ + filtering | Web graphics, screenshots, diagrams |
| **GIF** | Lossless | LZW | Simple animations, icons |
| **FLAC** | Lossless | Linear prediction + Rice coding | High-quality audio archiving |
| **7Z** | Lossless | LZMA | High-ratio file archiving |
| **JPEG** | Lossy | DCT + quantisation + Huffman | Photographs |
| **MP3** | Lossy | Psychoacoustic model + Huffman | Music, podcasts |
| **MP4/MPEG** | Lossy | Motion estimation + DCT | Video |
| **AAC** | Lossy | Improved psychoacoustic model | Music streaming (Apple, YouTube) |

<div class="exam-tip" markdown="1">
When recommending a compression method, consider the **type of data** and whether **quality loss is acceptable**. Text files and program code must use **lossless** compression (any data loss would corrupt them). Photos and music can use **lossy** compression because small quality reductions are often imperceptible.
</div>
