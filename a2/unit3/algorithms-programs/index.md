---
layout: topic
title: "Algorithms & Programs"
level: "A2 Level"
level_url: "/a2/"
unit_name: "Unit 3: Programming & System Development"
unit_url: "/a2/unit3/"
subtopics:
  - "Algorithm definition; pseudo-code and flowcharts"
  - "Recursion in algorithms and programs"
  - "Potential elegance of recursive approach"
  - "Validation and verification techniques"
  - "Sorting algorithms: Recursive and non-recursive"
  - "Merge sort: Describe characteristics"
  - "Quick sort: Describe characteristics"
  - "Compare efficiency of sorting algorithms"
  - "Searching: Tree-based data structures"
  - "Big O notation for time and space complexity"
  - "Reverse Polish (postfix) notation"
  - "Convert infix to postfix notation"
  - "Evaluate postfix expressions"
  - "Binary expression trees from postfix notation"
---

## Recursion

<div class="key-term" markdown="1">
**Recursion** -- a technique in which a function (or procedure) calls itself in order to solve a problem. Every recursive solution must have a **base case** (a condition that stops the recursion) and a **recursive case** (where the function calls itself with a smaller or simpler input).
</div>

### Base Case and Recursive Case

Every recursive function has two essential parts:

- **Base case:** The simplest instance of the problem that can be answered directly without further recursion. Without a base case, the recursion would continue forever (in practice, until the call stack overflows).
- **Recursive case:** The function calls itself with a modified argument that moves closer to the base case.

### The Call Stack and Stack Frames

<div class="key-term" markdown="1">
**Call stack** -- a region of memory that stores information about active function calls. Each time a function is called, a new **stack frame** is pushed onto the call stack containing the function's local variables, parameters, and return address. When the function returns, its frame is popped off the stack.
</div>

When a recursive function calls itself, each call creates a new stack frame. These frames accumulate on the stack until a base case is reached. Then, the frames are popped one by one as each call returns its result to the caller.

**Key points about the call stack:**

- The stack has a **finite size**. Too many recursive calls cause a **stack overflow**.
- Each stack frame stores the function's **local variables**, **parameters**, and the **return address** (where to resume after the call returns).
- Frames are processed in **LIFO** (Last In, First Out) order.

### Example: Factorial

The factorial of n is defined as:

- 0! = 1 (base case)
- n! = n x (n-1)! for n > 0 (recursive case)

```python
def factorial(n):
    if n == 0:          # Base case
        return 1
    else:               # Recursive case
        return n * factorial(n - 1)

print(factorial(5))     # Output: 120
```

```vb
Function Factorial(n As Integer) As Long
    If n = 0 Then       ' Base case
        Return 1
    Else                 ' Recursive case
        Return n * Factorial(n - 1)
    End If
End Function

Sub Main()
    Console.WriteLine(Factorial(5))   ' Output: 120
End Sub
```

**Tracing the call stack for `factorial(4)`:**

| Call | Stack state (top to bottom) | Returns |
|------|----------------------------|---------|
| factorial(4) | factorial(4) | 4 * factorial(3) |
| factorial(3) | factorial(3), factorial(4) | 3 * factorial(2) |
| factorial(2) | factorial(2), factorial(3), factorial(4) | 2 * factorial(1) |
| factorial(1) | factorial(1), factorial(2), factorial(3), factorial(4) | 1 * factorial(0) |
| factorial(0) | factorial(0), factorial(1), factorial(2), factorial(3), factorial(4) | 1 (base case) |

Then the stack unwinds: 1 * 1 = 1, then 2 * 1 = 2, then 3 * 2 = 6, then 4 * 6 = **24**.

### Example: Fibonacci

The Fibonacci sequence is defined as:

- fib(0) = 0 (base case)
- fib(1) = 1 (base case)
- fib(n) = fib(n-1) + fib(n-2) for n > 1 (recursive case)

```python
def fibonacci(n):
    if n == 0:              # Base case 1
        return 0
    elif n == 1:            # Base case 2
        return 1
    else:                   # Recursive case
        return fibonacci(n - 1) + fibonacci(n - 2)

for i in range(10):
    print(fibonacci(i), end=" ")
# Output: 0 1 1 2 3 5 8 13 21 34
```

```vb
Function Fibonacci(n As Integer) As Long
    If n = 0 Then            ' Base case 1
        Return 0
    ElseIf n = 1 Then        ' Base case 2
        Return 1
    Else                      ' Recursive case
        Return Fibonacci(n - 1) + Fibonacci(n - 2)
    End If
End Function

Sub Main()
    For i As Integer = 0 To 9
        Console.Write(Fibonacci(i) & " ")
    Next
    ' Output: 0 1 1 2 3 5 8 13 21 34
End Sub
```

<div class="exam-tip" markdown="1">
The naive recursive Fibonacci is extremely inefficient because it recalculates the same values many times. For example, `fibonacci(5)` calls `fibonacci(3)` twice and `fibonacci(2)` three times. Its time complexity is O(2^n). This is a classic exam point -- you may be asked to contrast this with the O(n) iterative approach.
</div>

---

## Elegance of Recursion vs Iteration

<div class="key-term" markdown="1">
**Elegance** in programming refers to a solution that is concise, clear, and closely mirrors the mathematical or logical definition of the problem. Recursive solutions are often considered elegant because they express the problem in terms of itself.
</div>

### Comparison

| Aspect | Recursion | Iteration |
|--------|-----------|-----------|
| Code length | Often shorter and more readable | May require more code (loop, variables) |
| Mirrors definition | Directly reflects mathematical definitions | Must manually manage state |
| Memory usage | Uses call stack space (O(n) or more) | Typically O(1) extra space |
| Risk of overflow | Stack overflow for deep recursion | No stack overflow risk |
| Performance | Function call overhead per recursion | Generally faster due to no call overhead |
| Suitability | Tree traversals, divide-and-conquer, backtracking | Simple loops, accumulation |

