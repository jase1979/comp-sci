---
layout: topic
title: "Organisation of Data"
level: "AS"
level_url: "/as/"
unit_name: "Unit 1: Fundamentals of Computer Science"
unit_url: "/as/unit1/"
prev_topic: "/as/unit1/data-structures/"
next_topic: "/as/unit1/database-systems/"
---

## Fields, Records, and Files

Data stored on a computer is typically organised into a clear hierarchy. Understanding this hierarchy is essential for working with files and databases.

<div class="key-term" markdown="1">
**Field:** A single item of data (e.g., a surname, a date of birth). **Record:** A collection of related fields describing one entity (e.g., one student). **File:** A collection of related records (e.g., all students in a school).
</div>

### Field

A **field** is the smallest meaningful unit of data. Each field has:
- A **field name** (e.g., `Surname`, `DateOfBirth`, `Mark`)
- A **data type** (e.g., String, Integer, Date, Boolean, Real)
- A **field size** (e.g., 20 characters for a name)

### Record

A **record** is a collection of related fields that together describe a single entity. For example, a `Student` record might contain:

| Field Name | Data Type | Example Value |
|---|---|---|
| StudentID | String | "S1024" |
| FirstName | String | "Alice" |
| Surname | String | "Williams" |
| DateOfBirth | Date | 15/03/2007 |
| Mark | Integer | 78 |
| Passed | Boolean | True |

### File

A **file** is a collection of related records stored together. A `Students` file would hold the records for all students. Files are stored on secondary storage (e.g., hard drive, SSD) so the data persists when the computer is turned off.

### The Data Hierarchy

```
File (e.g., Students.dat)
 └── Record 1 (Alice Williams)
 │    ├── Field: StudentID = "S1024"
 │    ├── Field: FirstName = "Alice"
 │    ├── Field: Surname = "Williams"
 │    └── Field: Mark = 78
 └── Record 2 (Bob Jones)
      ├── Field: StudentID = "S1025"
      ├── Field: FirstName = "Bob"
      ├── Field: Surname = "Jones"
      └── Field: Mark = 65
```

<div class="exam-tip" markdown="1">
The data hierarchy from smallest to largest is: **Bit → Byte → Field → Record → File → Database**. In exams, you may be asked to identify the fields, records, and file from a given scenario.
</div>

---

## Fixed-Length vs Variable-Length Records

When records are stored in a file, they can be formatted in two different ways: **fixed-length** or **variable-length**.

### Fixed-Length Records

Every record in the file occupies the **exact same amount of storage space**, regardless of the actual length of the data. Each field is allocated a maximum size, and if the data is shorter, the remaining space is padded (often with spaces or null characters).

**Example:** If `FirstName` is allocated 15 characters, the name "Sue" would be stored as `"Sue            "` (padded with 12 spaces).

**Structure:**

| StudentID (5) | FirstName (15) | Surname (20) | Mark (3) |
|---|---|---|---|
| S1024 | Alice           | Williams             | 078 |
| S1025 | Bob             | Jones                | 065 |

Each record = 5 + 15 + 20 + 3 = **43 bytes**.

**Calculating record position:**
The position of the *n*th record can be calculated directly:
`Position = (n - 1) × Record Length`

For example, to find record 50 in a file where each record is 43 bytes:
`Position = (50 - 1) × 43 = 2107 bytes from the start`

### Variable-Length Records

Each record only takes up as much space as the data actually requires. A **delimiter** (special character, such as a comma or pipe symbol) or a **length indicator** separates fields and records.

**Example (comma-delimited):**
```
S1024,Alice,Williams,78
S1025,Bob,Jones,65
```

### Comparison

| Feature | Fixed-Length Records | Variable-Length Records |
|---|---|---|
| **Storage space** | Wastes space due to padding | Efficient — no wasted space |
| **Access speed** | Fast — can calculate exact position of any record | Slow — must read from the start to find a record |
| **Simplicity** | Simple to program and manage | More complex — needs delimiters or length fields |
| **Insertion/Deletion** | Easy — overwrite at known position | Harder — may require rewriting the file |
| **Best for** | Records of similar length; random access needed | Records of very different lengths; storage is limited |

<div class="key-term" markdown="1">
**Fixed-length records** allocate the same amount of space for every record, allowing direct calculation of record positions. **Variable-length records** use only the space needed, separated by delimiters.
</div>

