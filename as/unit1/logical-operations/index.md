---
layout: topic
title: "Logical Operations"
level: "AS Level"
level_url: "/as/"
unit_name: "Unit 1: Fundamentals of Computer Science"
unit_url: "/as/unit1/"
prev_topic: "/as/unit1/hardware-communication/"
next_topic: "/as/unit1/data-transmission/"
---

## Truth Tables for AND, OR, NOT and XOR

**Logic gates** are the fundamental building blocks of digital circuits inside a computer. Each gate takes one or more binary inputs (0 or 1) and produces a single binary output based on a logical rule. These rules are formally described using **truth tables**, which show every possible combination of inputs and the resulting output.

### AND Gate

The AND gate outputs `1` only when **all** inputs are `1`. If any input is `0`, the output is `0`.

**Boolean expression:** `Q = A AND B` or `Q = A . B` or `Q = A /\ B`

| A | B | Q = A AND B |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

Think of AND as: "both must be true."

### OR Gate

The OR gate outputs `1` when **at least one** input is `1`. It only outputs `0` when all inputs are `0`.

**Boolean expression:** `Q = A OR B` or `Q = A + B` or `Q = A \/ B`

| A | B | Q = A OR B |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

Think of OR as: "at least one must be true."

### NOT Gate (Inverter)

The NOT gate has a single input and outputs the **opposite** (complement) of that input. It inverts the signal.

**Boolean expression:** `Q = NOT A` or `Q = A̅` or `Q = ¬A`

| A | Q = NOT A |
|---|---|
| 0 | 1 |
| 1 | 0 |

### XOR Gate (Exclusive OR)

The XOR gate outputs `1` when the inputs are **different**. It outputs `0` when the inputs are the same.

**Boolean expression:** `Q = A XOR B` or `Q = A ⊕ B`

| A | B | Q = A XOR B |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

Think of XOR as: "one or the other, but not both."

<div class="key-term" markdown="1">
A **truth table** is a table that shows every possible combination of inputs to a logic gate and the corresponding output. For a gate with `n` inputs, the truth table has `2^n` rows.
</div>

### NAND and NOR Gates

These are combinations of the basic gates:

**NAND (NOT AND):** The output is the inverse of AND. Outputs `0` only when both inputs are `1`.

| A | B | Q = A NAND B |
|---|---|---|
| 0 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

**NOR (NOT OR):** The output is the inverse of OR. Outputs `1` only when both inputs are `0`.

| A | B | Q = A NOR B |
|---|---|---|
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 0 |

NAND and NOR are called **universal gates** because any other logic gate can be built using only NAND gates or only NOR gates.

### Generating Truth Tables for Combined Expressions

For more complex expressions, work column by column, evaluating intermediate results before the final output.

**Example:** `Q = (A AND B) OR (NOT C)`

| A | B | C | A AND B | NOT C | Q = (A AND B) OR (NOT C) |
|---|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 1 | 1 |
| 0 | 0 | 1 | 0 | 0 | 0 |
| 0 | 1 | 0 | 0 | 1 | 1 |
| 0 | 1 | 1 | 0 | 0 | 0 |
| 1 | 0 | 0 | 0 | 1 | 1 |
| 1 | 0 | 1 | 0 | 0 | 0 |
| 1 | 1 | 0 | 1 | 1 | 1 |
| 1 | 1 | 1 | 1 | 0 | 1 |

<div class="exam-tip" markdown="1">
When building a truth table for a combined expression, always add **intermediate columns** for sub-expressions. Work from the innermost brackets outward. This avoids mistakes and earns method marks in exams.
</div>

---

## Apply Logical Operations in Programming (Clearing Registers, Masking)

Logical operations are not just theoretical -- they have critical practical applications in programming, especially for manipulating individual bits within binary data. This is called **bitwise manipulation**.

### Bitwise Operators in Programming

Most programming languages provide operators that apply logic gates to each corresponding pair of bits in two binary numbers:

| Operation | Python | VB.NET | Effect |
|---|---|---|---|
| AND | `&` | `And` | Returns 1 only where both bits are 1 |
| OR | `\|` | `Or` | Returns 1 where at least one bit is 1 |
| XOR | `^` | `Xor` | Returns 1 where bits are different |
| NOT | `~` | `Not` | Inverts all bits |
| Left shift | `<<` | `<<` | Shifts bits left (multiplies by 2) |
| Right shift | `>>` | `>>` | Shifts bits right (divides by 2) |

### Masking with AND (Extracting Bits)

**AND masking** is used to **extract** or **isolate** specific bits from a binary value. The mask contains `1` in the positions you want to keep and `0` in the positions you want to discard.

**Example:** Extract the lower 4 bits (nibble) from the byte `11010110`:

```
  Data:   1 1 0 1 0 1 1 0
  Mask:   0 0 0 0 1 1 1 1   (0x0F)
  Result: 0 0 0 0 0 1 1 0   (only lower nibble preserved)
```

