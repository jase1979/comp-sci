---
layout: topic
title: "Organisation & Structure of Data"
level: "A2 Level"
level_url: "/a2/"
unit_name: "Unit 4: Architecture, Data, Communication & Applications"
unit_url: "/a2/unit4/"
subtopics:
  - "File design: How files are created, organised, updated, processed"
  - "Purpose and use of hashing algorithms"
  - "Compare different hashing algorithms"
  - "Use of multi-level indexes"
  - "Techniques to manage overflow"
  - "Need for file re-organisation"
---

## File Design

### How Files Are Created and Organised

A **file** is a collection of related records stored on a secondary storage medium. The way records are organised within a file determines how efficiently they can be accessed, updated, and processed.

<div class="key-term" markdown="1">
A **record** is a collection of related fields that represent a single entity (e.g. one customer). A **field** is a single data item within a record (e.g. surname). A **key field** uniquely identifies each record.
</div>

### File Organisation Methods

There are four main methods of organising records within a file:

| Method | Description | Access | Use Case |
|--------|-------------|--------|----------|
| **Serial** | Records stored in the order they arrive (no particular order) | Must read from start sequentially | Transaction logs, temporary files |
| **Sequential** | Records stored in order of a key field | Must read sequentially but can stop when key is passed | Payroll, batch processing |
| **Random (Direct)** | Records stored at addresses calculated by a hashing algorithm | Direct access using key | Real-time systems, online lookups |
| **Indexed Sequential** | Records stored sequentially with an index to speed up access | Sequential or direct via index | Large databases needing both batch and real-time access |

### Serial File Organisation

Records are appended to the file in the order they are received. There is no sorting or ordering.

- **Advantages:** Simple to add new records (just append); no overhead for maintaining order
- **Disadvantages:** Searching requires reading every record from the start (linear search); very slow for large files
- **Typical use:** Transaction files that temporarily hold data before batch processing

### Sequential File Organisation

Records are sorted by a **key field** (e.g. employee number). New records must be inserted in the correct position, which usually means creating a new copy of the file.

- **Advantages:** Efficient for processing all records in order (batch processing); can stop searching once the key value is exceeded
- **Disadvantages:** Inserting or deleting records requires rewriting the file; not suitable for real-time individual lookups
- **Typical use:** Master files for payroll, billing, or any system that processes records in bulk

### Random (Direct) File Organisation

A **hashing algorithm** is applied to the key field to calculate the storage address where the record should be placed. To retrieve a record, the same algorithm is applied to the key to find its address directly.

- **Advantages:** Very fast access to individual records; no need to read other records first
- **Disadvantages:** Records are not in any logical order so sequential processing is inefficient; collisions must be handled; wasted space if the file is sparsely populated
- **Typical use:** Real-time systems such as airline booking, stock control, bank accounts

### Indexed Sequential File Organisation

Records are stored in key order (like sequential), but an **index** is maintained separately. The index maps key values to physical addresses, allowing direct access to any record without reading through the entire file.

- **Advantages:** Supports both sequential processing (for batch jobs) and direct access (for real-time queries); flexible
- **Disadvantages:** Index must be maintained and updated; overhead of storing the index; performance degrades as overflow records accumulate
- **Typical use:** Large databases where both batch processing and real-time queries are needed

<div class="exam-tip" markdown="1">
Exam questions often ask you to **recommend** a file organisation method for a given scenario. Match the access pattern to the method: batch processing of all records suggests sequential; fast individual lookups suggest random; a need for both suggests indexed sequential.
</div>

---

## How Files Are Updated and Processed

### Master Files and Transaction Files

<div class="key-term" markdown="1">
A **master file** is a permanent file containing the current state of data (e.g. customer accounts). A **transaction file** is a temporary file containing recent changes (additions, deletions, amendments) to be applied to the master file.
</div>

### Batch Update Process (Sequential Files)

When updating a sequential master file, the following process is used:

1. **Sort** the transaction file into the same key order as the master file
2. **Read** records from both files simultaneously, comparing keys
3. **If keys match** — apply the update (amendment or deletion) and write to the new master file
4. **If the master key is lower** — the master record is unchanged, write it to the new master file and read the next master record
5. **If the transaction key is lower** — it is a new record to insert, write it to the new master file
6. Continue until both files are exhausted
7. The **old master file** is kept as a backup (grandfather-father-son backup)

### Grandfather-Father-Son Backup

| Generation | Description |
|-----------|-------------|
| **Grandfather** | The master file from two updates ago |
| **Father** | The master file from the previous update |
| **Son** | The current master file (just created) |

If the son file is corrupted, it can be recreated by reprocessing the father file with the transaction file. This provides a built-in backup mechanism for sequential file processing.

### Real-Time Updating (Random/Indexed Sequential Files)

