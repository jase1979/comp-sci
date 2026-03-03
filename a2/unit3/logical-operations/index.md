---
layout: topic
title: "Logical Operations"
level: "A2 Level"
level_url: "/a2/"
unit_name: "Unit 3: Programming & System Development"
unit_url: "/a2/unit3/"
subtopics:
  - "Truth tables including NAND and NOR operations"
  - "Apply logical operations: Clearing registers, masking, encryption"
  - "Simplify Boolean expressions using identities, rules, De Morgan's laws"
---

## Truth Tables for Logic Gates

<div class="key-term" markdown="1">
**Logic gate** -- a digital circuit that performs a Boolean function on one or more binary inputs to produce a single binary output. The behaviour of every gate is completely defined by its truth table.
</div>

Logic gates are the fundamental building blocks of all digital circuits. At A2 level you must be able to construct and interpret truth tables for all six standard gates: AND, OR, NOT, XOR, NAND and NOR.

### AND Gate

The AND gate outputs 1 **only** when **all** inputs are 1.

| A | B | A AND B |
|---|---|---------|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

Boolean expression: **Q = A . B** (also written A AND B or A ^ B).

### OR Gate

The OR gate outputs 1 when **at least one** input is 1.

| A | B | A OR B |
|---|---|--------|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

Boolean expression: **Q = A + B** (also written A OR B or A v B).

### NOT Gate (Inverter)

The NOT gate has a single input and **inverts** it.

| A | NOT A |
|---|-------|
| 0 | 1 |
| 1 | 0 |

Boolean expression: **Q = A&#x0304;** (also written NOT A or ~A).

### XOR Gate (Exclusive OR)

The XOR gate outputs 1 when the inputs are **different**.

| A | B | A XOR B |
|---|---|---------|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

Boolean expression: **Q = A &#x2295; B**.

XOR can be expressed in terms of AND, OR and NOT as: A XOR B = (A AND NOT B) OR (NOT A AND B).

### NAND Gate (NOT AND)

The NAND gate is the **inverse of AND**. It outputs 0 only when all inputs are 1.

| A | B | A NAND B |
|---|---|----------|
| 0 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

Boolean expression: **Q = <span style="text-decoration:overline">A . B</span>**.

### NOR Gate (NOT OR)

The NOR gate is the **inverse of OR**. It outputs 1 only when all inputs are 0.

| A | B | A NOR B |
|---|---|---------|
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 0 |

Boolean expression: **Q = <span style="text-decoration:overline">A + B</span>**.

<div class="exam-tip" markdown="1">
When constructing truth tables for n inputs, there are 2^n rows. For two inputs there are 4 rows; for three inputs there are 8. Always list the input combinations systematically in binary counting order (00, 01, 10, 11) so you do not miss any.
</div>

### Three-Input Truth Table Example

For a three-input AND gate:

| A | B | C | A AND B AND C |
|---|---|---|---------------|
| 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 0 |
| 0 | 1 | 0 | 0 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 0 | 0 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 0 |
| 1 | 1 | 1 | 1 |

---

## NAND and NOR as Universal Gates

<div class="key-term" markdown="1">
**Universal gate** -- a gate that can be used on its own to implement any Boolean function. Both NAND and NOR are universal gates. AND, OR and NOT alone are not universal because none of them individually can produce all the others.
</div>

This is a critically important concept: **any** digital circuit can be built using only NAND gates, or only NOR gates. This is why NAND and NOR are called universal gates. In practice NAND is favoured because NAND gates are cheaper and faster to manufacture in silicon.

### Building NOT, AND and OR from NAND Gates Only

**NOT from NAND:** Connect both inputs of a NAND gate together.

- If A = 0: NAND(0,0) = 1
- If A = 1: NAND(1,1) = 0

So NAND(A, A) = NOT A.

**AND from NAND:** Use two NAND gates. First compute NAND(A, B), then invert the result with a second NAND used as NOT.

- A AND B = NAND( NAND(A,B), NAND(A,B) )

**OR from NAND:** Use three NAND gates. First invert each input, then NAND the results.