<div class="exam-tip" markdown="1">
The key trade-off is **speed vs. storage**. Fixed-length records are faster for direct access but waste space. Variable-length records save space but require sequential reading. Be ready to explain this trade-off in an exam.
</div>

---

## Serial File Organisation

In a **serial file**, records are stored **in the order they are added** (chronologically) with no particular sorting. New records are simply appended to the end of the file.

<div class="key-term" markdown="1">
A **serial file** stores records in the order they were entered, with no sorting or logical ordering applied.
</div>

### Characteristics

- Records are stored in **no particular order** (or in the order of entry)
- To find a specific record, a **linear search** must be performed — reading every record from the beginning until the target is found
- New records are added to the **end of the file**
- Deleting a record may require rewriting the entire file, or marking the record as deleted

### Advantages and Disadvantages

| Advantage | Disadvantage |
|---|---|
| Simple to implement | Slow to search — must read sequentially |
| Fast to add new records (append to end) | No ordering makes retrieval inefficient |
| Appropriate for small files or batch input | Not suitable for large files needing frequent lookups |

### Use Cases

- **Transaction logs** — events recorded in the order they occur
- **Batch processing input files** — data collected throughout the day, processed later
- **Backup files** — records dumped in the order they are read

---

## Sequential File Organisation

In a **sequential file**, records are stored **sorted by a key field** (e.g., sorted by `StudentID` or `Surname`). The file must be kept in order at all times.

<div class="key-term" markdown="1">
A **sequential file** stores records in order of a **key field**. Searching can be more efficient than serial because the search can stop once the key value has been passed.
</div>

### Characteristics

- Records are **sorted by a key field**
- To search, read through the file in order; once a key value greater than the target is found, the search can stop (the record is not in the file)
- Inserting a new record requires finding the correct position and **rewriting the file** from that point onwards (or creating a new file with the record inserted)
- Often used with **fixed-length records** for efficient processing

### Advantages and Disadvantages

| Advantage | Disadvantage |
|---|---|
| Faster searching than serial (can stop early) | Insertion is slow — file must be partially or fully rewritten |
| Efficient for processing all records in order (batch processing) | Not suitable for frequent additions/deletions |
| Can use binary search if records are fixed-length | Must maintain sort order at all times |

### Serial vs Sequential Comparison

| Feature | Serial | Sequential |
|---|---|---|
| **Order** | No order (order of entry) | Sorted by key field |
| **Adding records** | Append to end (fast) | Insert in correct position (slow) |
| **Searching** | Linear search only | Linear search (can stop early) or binary search |
| **Best use** | Temporary data, logs | Batch processing of ordered data |

---

## Random (Direct Access) File Organisation

In a **random access file** (also called **direct access**), records can be read or written **directly** without reading through preceding records. The position of a record is calculated using a **hashing algorithm** or an **address calculation** applied to the record's key field.

<div class="key-term" markdown="1">
**Random (direct) access** allows any record to be accessed directly by calculating its storage address from the key field, typically using a hash function.
</div>

### How It Works

1. A **hash function** is applied to the record's key field to produce a **storage address** (position in the file)
2. The record is stored at (or near) that address
3. To retrieve a record, the same hash function is applied to the key to calculate the address and go directly to it

### Handling Collisions

When two different keys produce the same hash value (a **collision**), the system must resolve it. Common methods include:
- **Open addressing** — store the record in the next available slot
- **Overflow area** — store colliding records in a separate overflow area with pointers

### Advantages and Disadvantages

| Advantage | Disadvantage |
|---|---|
| Very fast access to individual records — O(1) | Wasted storage space (empty slots in the hash table) |
| Ideal for applications requiring frequent lookups | Collisions reduce efficiency |
| No need to read through other records | Poor for processing all records in order |
| Records can be updated in place | Choosing a good hash function is important |

### Use Cases

- **Real-time systems** requiring instant lookup (e.g., airline booking systems)
- **Stock control systems** — look up a product by barcode
- **Bank account systems** — access an account by account number

---

## Indexed Sequential Access

**Indexed sequential access** combines the benefits of sequential and random access. Records are stored **sequentially** (sorted by key field), but an **index** is maintained that maps key values to their approximate positions in the file.

<div class="key-term" markdown="1">
**Indexed sequential access** stores records in key order with an **index** that enables fast lookup by pointing to the approximate location of a record, reducing the number of records that must be searched.
</div>

### How It Works