For random or indexed sequential files, records are updated **in place** as transactions occur:

1. The key field from the transaction is used to locate the record directly (via hashing or index lookup)
2. The record is read into memory
3. The update is applied
4. The record is written back to its original location

This approach does not create a new file, so a separate backup strategy is required (e.g. periodic dumps and transaction logs).

---

## Hashing Algorithms

### Purpose of Hashing

A **hashing algorithm** transforms a key field value into a **storage address** (also called a hash value or home address). This enables **direct access** to records without searching through the file.

<div class="key-term" markdown="1">
A **hashing algorithm** is a function that takes a key value as input and produces a storage address as output. The same key always produces the same address (deterministic).
</div>

### Division-Remainder Method

The most commonly used hashing method. The key is divided by a prime number and the **remainder** becomes the storage address.

```
Address = Key MOD TableSize
```

It is best practice to choose a **prime number** for the table size, as this produces a more even distribution of addresses and reduces collisions.

**Example:** Table size = 11 (prime)

| Key | Calculation | Address |
|-----|------------|---------|
| 2345 | 2345 MOD 11 | 1 |
| 5678 | 5678 MOD 11 | 2 |
| 1234 | 1234 MOD 11 | 2 |

Notice that keys 5678 and 1234 both hash to address 2 — this is a **collision**.

```python
def division_remainder_hash(key, table_size):
    return key % table_size

# Example
table_size = 11
keys = [2345, 5678, 1234]
for key in keys:
    address = division_remainder_hash(key, table_size)
    print(f"Key {key} -> Address {address}")
```

```vb
Function DivisionRemainderHash(key As Integer, tableSize As Integer) As Integer
    Return key Mod tableSize
End Function

' Example
Dim tableSize As Integer = 11
Dim keys() As Integer = {2345, 5678, 1234}
For Each key As Integer In keys
    Dim address As Integer = DivisionRemainderHash(key, tableSize)
    Console.WriteLine($"Key {key} -> Address {address}")
Next
```

### Mid-Square Method

1. **Square** the key value
2. **Extract the middle digits** of the result
3. Use the middle digits as the storage address

**Example:** Key = 4567

1. 4567² = 20,857,489
2. Middle digits (taking 2 from the centre): **57**
3. Address = 57

The number of middle digits extracted depends on the required address range. This method works well when keys do not have a lot of leading or trailing zeros.

### Folding Method

1. **Split** the key into equal-sized parts
2. **Add** the parts together
3. If necessary, discard any carry digits to fit the address range

**Example:** Key = 123456, address range 0–999

1. Split into parts of 3 digits: 123 | 456
2. Add: 123 + 456 = 579
3. Address = 579

**Another example:** Key = 987654321, address range 0–999

1. Split: 987 | 654 | 321
2. Add: 987 + 654 + 321 = 1962
3. Discard carry: Address = 962

---

## Comparing Hashing Algorithms

| Criterion | Division-Remainder | Mid-Square | Folding |
|-----------|-------------------|------------|---------|
| **Speed** | Very fast (single modulus operation) | Slower (squaring can produce very large numbers) | Fast (addition only) |
| **Distribution** | Good if table size is prime | Generally good; depends on key patterns | Can cluster if keys have similar digit patterns |
| **Collision rate** | Low with prime table size | Low for well-distributed keys | Moderate; sensitive to key structure |
| **Ease of implementation** | Very simple | Moderate (need to handle large numbers and extract digits) | Simple |
| **Best suited for** | General purpose; most common choice | Numeric keys without regular patterns | Keys of varying lengths |

<div class="exam-tip" markdown="1">
In the exam, you may be asked to **apply** a hashing algorithm to specific keys. Show every step of your working clearly. You may also be asked to **compare** two algorithms — focus on collision rates, speed, and how evenly they distribute records across the address space.
</div>

---

## Collision Resolution

A **collision** occurs when two different keys hash to the same address. Since two records cannot occupy the same location, a collision resolution strategy is needed.

### Open Addressing

With open addressing, when a collision occurs, the algorithm searches for the next available slot in the table itself.

#### Linear Probing

If address `h` is occupied, try `h+1`, then `h+2`, then `h+3`, and so on (wrapping around to the start of the table if necessary).

**Example:** Table size = 7, using division-remainder hashing

| Step | Key | Hash (Key MOD 7) | Action | Final Address |
|------|-----|------------------|--------|---------------|
| 1 | 10 | 3 | Slot 3 is empty — place here | 3 |
| 2 | 17 | 3 | Slot 3 occupied — try 4. Slot 4 empty — place here | 4 |
| 3 | 24 | 3 | Slot 3 occupied — try 4. Slot 4 occupied — try 5. Empty — place here | 5 |