### Factorial: Recursive vs Iterative

```python
# Recursive -- elegant but uses O(n) stack space
def factorial_recursive(n):
    if n == 0:
        return 1
    return n * factorial_recursive(n - 1)

# Iterative -- less elegant but O(1) extra space
def factorial_iterative(n):
    result = 1
    for i in range(2, n + 1):
        result *= i
    return result
```

```vb
' Recursive
Function FactorialRecursive(n As Integer) As Long
    If n = 0 Then Return 1
    Return n * FactorialRecursive(n - 1)
End Function

' Iterative
Function FactorialIterative(n As Integer) As Long
    Dim result As Long = 1
    For i As Integer = 2 To n
        result *= i
    Next
    Return result
End Function
```

### When Recursion is Truly Elegant

Some problems are **naturally recursive** and become awkward or complex when written iteratively:

- **Tree traversals** -- visiting every node in a binary tree is naturally expressed recursively.
- **Divide-and-conquer algorithms** -- merge sort and quick sort split the problem into subproblems.
- **Backtracking** -- problems like maze solving or the N-queens puzzle benefit from recursive exploration of possibilities.

For these problems, an iterative solution would require manually managing a stack data structure, which is essentially reimplementing what the call stack does automatically.

<div class="exam-tip" markdown="1">
The WJEC specification specifically asks about the "potential elegance" of recursion. Be prepared to argue **both sides**: recursion is elegant because it is concise and mirrors the problem definition, but iteration is sometimes preferable for performance and memory reasons. Always mention the trade-off.
</div>

---

## Merge Sort

<div class="key-term" markdown="1">
**Merge sort** -- a divide-and-conquer sorting algorithm that recursively splits a list in half, sorts each half, and then merges the two sorted halves back together. It is a **stable** sort with a guaranteed time complexity of **O(n log n)** in all cases.
</div>

### Algorithm

1. **Divide:** If the list has more than one element, split it into two roughly equal halves.
2. **Conquer:** Recursively sort each half.
3. **Merge:** Combine the two sorted halves into one sorted list by comparing elements from the front of each half and appending the smaller one.

### Worked Example

Sort the list: **[38, 27, 43, 3, 9, 82, 10]**

**Splitting phase:**

```
[38, 27, 43, 3, 9, 82, 10]
         /              \
  [38, 27, 43]      [3, 9, 82, 10]
    /      \           /         \
 [38]   [27, 43]   [3, 9]    [82, 10]
         /   \      /   \      /    \
       [27] [43]  [3]   [9] [82]  [10]
```

**Merging phase (bottom-up):**

```
       [27] [43]  -->  [27, 43]
 [38] + [27, 43]  -->  [27, 38, 43]

       [3] [9]    -->  [3, 9]
       [82] [10]  -->  [10, 82]
 [3, 9] + [10, 82]  -->  [3, 9, 10, 82]

 [27, 38, 43] + [3, 9, 10, 82]  -->  [3, 9, 10, 27, 38, 43, 82]
```

### Code

```python
def merge_sort(arr):
    if len(arr) <= 1:              # Base case
        return arr

    mid = len(arr) // 2
    left = merge_sort(arr[:mid])   # Recursively sort left half
    right = merge_sort(arr[mid:])  # Recursively sort right half

    return merge(left, right)

def merge(left, right):
    """Merge two sorted lists into one sorted list."""
    result = []
    i = 0   # Pointer for left list
    j = 0   # Pointer for right list

    while i < len(left) and j < len(right):
        if left[i] <= right[j]:    # <= ensures stability
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1

    # Append any remaining elements
    result.extend(left[i:])
    result.extend(right[j:])
    return result

data = [38, 27, 43, 3, 9, 82, 10]
print(merge_sort(data))
# Output: [3, 9, 10, 27, 38, 43, 82]
```

```vb
Function MergeSort(arr As List(Of Integer)) As List(Of Integer)
    If arr.Count <= 1 Then       ' Base case
        Return arr
    End If

    Dim mid As Integer = arr.Count \ 2
    Dim left As List(Of Integer) = MergeSort(arr.GetRange(0, mid))
    Dim right As List(Of Integer) = MergeSort(arr.GetRange(mid, arr.Count - mid))

    Return Merge(left, right)
End Function

Function Merge(left As List(Of Integer), right As List(Of Integer)) As List(Of Integer)
    Dim result As New List(Of Integer)
    Dim i As Integer = 0
    Dim j As Integer = 0

    While i < left.Count AndAlso j < right.Count
        If left(i) <= right(j) Then   ' <= ensures stability
            result.Add(left(i))
            i += 1
        Else
            result.Add(right(j))
            j += 1
        End If
    End While

    ' Append remaining elements
    While i < left.Count
        result.Add(left(i))
        i += 1
    End While
    While j < right.Count
        result.Add(right(j))
        j += 1
    End While

    Return result
End Function

Sub Main()
    Dim data As New List(Of Integer) From {38, 27, 43, 3, 9, 82, 10}
    Dim sorted As List(Of Integer) = MergeSort(data)
    Console.WriteLine(String.Join(", ", sorted))
    ' Output: 3, 9, 10, 27, 38, 43, 82
End Sub
```

### Characteristics of Merge Sort

| Characteristic | Detail |
|---------------|--------|
| Type | Divide and conquer |
| Time complexity (best) | O(n log n) |
| Time complexity (average) | O(n log n) |
| Time complexity (worst) | O(n log n) |
| Space complexity | O(n) -- requires additional space for merging |
| Stable | **Yes** -- equal elements maintain their original relative order |
| In-place | **No** -- requires O(n) extra memory |
| Recursive | Yes |

