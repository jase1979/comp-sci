---
layout: topic
title: "Data Representation & Data Types"
level: "A2 Level"
level_url: "/a2/"
unit_name: "Unit 4: Architecture, Data, Communication & Applications"
unit_url: "/a2/unit4/"
subtopics:
  - "Binary arithmetic techniques (A2 level)"
  - "Two's complement and sign and magnitude (A2 level)"
  - "Floating point form: Nature and uses (A2 level)"
  - "Advantages/disadvantages of integer vs floating point (A2 level)"
  - "Convert between real number and floating point (A2 level)"
  - "Truncation and rounding, effect on accuracy (A2 level)"
  - "Shift functions: Logical and arithmetic shifts"
  - "Interpret and apply shifts in algorithms and programs"
  - "Causes of overflow and underflow"
---

## Binary Arithmetic at A2 Level

### Binary Addition

Binary addition follows the same rules as denary addition, using four basic rules:

| Operation | Result | Carry |
|---|---|---|
| 0 + 0 | 0 | 0 |
| 0 + 1 | 1 | 0 |
| 1 + 0 | 1 | 0 |
| 1 + 1 | 0 | 1 |

When adding 1 + 1 + 1 (from a carry), the result is 1 with a carry of 1.

**Worked Example**: Add 01101010 (106) and 00110101 (53)

```
    1 1 1 1 1 0
    0 1 1 0 1 0 1 0    (106)
  + 0 0 1 1 0 1 0 1    ( 53)
  -------------------
    1 0 0 1 1 1 1 1    (159)
```

### Binary Subtraction Using Two's Complement

To subtract binary number B from binary number A, we add A to the two's complement of B. This avoids the need for a dedicated subtraction circuit.