**Problem:** Linear probing causes **primary clustering** — groups of consecutive occupied slots form, meaning subsequent collisions require longer probe sequences.

```python
def linear_probe_insert(table, key, table_size):
    address = key % table_size
    while table[address] is not None:
        address = (address + 1) % table_size
    table[address] = key
    return address

# Example
table_size = 7
table = [None] * table_size
for key in [10, 17, 24]:
    addr = linear_probe_insert(table, key, table_size)
    print(f"Key {key} placed at address {addr}")
print("Table:", table)
```

```vb
Sub LinearProbeInsert(table() As Integer, key As Integer, tableSize As Integer)
    Dim address As Integer = key Mod tableSize
    While table(address) <> -1  ' -1 represents empty
        address = (address + 1) Mod tableSize
    End While
    table(address) = key
    Console.WriteLine($"Key {key} placed at address {address}")
End Sub

' Example
Dim tableSize As Integer = 7
Dim table(tableSize - 1) As Integer
For i As Integer = 0 To tableSize - 1
    table(i) = -1  ' Initialise as empty
Next
LinearProbeInsert(table, 10, tableSize)
LinearProbeInsert(table, 17, tableSize)
LinearProbeInsert(table, 24, tableSize)
```

#### Quadratic Probing

Instead of trying `h+1`, `h+2`, `h+3`, try `h+1²`, `h+2²`, `h+3²` (i.e. `h+1`, `h+4`, `h+9`, ...).

**Example:** Key hashes to address 3 in a table of size 11

| Probe | Offset | Address tried |
|-------|--------|--------------|
| 1st | 1² = 1 | (3 + 1) MOD 11 = 4 |
| 2nd | 2² = 4 | (3 + 4) MOD 11 = 7 |
| 3rd | 3² = 9 | (3 + 9) MOD 11 = 1 |

**Advantage:** Reduces primary clustering because probes spread out more widely.

**Disadvantage:** May not visit every slot in the table (not all addresses may be probed), so insertion can fail even if the table is not full. Also causes **secondary clustering** — keys that hash to the same address follow the same probe sequence.

### Chaining (Separate Chaining)

Each slot in the hash table holds a **pointer to a linked list**. When a collision occurs, the new record is added to the linked list at that address.

**Example:**

```
Address 0: -> [14] -> [21] -> NULL
Address 1: -> [8] -> NULL
Address 2: (empty)
Address 3: -> [10] -> [17] -> [24] -> NULL
```

- **Advantage:** No clustering; the table never becomes "full" (lists can grow indefinitely); deletion is straightforward
- **Disadvantage:** Extra memory required for pointers; performance degrades if chains become very long; less cache-friendly than open addressing

```python
class HashTable:
    def __init__(self, size):
        self.size = size
        self.table = [[] for _ in range(size)]

    def insert(self, key):
        address = key % self.size
        self.table[address].append(key)

    def search(self, key):
        address = key % self.size
        return key in self.table[address]

    def display(self):
        for i, chain in enumerate(self.table):
            print(f"Address {i}: {chain}")

# Example
ht = HashTable(7)
for key in [10, 17, 24, 5, 12]:
    ht.insert(key)
ht.display()
```

```vb
' Using a List of Lists for chaining
Dim tableSize As Integer = 7
Dim table As New List(Of List(Of Integer))

For i As Integer = 0 To tableSize - 1
    table.Add(New List(Of Integer))
Next

Sub ChainInsert(key As Integer)
    Dim address As Integer = key Mod tableSize
    table(address).Add(key)
End Sub

' Insert keys
ChainInsert(10)
ChainInsert(17)
ChainInsert(24)
ChainInsert(5)
ChainInsert(12)

' Display table
For i As Integer = 0 To tableSize - 1
    Console.WriteLine($"Address {i}: {String.Join(" -> ", table(i))}")
Next
```

<div class="exam-tip" markdown="1">
When comparing collision resolution techniques, consider: **linear probing** is simple but causes clustering; **quadratic probing** reduces clustering but may miss slots; **chaining** avoids clustering entirely but uses extra memory for pointers. Be prepared to trace through insertions step by step.
</div>

---

## Multi-Level Indexes

### How Indexes Speed Up Access

An **index** is a separate, smaller file that maps key values to the physical addresses of records in the main data file. Rather than searching the entire data file, the system searches the much smaller index to find the required address.

<div class="key-term" markdown="1">
An **index** is an ordered list of key values paired with the physical addresses of the corresponding records in the data file. It works like the index at the back of a textbook — you look up a term to find the page number.
</div>

### Primary Index

A **primary index** is built on the **primary key** of the file. It contains one entry for each **block** (or page) of the data file, pointing to the first record in each block.

- Since the data file is sorted by primary key, the index can use the first key in each block as a reference point
- To find a record, search the index to identify the correct block, then search within that block
- The index is much smaller than the data file, so searching it is fast