- A OR B = NAND( NAND(A,A), NAND(B,B) )

### Building NOT, AND and OR from NOR Gates Only

**NOT from NOR:** Connect both inputs of a NOR gate together.

- NOR(A, A) = NOT A

**OR from NOR:** Use two NOR gates. First compute NOR(A, B), then invert.

- A OR B = NOR( NOR(A,B), NOR(A,B) )

**AND from NOR:** Use three NOR gates. First invert each input, then NOR the results.

- A AND B = NOR( NOR(A,A), NOR(B,B) )

### Verification by Truth Table

We can verify that NAND(NAND(A,A), NAND(B,B)) produces the same output as A OR B:

| A | B | NAND(A,A) = NOT A | NAND(B,B) = NOT B | NAND(NOT A, NOT B) | A OR B |
|---|---|--------------------|--------------------|---------------------|--------|
| 0 | 0 | 1 | 1 | 0 | 0 |
| 0 | 1 | 1 | 0 | 1 | 1 |
| 1 | 0 | 0 | 1 | 1 | 1 |
| 1 | 1 | 0 | 0 | 1 | 1 |

The outputs match, confirming the construction is correct.

<div class="exam-tip" markdown="1">
The exam may ask you to draw a circuit using only NAND (or only NOR) gates. Memorise the three constructions for NOT, AND and OR from NAND gates, and the three from NOR gates. From these you can build any circuit.
</div>

---

## Logical Operations on Binary Data

Logical operations are not just theoretical; they are used constantly in real programs and hardware for practical bit-level manipulation. You must understand three key applications: **clearing registers**, **masking** and **encryption**.

### Clearing a Register (AND with 0)

<div class="key-term" markdown="1">
**Clearing** -- setting specific bits in a binary word to 0 while leaving other bits unchanged. This is achieved by ANDing the word with a pattern that has 0s in the positions to clear and 1s elsewhere.
</div>

AND has the property that anything ANDed with 0 gives 0, and anything ANDed with 1 stays the same:

- X AND 0 = 0 (clears the bit)
- X AND 1 = X (preserves the bit)

**Example:** Clear the upper 4 bits of the byte 11010110.

```
  Data:     1 1 0 1 0 1 1 0
  Mask:     0 0 0 0 1 1 1 1
  ----------------------------
  Result:   0 0 0 0 0 1 1 0
```

The upper 4 bits have been forced to 0, while the lower 4 bits are preserved.

```python
data = 0b11010110      # 214 in decimal
mask = 0b00001111      # Mask to keep lower 4 bits
result = data & mask   # Bitwise AND
print(bin(result))     # Output: 0b110 (i.e. 00000110)
```

```vb
Dim data As Integer = &B11010110   ' 214 in decimal
Dim mask As Integer = &B00001111   ' Mask to keep lower 4 bits
Dim result As Integer = data And mask
Console.WriteLine(Convert.ToString(result, 2).PadLeft(8, "0"c))  ' Output: 00000110
```

### Masking (Selecting Specific Bits)

<div class="key-term" markdown="1">
**Masking** -- using a bitwise operation to extract or isolate certain bits from a binary word. AND masking selects bits (keeps them visible), while OR masking can force bits to 1.
</div>

Masking with AND lets you **read** specific bits. Masking with OR lets you **set** specific bits to 1.

**AND masking to extract bits:** To test whether bit 3 of a byte is set:

```
  Data:     1 0 1 1 0 1 0 0
  Mask:     0 0 0 0 1 0 0 0   (only bit 3 is 1)
  ----------------------------
  Result:   0 0 0 0 0 0 0 0   (bit 3 was 0)
```

**OR masking to set bits:** To force bit 7 to 1:

```
  Data:     0 0 1 1 0 1 0 0
  Mask:     1 0 0 0 0 0 0 0   (only bit 7 is 1)
  ----------------------------
  Result:   1 0 1 1 0 1 0 0   (bit 7 is now 1)
```

- X OR 0 = X (preserves the bit)
- X OR 1 = 1 (sets the bit)