**Method**: A - B = A + (two's complement of B)

**Worked Example**: Calculate 10010110 (150) - 00110010 (50) using 8-bit unsigned values converted to two's complement subtraction.

Step 1: Find two's complement of 00110010
- Flip all bits: 11001101
- Add 1:        11001110

Step 2: Add the original number to the two's complement
```
    1 1 1 1 1 1 0
    1 0 0 1 0 1 1 0    (150)
  + 1 1 0 0 1 1 1 0    (-50 in two's complement)
  -------------------
  1 0 1 1 0 0 1 0 0
```

Step 3: Discard the overflow (9th) bit. Result: **01100100** = 100.

150 - 50 = 100. Correct.

<div class="exam-tip" markdown="1">
When performing binary subtraction, always use the two's complement method: negate the number being subtracted (flip bits, add 1), then add. If there is a carry out of the most significant bit, discard it. Show every step of your working clearly in exam answers.
</div>

---

## Two's Complement Representation

<div class="key-term" markdown="1">
**Two's complement** is the standard method for representing signed (positive and negative) integers in binary. The most significant bit (MSB) acts as the sign bit: 0 for positive, 1 for negative. The key advantage is that addition and subtraction work identically for both positive and negative numbers without special handling.
</div>

### Converting Positive Numbers

Positive numbers in two's complement are identical to standard unsigned binary, with a leading 0 as the sign bit.

Example: +25 in 8-bit two's complement = **00011001**

### Converting Negative Numbers

To convert a negative denary number to two's complement:

1. Write the positive version in binary
2. Flip all bits (one's complement)
3. Add 1

**Worked Example**: Convert -25 to 8-bit two's complement

1. +25 = 00011001
2. Flip:  11100110
3. Add 1: **11100111**

### Converting Two's Complement Back to Denary

For a negative two's complement number (MSB = 1):

1. Flip all bits
2. Add 1
3. The result is the magnitude; apply a negative sign

**Worked Example**: Convert 11010100 to denary

1. Flip:  00101011
2. Add 1: 00101100 = 44
3. Answer: **-44**

Alternatively, you can calculate directly: the MSB has a place value of -128, and all other bits have their normal positive place values.

11010100 = -128 + 64 + 16 + 4 = **-44**

### Range of Two's Complement

For an n-bit two's complement number:

- **Minimum value**: -2^(n-1)
- **Maximum value**: 2^(n-1) - 1
- **Total values**: 2^n

| Bits | Minimum | Maximum |
|---|---|---|
| 4 | -8 | +7 |
| 8 | -128 | +127 |
| 16 | -32,768 | +32,767 |

### Two's Complement Arithmetic

**Worked Example**: Calculate -35 + 20 using 8-bit two's complement

-35 in two's complement:
1. 35 = 00100011
2. Flip:  11011100
3. Add 1: **11011101**

20 in two's complement: **00010100**

```
    1 1 1
    1 1 0 1 1 1 0 1    (-35)
  + 0 0 0 1 0 1 0 0    (+20)
  -------------------
    1 1 1 1 0 0 0 1
```

Convert result 11110001 back: flip = 00001110, add 1 = 00001111 = 15, so answer = **-15**

Check: -35 + 20 = -15. Correct.

---

## Sign and Magnitude Representation

<div class="key-term" markdown="1">
**Sign and magnitude** is a simpler method for representing signed integers. The most significant bit represents the sign (0 = positive, 1 = negative) and the remaining bits represent the magnitude (absolute value) of the number.
</div>

### Examples

- +25 in 8-bit sign and magnitude: **0**0011001 (sign bit 0, magnitude 25)
- -25 in 8-bit sign and magnitude: **1**0011001 (sign bit 1, magnitude 25)

### Range of Sign and Magnitude

For an n-bit sign and magnitude number:

- **Minimum value**: -(2^(n-1) - 1)
- **Maximum value**: +(2^(n-1) - 1)
- **Total unique values**: 2^n - 1 (because zero has two representations: +0 and -0)

| Bits | Minimum | Maximum |
|---|---|---|
| 4 | -7 | +7 |
| 8 | -127 | +127 |

### Comparison: Two's Complement vs Sign and Magnitude

| Feature | Two's Complement | Sign and Magnitude |
|---|---|---|
| Range (8-bit) | -128 to +127 | -127 to +127 |
| Representations of zero | One (00000000) | Two (+0 = 00000000, -0 = 10000000) |
| Arithmetic | Standard addition/subtraction works directly | Requires special handling for different signs |
| Hardware complexity | Simpler (single adder circuit) | More complex (must check signs, handle magnitude separately) |
| Industry use | Standard in virtually all modern computers | Rarely used for integers; used in some floating point mantissa representations |

<div class="exam-tip" markdown="1">
Two's complement is preferred over sign and magnitude because: (1) there is only one representation of zero, (2) the same addition circuit works for both positive and negative numbers, and (3) it has a slightly wider range (one extra negative value). These are the three key points examiners look for.
</div>

---

## Floating Point Representation

<div class="key-term" markdown="1">
**Floating point representation** stores real numbers (numbers with fractional parts) using two components: the **mantissa** (which holds the significant digits of the number) and the **exponent** (which determines the position of the binary point). This is analogous to scientific notation in denary.
</div>

A floating point number is calculated as:

**Value = Mantissa x 2^Exponent**

For example, using a 12-bit floating point with 8-bit mantissa and 4-bit exponent (both in two's complement):

- The mantissa represents a fixed-point fractional value with the binary point immediately after the sign bit
- The exponent is an integer in two's complement that shifts the binary point

### Normalisation

<div class="key-term" markdown="1">
**Normalisation** is the process of adjusting the mantissa and exponent so that the mantissa uses all available bits to store significant digits, thereby maximising the precision of the representation.
</div>

A normalised floating point number follows these rules:

- **Positive numbers**: the mantissa starts with **0.1** (the sign bit is 0, and the next bit is 1)
- **Negative numbers**: the mantissa starts with **1.0** (the sign bit is 1, and the next bit is 0)

In other words, the first two bits of the mantissa must be **different**.

**Why normalise?** An unnormalised mantissa has leading zeros (positive) or leading ones (negative) after the sign bit that waste bits without adding precision. Normalisation eliminates these redundant bits, giving the maximum number of significant digits for the available bit length.

**Example of unnormalised vs normalised**:

Unnormalised: mantissa = 0.0010110, exponent = 0101
Normalised:   mantissa = 0.1011000, exponent = 0011

Both represent the same value, but the normalised form has more significant bits available.

### Worked Example 1: Convert Denary to Floating Point

Convert **13.5** to a 12-bit floating point number with 8-bit mantissa and 4-bit exponent (both two's complement).

Step 1: Convert 13.5 to fixed-point binary
- 13 = 1101
- 0.5 = .1
- 13.5 = 1101.1

Step 2: Write in binary with the point after the sign bit position
- 0.11011 x 2^4 (shift the point 4 places left to get 0.1 at the start)

Step 3: Encode
- Mantissa: 0.1101100 = **01101100** (padded with trailing zeros)
- Exponent: 4 = **0100**

Result: **01101100 0100**

### Worked Example 2: Convert Negative Denary to Floating Point

Convert **-5.75** to a 12-bit floating point number with 8-bit mantissa and 4-bit exponent.

Step 1: Convert +5.75 to binary
- 5 = 101
- 0.75 = .11
- 5.75 = 101.11

Step 2: In normalised positive form: 0.10111 x 2^3

Step 3: Negate the mantissa using two's complement to represent -5.75
- Positive mantissa: 01011100
- Flip: 10100011
- Add 1: **10100100**

Step 4: Encode exponent: 3 = **0011**

Result: **10100100 0011**

Verify: Mantissa starts with 1.0 (sign bit = 1, next bit = 0), so it is correctly normalised for a negative number.

### Worked Example 3: Convert Floating Point to Denary

Convert mantissa = **01011000**, exponent = **0011** to denary.

Step 1: Mantissa as fixed-point fraction = 0.1011000

Step 2: Exponent = 0011 = 3

Step 3: Shift the binary point 3 places to the right: 0101.1000

Step 4: Convert to denary: 4 + 1 + 0.5 = **5.5**

### Worked Example 4: Convert Negative Floating Point to Denary

Convert mantissa = **10110000**, exponent = **0100** to denary.

Step 1: The mantissa is negative (MSB = 1). Find the magnitude using two's complement.
- Flip: 01001111
- Add 1: 01010000
- So the magnitude mantissa = 0.1010000

Step 2: Exponent = 0100 = 4

Step 3: Shift point 4 places right: 01010.000 = 10.0 (magnitude)

Wait, let's be more careful. The magnitude mantissa 0.1010000 with exponent 4 means shift 4 right: 01010.000 = 10.

Step 4: Apply the negative sign: **-10**

<div class="exam-tip" markdown="1">
To check normalisation: the first two bits of the mantissa must differ. For positive numbers: 01..., for negative numbers: 10.... If you see 00... or 11... at the start of the mantissa, it is **not** normalised. When converting negative numbers, negate the mantissa using two's complement after normalising the positive version.
</div>

---

## Advantages and Disadvantages: Integer vs Floating Point

| Feature | Integer | Floating Point |
|---|---|---|
| Precision | Exact representation of whole numbers | May introduce rounding errors |
| Range | Limited to whole numbers within a fixed range | Can represent very large and very small numbers |
| Speed | Faster arithmetic operations | Slower due to mantissa/exponent handling |
| Storage | More efficient (every bit stores magnitude) | Less efficient (bits split between mantissa and exponent) |
| Use cases | Counting, indexing, loop counters, exact values | Scientific calculations, measurements, currency (with care), graphics |

**Key trade-off**: Floating point provides a much larger range at the cost of precision. Integer provides exact precision for whole numbers but cannot represent fractional values.

The precision of floating point depends on the number of bits allocated to the mantissa. More mantissa bits means more significant figures, but fewer exponent bits, reducing the range. This is a fundamental trade-off in floating point design.

---

## Truncation and Rounding

When a number cannot be represented exactly in the available bits, it must be approximated. There are two main methods.

### Truncation

<div class="key-term" markdown="1">
**Truncation** simply removes (discards) the excess bits beyond the available precision. The remaining bits are left unchanged. This always rounds towards zero.
</div>

Example: Storing 0.1011011 in 5 fractional bits
- Truncated: 0.10110 (the last two bits are simply dropped)
- Actual value: 0.7109375
- Truncated value: 0.6875
- Error: 0.0234375

Truncation is simpler to implement but introduces a **systematic bias** towards zero, because it always makes positive numbers smaller and negative numbers larger (closer to zero).

### Rounding

<div class="key-term" markdown="1">
**Rounding** adjusts the value to the nearest representable number. If the discarded portion is greater than or equal to half the value of the last retained bit, the last retained bit is rounded up.
</div>

Example: Storing 0.1011011 in 5 fractional bits
- Look at the first discarded bit: 1 (which is >= half)
- Rounded: 0.10111 (the last retained bit is increased)
- Actual value: 0.7109375
- Rounded value: 0.71875
- Error: 0.0078125

Rounding produces smaller errors on average and does not introduce a systematic bias, but is more complex to implement.

### Absolute and Relative Errors

<div class="key-term" markdown="1">
**Absolute error** is the magnitude of the difference between the true value and the approximated value: |true value - stored value|.

**Relative error** is the absolute error expressed as a proportion of the true value: absolute error / |true value|. It is often expressed as a percentage.
</div>

**Worked Example**: A value of 7.3 is stored as 7 due to truncation.

- Absolute error = |7.3 - 7| = **0.3**
- Relative error = 0.3 / 7.3 = **0.0411** or **4.11%**

**Worked Example**: A value of 150.8 is stored as 151 due to rounding.

- Absolute error = |150.8 - 151| = **0.2**
- Relative error = 0.2 / 150.8 = **0.00133** or **0.133%**

Relative error is more meaningful than absolute error when comparing the significance of errors across different magnitudes. An absolute error of 0.5 is much more significant for the value 2 (25% relative error) than for the value 1000 (0.05% relative error).

<div class="exam-tip" markdown="1">
Exam questions often ask you to compare truncation and rounding. Key points: truncation is simpler but introduces systematic bias; rounding is more accurate on average but more complex. Always calculate both absolute and relative error when asked, and show your formula and working.
</div>

---

## Shift Functions

Shift operations move all bits in a binary number left or right by a specified number of positions. They are fundamental to efficient multiplication and division.

### Logical Shift Left

<div class="key-term" markdown="1">
**Logical shift left** moves all bits to the left by the specified number of positions. Vacated positions on the right are filled with **0s**. Bits shifted out of the left end are lost. Each shift left **multiplies** the value by 2.
</div>

Example: Logical shift left by 2 on 00101100 (44)

```
Before:  0 0 1 0 1 1 0 0    (44)
After:   1 0 1 1 0 0 0 0    (176)
```

44 x 2^2 = 44 x 4 = 176. Correct.

### Logical Shift Right

<div class="key-term" markdown="1">
**Logical shift right** moves all bits to the right by the specified number of positions. Vacated positions on the left are filled with **0s**. Bits shifted out of the right end are lost. Each shift right **divides** the value by 2 (integer division, truncating any remainder).
</div>

Example: Logical shift right by 1 on 00101100 (44)

```
Before:  0 0 1 0 1 1 0 0    (44)
After:   0 0 0 1 0 1 1 0    (22)
```

44 / 2 = 22. Correct.

### Arithmetic Shift Left

<div class="key-term" markdown="1">
**Arithmetic shift left** works identically to logical shift left: bits move left, vacated positions on the right are filled with 0s. The sign bit may change, potentially causing overflow.
</div>

For signed numbers, arithmetic shift left is the same operation as logical shift left, but the programmer must watch for overflow if the sign bit changes.

### Arithmetic Shift Right

<div class="key-term" markdown="1">
**Arithmetic shift right** moves all bits to the right by the specified number of positions. Vacated positions on the left are filled with a copy of the **sign bit** (the MSB). This preserves the sign of the number, making it suitable for dividing signed (two's complement) numbers by powers of 2.
</div>

Example: Arithmetic shift right by 1 on 11010100 (-44 in two's complement)

```
Before:  1 1 0 1 0 1 0 0    (-44)
After:   1 1 1 0 1 0 1 0    (-22)
```

The sign bit (1) is preserved and copied into the vacated position. -44 / 2 = -22. Correct.

### Difference Between Logical and Arithmetic Shifts

| Feature | Logical Shift | Arithmetic Shift |
|---|---|---|
| Left shift fill | 0s on right | 0s on right (same as logical) |
| Right shift fill | **0s on left** | **Copy of sign bit on left** |
| Treats number as | Unsigned | Signed (two's complement) |
| Right shift of negative number | Produces incorrect result (becomes positive) | Preserves sign (correct division) |
| Use case | Unsigned binary manipulation, bit masking | Signed integer multiplication/division |

### Applying Shifts for Multiplication and Division

Shifting is much faster than using the ALU's multiply/divide circuits, so compilers often replace multiplication/division by powers of 2 with shift operations.

| Operation | Shift | Example |
|---|---|---|
| Multiply by 2 | Shift left by 1 | 5 << 1 = 10 |
| Multiply by 4 | Shift left by 2 | 5 << 2 = 20 |
| Multiply by 8 | Shift left by 3 | 5 << 3 = 40 |
| Multiply by 2^n | Shift left by n | General rule |
| Divide by 2 | Shift right by 1 | 20 >> 1 = 10 |
| Divide by 4 | Shift right by 2 | 20 >> 2 = 5 |
| Divide by 2^n | Shift right by n | General rule |

#### Code Examples

```python
# Python shift operations
value = 12

# Shift left (multiply)
result = value << 1   # 12 * 2 = 24
print(f"{value} << 1 = {result}")

result = value << 3   # 12 * 8 = 96
print(f"{value} << 3 = {result}")

# Shift right (divide)
result = value >> 1   # 12 / 2 = 6
print(f"{value} >> 1 = {result}")

result = value >> 2   # 12 / 4 = 3
print(f"{value} >> 2 = {result}")

# Combining shifts for multiplication by non-powers of 2
# Multiply by 10 = multiply by 8 + multiply by 2
x = 7
result = (x << 3) + (x << 1)  # (7*8) + (7*2) = 56 + 14 = 70
print(f"{x} * 10 = {result}")
```

```vb
' VB.NET shift operations
Dim value As Integer = 12

' Shift left (multiply)
Dim result As Integer = value << 1   ' 12 * 2 = 24
Console.WriteLine($"{value} << 1 = {result}")

result = value << 3   ' 12 * 8 = 96
Console.WriteLine($"{value} << 3 = {result}")

' Shift right (divide)
result = value >> 1   ' 12 / 2 = 6
Console.WriteLine($"{value} >> 1 = {result}")

result = value >> 2   ' 12 / 4 = 3
Console.WriteLine($"{value} >> 2 = {result}")

' Combining shifts for multiplication by non-powers of 2
' Multiply by 10 = multiply by 8 + multiply by 2
Dim x As Integer = 7
result = (x << 3) + (x << 1)  ' (7*8) + (7*2) = 56 + 14 = 70
Console.WriteLine($"{x} * 10 = {result}")
```

<div class="exam-tip" markdown="1">
When answering shift questions, always state whether the shift is logical or arithmetic and what fills the vacated bits. For multiplication, shift LEFT; for division, shift RIGHT. Remember that shifting right by n is integer division: any fractional part is lost. For example, 7 >> 1 = 3 (not 3.5). To multiply by a number that is not a power of 2, combine shifts and additions (e.g. multiply by 6 = shift left 2 then add shift left 1, since 6 = 4 + 2).
</div>

---

## Overflow and Underflow

### Overflow

<div class="key-term" markdown="1">
**Overflow** occurs when the result of an arithmetic operation is too large (positive) or too small (negative) to be represented in the available number of bits.
</div>

**Causes of overflow**:

- Adding two large positive numbers whose sum exceeds the maximum representable value
- Adding two large negative numbers whose sum is below the minimum representable value
- Shifting bits left so that significant bits are lost from the MSB
- In floating point: when the exponent exceeds its maximum positive value

**Example (8-bit two's complement, range -128 to +127)**:

```
    0 1 1 1 1 1 1 1    (+127)
  + 0 0 0 0 0 0 0 1    (+1)
  -------------------
    1 0 0 0 0 0 0 0    (-128 in two's complement!)
```

Adding 127 + 1 should give 128, but this cannot be stored in 8-bit two's complement (max +127). The result wraps around to -128, which is incorrect.

**Detecting overflow in two's complement**: Overflow has occurred if:
- Two positive numbers are added and the result is negative, OR
- Two negative numbers are added and the result is positive

Overflow **cannot** occur when adding a positive and a negative number.

### Underflow

<div class="key-term" markdown="1">
**Underflow** occurs in floating point arithmetic when a number is too close to zero to be represented. The exponent becomes more negative than the minimum allowed value, and the number collapses to zero. This is different from overflow, which involves numbers that are too large.
</div>

**Causes of underflow**:

- Dividing a very small floating point number by a very large number
- Multiplying two very small floating point numbers
- Subtracting two nearly equal floating point numbers
- When the exponent goes below its minimum negative value

**Example**: With a 4-bit two's complement exponent (range -8 to +7), if a calculation requires an exponent of -9, underflow occurs because -9 is outside the representable range. The number is too small to store and is typically rounded to zero.

### Consequences of Overflow and Underflow

| Issue | Consequence |
|---|---|
| **Overflow** | Result wraps around to an incorrect value (e.g. large positive becomes negative); silent errors in programs that do not check; potential security vulnerabilities (e.g. buffer overflow exploits) |
| **Underflow** | Small values collapse to zero; loss of precision in calculations; division by zero errors if the underflowed value is subsequently used as a divisor |

#### Detecting and Handling in Code

```python
# Python handles arbitrary precision integers natively,
# so integer overflow does not occur in Python.
# However, we can demonstrate the concept:

import sys

# Python integers have no fixed size, but we can simulate 8-bit
max_8bit = 127
result = max_8bit + 1
print(f"In Python: 127 + 1 = {result}")  # 128 (no overflow)

# For floating point, Python can detect overflow:
try:
    huge = 1.7976931348623157e+308 * 2
    print(f"Result: {huge}")  # Will print 'inf'
except OverflowError:
    print("Floating point overflow detected")

# Underflow example
tiny = 5e-324  # Smallest positive float
result = tiny / 2
print(f"Underflow: {tiny} / 2 = {result}")  # Prints 0.0
```

```vb
' VB.NET overflow detection
Module OverflowDemo
    Sub Main()
        ' Integer overflow detection
        Try
            Dim max As Integer = Integer.MaxValue  ' 2,147,483,647
            Dim result As Integer = checked(max + 1)
            ' The checked keyword forces overflow checking
        Catch ex As OverflowException
            Console.WriteLine("Integer overflow detected!")
        End Try

        ' Floating point overflow
        Dim huge As Double = Double.MaxValue * 2
        If Double.IsInfinity(huge) Then
            Console.WriteLine("Floating point overflow: result is infinity")
        End If

        ' Floating point underflow
        Dim tiny As Double = Double.Epsilon / 2
        Console.WriteLine($"Underflow result: {tiny}")  ' Prints 0
    End Sub
End Module
```

<div class="exam-tip" markdown="1">
Overflow and underflow are distinct concepts. **Overflow** = result too large to represent (applies to both integers and floating point). **Underflow** = result too close to zero to represent (applies only to floating point). For integer overflow detection in two's complement, check whether the signs of the inputs and the sign of the result are inconsistent. In exam answers, always give a specific numerical example to demonstrate the error.
</div>