### Secondary Index

A **secondary index** is built on a **non-key field** (e.g. surname, department). It allows fast access based on fields other than the primary key.

- A secondary index may contain one entry per record (dense index) or one entry per unique value of the indexed field
- Multiple records may share the same value for the indexed field, so each index entry may point to a **list of addresses**
- A file can have multiple secondary indexes on different fields

### Multi-Level Index Structure

When an index itself becomes too large to search efficiently, it can be indexed again, creating a **multi-level index**:

| Level | Contains | Purpose |
|-------|----------|---------|
| **Level 1 (Top)** | Pointers to sections of Level 2 | Narrows search to a section of the second-level index |
| **Level 2** | Pointers to blocks of the data file | Narrows search to a specific block |
| **Data file** | The actual records | Contains the data |

**How a search works:**

1. Search the **top-level index** to find which section of the second-level index to examine
2. Search that section of the **second-level index** to find the data block address
3. Read the **data block** and find the record

Each level reduces the search space dramatically. This is the principle behind **B-trees** and **B+ trees** used in modern database systems.

**Example:** A file with 1,000,000 records, 100 records per block = 10,000 blocks

- Without an index: up to 10,000 block reads (linear search)
- With a single-level index (10,000 entries, 100 per block = 100 index blocks): up to 100 block reads to search the index + 1 to read the data block = 101
- With a two-level index: top level fits in 1 block (100 entries pointing to 100 sections), then 1 block read at level 2, then 1 data block read = **3 block reads**

---

## Overflow Management

### The Overflow Problem

In indexed sequential files, records are stored in key order. When a new record needs to be inserted between two existing records and the target block is full, the new record must go into an **overflow area**.

Over time, as more records are inserted and deleted, the overflow area grows and performance degrades because accessing overflow records requires following pointers away from the main data area.

### Overflow Areas

An **overflow area** is a designated section of the file (or a separate file) where records that do not fit in their home block are stored.

| Type | Description |
|------|-------------|
| **Local overflow** | Each block has its own small overflow area nearby |
| **Global overflow** | A single shared overflow area for the entire file |

### Linked Overflow Chains

When a record is placed in the overflow area, a **pointer** in the original block links to it. If multiple overflow records exist for the same block, they form a **linked chain**:

```
Main Block 5: [Record A] [Record B] [Record C] -> Overflow pointer
    |
    v
Overflow: [Record D] -> [Record E] -> NULL
```

To find a record that has overflowed:

1. Hash or index to the correct block
2. Search the block — record not found
3. Follow the overflow pointer to the overflow area
4. Search the overflow chain sequentially until the record is found (or the chain ends)

The longer the overflow chain, the slower the access time, because each link in the chain may require an additional disk read.

---

## Need for File Reorganisation

### Why Reorganisation Is Necessary

Over time, the performance of an indexed sequential file degrades for several reasons:

| Problem | Cause | Effect |
|---------|-------|--------|
| **Accumulated overflow records** | Insertions that cannot fit in the main data area | Longer overflow chains mean slower access |
| **Deleted records leaving gaps** | Records are marked as deleted but space is not reclaimed | Wasted storage; sequential processing reads empty slots |
| **Index becomes outdated** | Index entries may point to overflow chains rather than main blocks | Index lookups become slower |
| **Uneven distribution** | Some blocks may be nearly empty while others overflow | Poor utilisation of storage; inconsistent access times |

### What Reorganisation Involves

File reorganisation involves:

1. **Reading** all valid (non-deleted) records from the existing file, including those in overflow areas
2. **Sorting** the records back into key order
3. **Writing** the records to a new file with even distribution across blocks
4. **Rebuilding** the index from scratch based on the new file structure
5. **Clearing** the overflow area

### When to Reorganise

Reorganisation is typically triggered when:

- The **overflow area reaches a threshold** (e.g. more than 20% of records are in overflow)
- **Access times have noticeably degraded** compared to the original performance
- A **scheduled maintenance window** is reached (e.g. weekly or monthly)
- The ratio of **deleted to active records** exceeds an acceptable level

<div class="exam-tip" markdown="1">
Reorganisation is an **expensive operation** — the file is unavailable during the process, and it requires reading and writing every record. This is why it is done periodically rather than continuously. Be prepared to explain both **why** reorganisation is needed and **what** happens during the process.
</div>

### Trade-offs

| Factor | Without Reorganisation | After Reorganisation |
|--------|----------------------|---------------------|
| Access time | Degrades over time | Restored to optimal |
| Storage utilisation | Wasted space from deletions and sparse blocks | Efficient, compact storage |
| Index accuracy | May reference overflow chains | Directly references main blocks |
| System availability | File remains online | File is offline during reorganisation |