<div class="exam-tip" markdown="1">
Merge sort **always** takes O(n log n) time regardless of the initial order of the data. This makes it predictable, but it uses O(n) extra memory. This is a key distinction from quick sort, which is in-place but has a worse worst case.
</div>

---

## Quick Sort

<div class="key-term" markdown="1">
**Quick sort** -- a divide-and-conquer sorting algorithm that selects a **pivot** element, partitions the list into elements less than the pivot and elements greater than the pivot, then recursively sorts the two partitions. Average time complexity is **O(n log n)** but worst case is **O(n^2)**.
</div>

### Algorithm

1. **Choose a pivot** -- commonly the first element, last element, middle element, or a random element.
2. **Partition** -- rearrange elements so that all elements less than the pivot are to its left, and all elements greater are to its right. The pivot is now in its final sorted position.
3. **Recurse** -- recursively apply quick sort to the left partition and the right partition.
4. **Base case** -- a list with 0 or 1 elements is already sorted.

### Pivot Selection

The choice of pivot affects performance:

| Strategy | Description | Risk |
|----------|-------------|------|
| First element | Simple but poor for already-sorted data | O(n^2) on sorted input |
| Last element | Simple but same risk as first | O(n^2) on sorted input |
| Middle element | Reasonable compromise | Less likely to hit worst case |
| Median-of-three | Median of first, middle, last | Good balance of simplicity and performance |
| Random | Choose a random element | Statistically avoids worst case |

### Worked Example

Sort the list: **[7, 2, 1, 6, 8, 5, 3, 4]** using last element as pivot.

**Pass 1:** Pivot = 4

Partition around 4: elements < 4 go left, elements > 4 go right.

```
[2, 1, 3] [4] [7, 6, 8, 5]
```

4 is now in its final position (index 3).

**Pass 2a:** Sort left partition [2, 1, 3], pivot = 3

```
[2, 1] [3]
```

3 is in its final position.

**Pass 2b:** Sort right partition [7, 6, 8, 5], pivot = 5

```
[5] [7, 6, 8]
```

5 is in its final position.

**Pass 3a:** Sort [2, 1], pivot = 1

```
[1] [2]
```

**Pass 3b:** Sort [7, 6, 8], pivot = 8

```
[7, 6] [8]
```

**Pass 4:** Sort [7, 6], pivot = 6

```
[6] [7]
```

**Final sorted list: [1, 2, 3, 4, 5, 6, 7, 8]**

### Code

```python
def quick_sort(arr):
    if len(arr) <= 1:              # Base case
        return arr

    pivot = arr[-1]                # Choose last element as pivot
    left = []                      # Elements less than pivot
    right = []                     # Elements greater than pivot
    equal = []                     # Elements equal to pivot

    for item in arr:
        if item < pivot:
            left.append(item)
        elif item > pivot:
            right.append(item)
        else:
            equal.append(item)

    return quick_sort(left) + equal + quick_sort(right)

data = [7, 2, 1, 6, 8, 5, 3, 4]
print(quick_sort(data))
# Output: [1, 2, 3, 4, 5, 6, 7, 8]
```

An **in-place** version (more memory-efficient, uses partitioning):

```python
def quick_sort_in_place(arr, low, high):
    if low < high:
        pivot_index = partition(arr, low, high)
        quick_sort_in_place(arr, low, pivot_index - 1)
        quick_sort_in_place(arr, pivot_index + 1, high)

def partition(arr, low, high):
    pivot = arr[high]              # Pivot is last element
    i = low - 1                    # Index of smaller element boundary

    for j in range(low, high):
        if arr[j] <= pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]   # Swap

    arr[i + 1], arr[high] = arr[high], arr[i + 1]  # Place pivot
    return i + 1

data = [7, 2, 1, 6, 8, 5, 3, 4]
quick_sort_in_place(data, 0, len(data) - 1)
print(data)
# Output: [1, 2, 3, 4, 5, 6, 7, 8]
```

```vb
' Simple version (not in-place, easier to understand)
Function QuickSort(arr As List(Of Integer)) As List(Of Integer)
    If arr.Count <= 1 Then         ' Base case
        Return arr
    End If

    Dim pivot As Integer = arr(arr.Count - 1)   ' Last element as pivot
    Dim left As New List(Of Integer)
    Dim right As New List(Of Integer)
    Dim equal As New List(Of Integer)

    For Each item As Integer In arr
        If item < pivot Then
            left.Add(item)
        ElseIf item > pivot Then
            right.Add(item)
        Else
            equal.Add(item)
        End If
    Next

    Dim result As New List(Of Integer)
    result.AddRange(QuickSort(left))
    result.AddRange(equal)
    result.AddRange(QuickSort(right))
    Return result
End Function

' In-place version
Sub QuickSortInPlace(arr As List(Of Integer), low As Integer, high As Integer)
    If low < high Then
        Dim pivotIndex As Integer = Partition(arr, low, high)
        QuickSortInPlace(arr, low, pivotIndex - 1)
        QuickSortInPlace(arr, pivotIndex + 1, high)
    End If
End Sub

Function Partition(arr As List(Of Integer), low As Integer, high As Integer) As Integer
    Dim pivot As Integer = arr(high)
    Dim i As Integer = low - 1

    For j As Integer = low To high - 1
        If arr(j) <= pivot Then
            i += 1
            ' Swap arr(i) and arr(j)
            Dim temp As Integer = arr(i)
            arr(i) = arr(j)
            arr(j) = temp
        End If
    Next

    ' Place pivot in correct position
    Dim temp2 As Integer = arr(i + 1)
    arr(i + 1) = arr(high)
    arr(high) = temp2
    Return i + 1
End Function

Sub Main()
    Dim data As New List(Of Integer) From {7, 2, 1, 6, 8, 5, 3, 4}
    QuickSortInPlace(data, 0, data.Count - 1)
    Console.WriteLine(String.Join(", ", data))
    ' Output: 1, 2, 3, 4, 5, 6, 7, 8
End Sub
```