1. Records are stored in **sequential order** by key field
2. An **index** is created that stores the key value and the address of certain records (e.g., the first record on each page or block)
3. To find a record, the system first searches the **index** to find the approximate location, then reads sequentially from that point
4. Multiple levels of index can be used (like a multi-level index) for very large files

### Example

Consider a file of students sorted by StudentID, with a block index:

**Index:**

| Key Range | Block Address |
|---|---|
| S1000 - S1099 | Block 1 |
| S1100 - S1199 | Block 2 |
| S1200 - S1299 | Block 3 |

To find student `S1157`, the system checks the index, jumps directly to Block 2, then searches sequentially within that block.

### Advantages and Disadvantages

| Advantage | Disadvantage |
|---|---|
| Much faster than purely sequential search | Index requires additional storage space |
| Supports both sequential and direct access | Index must be maintained when records are added/deleted |
| Efficient for large files | More complex to implement |
| Good for batch and interactive processing | Overflow handling needed for insertions |

---

## Comparison of File Organisation Methods

| Feature | Serial | Sequential | Random (Direct) | Indexed Sequential |
|---|---|---|---|---|
| **Order** | None | Sorted by key | None (hash-based) | Sorted by key + index |
| **Search speed** | Slow (linear) | Medium (linear, can stop early) | Fast (O(1) via hash) | Fast (index then short search) |
| **Insertion** | Fast (append) | Slow (rewrite) | Fast (hash to position) | Medium (may need index update) |
| **Deletion** | Slow (rewrite or mark) | Slow (rewrite) | Fast (mark as empty) | Medium |
| **Best for** | Logs, batch input | Batch processing | Real-time lookups | Large files needing both access types |
| **Storage efficiency** | High | High | Low (empty slots) | Medium (index overhead) |

<div class="exam-tip" markdown="1">
In the exam, you may be asked to recommend a file organisation method for a given scenario. Think about whether the application needs **frequent individual lookups** (random access), **batch processing in order** (sequential), or **both** (indexed sequential). Serial is mainly used for temporary or log data.
</div>

---

## File Handling — Code Examples

Working with files in code involves **opening**, **reading from**, **writing to**, and **closing** files. The two most common modes are:
- **Writing** — creates a new file or overwrites an existing one
- **Reading** — opens an existing file for reading
- **Appending** — adds data to the end of an existing file

### Writing to a Text File

```python
# Python — Writing to a text file
# Writing records to a file (overwrites if file exists)
file = open("students.txt", "w")
file.write("S1024,Alice,Williams,78\n")
file.write("S1025,Bob,Jones,65\n")
file.write("S1026,Charlie,Brown,82\n")
file.close()

# Better practice: using 'with' to auto-close the file
with open("students.txt", "w") as file:
    file.write("S1024,Alice,Williams,78\n")
    file.write("S1025,Bob,Jones,65\n")
    file.write("S1026,Charlie,Brown,82\n")
```

```vb
' VB.NET — Writing to a text file
Imports System.IO

' Writing records to a file (overwrites if file exists)
Dim writer As New StreamWriter("students.txt")
writer.WriteLine("S1024,Alice,Williams,78")
writer.WriteLine("S1025,Bob,Jones,65")
writer.WriteLine("S1026,Charlie,Brown,82")
writer.Close()

' Alternative using Using block (auto-closes the file)
Using writer As New StreamWriter("students.txt")
    writer.WriteLine("S1024,Alice,Williams,78")
    writer.WriteLine("S1025,Bob,Jones,65")
    writer.WriteLine("S1026,Charlie,Brown,82")
End Using
```

### Reading from a Text File

```python
# Python — Reading from a text file

# Reading the entire file
with open("students.txt", "r") as file:
    contents = file.read()
    print(contents)

# Reading line by line
with open("students.txt", "r") as file:
    for line in file:
        line = line.strip()  # Remove newline character
        fields = line.split(",")  # Split by comma delimiter
        student_id = fields[0]
        first_name = fields[1]
        surname = fields[2]
        mark = int(fields[3])
        print(f"{first_name} {surname} (ID: {student_id}) scored {mark}")
```

```vb
' VB.NET — Reading from a text file
Imports System.IO

' Reading line by line
Dim reader As New StreamReader("students.txt")
Dim line As String

While Not reader.EndOfStream
    line = reader.ReadLine()
    Dim fields() As String = line.Split(",")
    Dim studentID As String = fields(0)
    Dim firstName As String = fields(1)
    Dim surname As String = fields(2)
    Dim mark As Integer = CInt(fields(3))
    Console.WriteLine(firstName & " " & surname & " (ID: " & studentID & ") scored " & mark)
End While
reader.Close()
```