```python
# AND mask: extract bits 4-7 (upper nibble)
data = 0b10110100
mask = 0b11110000
upper_nibble = (data & mask) >> 4
print(upper_nibble)  # Output: 11 (0b1011)

# OR mask: set bit 0 to 1
data = 0b10110100
mask = 0b00000001
result = data | mask
print(bin(result))   # Output: 0b10110101
```

```vb
' AND mask: extract bits 4-7 (upper nibble)
Dim data As Integer = &B10110100
Dim mask As Integer = &B11110000
Dim upperNibble As Integer = (data And mask) >> 4
Console.WriteLine(upperNibble)  ' Output: 11

' OR mask: set bit 0 to 1
data = &B10110100
mask = &B00000001
Dim result As Integer = data Or mask
Console.WriteLine(Convert.ToString(result, 2))  ' Output: 10110101
```

### Encryption Using XOR Cipher

<div class="key-term" markdown="1">
**XOR cipher** -- a simple symmetric encryption technique where each bit (or byte) of plaintext is XORed with the corresponding bit (or byte) of a key. Applying the same XOR operation a second time with the same key recovers the original plaintext.
</div>

XOR has the crucial property that it is **self-inverse**:

- (A XOR K) XOR K = A

This means the same operation encrypts and decrypts.

**Worked example with single bytes:**

```
  Plaintext:   0 1 0 0 1 0 1 0   (ASCII 'J' = 74)
  Key:         1 1 0 0 1 1 0 0   (key = 204)
  XOR:         1 0 0 0 0 1 1 0   (ciphertext = 134)

  Ciphertext:  1 0 0 0 0 1 1 0   (134)
  Key:         1 1 0 0 1 1 0 0   (204)
  XOR:         0 1 0 0 1 0 1 0   (plaintext restored = 74 = 'J')
```

```python
def xor_cipher(text, key):
    """Encrypt or decrypt using XOR cipher with a repeating key."""
    result = ""
    for i in range(len(text)):
        # XOR each character with the corresponding key character
        char_code = ord(text[i]) ^ ord(key[i % len(key)])
        result += chr(char_code)
    return result

plaintext = "Hello"
key = "KEY"

# Encrypt
ciphertext = xor_cipher(plaintext, key)
print("Encrypted bytes:", [ord(c) for c in ciphertext])

# Decrypt (same operation with same key)
decrypted = xor_cipher(ciphertext, key)
print("Decrypted:", decrypted)  # Output: Hello
```

```vb
Function XorCipher(text As String, key As String) As String
    Dim result As String = ""
    For i As Integer = 0 To text.Length - 1
        ' XOR each character with the corresponding key character
        Dim charCode As Integer = Asc(text(i)) Xor Asc(key(i Mod key.Length))
        result &= Chr(charCode)
    Next
    Return result
End Function

Sub Main()
    Dim plaintext As String = "Hello"
    Dim key As String = "KEY"

    ' Encrypt
    Dim ciphertext As String = XorCipher(plaintext, key)
    Console.WriteLine("Encrypted bytes: " & String.Join(", ",
        ciphertext.Select(Function(c) Asc(c).ToString()).ToArray()))

    ' Decrypt (same operation with same key)
    Dim decrypted As String = XorCipher(ciphertext, key)
    Console.WriteLine("Decrypted: " & decrypted)  ' Output: Hello
End Sub
```

<div class="exam-tip" markdown="1">
A common exam question asks why XOR is used for encryption rather than AND or OR. The answer is that XOR is **reversible** -- no information is lost. AND with 0 destroys information (you cannot recover the original bit), and OR with 1 similarly destroys information. Only XOR preserves all information and allows perfect decryption.
</div>

### Summary of Bitwise Operation Applications

| Operation | Mask Pattern | Effect | Use Case |
|-----------|-------------|--------|----------|
| AND | 0 bits in target positions | Clears bits to 0 | Clearing registers, extracting bits |
| AND | 1 bits in target positions | Preserves bits | Reading specific bit fields |
| OR | 1 bits in target positions | Sets bits to 1 | Setting flags, turning on bits |
| OR | 0 bits in target positions | Preserves bits | Leaving other bits unchanged |
| XOR | Key pattern | Toggles bits | Encryption, toggling flags |
| NOT | (no mask needed) | Inverts all bits | One's complement, flipping bits |