### Characteristics of Quick Sort

| Characteristic | Detail |
|---------------|--------|
| Type | Divide and conquer |
| Time complexity (best) | O(n log n) |
| Time complexity (average) | O(n log n) |
| Time complexity (worst) | O(n^2) -- when pivot is always smallest or largest |
| Space complexity | O(log n) for the call stack (in-place version) |
| Stable | **No** -- relative order of equal elements may change |
| In-place | **Yes** (in-place version) -- does not require O(n) extra memory |
| Recursive | Yes |

<div class="exam-tip" markdown="1">
Quick sort's worst case O(n^2) occurs when the pivot is consistently the smallest or largest element -- this happens with already-sorted data if you pick the first or last element as pivot. Despite this, quick sort is often **faster in practice** than merge sort because it has better cache performance and lower constant factors. The exam may ask you to identify scenarios where each algorithm is preferable.
</div>

---

## Comparing Sorting Algorithms

The following table compares the key sorting algorithms you need to know at A2 level:

| Algorithm | Best Case | Average Case | Worst Case | Space | Stable | In-Place | Method |
|-----------|-----------|-------------|------------|-------|--------|----------|--------|
| Bubble sort | O(n) | O(n^2) | O(n^2) | O(1) | Yes | Yes | Comparison / swapping |
| Insertion sort | O(n) | O(n^2) | O(n^2) | O(1) | Yes | Yes | Comparison / insertion |
| Merge sort | O(n log n) | O(n log n) | O(n log n) | O(n) | Yes | No | Divide and conquer |
| Quick sort | O(n log n) | O(n log n) | O(n^2) | O(log n) | No | Yes | Divide and conquer |

### Key Points for Comparison

- **Bubble sort and insertion sort** are O(n^2) algorithms. They are simple but only practical for small datasets. Insertion sort is efficient on nearly-sorted data (O(n) best case).
- **Merge sort** guarantees O(n log n) in all cases but requires O(n) extra space. It is the best choice when consistent performance is needed and memory is not constrained.
- **Quick sort** is O(n log n) on average and typically the fastest in practice due to good cache locality. However, its O(n^2) worst case can be a problem. It is in-place (O(log n) stack space).
- For **large datasets**, merge sort and quick sort are preferred. For **small or nearly-sorted datasets**, insertion sort can be very efficient.

<div class="exam-tip" markdown="1">
The exam often asks you to recommend a sorting algorithm for a given scenario. Consider: How large is the dataset? Is memory constrained? Is the data nearly sorted? Is stability required? Use these factors to justify your choice.
</div>

---

## Searching Tree-Based Data Structures

<div class="key-term" markdown="1">
**Binary Search Tree (BST)** -- a binary tree in which, for every node, all values in its left subtree are less than the node's value, and all values in its right subtree are greater than the node's value. This property enables efficient searching.
</div>

### BST Search Algorithm

To search for a value in a BST:

1. Start at the root.
2. If the current node is null, the value is not in the tree -- return "not found".
3. If the value equals the current node's data, return the node -- found.
4. If the value is less than the current node's data, search the **left** subtree.
5. If the value is greater than the current node's data, search the **right** subtree.

This is inherently recursive and mirrors binary search on a sorted array.

### Worked Example

Given this BST:

```
         8
       /   \
      3     10
     / \      \
    1   6     14
       / \   /
      4   7 13
```

**Search for 7:**

- Start at 8. 7 < 8, go left.
- At 3. 7 > 3, go right.
- At 6. 7 > 6, go right.
- At 7. Found.

Visited 4 nodes out of 9. This is much faster than checking all elements.

**Search for 5:**

- Start at 8. 5 < 8, go left.
- At 3. 5 > 3, go right.
- At 6. 5 < 6, go left.
- At 4. 5 > 4, go right.
- Right child is null. Not found.

### Code

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

def bst_search(root, target):
    """Search for a value in a BST. Returns the node if found, None otherwise."""
    if root is None:               # Base case: not found
        return None
    if target == root.data:        # Base case: found
        return root
    elif target < root.data:       # Recursive case: search left
        return bst_search(root.left, target)
    else:                          # Recursive case: search right
        return bst_search(root.right, target)

def bst_insert(root, data):
    """Insert a value into a BST."""
    if root is None:
        return Node(data)
    if data < root.data:
        root.left = bst_insert(root.left, data)
    elif data > root.data:
        root.right = bst_insert(root.right, data)
    return root

# Build the example tree
root = None
for val in [8, 3, 10, 1, 6, 14, 4, 7, 13]:
    root = bst_insert(root, val)

# Search
result = bst_search(root, 7)
print("Found" if result else "Not found")  # Output: Found

result = bst_search(root, 5)
print("Found" if result else "Not found")  # Output: Not found
```

```vb
Class Node
    Public Data As Integer
    Public Left As Node
    Public Right As Node

    Sub New(data As Integer)
        Me.Data = data
        Me.Left = Nothing
        Me.Right = Nothing
    End Sub
End Class

Function BSTSearch(root As Node, target As Integer) As Node
    If root Is Nothing Then          ' Base case: not found
        Return Nothing
    End If
    If target = root.Data Then       ' Base case: found
        Return root
    ElseIf target < root.Data Then   ' Search left
        Return BSTSearch(root.Left, target)
    Else                              ' Search right
        Return BSTSearch(root.Right, target)
    End If
End Function