### Appending to a Text File

```python
# Python — Appending to a text file
with open("students.txt", "a") as file:
    file.write("S1027,Diana,Evans,91\n")
```

```vb
' VB.NET — Appending to a text file
Imports System.IO

' Append mode (True = append)
Using writer As New StreamWriter("students.txt", True)
    writer.WriteLine("S1027,Diana,Evans,91")
End Using
```

### Searching for a Record in a File

```python
# Python — Searching for a record by StudentID
def search_student(filename, search_id):
    with open(filename, "r") as file:
        for line in file:
            line = line.strip()
            fields = line.split(",")
            if fields[0] == search_id:
                return {
                    "id": fields[0],
                    "first_name": fields[1],
                    "surname": fields[2],
                    "mark": int(fields[3])
                }
    return None  # Not found

result = search_student("students.txt", "S1025")
if result is not None:
    print(f"Found: {result['first_name']} {result['surname']}")
else:
    print("Student not found")
```

```vb
' VB.NET — Searching for a record by StudentID
Imports System.IO

Sub SearchStudent(filename As String, searchID As String)
    Dim reader As New StreamReader(filename)
    Dim found As Boolean = False
    Dim line As String

    While Not reader.EndOfStream
        line = reader.ReadLine()
        Dim fields() As String = line.Split(",")
        If fields(0) = searchID Then
            Console.WriteLine("Found: " & fields(1) & " " & fields(2))
            found = True
            Exit While
        End If
    End While

    reader.Close()

    If Not found Then
        Console.WriteLine("Student not found")
    End If
End Sub
```

### File Modes Summary

| Mode | Python | VB.NET | Description |
|---|---|---|---|
| **Read** | `"r"` | `New StreamReader(path)` | Open for reading; file must exist |
| **Write** | `"w"` | `New StreamWriter(path)` | Open for writing; creates or overwrites |
| **Append** | `"a"` | `New StreamWriter(path, True)` | Open for appending; adds to end |

<div class="exam-tip" markdown="1">
In exam pseudocode, you may see simplified file operations such as `OPENFILE`, `READLINE`, `WRITELINE`, and `CLOSEFILE`. Make sure you understand the difference between **write** mode (which overwrites existing content) and **append** mode (which adds to the end). Always close a file after use to ensure data is saved properly.
</div>

---

## Master Files and Transaction Files

In many real-world systems, data processing involves two key types of file working together.

<div class="key-term" markdown="1">
**Master file** — the main, permanent data store that holds the current state of all records. It is updated periodically but is not changed during daily operations. Examples include a payroll file, customer database, or stock file.
</div>

<div class="key-term" markdown="1">
**Transaction file** — a temporary file that holds all the changes (additions, deletions, modifications) that need to be applied to the master file. Transactions are collected over a period and then processed in a batch.
</div>

### The File Update Process

The process of applying a transaction file to a master file follows these steps:

1. **Sort the transaction file** by the same key field as the master file
2. **Open both files** — the old master file for reading and a new master file for writing
3. **Read a record from each file** and compare their key fields
4. **If the keys match** — apply the transaction (update or delete the record) and write to the new master file
5. **If the master key is smaller** — the record is unchanged; copy it to the new master file
6. **If the transaction key is smaller** — it is a new record; write it to the new master file
7. **Repeat** until both files have been fully processed
8. The **old master file is kept** as a backup (the "grandfather" in the GFS scheme)

### Real-World File Processing Examples

| Application | Master File | Transaction File | Update Frequency |
|-------------|-------------|-----------------|------------------|
| **Payroll** | Employee records (name, salary, tax code, bank details) | Hours worked, overtime, bonuses for the pay period | Weekly or monthly |
| **Utility billing** | Customer accounts (address, tariff, meter readings) | New meter readings for the billing period | Quarterly |
| **Banking** | Account records (balance, account holder, account type) | Daily deposits, withdrawals, transfers | Daily (overnight batch) |
| **Retail stock** | Product records (stock level, price, supplier) | Sales transactions, deliveries, returns | Daily |

<div class="exam-tip" markdown="1">
When describing the file update process, always mention that both files must be **sorted by the same key field** before processing begins. Also note that the old master file is **not deleted** — it is kept as a backup generation. This is a common source of marks in exam questions.
</div>
