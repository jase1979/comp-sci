---
layout: topic
title: "Data Representation"
level: "AS Level"
level_url: "/as/"
unit_name: "Unit 1: Fundamentals of Computer Science"
unit_url: "/as/unit1/"
prev_topic: "/as/unit1/data-transmission/"
next_topic: "/as/unit1/data-structures/"
---

## Bit, Byte and Word

All data in a computer is ultimately represented as **binary** -- patterns of 0s and 1s. The fundamental units of digital data are:

<div class="key-term" markdown="1">
A **bit** (binary digit) is the smallest unit of data, holding a value of either `0` or `1`. A **byte** is a group of 8 bits. A **word** is a fixed-size group of bits that the processor can handle as a single unit.
</div>

| Unit | Size | Notes |
|---|---|---|
| **Bit** | 1 binary digit | Either 0 or 1 |
| **Nibble** | 4 bits | Can represent one hexadecimal digit (0-F) |
| **Byte** | 8 bits | Can represent 2^8 = 256 different values (0-255 unsigned) |
| **Word** | Processor-dependent | Typically 16, 32, or 64 bits in modern systems |

The **word length** of a processor determines:
- How much data the CPU can process in a single operation
- The width of the data bus
- The size of the CPU's general-purpose registers
- A 64-bit processor has a 64-bit word length, meaning it can process 64 bits of data per instruction

Larger data quantities use standard prefixes:

| Unit | Approximate Size | Exact Size (Binary) |
|---|---|---|
| **Kilobyte (KB)** | 1,000 bytes | 1,024 bytes (2^10) |
| **Megabyte (MB)** | 1,000,000 bytes | 1,048,576 bytes (2^20) |
| **Gigabyte (GB)** | 1,000,000,000 bytes | 1,073,741,824 bytes (2^30) |
| **Terabyte (TB)** | 1,000,000,000,000 bytes | 1,099,511,627,776 bytes (2^40) |

<div class="exam-tip" markdown="1">
The word size varies between processors. A 32-bit processor has a word length of 32 bits (4 bytes), while a 64-bit processor has a word length of 64 bits (8 bytes). Word size affects the maximum value that can be processed in one operation and the maximum addressable memory.
</div>

---

## Binary and Hexadecimal Number Systems

### Binary (Base-2)

Binary uses only two digits: `0` and `1`. Each position in a binary number represents a power of 2, increasing from right to left.

**Place values for an 8-bit binary number:**

| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
|---|---|---|---|---|---|---|---|
| 2^7 | 2^6 | 2^5 | 2^4 | 2^3 | 2^2 | 2^1 | 2^0 |

**Converting binary to decimal:** Add together the place values where there is a `1`.

Example: `10110101` = 128 + 0 + 32 + 16 + 0 + 4 + 0 + 1 = **181**

**Converting decimal to binary:** Repeatedly divide by 2 and record the remainders (read from bottom to top), or subtract the largest possible power of 2 at each step.

Example: Convert 200 to binary:
- 200 - 128 = 72 (bit 7 = 1)
- 72 - 64 = 8 (bit 6 = 1)
- 8 - 8 = 0 (bit 3 = 1)
- Result: **11001000**

### Hexadecimal (Base-16)

Hexadecimal uses 16 symbols: `0-9` and `A-F` (where A=10, B=11, C=12, D=13, E=14, F=15). Each hex digit represents exactly 4 binary bits (one nibble).

| Decimal | Binary | Hex |
|:---:|:---:|:---:|
| 0 | 0000 | 0 |
| 1 | 0001 | 1 |
| 2 | 0010 | 2 |
| 3 | 0011 | 3 |
| 4 | 0100 | 4 |
| 5 | 0101 | 5 |
| 6 | 0110 | 6 |
| 7 | 0111 | 7 |
| 8 | 1000 | 8 |
| 9 | 1001 | 9 |
| 10 | 1010 | A |
| 11 | 1011 | B |
| 12 | 1100 | C |
| 13 | 1101 | D |
| 14 | 1110 | E |
| 15 | 1111 | F |