Function BSTInsert(root As Node, data As Integer) As Node
    If root Is Nothing Then
        Return New Node(data)
    End If
    If data < root.Data Then
        root.Left = BSTInsert(root.Left, data)
    ElseIf data > root.Data Then
        root.Right = BSTInsert(root.Right, data)
    End If
    Return root
End Function

Sub Main()
    Dim root As Node = Nothing
    For Each val As Integer In {8, 3, 10, 1, 6, 14, 4, 7, 13}
        root = BSTInsert(root, val)
    Next

    Dim result As Node = BSTSearch(root, 7)
    Console.WriteLine(If(result IsNot Nothing, "Found", "Not found"))  ' Output: Found

    result = BSTSearch(root, 5)
    Console.WriteLine(If(result IsNot Nothing, "Found", "Not found"))  ' Output: Not found
End Sub
```

### BST Search Complexity

| Case | Time Complexity | When it occurs |
|------|----------------|---------------|
| Best | O(1) | Target is at the root |
| Average | O(log n) | Tree is reasonably balanced |
| Worst | O(n) | Tree is completely unbalanced (degenerates to a linked list) |

The average case O(log n) arises because a balanced BST has a height of approximately log2(n), and each comparison eliminates half the remaining nodes.

---

## Big O Notation

<div class="key-term" markdown="1">
**Big O notation** -- a mathematical notation that describes the **upper bound** of an algorithm's growth rate as the input size increases. It classifies algorithms by how their time or space requirements scale, ignoring constants and lower-order terms. For example, O(n^2) means the time roughly quadruples when the input doubles.
</div>

### Common Time Complexities

| Big O | Name | Description | Example |
|-------|------|-------------|---------|
| O(1) | Constant | Time does not change with input size | Accessing an array element by index |
| O(log n) | Logarithmic | Time increases slowly; halving the problem each step | Binary search |
| O(n) | Linear | Time grows proportionally to input size | Linear search, traversing a list |
| O(n log n) | Linearithmic | Slightly worse than linear; typical of efficient sorts | Merge sort, quick sort (average) |
| O(n^2) | Quadratic | Time grows with the square of input size | Bubble sort, insertion sort (worst), nested loops |
| O(2^n) | Exponential | Time doubles with each additional input element | Naive recursive Fibonacci, brute-force subset enumeration |

### Growth Rate Comparison

For an input of size n, the approximate number of operations:

| n | O(1) | O(log n) | O(n) | O(n log n) | O(n^2) | O(2^n) |
|---|------|----------|------|------------|--------|--------|
| 1 | 1 | 0 | 1 | 0 | 1 | 2 |
| 10 | 1 | 3 | 10 | 33 | 100 | 1,024 |
| 100 | 1 | 7 | 100 | 664 | 10,000 | 1.27 x 10^30 |
| 1,000 | 1 | 10 | 1,000 | 9,966 | 1,000,000 | too large |
| 10,000 | 1 | 13 | 10,000 | 132,877 | 100,000,000 | too large |

This table makes it clear why O(2^n) algorithms are impractical for anything beyond very small inputs, and why O(n log n) sorting algorithms are vastly superior to O(n^2) ones for large datasets.

### Graphical Description of Growth Rates

```
Operations
    ^
    |                                                    / O(2^n)
    |                                                  /
    |                                               /
    |                                            /
    |                                        /
    |                         ___---------- O(n^2)
    |                  __---
    |             __--
    |          _-           ___----------- O(n log n)
    |        /       __----
    |      /    __---
    |     /  _--        __________________ O(n)
    |    / /     ______/
    |   //_____/     _____________________ O(log n)
    |  //___________/
    | //_________________________________  O(1)
    +----------------------------------------------> n