---

## Boolean Algebra Identities and Laws

<div class="key-term" markdown="1">
**Boolean algebra** -- a branch of algebra in which variables can only take the values 0 (false) or 1 (true), and the operations are AND (.), OR (+) and NOT (overbar). It provides a formal mathematical framework for simplifying logic circuits and expressions.
</div>

You must memorise all of the following identities and laws. They are the tools you use to simplify Boolean expressions.

### Identity Law

A variable combined with the identity element is unchanged.

- A + 0 = A (0 is the identity for OR)
- A . 1 = A (1 is the identity for AND)

### Null (Annulment) Law

A variable combined with its annihilator produces the annihilator.

- A + 1 = 1
- A . 0 = 0

### Idempotent Law

A variable combined with itself is unchanged.

- A + A = A
- A . A = A

### Inverse (Complement) Law

A variable combined with its complement produces a constant.

- A + A&#x0304; = 1
- A . A&#x0304; = 0

### Double Complement (Involution) Law

Complementing a variable twice returns the original.

- <span style="text-decoration: overline"><span style="text-decoration: overline">A</span></span> = A

### Absorption Law

- A + (A . B) = A
- A . (A + B) = A

To see why: if A = 1, both expressions give 1 regardless of B. If A = 0, both expressions give 0 regardless of B. So the result depends only on A.

### Distributive Law

- A . (B + C) = (A . B) + (A . C) -- AND distributes over OR
- A + (B . C) = (A + B) . (A + C) -- OR distributes over AND

Note that the second form has no equivalent in ordinary algebra.

### Associative Law

- (A + B) + C = A + (B + C) = A + B + C
- (A . B) . C = A . (B . C) = A . B . C

### Commutative Law

- A + B = B + A
- A . B = B . A

### De Morgan's Laws

<div class="key-term" markdown="1">
**De Morgan's Laws** -- two transformation rules that relate AND and OR operations through complementation:

- **First law:** <span style="text-decoration:overline">A . B</span> = A&#x0304; + B&#x0304; (the complement of AND equals OR of complements)
- **Second law:** <span style="text-decoration:overline">A + B</span> = A&#x0304; . B&#x0304; (the complement of OR equals AND of complements)

In words: "break the bar, change the sign."
</div>

### Summary Table of All Identities

| Law | OR Form (+ ) | AND Form (.) |
|-----|-------------|-------------|
| Identity | A + 0 = A | A . 1 = A |
| Null | A + 1 = 1 | A . 0 = 0 |
| Idempotent | A + A = A | A . A = A |
| Inverse | A + A&#x0304; = 1 | A . A&#x0304; = 0 |
| Absorption | A + (A . B) = A | A . (A + B) = A |
| Distributive | A + (B . C) = (A + B) . (A + C) | A . (B + C) = A . B + A . C |
| Associative | (A + B) + C = A + (B + C) | (A . B) . C = A . (B . C) |
| Commutative | A + B = B + A | A . B = B . A |
| De Morgan's | <span style="text-decoration:overline">A + B</span> = A&#x0304; . B&#x0304; | <span style="text-decoration:overline">A . B</span> = A&#x0304; + B&#x0304; |

<div class="exam-tip" markdown="1">
A helpful mnemonic for De Morgan's laws is: **"break the bar, change the sign."** When you "break" the bar over an expression, every AND becomes OR and every OR becomes AND, and each variable gets complemented.
</div>

---

## De Morgan's Laws: Proofs via Truth Tables

It is important to be able to **prove** De Morgan's laws. The most accessible method is proof by exhaustion using truth tables.

### Proof of First Law: <span style="text-decoration:overline">A . B</span> = A&#x0304; + B&#x0304;

| A | B | A . B | <span style="text-decoration:overline">A . B</span> | A&#x0304; | B&#x0304; | A&#x0304; + B&#x0304; |
|---|---|-------|------|-----|-----|-----------|
| 0 | 0 | 0 | **1** | 1 | 1 | **1** |
| 0 | 1 | 0 | **1** | 1 | 0 | **1** |
| 1 | 0 | 0 | **1** | 0 | 1 | **1** |
| 1 | 1 | 1 | **0** | 0 | 0 | **0** |