**Why hexadecimal is used in computing:**
- More **compact** than binary -- one hex digit replaces four binary digits
- Easier for humans to **read and remember** than long binary strings
- Direct conversion to and from binary (each hex digit = 4 bits)
- Used for: memory addresses, colour codes (e.g., #FF5733), MAC addresses, error codes, machine code

**Converting binary to hex:** Split into groups of 4 bits (nibbles) from the right, then convert each group.

Example: `11010110` -> `1101` `0110` -> **D6**

**Converting hex to decimal:** Multiply each digit by its place value (powers of 16).

Example: `3A` = (3 x 16) + (10 x 1) = 48 + 10 = **58**

```python
# Number system conversions
decimal_value = 200

# Decimal to binary
binary_str = bin(decimal_value)        # '0b11001000'
print(f"Decimal {decimal_value} = Binary {binary_str}")
print(f"Formatted: {decimal_value:08b}")

# Decimal to hexadecimal
hex_str = hex(decimal_value)           # '0xc8'
print(f"Decimal {decimal_value} = Hex {hex_str}")
print(f"Formatted: {decimal_value:02X}")

# Binary to decimal
binary_input = "10110101"
decimal_result = int(binary_input, 2)  # 181
print(f"Binary {binary_input} = Decimal {decimal_result}")

# Hex to decimal
hex_input = "D6"
decimal_result = int(hex_input, 16)    # 214
print(f"Hex {hex_input} = Decimal {decimal_result}")

# Manual binary to decimal conversion
def binary_to_decimal(binary_string):
    total = 0
    for i, bit in enumerate(reversed(binary_string)):
        if bit == '1':
            total += 2 ** i
    return total

print(f"Manual conversion: 10110101 = {binary_to_decimal('10110101')}")
```

```vb
' Number system conversions
Module NumberSystemsDemo
    Sub Main()
        Dim decimalValue As Integer = 200

        ' Decimal to binary
        Dim binaryStr As String = Convert.ToString(decimalValue, 2).PadLeft(8, "0"c)
        Console.WriteLine($"Decimal {decimalValue} = Binary {binaryStr}")

        ' Decimal to hexadecimal
        Dim hexStr As String = decimalValue.ToString("X2")
        Console.WriteLine($"Decimal {decimalValue} = Hex {hexStr}")

        ' Binary to decimal
        Dim binaryInput As String = "10110101"
        Dim decimalResult As Integer = Convert.ToInt32(binaryInput, 2)
        Console.WriteLine($"Binary {binaryInput} = Decimal {decimalResult}")

        ' Hex to decimal
        Dim hexInput As String = "D6"
        decimalResult = Convert.ToInt32(hexInput, 16)
        Console.WriteLine($"Hex {hexInput} = Decimal {decimalResult}")

        ' Manual binary to decimal conversion
        Console.WriteLine($"Manual conversion: 10110101 = {BinaryToDecimal("10110101")}")
    End Sub

    Function BinaryToDecimal(binaryString As String) As Integer
        Dim total As Integer = 0
        For i As Integer = 0 To binaryString.Length - 1
            If binaryString(binaryString.Length - 1 - i) = "1"c Then
                total += CInt(2 ^ i)
            End If
        Next
        Return total
    End Function
End Module
```

<div class="key-term" markdown="1">
**Hexadecimal** is a base-16 number system using digits 0-9 and letters A-F. It provides a compact, human-readable way to represent binary data, where each hexadecimal digit corresponds to exactly 4 binary bits.
</div>

<div class="exam-tip" markdown="1">
You must be able to convert quickly and accurately between binary, decimal, and hexadecimal in all directions. Practise until these conversions are automatic. A common approach for hex-to-decimal is to convert hex to binary first, then binary to decimal.
</div>

---

## Storage of Characters in Binary Form

Computers store all data -- including text characters -- as binary numbers. Each character (letter, digit, punctuation mark, control character) is assigned a unique numeric code according to a **character set** (also called a character encoding).

When you press a key on a keyboard, the character is converted to its binary code for storage and processing. When the character is displayed on screen, the binary code is converted back to a visual symbol using a font.

**Example:** The character `A` is stored as:
- ASCII code: 65 (decimal) = `01000001` (binary) = `41` (hex)
- The character `a` (lowercase) is ASCII code 97 = `01100001` = `61`

Note that uppercase and lowercase letters have **different** codes. The difference between `A` (65) and `a` (97) is exactly 32 -- this is by design and allows easy case conversion by flipping a single bit.

```python
# Character to binary representation
for char in "Hello!":
    code = ord(char)
    print(f"'{char}' -> ASCII: {code:3d} -> Binary: {code:08b} -> Hex: {code:02X}")

# Case conversion using bit manipulation
upper_a = ord('A')    # 65 = 01000001
lower_a = ord('a')    # 97 = 01100001
print(f"\n'A' = {upper_a:08b}")
print(f"'a' = {lower_a:08b}")
print(f"Difference = {lower_a - upper_a} (bit 5 is toggled)")

# Convert uppercase to lowercase by setting bit 5
char = 'H'
lower = chr(ord(char) | 0b00100000)  # Set bit 5
print(f"'{char}' -> '{lower}' (OR with 00100000)")
```

```vb
' Character to binary representation
Module CharacterDemo
    Sub Main()
        For Each c In "Hello!"
            Dim code As Integer = Asc(c)
            Console.WriteLine($"'{c}' -> ASCII: {code,3} -> Binary: {Convert.ToString(code, 2).PadLeft(8, "0"c)} -> Hex: {code:X2}")
        Next

        ' Case conversion
        Dim upperA As Integer = Asc("A"c)  ' 65
        Dim lowerA As Integer = Asc("a"c)  ' 97
        Console.WriteLine()
        Console.WriteLine($"'A' = {Convert.ToString(upperA, 2).PadLeft(8, "0"c)}")
        Console.WriteLine($"'a' = {Convert.ToString(lowerA, 2).PadLeft(8, "0"c)}")
        Console.WriteLine($"Difference = {lowerA - upperA} (bit 5 is toggled)")

        ' Convert uppercase to lowercase by setting bit 5
        Dim ch As Char = "H"c
        Dim lowerCh As Char = Chr(Asc(ch) Or &B00100000)
        Console.WriteLine($"'{ch}' -> '{lowerCh}' (OR with 00100000)")
    End Sub
End Module
```

---

## Standardised Character Sets

### ASCII (American Standard Code for Information Interchange)

- Uses **7 bits** per character, giving 128 possible characters (codes 0-127)
- Extended ASCII uses 8 bits (1 byte), giving 256 characters (codes 0-255)
- Covers uppercase and lowercase English letters, digits 0-9, punctuation, and control characters (e.g., newline, tab, backspace)
- Does **not** support characters from non-Latin scripts (Chinese, Arabic, Hindi, etc.)

| Code Range | Characters |
|---|---|
| 0-31 | Control characters (non-printable) |
| 32-47 | Space, punctuation, symbols |
| 48-57 | Digits 0-9 |
| 65-90 | Uppercase letters A-Z |
| 97-122 | Lowercase letters a-z |
| 128-255 | Extended ASCII (varies by encoding) |

### Unicode

- A universal standard designed to represent **every character** from every writing system in the world
- Currently defines over 149,000 characters from 161 scripts
- Several encoding formats:
  - **UTF-8:** Variable-length encoding using 1-4 bytes per character. ASCII characters use 1 byte, making it backward-compatible with ASCII. The most widely used encoding on the web
  - **UTF-16:** Uses 2 or 4 bytes per character. Used internally by Windows and Java
  - **UTF-32:** Uses a fixed 4 bytes per character. Simple but wasteful of storage

| Feature | ASCII | Unicode (UTF-8) |
|---|---|---|
| **Bits per character** | 7 (or 8 extended) | 8-32 (variable) |
| **Characters supported** | 128 (or 256) | Over 149,000 |
| **Languages** | English only | All world languages |
| **Storage per English char** | 1 byte | 1 byte (same as ASCII) |
| **Storage per non-English char** | Not supported | 2-4 bytes |
| **Backward compatibility** | N/A | UTF-8 is backward-compatible with ASCII |

<div class="key-term" markdown="1">
**ASCII** is a 7-bit character encoding standard representing 128 characters, primarily English letters, digits, and symbols. **Unicode** is a universal standard that assigns a unique code point to every character from every writing system, with UTF-8 being its most common encoding.
</div>

<div class="exam-tip" markdown="1">
ASCII uses 1 byte per character. Unicode (UTF-8) uses 1-4 bytes. This means Unicode files containing non-English text will be **larger** than equivalent ASCII files. However, for pure English text, UTF-8 and ASCII use the same amount of storage.
</div>

---

## Primitive Data Types: Boolean, Character, String, Integer, Real

A **data type** defines what kind of value a variable can hold and what operations can be performed on it. **Primitive data types** (also called simple or elementary data types) are the basic building blocks provided by a programming language.

| Data Type | Description | Example Values |
|---|---|---|
| **Boolean** | Holds only two values: `True` or `False` | `True`, `False` |
| **Character** | A single character (letter, digit, or symbol) | `'A'`, `'7'`, `'!'` |
| **String** | A sequence of zero or more characters | `"Hello"`, `""`, `"42"` |
| **Integer** | A whole number (positive, negative, or zero) | `42`, `-7`, `0` |
| **Real (Float)** | A number with a fractional part (decimal point) | `3.14`, `-0.5`, `2.0` |

```python
# Demonstrating primitive data types
is_active = True              # Boolean
grade = 'A'                   # Character (Python uses strings of length 1)
name = "Alice Smith"          # String
age = 17                      # Integer
height = 1.73                 # Real (float)

print(f"Boolean:   {is_active}  -> type: {type(is_active).__name__}")
print(f"Character: {grade}     -> type: {type(grade).__name__}")
print(f"String:    {name}  -> type: {type(name).__name__}")
print(f"Integer:   {age}       -> type: {type(age).__name__}")
print(f"Real:      {height}    -> type: {type(height).__name__}")

# Type matters for operations
print(f"\n'5' + '3' = {'5' + '3'}")      # String concatenation: '53'
print(f" 5  +  3  = {5 + 3}")            # Integer addition: 8
print(f" 5.0 + 3.0 = {5.0 + 3.0}")      # Float addition: 8.0
```

```vb
' Demonstrating primitive data types
Module DataTypesDemo
    Sub Main()
        Dim isActive As Boolean = True          ' Boolean
        Dim grade As Char = "A"c                ' Character
        Dim name As String = "Alice Smith"      ' String
        Dim age As Integer = 17                 ' Integer
        Dim height As Double = 1.73             ' Real (Double)

        Console.WriteLine($"Boolean:   {isActive}  -> type: {isActive.GetType().Name}")
        Console.WriteLine($"Character: {grade}     -> type: {grade.GetType().Name}")
        Console.WriteLine($"String:    {name}  -> type: {name.GetType().Name}")
        Console.WriteLine($"Integer:   {age}       -> type: {age.GetType().Name}")
        Console.WriteLine($"Real:      {height}    -> type: {height.GetType().Name}")

        ' Type matters for operations
        Console.WriteLine()
        Console.WriteLine($"'5' & '3' = {"5" & "3"}")         ' String concatenation: 53
        Console.WriteLine($" 5  +  3  = {5 + 3}")             ' Integer addition: 8
        Console.WriteLine($" 5.0 + 3.0 = {5.0 + 3.0}")       ' Double addition: 8.0
    End Sub
End Module
```

<div class="key-term" markdown="1">
**Primitive data types** are the simplest data types provided by a programming language, from which more complex data structures are built. They include Boolean, character, string, integer, and real (floating point).
</div>

---

## Storage Requirements for Each Data Type

The amount of memory required to store a value depends on its data type. Different languages and systems may use slightly different sizes, but typical values are:

| Data Type | Typical Storage | Range / Capacity |
|---|---|---|
| **Boolean** | 1 bit (often stored as 1 byte for alignment) | `True` or `False` |
| **Character (ASCII)** | 1 byte (8 bits) | 256 characters |
| **Character (Unicode)** | 1-4 bytes (UTF-8) or 2 bytes (UTF-16) | Over 149,000 characters |
| **Short Integer** | 2 bytes (16 bits) | -32,768 to 32,767 (signed) |
| **Integer** | 4 bytes (32 bits) | -2,147,483,648 to 2,147,483,647 (signed) |
| **Long Integer** | 8 bytes (64 bits) | Approximately -9.2 x 10^18 to 9.2 x 10^18 |
| **Single (float)** | 4 bytes (32 bits) | Approximately +/-3.4 x 10^38 (7 significant digits) |
| **Double** | 8 bytes (64 bits) | Approximately +/-1.7 x 10^308 (15 significant digits) |
| **String** | 1 byte per character (ASCII) + overhead | Variable length |

### Calculating Storage Requirements

To calculate the storage needed for a data set:

**Example:** A database stores 1000 student records, each containing:
- Name (30 characters, ASCII): 30 bytes
- Student ID (integer): 4 bytes
- Average mark (real/double): 8 bytes
- Active (boolean): 1 byte

Storage per record: 30 + 4 + 8 + 1 = **43 bytes**
Total for 1000 records: 43 x 1000 = **43,000 bytes** (approximately 42 KB)

```python
# Calculating storage requirements
import sys

# Python's internal sizes (may differ from theoretical minimums)
print("Python object sizes:")
print(f"  Boolean:   {sys.getsizeof(True)} bytes (Python overhead)")
print(f"  Integer:   {sys.getsizeof(42)} bytes (Python overhead)")
print(f"  Float:     {sys.getsizeof(3.14)} bytes (Python overhead)")
print(f"  Char:      {sys.getsizeof('A')} bytes (Python overhead)")
print(f"  String(5): {sys.getsizeof('Hello')} bytes (Python overhead)")

# Theoretical storage calculation
print("\nTheoretical storage for 1000 student records:")
name_bytes = 30       # 30 ASCII characters
id_bytes = 4          # 32-bit integer
mark_bytes = 8        # 64-bit double
active_bytes = 1      # Boolean

record_size = name_bytes + id_bytes + mark_bytes + active_bytes
total_size = record_size * 1000

print(f"  Per record: {record_size} bytes")
print(f"  1000 records: {total_size} bytes ({total_size / 1024:.1f} KB)")
```

```vb
' Calculating storage requirements
Module StorageDemo
    Sub Main()
        ' VB.NET data type sizes
        Console.WriteLine("VB.NET data type sizes:")
        Console.WriteLine($"  Boolean:   {Len(True)} byte(s)")
        Console.WriteLine($"  Char:      {Len("A"c)} byte(s)")
        Console.WriteLine($"  Short:     {Len(CShort(0))} bytes")
        Console.WriteLine($"  Integer:   {Len(CInt(0))} bytes")
        Console.WriteLine($"  Long:      {Len(CLng(0))} bytes")
        Console.WriteLine($"  Single:    {Len(CSng(0))} bytes")
        Console.WriteLine($"  Double:    {Len(CDbl(0))} bytes")

        ' Theoretical storage calculation
        Console.WriteLine()
        Console.WriteLine("Theoretical storage for 1000 student records:")
        Dim nameBytes As Integer = 30      ' 30 ASCII characters
        Dim idBytes As Integer = 4         ' Integer
        Dim markBytes As Integer = 8       ' Double
        Dim activeBytes As Integer = 1     ' Boolean

        Dim recordSize As Integer = nameBytes + idBytes + markBytes + activeBytes
        Dim totalSize As Integer = recordSize * 1000

        Console.WriteLine($"  Per record: {recordSize} bytes")
        Console.WriteLine($"  1000 records: {totalSize} bytes ({totalSize / 1024:F1} KB)")
    End Sub
End Module
```

<div class="exam-tip" markdown="1">
When calculating storage requirements in exams, clearly show your working: list each field, its data type, and its byte size, then multiply by the number of records. Remember that a string of `n` ASCII characters requires `n` bytes.
</div>

---

## Binary Arithmetic Techniques

### Binary Addition

Binary addition follows the same principles as decimal addition, with the following rules:

| A | B | Sum | Carry |
|---|---|---|---|
| 0 | 0 | 0 | 0 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 1 |

When adding three bits (including a carry): `1 + 1 + 1 = 1` with a carry of `1`.

**Example:** Add `01101011` + `00110101`

```
    1 1 1 1 1       (carry bits)
    0 1 1 0 1 0 1 1  (107)
  + 0 0 1 1 0 1 0 1  ( 53)
  -------------------
    1 0 1 0 0 0 0 0  (160)
```

### Binary Subtraction

Binary subtraction can be performed by adding the **two's complement** of the number to be subtracted (see the next section). Alternatively, the direct subtraction rules are:

| A | B | Difference | Borrow |
|---|---|---|---|
| 0 | 0 | 0 | 0 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 0 |
| 0 | 1 | 1 | 1 (borrow from next column) |

### Binary Multiplication

Binary multiplication is simpler than decimal multiplication because you only multiply by 0 or 1:

**Example:** `1101` x `1011` (13 x 11 = 143)

```
        1 1 0 1     (13)
      x 1 0 1 1     (11)
    -----------
        1 1 0 1     (1101 x 1)
      1 1 0 1 0     (1101 x 1, shifted left 1)
    0 0 0 0 0 0 0   (1101 x 0, shifted left 2)
  1 1 0 1 0 0 0 0   (1101 x 1, shifted left 3)
  ---------------
  1 0 0 0 1 1 1 1   (143)
```

### Logical Shifts

A **logical shift** moves all bits left or right by a specified number of positions. Empty positions are filled with zeros.

- **Left shift by 1:** Multiplies by 2 (each bit moves to a higher place value)
- **Right shift by 1:** Divides by 2 (integer division; each bit moves to a lower place value)
- **Left shift by n:** Multiplies by 2^n
- **Right shift by n:** Divides by 2^n

**Example:** Logical left shift of `00010110` (22) by 2 positions:
- `00010110` -> `01011000` (88) -- multiplied by 4

**Example:** Logical right shift of `00010110` (22) by 1 position:
- `00010110` -> `00001011` (11) -- divided by 2

```python
# Binary arithmetic operations
a = 0b01101011  # 107
b = 0b00110101  # 53

# Addition
result_add = a + b
print(f"Addition: {a:08b} ({a}) + {b:08b} ({b}) = {result_add:08b} ({result_add})")

# Subtraction
result_sub = a - b
print(f"Subtraction: {a:08b} ({a}) - {b:08b} ({b}) = {result_sub:08b} ({result_sub})")

# Multiplication
c = 0b1101  # 13
d = 0b1011  # 11
result_mul = c * d
print(f"Multiplication: {c:04b} ({c}) x {d:04b} ({d}) = {result_mul:08b} ({result_mul})")

# Logical shifts
value = 0b00010110  # 22
left_shift = value << 2     # Multiply by 4
right_shift = value >> 1    # Divide by 2

print(f"\nShifts on {value:08b} ({value}):")
print(f"  Left shift by 2:  {left_shift:08b} ({left_shift})")
print(f"  Right shift by 1: {right_shift:08b} ({right_shift})")
```

```vb
' Binary arithmetic operations
Module BinaryArithmeticDemo
    Sub Main()
        Dim a As Integer = &B01101011  ' 107
        Dim b As Integer = &B00110101  ' 53

        ' Addition
        Dim resultAdd As Integer = a + b
        Console.WriteLine($"Addition: {Convert.ToString(a, 2).PadLeft(8, "0"c)} ({a}) + {Convert.ToString(b, 2).PadLeft(8, "0"c)} ({b}) = {Convert.ToString(resultAdd, 2).PadLeft(8, "0"c)} ({resultAdd})")

        ' Subtraction
        Dim resultSub As Integer = a - b
        Console.WriteLine($"Subtraction: {Convert.ToString(a, 2).PadLeft(8, "0"c)} ({a}) - {Convert.ToString(b, 2).PadLeft(8, "0"c)} ({b}) = {Convert.ToString(resultSub, 2).PadLeft(8, "0"c)} ({resultSub})")

        ' Multiplication
        Dim c As Integer = &B1101  ' 13
        Dim d As Integer = &B1011  ' 11
        Dim resultMul As Integer = c * d
        Console.WriteLine($"Multiplication: {Convert.ToString(c, 2).PadLeft(4, "0"c)} ({c}) x {Convert.ToString(d, 2).PadLeft(4, "0"c)} ({d}) = {Convert.ToString(resultMul, 2).PadLeft(8, "0"c)} ({resultMul})")

        ' Logical shifts
        Dim value As Integer = &B00010110  ' 22
        Dim leftShift As Integer = value << 2
        Dim rightShift As Integer = value >> 1

        Console.WriteLine()
        Console.WriteLine($"Shifts on {Convert.ToString(value, 2).PadLeft(8, "0"c)} ({value}):")
        Console.WriteLine($"  Left shift by 2:  {Convert.ToString(leftShift, 2).PadLeft(8, "0"c)} ({leftShift})")
        Console.WriteLine($"  Right shift by 1: {Convert.ToString(rightShift, 2).PadLeft(8, "0"c)} ({rightShift})")
    End Sub
End Module
```

<div class="exam-tip" markdown="1">
When performing binary addition in an exam, write the carry bits above each column to keep track. **Overflow** occurs when the result is too large to fit in the available number of bits -- for example, adding two positive 8-bit numbers that produce a 9-bit result.
</div>

---

## Two's Complement and Sign and Magnitude Representation

Computers need to represent both **positive and negative** integers. There are two main methods.

### Sign and Magnitude

- The **most significant bit (MSB)** represents the sign: `0` = positive, `1` = negative
- The remaining bits represent the magnitude (absolute value) of the number
- Simple for humans to understand

**Example (8 bits):**
- `+42` = `00101010` (MSB is 0 = positive, remaining 7 bits = 42)
- `-42` = `10101010` (MSB is 1 = negative, remaining 7 bits = 42)

**Problems with sign and magnitude:**
- There are two representations of zero: `00000000` (+0) and `10000000` (-0)
- Arithmetic is complicated -- the processor must check signs before performing addition/subtraction
- Range for 8 bits: -127 to +127

### Two's Complement

Two's complement is the **standard method** used in modern computers to represent signed integers.

- The MSB has a **negative** place value: -128 for an 8-bit number
- All other bits have their usual positive place values
- Only one representation of zero (`00000000`)
- Arithmetic is straightforward -- addition and subtraction work normally without checking signs

**Converting positive to negative (and vice versa):**
1. Write the positive number in binary
2. **Invert** all bits (change 0 to 1 and 1 to 0) -- this gives the one's complement
3. **Add 1** to the result

**Example:** Convert +42 to -42 in 8-bit two's complement:
1. +42 = `00101010`
2. Invert: `11010101`
3. Add 1: `11010110`

So -42 = `11010110`

**Verify:** -128 + 64 + 16 + 4 + 2 = -128 + 86 = -42

**Range for n bits:**
- Minimum: `-2^(n-1)` (e.g., -128 for 8 bits)
- Maximum: `2^(n-1) - 1` (e.g., +127 for 8 bits)
- Total values: 2^n

| Feature | Sign and Magnitude | Two's Complement |
|---|---|---|
| MSB meaning | Sign bit (0=+, 1=-) | Negative place value |
| Zero representations | Two (+0 and -0) | One (0 only) |
| 8-bit range | -127 to +127 | -128 to +127 |
| Arithmetic | Complex (must check signs) | Simple (standard addition works) |
| Modern usage | Rarely used | Standard in all modern processors |

```python
# Two's complement operations
def to_twos_complement(value, bits=8):
    """Convert a signed integer to two's complement binary string."""
    if value >= 0:
        return format(value, f'0{bits}b')
    else:
        # Two's complement for negative numbers
        return format((1 << bits) + value, f'0{bits}b')

def from_twos_complement(binary_str):
    """Convert a two's complement binary string to a signed integer."""
    bits = len(binary_str)
    value = int(binary_str, 2)
    if binary_str[0] == '1':  # Negative number
        value -= (1 << bits)
    return value

# Demonstrate conversions
for num in [42, -42, 127, -128, 0, -1]:
    tc = to_twos_complement(num)
    back = from_twos_complement(tc)
    print(f"{num:>5d} -> {tc} -> {back:>5d}")

# Show the invert-and-add-one process
positive = 42
binary = format(positive, '08b')
inverted = ''.join('1' if b == '0' else '0' for b in binary)
result = format(int(inverted, 2) + 1, '08b')
print(f"\nConverting +{positive} to negative:")
print(f"  Original:  {binary}  ({positive})")
print(f"  Inverted:  {inverted}")
print(f"  Add 1:     {result}  ({from_twos_complement(result)})")
```

```vb
' Two's complement operations
Module TwosComplementDemo
    Function ToTwosComplement(value As Integer, Optional bits As Integer = 8) As String
        If value >= 0 Then
            Return Convert.ToString(value, 2).PadLeft(bits, "0"c)
        Else
            ' Two's complement for negative numbers
            Return Convert.ToString((1 << bits) + value, 2).PadLeft(bits, "0"c)
        End If
    End Function

    Function FromTwosComplement(binaryStr As String) As Integer
        Dim bits As Integer = binaryStr.Length
        Dim value As Integer = Convert.ToInt32(binaryStr, 2)
        If binaryStr(0) = "1"c Then  ' Negative number
            value -= (1 << bits)
        End If
        Return value
    End Function

    Sub Main()
        ' Demonstrate conversions
        Dim numbers() As Integer = {42, -42, 127, -128, 0, -1}
        For Each num In numbers
            Dim tc As String = ToTwosComplement(num)
            Dim back As Integer = FromTwosComplement(tc)
            Console.WriteLine($"{num,5} -> {tc} -> {back,5}")
        Next

        ' Show the invert-and-add-one process
        Dim positive As Integer = 42
        Dim binary As String = Convert.ToString(positive, 2).PadLeft(8, "0"c)
        Dim inverted As String = ""
        For Each b In binary
            inverted &= If(b = "0"c, "1", "0")
        Next
        Dim result As String = Convert.ToString(Convert.ToInt32(inverted, 2) + 1, 2).PadLeft(8, "0"c)
        Console.WriteLine($"{vbCrLf}Converting +{positive} to negative:")
        Console.WriteLine($"  Original:  {binary}  ({positive})")
        Console.WriteLine($"  Inverted:  {inverted}")
        Console.WriteLine($"  Add 1:     {result}  ({FromTwosComplement(result)})")
    End Sub
End Module
```

<div class="key-term" markdown="1">
**Two's complement** is a method for representing signed integers where the most significant bit has a negative place value. To negate a number: invert all bits and add 1.
</div>

<div class="exam-tip" markdown="1">
Common exam task: convert a negative decimal to two's complement binary. Always state the number of bits you are using. Remember that the "invert and add 1" trick works in both directions -- it converts positive to negative AND negative to positive.
</div>

---

## Floating Point Form: Nature and Uses

### Why Floating Point Is Needed

Integers can only represent whole numbers. To represent **real numbers** (numbers with fractional parts, like 3.14 or -0.001), computers use **floating point representation**.

Floating point is analogous to **scientific notation** in decimal:
- Decimal scientific notation: 6.022 x 10^23
- Binary floating point: mantissa x 2^exponent

### Structure of a Floating Point Number

A floating point number is stored in two parts:

- **Mantissa (M):** Contains the significant digits of the number. Determines the **precision** (how many significant figures can be stored).
- **Exponent (E):** Indicates how far and in which direction to shift the binary point. Determines the **range** (how large or small the number can be).

Both the mantissa and exponent are typically stored in **two's complement** form.

The value represented is: **M x 2^E**

### Normalisation

A floating point number is **normalised** to ensure a unique representation for every value and to maximise the precision of the mantissa.

**Rules for normalisation:**
- For a **positive** number: the mantissa must begin with `0.1...` (the first two bits are `01`)
- For a **negative** number: the mantissa must begin with `1.0...` (the first two bits are `10`)

If the mantissa does not follow these rules, shift it left or right and adjust the exponent accordingly.

**Example:** Normalise `0.00101` with exponent `0101` (5):
- Shift mantissa left by 2 to get `0.10100`
- Decrease exponent by 2: `0101` - `0010` = `0011` (3)
- Normalised: mantissa = `0.10100`, exponent = `0011`

### Worked Example: Converting Decimal to Floating Point

Convert **6.75** to normalised floating point with 8-bit mantissa and 4-bit exponent (both in two's complement).

1. Convert 6.75 to binary: `110.11` (4 + 2 + 0.5 + 0.25 = 6.75)
2. Normalise so mantissa starts with `0.1`: `0.110110` x 2^3
3. Mantissa (8 bits): `01101100`
4. Exponent (4 bits): `0011` (3 in two's complement)
5. Stored as: `01101100 0011`

### Worked Example: Converting Floating Point to Decimal

Given: mantissa = `01011000`, exponent = `0100` (both two's complement)

1. Exponent = `0100` = 4
2. Starting with mantissa `0.1011000`, shift binary point 4 places right: `01011.000`
3. Convert to decimal: 8 + 2 + 1 = **11.0**

```python
# Floating point representation simulation
def decimal_to_float_parts(value, mantissa_bits=8, exponent_bits=4):
    """Demonstrate the concept of floating point decomposition."""
    if value == 0:
        return "0" * mantissa_bits, "0" * exponent_bits

    # Determine sign
    negative = value < 0
    value = abs(value)

    # Convert to binary
    integer_part = int(value)
    fractional_part = value - integer_part

    # Integer part to binary
    int_binary = bin(integer_part)[2:] if integer_part > 0 else "0"

    # Fractional part to binary
    frac_binary = ""
    for _ in range(mantissa_bits):
        fractional_part *= 2
        if fractional_part >= 1:
            frac_binary += "1"
            fractional_part -= 1
        else:
            frac_binary += "0"

    full_binary = int_binary + "." + frac_binary
    print(f"  Binary: {full_binary}")

    # Count shifts needed to normalise (move point after leading 0)
    exponent = len(int_binary)

    # Build normalised mantissa
    mantissa = "0" + int_binary + frac_binary
    mantissa = mantissa[:mantissa_bits]

    if negative:
        print(f"  (Negative number - mantissa would use two's complement)")

    print(f"  Normalised mantissa: 0.{mantissa[1:]}")
    print(f"  Exponent: {exponent}")

    return mantissa, format(exponent, f'0{exponent_bits}b')

# Examples
for value in [6.75, 11.0, 0.375, -3.5]:
    print(f"\nConverting {value}:")
    m, e = decimal_to_float_parts(value)
    print(f"  Mantissa bits: {m}")
    print(f"  Exponent bits: {e}")
```

```vb
' Floating point representation simulation
Module FloatingPointDemo
    Sub DecimalToFloatParts(value As Double, Optional mantissaBits As Integer = 8, Optional exponentBits As Integer = 4)
        Console.WriteLine($"Converting {value}:")

        Dim negative As Boolean = value < 0
        Dim absValue As Double = Math.Abs(value)

        ' Integer part to binary
        Dim intPart As Integer = CInt(Math.Floor(absValue))
        Dim fracPart As Double = absValue - intPart
        Dim intBinary As String = Convert.ToString(intPart, 2)

        ' Fractional part to binary
        Dim fracBinary As String = ""
        Dim tempFrac As Double = fracPart
        For i As Integer = 1 To mantissaBits
            tempFrac *= 2
            If tempFrac >= 1 Then
                fracBinary &= "1"
                tempFrac -= 1
            Else
                fracBinary &= "0"
            End If
        Next

        Console.WriteLine($"  Binary: {intBinary}.{fracBinary}")

        Dim exponent As Integer = intBinary.Length
        Dim mantissa As String = ("0" & intBinary & fracBinary).Substring(0, mantissaBits)

        If negative Then
            Console.WriteLine("  (Negative number - mantissa would use two's complement)")
        End If

        Console.WriteLine($"  Normalised mantissa: 0.{mantissa.Substring(1)}")
        Console.WriteLine($"  Exponent: {exponent}")
        Console.WriteLine($"  Mantissa bits: {mantissa}")
        Console.WriteLine($"  Exponent bits: {Convert.ToString(exponent, 2).PadLeft(exponentBits, "0"c)}")
    End Sub

    Sub Main()
        DecimalToFloatParts(6.75)
        Console.WriteLine()
        DecimalToFloatParts(11.0)
        Console.WriteLine()
        DecimalToFloatParts(0.375)
        Console.WriteLine()
        DecimalToFloatParts(-3.5)
    End Sub
End Module
```

<div class="key-term" markdown="1">
**Floating point representation** stores a real number as a **mantissa** (the significant digits) and an **exponent** (the power of 2), allowing both very large and very small numbers to be represented. **Normalisation** ensures the mantissa starts with `01` (positive) or `10` (negative) to maximise precision.
</div>

---

## Advantages/Disadvantages of Integer vs Floating Point

Choosing between integer and floating point representation depends on the requirements of the application.

| Feature | Integer | Floating Point |
|---|---|---|
| **Values represented** | Whole numbers only | Numbers with fractional parts |
| **Precision** | Exact (within range) | May have rounding errors |
| **Range** | Limited (e.g., -2 billion to +2 billion for 32-bit) | Very large (e.g., up to ~10^308 for 64-bit double) |
| **Speed** | Faster arithmetic | Slower arithmetic |
| **Storage** | Fixed and predictable | Fixed but complex internal structure |
| **Use cases** | Counting, indexing, loops, exact values | Scientific calculations, measurements, graphics |

**Advantages of integer representation:**
- **Exact** -- no rounding errors; 5 + 3 is always exactly 8
- **Faster** -- integer arithmetic is simpler for the processor
- **Simpler** -- straightforward binary representation
- Best for: counting items, loop counters, array indices, currency (stored in pence/cents)

**Disadvantages of integer representation:**
- Cannot represent fractional values
- Limited range compared to floating point with the same number of bits

**Advantages of floating point representation:**
- Can represent fractional values and very large/small numbers
- Wide range of values
- Suitable for scientific and engineering calculations

**Disadvantages of floating point representation:**
- **Rounding errors** -- not all real numbers can be represented exactly
- **Slower** -- floating point operations are more complex
- **Comparisons are unreliable** -- two floating point numbers that should be equal may differ slightly due to rounding

```python
# Demonstrating integer precision vs floating point rounding
# Integer: exact
total_int = 0
for i in range(10):
    total_int += 1
print(f"Integer sum of ten 1s: {total_int}")  # Exactly 10

# Floating point: potential rounding error
total_float = 0.0
for i in range(10):
    total_float += 0.1
print(f"Float sum of ten 0.1s: {total_float}")  # Not exactly 1.0!
print(f"Is it exactly 1.0? {total_float == 1.0}")  # False!
print(f"Actual value: {total_float:.20f}")

# Why 0.1 cannot be represented exactly in binary
# 0.1 in binary is 0.0001100110011... (repeating), like 1/3 in decimal
```

```vb
' Demonstrating integer precision vs floating point rounding
Module IntVsFloatDemo
    Sub Main()
        ' Integer: exact
        Dim totalInt As Integer = 0
        For i As Integer = 1 To 10
            totalInt += 1
        Next
        Console.WriteLine($"Integer sum of ten 1s: {totalInt}")  ' Exactly 10

        ' Floating point: potential rounding error
        Dim totalFloat As Double = 0.0
        For i As Integer = 1 To 10
            totalFloat += 0.1
        Next
        Console.WriteLine($"Float sum of ten 0.1s: {totalFloat}")
        Console.WriteLine($"Is it exactly 1.0? {totalFloat = 1.0}")
        Console.WriteLine($"Actual value: {totalFloat:F20}")

        ' Comparison issue
        Dim a As Double = 0.1 + 0.2
        Dim b As Double = 0.3
        Console.WriteLine($"{vbCrLf}0.1 + 0.2 = {a:F20}")
        Console.WriteLine($"      0.3 = {b:F20}")
        Console.WriteLine($"Are they equal? {a = b}")
    End Sub
End Module
```

<div class="exam-tip" markdown="1">
A classic exam question: "Why might `0.1 + 0.2` not equal `0.3` in a program?" Answer: because 0.1 cannot be represented exactly in binary floating point (it is a repeating binary fraction), so small rounding errors accumulate. This is why you should **never compare floating point numbers for exact equality**.
</div>

---

## Convert Between Real Number and Floating Point Form

### Decimal to Normalised Floating Point

**Example:** Convert **-5.5** to normalised floating point with a 8-bit mantissa and 4-bit exponent (both two's complement).

**Step 1:** Convert the positive value to binary.
- 5.5 = `101.1` in binary

**Step 2:** Normalise (positive form first).
- `0.1011` x 2^3 (shift binary point 3 places left)
- Mantissa (positive): `01011000`

**Step 3:** Negate the mantissa (because the original number is negative).
- Invert `01011000` -> `10100111`
- Add 1: `10101000`
- Mantissa: `10101000`

**Step 4:** Exponent = 3 = `0011` in 4-bit two's complement.

**Result:** `10101000 0011`

**Verify:** Start with mantissa `10101000`:
- This is negative (starts with 1). Value = -128 + 32 + 8 = -88 out of 128 = -88/128 = -0.6875
- Exponent = 3, so multiply by 2^3 = 8
- -0.6875 x 8 = **-5.5**

### Floating Point to Decimal

**Example:** Convert mantissa `01100000`, exponent `0101` to decimal.

**Step 1:** Determine the exponent value.
- `0101` = 5

**Step 2:** Write the mantissa with the binary point after the first bit.
- `0.1100000`

**Step 3:** Shift the binary point right by 5 positions.
- `011000.00`

**Step 4:** Convert to decimal.
- `011000` = 16 + 8 = **24**

**Example with negative mantissa:** mantissa `10110000`, exponent `0011`

**Step 1:** Exponent = `0011` = 3

**Step 2:** The mantissa starts with `1`, so it is negative (two's complement).
- `1.0110000`

**Step 3:** Shift the binary point right by 3.
- `1011.0000`

**Step 4:** Convert from two's complement: -8 + 2 + 1 = **-5**

```python
# Converting between decimal and floating point representation
def decimal_to_normalised_fp(value, m_bits=8, e_bits=4):
    """Convert decimal to normalised floating point."""
    if value == 0:
        return "0" * m_bits, "0" * e_bits, 0

    negative = value < 0
    abs_val = abs(value)

    # Convert to binary string with fractional part
    int_part = int(abs_val)
    frac_part = abs_val - int_part
    int_bin = bin(int_part)[2:] if int_part > 0 else ""
    frac_bin = ""
    temp = frac_part
    for _ in range(m_bits * 2):
        temp *= 2
        if temp >= 1:
            frac_bin += "1"
            temp -= 1
        else:
            frac_bin += "0"
        if temp == 0:
            break

    if int_part > 0:
        exponent = len(int_bin)
        mantissa_digits = int_bin + frac_bin
    else:
        # Find first 1 in fractional part
        first_one = frac_bin.index('1')
        exponent = -(first_one)
        mantissa_digits = frac_bin[first_one:]

    # Build mantissa: "0" + significant digits, padded to m_bits
    mantissa_str = "0" + mantissa_digits
    mantissa_str = mantissa_str[:m_bits].ljust(m_bits, '0')

    if negative:
        # Two's complement of mantissa
        val = int(mantissa_str, 2)
        val = (1 << m_bits) - val
        mantissa_str = format(val, f'0{m_bits}b')

    # Exponent in two's complement
    if exponent < 0:
        exp_str = format((1 << e_bits) + exponent, f'0{e_bits}b')
    else:
        exp_str = format(exponent, f'0{e_bits}b')

    return mantissa_str, exp_str, exponent

# Test conversions
test_values = [6.75, -5.5, 11.0, 0.375]
for val in test_values:
    m, e, exp_dec = decimal_to_normalised_fp(val)
    print(f"{val:>7} -> Mantissa: {m}  Exponent: {e} ({exp_dec})")
```

```vb
' Converting between decimal and floating point representation
Module FPConversionDemo
    Sub ConvertToFP(value As Double, Optional mBits As Integer = 8, Optional eBits As Integer = 4)
        Console.Write($"{value,7} -> ")

        Dim negative As Boolean = value < 0
        Dim absVal As Double = Math.Abs(value)

        ' Convert integer part to binary
        Dim intPart As Integer = CInt(Math.Floor(absVal))
        Dim fracPart As Double = absVal - intPart
        Dim intBin As String = If(intPart > 0, Convert.ToString(intPart, 2), "")

        ' Convert fractional part to binary
        Dim fracBin As String = ""
        Dim temp As Double = fracPart
        For i As Integer = 1 To mBits * 2
            temp *= 2
            If temp >= 1 Then
                fracBin &= "1"
                temp -= 1
            Else
                fracBin &= "0"
            End If
            If temp = 0 Then Exit For
        Next

        Dim exponent As Integer = intBin.Length

        ' Build mantissa
        Dim mantissa As String = ("0" & intBin & fracBin)
        If mantissa.Length > mBits Then
            mantissa = mantissa.Substring(0, mBits)
        Else
            mantissa = mantissa.PadRight(mBits, "0"c)
        End If

        If negative Then
            ' Two's complement
            Dim val As Integer = Convert.ToInt32(mantissa, 2)
            val = (1 << mBits) - val
            mantissa = Convert.ToString(val, 2).PadLeft(mBits, "0"c)
        End If

        Dim expStr As String
        If exponent < 0 Then
            expStr = Convert.ToString((1 << eBits) + exponent, 2).PadLeft(eBits, "0"c)
        Else
            expStr = Convert.ToString(exponent, 2).PadLeft(eBits, "0"c)
        End If

        Console.WriteLine($"Mantissa: {mantissa}  Exponent: {expStr} ({exponent})")
    End Sub

    Sub Main()
        ConvertToFP(6.75)
        ConvertToFP(-5.5)
        ConvertToFP(11.0)
        ConvertToFP(0.375)
    End Sub
End Module
```

<div class="exam-tip" markdown="1">
When converting between decimal and floating point in exams, always clearly show: (1) the binary conversion, (2) the normalisation step, (3) the final mantissa and exponent in the specified format. State whether you are using two's complement for both parts. Verify your answer by converting back.
</div>

---

## Truncation and Rounding, Effect on Accuracy

When a number cannot be represented exactly in the available number of bits, it must be approximated. There are two main methods: **truncation** and **rounding**.

### Truncation

**Truncation** simply discards (cuts off) the digits or bits beyond the available precision. No adjustment is made to the remaining digits.

**Example (decimal):** Storing 3.14159 with 2 decimal places by truncation gives **3.14** (the remaining digits are simply dropped).

**Example (binary):** If the mantissa has 8 bits and the true value requires 12 bits:
- Full value: `0.10110111 0101`
- Truncated to 8 bits: `01011011`
- The bits `0101` are lost

Truncation always rounds **towards zero**. Positive numbers become slightly smaller; negative numbers become slightly closer to zero (less negative).

### Rounding

**Rounding** adjusts the last retained bit based on the value of the first discarded bit. If the first discarded bit is `1`, the last retained bit is rounded up (incremented by 1). If it is `0`, the value is left unchanged.

**Example (decimal):** Storing 3.14159 with 2 decimal places by rounding gives **3.14** (since the third decimal digit, 1, is less than 5).

**Example (binary):** Truncated mantissa: `01011011`, first discarded bit: `1`
- Round up: `01011011` + `1` = `01011100`

Rounding generally produces a **more accurate** result than truncation because it finds the closest representable value.

### Comparison

| Aspect | Truncation | Rounding |
|---|---|---|
| Method | Discard excess bits | Adjust based on first discarded bit |
| Direction of error | Always towards zero | Closest representable value |
| Accuracy | Less accurate | More accurate |
| Simplicity | Simpler to implement | Slightly more complex |
| Bias | Systematic bias (always reduces magnitude) | Less biased (errors can go either way) |

### Effect on Accuracy

Both truncation and rounding introduce **representation errors** (also called quantisation errors). These errors can have significant effects:

- **Accumulation:** Small errors can accumulate over many calculations, leading to large inaccuracies in final results
- **Loss of significance:** When subtracting two nearly equal floating point numbers, the significant digits cancel out and the result may be dominated by rounding errors
- **Comparison failures:** Two values that should be mathematically equal may differ slightly due to rounding, making direct comparison unreliable

### Precision vs Range Trade-off

Given a fixed total number of bits for a floating point number:

- **More mantissa bits** -> higher precision (more significant figures) but smaller range
- **More exponent bits** -> larger range (bigger and smaller numbers) but lower precision

This fundamental trade-off means that no single floating point format is perfect for all applications. Different applications may require different balances:
- Scientific computing often needs high precision (many mantissa bits)
- Graphics rendering may need large range (many exponent bits)

```python
# Demonstrating truncation vs rounding
import math

# Decimal example
value = 3.14159265

# Truncation (towards zero)
def truncate(number, decimals):
    factor = 10 ** decimals
    return int(number * factor) / factor

# Rounding
truncated = truncate(value, 2)
rounded = round(value, 2)

print(f"Original value: {value}")
print(f"Truncated to 2dp: {truncated}")
print(f"Rounded to 2dp:   {rounded}")
print(f"Truncation error: {abs(value - truncated):.10f}")
print(f"Rounding error:   {abs(value - rounded):.10f}")

# Accumulation of errors
print("\nError accumulation over 1000 additions of 0.1:")
total = 0.0
for _ in range(1000):
    total += 0.1
expected = 100.0
print(f"  Expected: {expected}")
print(f"  Actual:   {total:.15f}")
print(f"  Error:    {abs(total - expected):.15f}")

# Loss of significance
a = 1.000000001
b = 1.000000000
print(f"\nLoss of significance:")
print(f"  a = {a:.12f}")
print(f"  b = {b:.12f}")
print(f"  a - b = {a - b:.15f} (expected 0.000000001)")
```

```vb
' Demonstrating truncation vs rounding
Module AccuracyDemo
    Function Truncate(number As Double, decimals As Integer) As Double
        Dim factor As Double = 10 ^ decimals
        Return Math.Floor(number * factor) / factor
    End Function

    Sub Main()
        Dim value As Double = 3.14159265

        ' Truncation vs rounding
        Dim truncated As Double = Truncate(value, 2)
        Dim rounded As Double = Math.Round(value, 2)

        Console.WriteLine($"Original value: {value}")
        Console.WriteLine($"Truncated to 2dp: {truncated}")
        Console.WriteLine($"Rounded to 2dp:   {rounded}")
        Console.WriteLine($"Truncation error: {Math.Abs(value - truncated):F10}")
        Console.WriteLine($"Rounding error:   {Math.Abs(value - rounded):F10}")

        ' Accumulation of errors
        Console.WriteLine()
        Console.WriteLine("Error accumulation over 1000 additions of 0.1:")
        Dim total As Double = 0.0
        For i As Integer = 1 To 1000
            total += 0.1
        Next
        Dim expected As Double = 100.0
        Console.WriteLine($"  Expected: {expected}")
        Console.WriteLine($"  Actual:   {total:F15}")
        Console.WriteLine($"  Error:    {Math.Abs(total - expected):F15}")

        ' Loss of significance
        Dim a As Double = 1.000000001
        Dim b As Double = 1.0
        Console.WriteLine()
        Console.WriteLine("Loss of significance:")
        Console.WriteLine($"  a = {a:F12}")
        Console.WriteLine($"  b = {b:F12}")
        Console.WriteLine($"  a - b = {(a - b):F15} (expected 0.000000001)")
    End Sub
End Module
```

<div class="key-term" markdown="1">
**Truncation** discards excess bits without adjustment, always introducing an error towards zero. **Rounding** adjusts the last retained bit based on the discarded bits, producing a closer approximation. Both introduce errors, but rounding is generally more accurate.
</div>

<div class="exam-tip" markdown="1">
When discussing floating point accuracy, always mention: (1) the trade-off between mantissa bits (precision) and exponent bits (range), (2) that truncation/rounding errors can accumulate over many calculations, and (3) that this is why floating point numbers should never be compared for exact equality. Give the example of `0.1 + 0.2 != 0.3`.
</div>