```

### Space Complexity

<div class="key-term" markdown="1">
**Space complexity** -- a measure of how much additional memory an algorithm requires relative to the input size. Like time complexity, it is expressed using Big O notation. It typically measures **auxiliary space** (extra space beyond the input itself).
</div>

| Algorithm | Time Complexity | Space Complexity | Notes |
|-----------|----------------|-----------------|-------|
| Linear search | O(n) | O(1) | Only needs a loop variable |
| Binary search (iterative) | O(log n) | O(1) | Only needs low, high, mid variables |
| Binary search (recursive) | O(log n) | O(log n) | Call stack depth |
| Bubble sort | O(n^2) | O(1) | Sorts in place |
| Merge sort | O(n log n) | O(n) | Needs temporary arrays for merging |
| Quick sort (in-place) | O(n log n) avg | O(log n) | Call stack depth |
| BST search | O(log n) avg | O(log n) recursive / O(1) iterative | Depends on implementation |

<div class="exam-tip" markdown="1">
The exam may ask you to determine the Big O complexity of a given code snippet. Key strategies: count the nesting depth of loops (one loop = O(n), nested loop = O(n^2)), look for halving (suggests O(log n)), and look for recursive calls that split the problem (suggests O(n log n) for divide-and-conquer). Always state the **worst case** unless told otherwise.
</div>

---

## Reverse Polish Notation (Postfix Notation)

<div class="key-term" markdown="1">
**Reverse Polish Notation (RPN)** -- also called **postfix notation** -- is a way of writing arithmetic expressions where the operator comes **after** its operands. For example, the infix expression `3 + 4` is written as `3 4 +` in RPN. It eliminates the need for brackets and operator precedence rules.
</div>

### Why RPN is Used

| Reason | Explanation |
|--------|-------------|
| No brackets needed | Operator order is unambiguous without parentheses |
| No precedence rules | Operators are applied in the order they appear |
| Easy to evaluate | Can be evaluated using a simple stack-based algorithm |
| Efficient for computers | Used internally by compilers and calculators (especially HP calculators) |
| Maps to hardware | Stack-based CPUs can execute postfix directly |

### Infix vs Postfix Examples

| Infix | Postfix (RPN) |
|-------|---------------|
| 3 + 4 | 3 4 + |
| 3 + 4 * 5 | 3 4 5 * + |
| (3 + 4) * 5 | 3 4 + 5 * |
| (A + B) * (C - D) | A B + C D - * |
| A + B * C - D / E | A B C * + D E / - |

---

## Converting Infix to Postfix: The Shunting Yard Algorithm

<div class="key-term" markdown="1">
**Shunting yard algorithm** -- an algorithm invented by Edsger Dijkstra that converts infix expressions to postfix (or prefix) notation using a stack. It processes tokens left to right, using the stack to hold operators temporarily while respecting precedence and associativity.
</div>

### Algorithm Steps

1. Create an empty **operator stack** and an empty **output queue**.
2. Read tokens from left to right:
   - **If the token is a number/operand:** add it directly to the output queue.
   - **If the token is an operator (O1):**
     - While there is an operator O2 on top of the stack, and either:
       - O2 has greater precedence than O1, or
       - O2 has equal precedence and O1 is left-associative
     - Pop O2 from the stack to the output queue.
     - Push O1 onto the stack.
   - **If the token is a left bracket `(`:** push it onto the stack.
   - **If the token is a right bracket `)`:** pop operators from the stack to the output queue until a left bracket is found. Discard both brackets.
3. When all tokens are read, pop all remaining operators from the stack to the output queue.

### Operator Precedence

| Operator | Precedence | Associativity |
|----------|-----------|---------------|
| ^ (power) | 3 (highest) | Right |
| * / | 2 | Left |
| + - | 1 (lowest) | Left |

### Worked Example

**Convert:** `( 3 + 4 ) * 5 - 6 / 2`

| Token | Action | Output Queue | Operator Stack |
|-------|--------|-------------|----------------|
| ( | Push to stack | | ( |
| 3 | Output | 3 | ( |
| + | Push to stack | 3 | ( + |
| 4 | Output | 3 4 | ( + |
| ) | Pop until ( | 3 4 + | |
| * | Push to stack | 3 4 + | * |
| 5 | Output | 3 4 + 5 | * |
| - | Pop * (higher prec), push - | 3 4 + 5 * | - |
| 6 | Output | 3 4 + 5 * 6 | - |
| / | Push (higher prec than -) | 3 4 + 5 * 6 | - / |
| 2 | Output | 3 4 + 5 * 6 2 | - / |
| End | Pop all | 3 4 + 5 * 6 2 / - | |

**Result:** `3 4 + 5 * 6 2 / -`

**Verification:** (3 + 4) * 5 - 6 / 2 = 7 * 5 - 3 = 35 - 3 = 32.

### Worked Example 2

**Convert:** `A + B * C - D`

| Token | Action | Output Queue | Operator Stack |
|-------|--------|-------------|----------------|
| A | Output | A | |
| + | Push | A | + |
| B | Output | A B | + |
| * | Push (* higher than +) | A B | + * |
| C | Output | A B C | + * |
| - | Pop * (higher prec), pop + (equal prec, left-assoc), push - | A B C * + | - |
| D | Output | A B C * + D | - |
| End | Pop all | A B C * + D - | |

**Result:** `A B C * + D -`

### Code: Shunting Yard Algorithm

```python
def infix_to_postfix(expression):
    """Convert infix expression string to postfix using shunting yard algorithm."""
    precedence = {'+': 1, '-': 1, '*': 2, '/': 2, '^': 3}
    right_associative = {'^'}
    output = []
    operator_stack = []
    tokens = expression.split()

    for token in tokens:
        if token not in precedence and token not in ('(', ')'):
            # Operand (number or variable)
            output.append(token)
        elif token == '(':
            operator_stack.append(token)
        elif token == ')':
            # Pop until matching left bracket
            while operator_stack and operator_stack[-1] != '(':
                output.append(operator_stack.pop())
            operator_stack.pop()   # Remove the '('
        else:
            # Operator
            while (operator_stack and
                   operator_stack[-1] != '(' and
                   operator_stack[-1] in precedence and
                   (precedence[operator_stack[-1]] > precedence[token] or
                    (precedence[operator_stack[-1]] == precedence[token]
                     and token not in right_associative))):
                output.append(operator_stack.pop())
            operator_stack.append(token)

    # Pop remaining operators
    while operator_stack:
        output.append(operator_stack.pop())

    return ' '.join(output)

# Test examples
print(infix_to_postfix("( 3 + 4 ) * 5 - 6 / 2"))
# Output: 3 4 + 5 * 6 2 / -

print(infix_to_postfix("A + B * C - D"))
# Output: A B C * + D -
```

```vb
Function InfixToPostfix(expression As String) As String
    Dim precedence As New Dictionary(Of String, Integer) From {
        {"+", 1}, {"-", 1}, {"*", 2}, {"/", 2}, {"^", 3}
    }
    Dim rightAssociative As New HashSet(Of String) From {"^"}
    Dim output As New List(Of String)
    Dim operatorStack As New Stack(Of String)
    Dim tokens() As String = expression.Split(" "c)

    For Each token As String In tokens
        If Not precedence.ContainsKey(token) AndAlso token <> "(" AndAlso token <> ")" Then
            ' Operand
            output.Add(token)
        ElseIf token = "(" Then
            operatorStack.Push(token)
        ElseIf token = ")" Then
            ' Pop until matching left bracket
            While operatorStack.Count > 0 AndAlso operatorStack.Peek() <> "("
                output.Add(operatorStack.Pop())
            End While
            operatorStack.Pop()   ' Remove the "("
        Else
            ' Operator
            While operatorStack.Count > 0 AndAlso
                  operatorStack.Peek() <> "(" AndAlso
                  precedence.ContainsKey(operatorStack.Peek()) AndAlso
                  (precedence(operatorStack.Peek()) > precedence(token) OrElse
                   (precedence(operatorStack.Peek()) = precedence(token) AndAlso
                    Not rightAssociative.Contains(token)))
                output.Add(operatorStack.Pop())
            End While
            operatorStack.Push(token)
        End If
    Next

    ' Pop remaining operators
    While operatorStack.Count > 0
        output.Add(operatorStack.Pop())
    End While

    Return String.Join(" ", output)