```python
# AND masking to extract the lower nibble
data = 0b11010110      # 214 in decimal
mask = 0b00001111      # 0x0F - keeps lower 4 bits

lower_nibble = data & mask

print(f"Data:         {data:08b}  ({data})")
print(f"Mask:         {mask:08b}  ({mask})")
print(f"Lower nibble: {lower_nibble:08b}  ({lower_nibble})")

# Practical use: extracting the red component from an RGB colour
colour = 0xE85A2F  # A colour value (R=232, G=90, B=47)
red   = (colour >> 16) & 0xFF
green = (colour >> 8) & 0xFF
blue  = colour & 0xFF
print(f"\nColour: #{colour:06X}")
print(f"Red: {red}, Green: {green}, Blue: {blue}")
```

```vb
' AND masking to extract the lower nibble
Module MaskingDemo
    Sub Main()
        Dim data As Integer = &B11010110     ' 214 in decimal
        Dim mask As Integer = &B00001111     ' 0x0F - keeps lower 4 bits

        Dim lowerNibble As Integer = data And mask

        Console.WriteLine($"Data:         {Convert.ToString(data, 2).PadLeft(8, "0"c)}  ({data})")
        Console.WriteLine($"Mask:         {Convert.ToString(mask, 2).PadLeft(8, "0"c)}  ({mask})")
        Console.WriteLine($"Lower nibble: {Convert.ToString(lowerNibble, 2).PadLeft(8, "0"c)}  ({lowerNibble})")

        ' Practical use: extracting the red component from an RGB colour
        Dim colour As Integer = &HE85A2F
        Dim red As Integer = (colour >> 16) And &HFF
        Dim green As Integer = (colour >> 8) And &HFF
        Dim blue As Integer = colour And &HFF
        Console.WriteLine()
        Console.WriteLine($"Colour: #{colour:X6}")
        Console.WriteLine($"Red: {red}, Green: {green}, Blue: {blue}")
    End Sub
End Module
```

### Masking with OR (Setting Bits)

**OR masking** is used to **set** specific bits to `1` without affecting the other bits. The mask contains `1` in the positions you want to force to `1` and `0` in the positions you want to leave unchanged.

**Example:** Set bit 7 (the most significant bit) of the byte `00110100`:

```
  Data:   0 0 1 1 0 1 0 0
  Mask:   1 0 0 0 0 0 0 0   (0x80)
  Result: 1 0 1 1 0 1 0 0   (bit 7 is now set)
```

```python
# OR masking to set specific bits
data = 0b00110100
mask = 0b10000000  # Set bit 7

result = data | mask
print(f"Data:   {data:08b}")
print(f"Mask:   {mask:08b}")
print(f"Result: {result:08b}  (bit 7 is now set)")
```

```vb
' OR masking to set specific bits
Module OrMaskDemo
    Sub Main()
        Dim data As Integer = &B00110100
        Dim mask As Integer = &B10000000  ' Set bit 7

        Dim result As Integer = data Or mask
        Console.WriteLine($"Data:   {Convert.ToString(data, 2).PadLeft(8, "0"c)}")
        Console.WriteLine($"Mask:   {Convert.ToString(mask, 2).PadLeft(8, "0"c)}")
        Console.WriteLine($"Result: {Convert.ToString(result, 2).PadLeft(8, "0"c)}  (bit 7 is now set)")
    End Sub
End Module
```

### Masking with XOR (Toggling Bits)

**XOR masking** is used to **toggle** (flip) specific bits. A `1` in the mask flips the corresponding bit; a `0` leaves it unchanged.

```python
# XOR masking to toggle bits
data = 0b11010110
mask = 0b11110000  # Toggle the upper nibble

result = data ^ mask
print(f"Data:   {data:08b}")
print(f"Mask:   {mask:08b}")
print(f"Result: {result:08b}  (upper nibble toggled)")
```

```vb
' XOR masking to toggle bits
Module XorMaskDemo
    Sub Main()
        Dim data As Integer = &B11010110
        Dim mask As Integer = &B11110000  ' Toggle the upper nibble

        Dim result As Integer = data Xor mask
        Console.WriteLine($"Data:   {Convert.ToString(data, 2).PadLeft(8, "0"c)}")
        Console.WriteLine($"Mask:   {Convert.ToString(mask, 2).PadLeft(8, "0"c)}")
        Console.WriteLine($"Result: {Convert.ToString(result, 2).PadLeft(8, "0"c)}  (upper nibble toggled)")
    End Sub
End Module
```

### Clearing a Register

To **clear a register** (set all bits to zero), you AND the register with `0`:

```
  Register: 1 1 0 1 0 1 1 0
  AND with: 0 0 0 0 0 0 0 0
  Result:   0 0 0 0 0 0 0 0
```

Alternatively, XOR a register with itself to clear it (this is a common assembly language trick):

```
  Register: 1 1 0 1 0 1 1 0
  XOR with: 1 1 0 1 0 1 1 0   (same value)
  Result:   0 0 0 0 0 0 0 0
```