Columns 4 and 7 are identical for all input combinations. Therefore <span style="text-decoration:overline">A . B</span> = A&#x0304; + B&#x0304;. **QED.**

### Proof of Second Law: <span style="text-decoration:overline">A + B</span> = A&#x0304; . B&#x0304;

| A | B | A + B | <span style="text-decoration:overline">A + B</span> | A&#x0304; | B&#x0304; | A&#x0304; . B&#x0304; |
|---|---|-------|------|-----|-----|-----------|
| 0 | 0 | 0 | **1** | 1 | 1 | **1** |
| 0 | 1 | 1 | **0** | 1 | 0 | **0** |
| 1 | 0 | 1 | **0** | 0 | 1 | **0** |
| 1 | 1 | 1 | **0** | 0 | 0 | **0** |

Columns 4 and 7 are identical for all input combinations. Therefore <span style="text-decoration:overline">A + B</span> = A&#x0304; . B&#x0304;. **QED.**

<div class="exam-tip" markdown="1">
In the WJEC exam, when asked to "prove" a Boolean identity, a truth table proof is always acceptable. Build the table carefully, evaluate both sides of the equation independently, and state explicitly that the columns match for all input combinations.
</div>

---

## Simplifying Boolean Expressions

Simplifying Boolean expressions is a core exam skill. You must show each step and state which law or identity you have applied.

### Worked Example 1

**Simplify:** A . B + A . B&#x0304;