End Function

Sub Main()
    Console.WriteLine(InfixToPostfix("( 3 + 4 ) * 5 - 6 / 2"))
    ' Output: 3 4 + 5 * 6 2 / -

    Console.WriteLine(InfixToPostfix("A + B * C - D"))
    ' Output: A B C * + D -
End Sub
```

---

## Evaluating Postfix Expressions Using a Stack

<div class="key-term" markdown="1">
**Postfix evaluation** -- the process of computing the result of a postfix expression using a stack. Operands are pushed onto the stack; when an operator is encountered, the required number of operands are popped, the operation is applied, and the result is pushed back.
</div>

### Algorithm

1. Read tokens from left to right.
2. If the token is a **number**, push it onto the stack.
3. If the token is an **operator**, pop two operands from the stack (the first popped is the right operand, the second is the left operand), apply the operator, and push the result.
4. After all tokens are processed, the single value remaining on the stack is the result.

### Worked Example

**Evaluate:** `3 4 + 5 * 6 2 / -`

| Token | Action | Stack (top on right) |
|-------|--------|---------------------|
| 3 | Push | 3 |
| 4 | Push | 3, 4 |
| + | Pop 4 and 3, compute 3+4=7, push | 7 |
| 5 | Push | 7, 5 |
| * | Pop 5 and 7, compute 7*5=35, push | 35 |
| 6 | Push | 35, 6 |
| 2 | Push | 35, 6, 2 |
| / | Pop 2 and 6, compute 6/2=3, push | 35, 3 |
| - | Pop 3 and 35, compute 35-3=32, push | 32 |

**Result: 32**

This matches (3 + 4) * 5 - 6 / 2 = 32.

### Worked Example 2

**Evaluate:** `5 3 2 * + 4 -`

| Token | Action | Stack |
|-------|--------|-------|
| 5 | Push | 5 |
| 3 | Push | 5, 3 |
| 2 | Push | 5, 3, 2 |
| * | Pop 2 and 3, compute 3*2=6, push | 5, 6 |
| + | Pop 6 and 5, compute 5+6=11, push | 11 |
| 4 | Push | 11, 4 |
| - | Pop 4 and 11, compute 11-4=7, push | 7 |

**Result: 7** (equivalent infix: 5 + 3 * 2 - 4 = 7)

### Code

```python
def evaluate_postfix(expression):
    """Evaluate a postfix expression and return the numeric result."""
    stack = []
    tokens = expression.split()
    operators = {'+', '-', '*', '/'}

    for token in tokens:
        if token in operators:
            right = stack.pop()    # First popped = right operand
            left = stack.pop()     # Second popped = left operand
            if token == '+':
                stack.append(left + right)
            elif token == '-':
                stack.append(left - right)
            elif token == '*':
                stack.append(left * right)
            elif token == '/':
                stack.append(left / right)
        else:
            stack.append(float(token))

    return stack[0]

print(evaluate_postfix("3 4 + 5 * 6 2 / -"))   # Output: 32.0
print(evaluate_postfix("5 3 2 * + 4 -"))         # Output: 7.0
```

```vb
Function EvaluatePostfix(expression As String) As Double
    Dim stack As New Stack(Of Double)
    Dim tokens() As String = expression.Split(" "c)
    Dim operators As New HashSet(Of String) From {"+", "-", "*", "/"}

    For Each token As String In tokens
        If operators.Contains(token) Then
            Dim right As Double = stack.Pop()    ' First popped = right operand
            Dim left As Double = stack.Pop()     ' Second popped = left operand
            Select Case token
                Case "+"
                    stack.Push(left + right)
                Case "-"
                    stack.Push(left - right)
                Case "*"
                    stack.Push(left * right)
                Case "/"
                    stack.Push(left / right)
            End Select
        Else
            stack.Push(Double.Parse(token))
        End If
    Next

    Return stack.Pop()
End Function

Sub Main()
    Console.WriteLine(EvaluatePostfix("3 4 + 5 * 6 2 / -"))   ' Output: 32
    Console.WriteLine(EvaluatePostfix("5 3 2 * + 4 -"))        ' Output: 7
End Sub
```

<div class="exam-tip" markdown="1">
When evaluating postfix expressions, the **order of operands matters** for subtraction and division. The second value popped is the left operand and the first value popped is the right operand. So if you pop B then A, the result is A operator B, not B operator A. Getting this wrong is a very common mistake.
</div>

---

## Binary Expression Trees from Postfix Notation

<div class="key-term" markdown="1">
**Binary expression tree** -- a binary tree that represents an arithmetic expression. Each **leaf node** contains an operand (number or variable), and each **internal node** contains an operator. The left and right children of an operator node are its operands (or sub-expressions).
</div>

### Building a Binary Expression Tree from Postfix

The algorithm is very similar to postfix evaluation, but instead of computing values, we build tree nodes:

1. Read tokens left to right.
2. If the token is an **operand**, create a leaf node and push it onto the stack.
3. If the token is an **operator**, pop two nodes from the stack (first popped becomes right child, second becomes left child), create a new node with the operator and these children, and push the new node.
4. The final node on the stack is the root of the expression tree.

### Worked Example

**Build a tree from:** `3 4 + 5 *`

| Token | Action | Stack (tree nodes) |
|-------|--------|-------------------|
| 3 | Create leaf [3], push | [3] |
| 4 | Create leaf [4], push | [3], [4] |
| + | Pop [4] and [3], create [+] with left=[3], right=[4], push | [+] |
| 5 | Create leaf [5], push | [+], [5] |
| * | Pop [5] and [+], create [*] with left=[+], right=[5], push | [*] |

**Resulting tree:**

```
       *
      / \
     +   5
    / \
   3   4