```python
# Clearing a register
register = 0b11010110

# Method 1: AND with zero
cleared = register & 0b00000000
print(f"AND with 0: {cleared:08b}")

# Method 2: XOR with itself
cleared = register ^ register
print(f"XOR with self: {cleared:08b}")
```

```vb
' Clearing a register
Module ClearRegisterDemo
    Sub Main()
        Dim register As Integer = &B11010110

        ' Method 1: AND with zero
        Dim cleared As Integer = register And 0
        Console.WriteLine($"AND with 0: {Convert.ToString(cleared, 2).PadLeft(8, "0"c)}")

        ' Method 2: XOR with itself
        cleared = register Xor register
        Console.WriteLine($"XOR with self: {Convert.ToString(cleared, 2).PadLeft(8, "0"c)}")
    End Sub
End Module
```

<div class="key-term" markdown="1">
**Bit masking** is the technique of using a logical operation (AND, OR, XOR) with a carefully chosen pattern of bits (the mask) to extract, set, toggle, or clear specific bits within a binary value.
</div>

<div class="exam-tip" markdown="1">
Remember the masking rules: **AND to extract/clear** bits (0 in the mask clears, 1 preserves), **OR to set** bits (1 in the mask sets, 0 preserves), **XOR to toggle** bits (1 in the mask flips, 0 preserves). These are frequently tested in exams.
</div>

---

## Simplify Boolean Expressions Using Identities and Rules

Boolean algebra allows us to simplify complex logical expressions, which in turn simplifies the digital circuits needed to implement them (fewer gates = cheaper, faster, less power).

### Boolean Identities

These fundamental identities form the basis of Boolean simplification:

**Identity Laws:**
- `A AND 1 = A` (ANDing with 1 leaves the value unchanged)
- `A OR 0 = A` (ORing with 0 leaves the value unchanged)

**Null (Annihilation) Laws:**
- `A AND 0 = 0` (ANDing with 0 always gives 0)
- `A OR 1 = 1` (ORing with 1 always gives 1)

**Idempotent Laws:**
- `A AND A = A`
- `A OR A = A`

**Complement Laws:**
- `A AND (NOT A) = 0` (a value ANDed with its complement is always 0)
- `A OR (NOT A) = 1` (a value ORed with its complement is always 1)

**Double Negation (Involution):**
- `NOT (NOT A) = A`

**Commutative Laws:**
- `A AND B = B AND A`
- `A OR B = B OR A`

**Associative Laws:**
- `(A AND B) AND C = A AND (B AND C)`
- `(A OR B) OR C = A OR (B OR C)`

**Distributive Laws:**
- `A AND (B OR C) = (A AND B) OR (A AND C)`
- `A OR (B AND C) = (A OR B) AND (A OR C)`

**Absorption Laws:**
- `A OR (A AND B) = A`
- `A AND (A OR B) = A`

### De Morgan's Laws

De Morgan's Laws are essential for simplifying expressions involving NOT applied to compound expressions:

- `NOT (A AND B) = (NOT A) OR (NOT B)` -- "break the bar, change the sign"
- `NOT (A OR B) = (NOT A) AND (NOT B)`

Using the shorthand notation (overbar for NOT, `.` for AND, `+` for OR):

- `(A . B)̅ = A̅ + B̅`
- `(A + B)̅ = A̅ . B̅`

### Worked Examples

**Example 1:** Simplify `(A AND B) OR (A AND (NOT B))`

Using the notation `A.B + A.B̅`:

```
  A.B + A.B̅
= A.(B + B̅)      [Distributive law - factor out A]
= A.1             [Complement law: B + B̅ = 1]
= A               [Identity law: A.1 = A]
```

**Example 2:** Simplify `(NOT A AND NOT B) OR (NOT A AND B)`

Using the notation `A̅.B̅ + A̅.B`:

```
  A̅.B̅ + A̅.B
= A̅.(B̅ + B)      [Distributive law - factor out A̅]
= A̅.1             [Complement law: B̅ + B = 1]
= A̅               [Identity law]
= NOT A
```

**Example 3:** Simplify `A OR (A AND B)`

```
  A + A.B
= A               [Absorption law]
```

**Example 4:** Apply De Morgan's to `NOT(A OR B)`

```
  NOT(A OR B)
= (NOT A) AND (NOT B)    [De Morgan's law]
= A̅.B̅
```

**Example 5:** Simplify `(A AND B) OR (A AND B AND C)`

```
  A.B + A.B.C
= A.B.(1 + C)     [Distributive law - factor out A.B]
= A.B.1           [Null law: 1 + C = 1]
= A.B             [Identity law]
```

<div class="key-term" markdown="1">
**De Morgan's Laws** state that the complement of a conjunction (AND) is the disjunction (OR) of the complements, and vice versa. In simpler terms: "break the bar, change the sign."
</div>

<div class="exam-tip" markdown="1">
When simplifying Boolean expressions in an exam, **show every step** and **name the law** you are applying at each stage. Common mistakes include forgetting to apply the distributive law correctly or misapplying De Morgan's. Always verify your simplified expression produces the same truth table as the original.
</div>