| Step | Expression | Law Applied |
|------|-----------|-------------|
| 1 | A . B + A . B&#x0304; | Original expression |
| 2 | A . (B + B&#x0304;) | Distributive law (factor out A) |
| 3 | A . 1 | Inverse law (B + B&#x0304; = 1) |
| 4 | **A** | Identity law (A . 1 = A) |

### Worked Example 2

**Simplify:** A + A . B

| Step | Expression | Law Applied |
|------|-----------|-------------|
| 1 | A + A . B | Original expression |
| 2 | **A** | Absorption law (A + A . B = A) |

Alternatively, step by step without using absorption directly:

| Step | Expression | Law Applied |
|------|-----------|-------------|
| 1 | A + A . B | Original expression |
| 2 | A . 1 + A . B | Identity law (A = A . 1) |
| 3 | A . (1 + B) | Distributive law (factor out A) |
| 4 | A . 1 | Null law (1 + B = 1) |
| 5 | **A** | Identity law (A . 1 = A) |

### Worked Example 3

**Simplify:** (A + B) . (A + B&#x0304;)

| Step | Expression | Law Applied |
|------|-----------|-------------|
| 1 | (A + B) . (A + B&#x0304;) | Original expression |
| 2 | A + (B . B&#x0304;) | Distributive law (OR over AND form) |
| 3 | A + 0 | Inverse law (B . B&#x0304; = 0) |
| 4 | **A** | Identity law (A + 0 = A) |

### Worked Example 4

**Simplify:** A&#x0304; . B&#x0304; + A&#x0304; . B + A . B&#x0304;

| Step | Expression | Law Applied |
|------|-----------|-------------|
| 1 | A&#x0304; . B&#x0304; + A&#x0304; . B + A . B&#x0304; | Original expression |
| 2 | A&#x0304; . (B&#x0304; + B) + A . B&#x0304; | Distributive law (factor out A&#x0304; from first two terms) |
| 3 | A&#x0304; . 1 + A . B&#x0304; | Inverse law (B&#x0304; + B = 1) |
| 4 | A&#x0304; + A . B&#x0304; | Identity law (A&#x0304; . 1 = A&#x0304;) |
| 5 | **A&#x0304; + B&#x0304;** | Absorption-like: since A&#x0304; + A . B&#x0304; = A&#x0304; + B&#x0304; (by factoring, or note this equals <span style="text-decoration:overline">A . B</span> by De Morgan's) |

To verify step 5 rigorously: A&#x0304; + A . B&#x0304; = (A&#x0304; + A) . (A&#x0304; + B&#x0304;) = 1 . (A&#x0304; + B&#x0304;) = A&#x0304; + B&#x0304;.

### Worked Example 5: Using De Morgan's Laws

**Simplify:** <span style="text-decoration:overline">(A&#x0304; + B) . (A + B&#x0304;)</span>

| Step | Expression | Law Applied |
|------|-----------|-------------|
| 1 | <span style="text-decoration:overline">(A&#x0304; + B) . (A + B&#x0304;)</span> | Original expression |
| 2 | <span style="text-decoration:overline">(A&#x0304; + B)</span> + <span style="text-decoration:overline">(A + B&#x0304;)</span> | De Morgan's first law (break bar over AND, change to OR) |
| 3 | (A . B&#x0304;) + (A&#x0304; . B) | De Morgan's second law on each term (break bar over OR, change to AND) |
| 4 | **A . B&#x0304; + A&#x0304; . B** | This is actually A XOR B |

### Worked Example 6: A Larger Expression

**Simplify:** A . B . C + A . B . C&#x0304; + A . B&#x0304; . C

| Step | Expression | Law Applied |
|------|-----------|-------------|
| 1 | A . B . C + A . B . C&#x0304; + A . B&#x0304; . C | Original expression |
| 2 | A . B . (C + C&#x0304;) + A . B&#x0304; . C | Distributive (factor A . B from first two terms) |
| 3 | A . B . 1 + A . B&#x0304; . C | Inverse law (C + C&#x0304; = 1) |
| 4 | A . B + A . B&#x0304; . C | Identity law (A . B . 1 = A . B) |
| 5 | A . (B + B&#x0304; . C) | Distributive (factor out A) |
| 6 | A . ((B + B&#x0304;) . (B + C)) | Distributive (OR over AND on inner expression) |
| 7 | A . (1 . (B + C)) | Inverse law |
| 8 | **A . (B + C)** | Identity law |

<div class="exam-tip" markdown="1">
In the exam, always show every step of your simplification and name the law you used. Marks are awarded for the **process**, not just the final answer. Look for common patterns: complementary pairs (X + X&#x0304; = 1, X . X&#x0304; = 0), opportunities to factor out common terms, and absorption. If you are stuck, try expanding using the distributive law to see if complementary pairs appear.
</div>

### Implementing Boolean Expressions in Code

You can verify your simplifications programmatically by comparing truth tables:

```python
def verify_simplification():
    """Verify that A.B.C + A.B.C' + A.B'.C = A.(B+C)"""
    print(f"{'A':>3} {'B':>3} {'C':>3} | {'Original':>10} {'Simplified':>12}")
    print("-" * 40)
    for a in (0, 1):
        for b in (0, 1):
            for c in (0, 1):
                # Original expression: A.B.C + A.B.C' + A.B'.C
                original = (a & b & c) | (a & b & (1-c)) | (a & (1-b) & c)
                # Simplified expression: A.(B + C)
                simplified = a & (b | c)
                match = "OK" if original == simplified else "MISMATCH"
                print(f"{a:>3} {b:>3} {c:>3} | {original:>10} {simplified:>12}  {match}")

verify_simplification()
```

```vb
Sub VerifySimplification()
    Console.WriteLine($"{'A',3} {'B',3} {'C',3} | {'Original',10} {'Simplified',12}")
    Console.WriteLine(New String("-"c, 40))
    For a As Integer = 0 To 1
        For b As Integer = 0 To 1
            For c As Integer = 0 To 1
                ' Original: A.B.C + A.B.C' + A.B'.C
                Dim original As Integer = (a And b And c) Or
                    (a And b And (1 - c)) Or (a And (1 - b) And c)
                ' Simplified: A.(B + C)
                Dim simplified As Integer = a And (b Or c)
                Dim match As String = If(original = simplified, "OK", "MISMATCH")
                Console.WriteLine($"{a,3} {b,3} {c,3} | {original,10} {simplified,12}  {match}")
            Next
        Next
    Next
End Sub
```