```

This represents the infix expression: (3 + 4) * 5 = 35.

### Larger Worked Example

**Build a tree from:** `A B + C D - *`

| Token | Action | Stack |
|-------|--------|-------|
| A | Leaf [A], push | [A] |
| B | Leaf [B], push | [A], [B] |
| + | Pop [B] and [A], create [+], push | [+] |
| C | Leaf [C], push | [+], [C] |
| D | Leaf [D], push | [+], [C], [D] |
| - | Pop [D] and [C], create [-], push | [+], [-] |
| * | Pop [-] and [+], create [*], push | [*] |

**Resulting tree:**

```
         *
       /   \
      +     -
     / \   / \
    A   B C   D
```

This represents: (A + B) * (C - D).

### Traversals of Expression Trees

Different tree traversals produce different notations:

| Traversal | Order | Produces | Result for above tree |
|-----------|-------|----------|----------------------|
| In-order | Left, Root, Right | Infix notation | A + B * C - D (needs brackets for correctness) |
| Pre-order | Root, Left, Right | Prefix notation | * + A B - C D |
| Post-order | Left, Right, Root | Postfix notation | A B + C D - * |

### Code

```python
class ExpressionNode:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None

def build_expression_tree(postfix):
    """Build a binary expression tree from a postfix expression."""
    stack = []
    operators = {'+', '-', '*', '/', '^'}
    tokens = postfix.split()

    for token in tokens:
        node = ExpressionNode(token)
        if token in operators:
            node.right = stack.pop()   # First popped = right child
            node.left = stack.pop()    # Second popped = left child
        stack.append(node)

    return stack[0]   # Root of the tree

def inorder(node):
    """In-order traversal: produces infix notation (with brackets)."""
    if node is None:
        return ""
    if node.left is None and node.right is None:
        return node.value
    return f"({inorder(node.left)} {node.value} {inorder(node.right)})"

def preorder(node):
    """Pre-order traversal: produces prefix notation."""
    if node is None:
        return ""
    if node.left is None and node.right is None:
        return node.value
    return f"{node.value} {preorder(node.left)} {preorder(node.right)}"

def postorder(node):
    """Post-order traversal: produces postfix notation."""
    if node is None:
        return ""
    if node.left is None and node.right is None:
        return node.value
    return f"{postorder(node.left)} {postorder(node.right)} {node.value}"

# Build tree from postfix: A B + C D - *
root = build_expression_tree("A B + C D - *")

print("Infix:  ", inorder(root))     # Output: ((A + B) * (C - D))
print("Prefix: ", preorder(root))    # Output: * + A B - C D
print("Postfix:", postorder(root))   # Output: A B + C D - *
```

```vb
Class ExpressionNode
    Public Value As String
    Public Left As ExpressionNode
    Public Right As ExpressionNode

    Sub New(value As String)
        Me.Value = value
        Me.Left = Nothing
        Me.Right = Nothing
    End Sub
End Class

Function BuildExpressionTree(postfix As String) As ExpressionNode
    Dim stack As New Stack(Of ExpressionNode)
    Dim operators As New HashSet(Of String) From {"+", "-", "*", "/", "^"}
    Dim tokens() As String = postfix.Split(" "c)

    For Each token As String In tokens
        Dim node As New ExpressionNode(token)
        If operators.Contains(token) Then
            node.Right = stack.Pop()   ' First popped = right child
            node.Left = stack.Pop()    ' Second popped = left child
        End If
        stack.Push(node)
    Next

    Return stack.Pop()   ' Root of the tree
End Function

Function Inorder(node As ExpressionNode) As String
    If node Is Nothing Then Return ""
    If node.Left Is Nothing AndAlso node.Right Is Nothing Then
        Return node.Value
    End If
    Return $"({Inorder(node.Left)} {node.Value} {Inorder(node.Right)})"
End Function

Function Preorder(node As ExpressionNode) As String
    If node Is Nothing Then Return ""
    If node.Left Is Nothing AndAlso node.Right Is Nothing Then
        Return node.Value
    End If
    Return $"{node.Value} {Preorder(node.Left)} {Preorder(node.Right)}"
End Function

Function Postorder(node As ExpressionNode) As String
    If node Is Nothing Then Return ""
    If node.Left Is Nothing AndAlso node.Right Is Nothing Then
        Return node.Value
    End If
    Return $"{Postorder(node.Left)} {Postorder(node.Right)} {node.Value}"
End Function

Sub Main()
    ' Build tree from postfix: A B + C D - *
    Dim root As ExpressionNode = BuildExpressionTree("A B + C D - *")

    Console.WriteLine("Infix:   " & Inorder(root))     ' Output: ((A + B) * (C - D))
    Console.WriteLine("Prefix:  " & Preorder(root))    ' Output: * + A B - C D
    Console.WriteLine("Postfix: " & Postorder(root))   ' Output: A B + C D - *
End Sub
```

<div class="exam-tip" markdown="1">
Binary expression trees connect three major topics: **postfix notation**, **trees**, and **traversals**. The exam may ask you to build a tree from a postfix expression, or to perform traversals to produce different notations. Remember: **in-order** gives infix (but you need brackets), **pre-order** gives prefix (Polish notation), and **post-order** gives postfix (Reverse Polish Notation). Practise building trees by hand -- draw the tree and verify by performing a post-order traversal to recover the original postfix expression.
</div>
