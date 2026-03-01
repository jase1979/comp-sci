---
layout: topic
title: "Organisation & Structure of Data"
level: "GCSE"
level_url: "/gcse/"
unit_name: "Unit 1: Understanding Computer Science"
unit_url: "/gcse/unit1/"
prev_topic: "/gcse/unit1/communication/"
next_topic: "/gcse/unit1/system-software/"
---

## Number systems: Denary, binary (up to 16 bits), hexadecimal

Computers store and process all data as **binary** (base-2), but humans commonly use **denary** (base-10) and **hexadecimal** (base-16).

### Denary (Base-10)

- The number system we use every day
- Uses digits **0–9**
- Each column is a power of 10 (units, tens, hundreds, thousands...)

### Binary (Base-2)

- Used by computers because electronic circuits have two states: **on (1)** and **off (0)**
- Uses digits **0 and 1** only
- Each column is a power of 2

For an 8-bit binary number, the column values are:

| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
|-----|----|----|----|----|---|---|---|

**Example:** Convert binary `11001010` to denary:

128 + 64 + 0 + 0 + 8 + 0 + 2 + 0 = **202**

**Example:** Convert denary `45` to binary:

32 + 8 + 4 + 1 = 45, so the binary is `00101101`

### Hexadecimal (Base-16)

- Uses digits **0–9** and letters **A–F** (where A=10, B=11, C=12, D=13, E=14, F=15)
- Each column is a power of 16
- Provides a more compact way to represent large binary numbers

| Denary | Binary (4-bit) | Hex |
|--------|----------------|-----|
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

<div class="key-term" markdown="1">
**Binary** — base-2 number system using 0 and 1, the native language of computers. **Denary** — base-10 number system used by humans. **Hexadecimal** — base-16 number system using 0–9 and A–F, used as a compact representation of binary.
</div>

---

## Hexadecimal as shorthand for binary

Hexadecimal is used as a **shorthand** for binary because it is much easier for humans to read and less error-prone.

### Why hexadecimal?

- One hex digit represents **exactly 4 binary bits** (a nybble)
- An 8-bit byte can be written as just **2 hex digits** instead of 8 binary digits
- This makes large binary values much **easier to read, write, and debug**

### Converting binary to hexadecimal

1. Split the binary number into groups of **4 bits** (starting from the right)
2. Convert each group to its hex equivalent

**Example:** `11010110` → split into `1101` and `0110` → D and 6 → **D6**

### Converting hexadecimal to binary

1. Convert each hex digit to its **4-bit binary** equivalent
2. Join the groups together

**Example:** `A3` → A = `1010`, 3 = `0011` → **10100011**

### Common uses of hexadecimal

- **Colour codes** in web design (e.g. `#FF5733` — two hex digits each for red, green, blue)
- **MAC addresses** for network devices (e.g. `4A:1B:8C:3D:2E:7F`)
- **Memory addresses** — shorter and clearer than binary
- **Error codes** — easier for programmers to read than raw binary

<div class="exam-tip" markdown="1">
When converting between binary and hex, always work with groups of **4 bits**. If the binary number does not divide evenly into groups of 4, add leading zeros to the left (e.g. `10110` becomes `0001 0110` → **16**).
</div>

---

## Arithmetic shift functions and their effect

An **arithmetic shift** moves all the bits in a binary number to the left or right by a specified number of positions. It is a quick way to multiply or divide by powers of 2.

### Left shift

- Each position shifted left **multiplies** the number by 2
- New bits on the right are filled with **0**
- Bits shifted off the left are lost

**Example:** Shift `00001100` (12 in denary) left by 2 places:

`00110000` = 48 (12 x 2 x 2 = 12 x 4 = 48)

### Right shift

- Each position shifted right **divides** the number by 2 (integer division)
- For unsigned numbers, new bits on the left are filled with **0**
- Bits shifted off the right are lost (any remainder is discarded)

**Example:** Shift `00110000` (48 in denary) right by 3 places:

`00000110` = 6 (48 / 2 / 2 / 2 = 48 / 8 = 6)

| Shift | Effect | Formula |
|-------|--------|---------|
| Left by 1 | Multiply by 2 | x * 2 |
| Left by 2 | Multiply by 4 | x * 4 |
| Left by 3 | Multiply by 8 | x * 8 |
| Right by 1 | Divide by 2 | x / 2 |
| Right by 2 | Divide by 4 | x / 4 |
| Right by 3 | Divide by 8 | x / 8 |

<div class="exam-tip" markdown="1">
A left shift by *n* positions multiplies by **2ⁿ**. A right shift by *n* positions divides by **2ⁿ**. Be careful — bits shifted out are lost, which can cause incorrect results (overflow on the left, loss of precision on the right).
</div>

---

## Signed binary: Sign and magnitude and two's complement

So far, the binary numbers covered have been **unsigned** — they can only represent positive values. To represent **negative** numbers, we use one of two systems.

### Sign and magnitude

- The **most significant bit (MSB)** is used as a **sign bit**: **0 = positive**, **1 = negative**
- The remaining bits represent the **magnitude** (absolute value) of the number
- In an 8-bit number, 7 bits hold the value and 1 bit holds the sign

**Example (8-bit):**

| Binary | Sign bit | Magnitude bits | Denary value |
|--------|----------|---------------|--------------|
| `00001101` | 0 (positive) | 0001101 = 13 | +13 |
| `10001101` | 1 (negative) | 0001101 = 13 | -13 |

**Problem with sign and magnitude:** There are **two representations of zero** (`00000000` = +0 and `10000000` = -0), and binary arithmetic does not work correctly without special handling.

### Two's complement

Two's complement is the system actually used by computers to represent signed integers. It avoids the problems of sign and magnitude.

**Key idea:** The MSB has a **negative place value**. In an 8-bit two's complement number, the column values are:

| -128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
|------|----|----|----|----|---|---|---|

#### Converting denary to two's complement

**Method (for negative numbers):**

1. Write the positive version of the number in binary
2. **Flip** (invert) all the bits (0 becomes 1, 1 becomes 0)
3. **Add 1** to the result

**Example:** Convert **-35** to 8-bit two's complement:

1. +35 in binary: `00100011`
2. Flip all bits: `11011100`
3. Add 1: `11011101`

So **-35** in two's complement is `11011101`.

#### Converting two's complement to denary

**Method:** Use the column values, remembering the MSB column is **negative**.

**Example:** Convert `11011101` to denary:

-128 + 64 + 0 + 16 + 8 + 4 + 0 + 1 = **-35**

#### Another worked example

**Convert -100 to 8-bit two's complement:**

1. +100 in binary: `01100100`
2. Flip all bits: `10011011`
3. Add 1: `10011100`

**Check:** -128 + 0 + 0 + 16 + 8 + 4 + 0 + 0 = **-100** ✓

### Range of values

For an **n-bit** two's complement number, the range of values is:

```
Minimum: -2^(n-1)
Maximum:  2^(n-1) - 1
```

| Bits | Minimum | Maximum |
|------|---------|---------|
| 4 | -8 | +7 |
| 8 | -128 | +127 |
| 16 | -32,768 | +32,767 |

### Why two's complement is preferred

| Feature | Sign and magnitude | Two's complement |
|---------|--------------------|------------------|
| Representations of zero | Two (+0 and -0) | One (only 0) |
| Binary addition | Requires special rules | Works normally with standard addition |
| Range (8-bit) | -127 to +127 | -128 to +127 |
| Used in hardware | Rarely | Yes — used by all modern processors |

<div class="key-term" markdown="1">
**Sign and magnitude** — a method of representing signed binary where the MSB indicates the sign (0 = positive, 1 = negative) and the remaining bits represent the value. **Two's complement** — the standard method used by computers to represent signed integers; negative numbers are formed by flipping all bits and adding 1.
</div>

<div class="exam-tip" markdown="1">
To check your two's complement conversion, convert the result back to denary using the negative MSB column value. If you apply the "flip and add 1" process **twice**, you get back to the original number — this works in both directions.
</div>

---

## Binary addition techniques

Binary addition follows the same principles as denary addition, but with only two digits (0 and 1).

### Rules of binary addition

| A | B | Sum | Carry |
|---|---|-----|-------|
| 0 | 0 | 0 | 0 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 1 |

When adding three bits (two inputs plus a carry): 1 + 1 + 1 = 1 with a carry of 1.

### Worked example

Add `01101011` (107) and `00110101` (53):

```
    1 1 1 1 1       ← carry row
    0 1 1 0 1 0 1 1  (107)
  + 0 0 1 1 0 1 0 1  (53)
  ─────────────────
    1 0 1 0 0 0 0 0  (160)
```

**Step by step (right to left):**
1. 1 + 1 = 0, carry 1
2. 1 + 0 + carry 1 = 0, carry 1
3. 0 + 1 + carry 1 = 0, carry 1
4. 1 + 1 + carry 1 = 1, carry 1
5. 0 + 0 + carry 1 = 1, carry 0
6. 1 + 1 = 0, carry 1
7. 1 + 0 + carry 1 = 0, carry 1
8. 0 + 0 + carry 1 = 1

Result: `10100000` = 160 (107 + 53 = 160)

<div class="exam-tip" markdown="1">
Always show the **carry row** above your working. This earns method marks and helps you avoid errors. Work from **right to left**, just as you would with denary addition.
</div>

---

## Concept of overflow

**Overflow** occurs when the result of a calculation is **too large** to be stored in the available number of bits.

### How overflow happens

- If two 8-bit numbers are added and the result requires 9 bits, an overflow has occurred
- The extra bit is lost, and the stored result is **incorrect**

**Example:** Add `11001000` (200) and `01100100` (100):

```
    1 1
    1 1 0 0 1 0 0 0  (200)
  + 0 1 1 0 0 1 0 0  (100)
  ─────────────────
  1 0 0 1 0 1 1 0 0  (300)
```

The result `100101100` needs **9 bits**, but if only 8 bits are available, the leading 1 is lost, leaving `00101100` = 44, which is incorrect.

<div class="key-term" markdown="1">
**Overflow** — an error that occurs when the result of an arithmetic operation exceeds the maximum value that can be stored in the available number of bits. The result wraps around and becomes incorrect.
</div>

### Consequences of overflow

- The stored result is **wrong** — it wraps around to a small number
- Programs may produce unexpected or incorrect outputs
- Processors have an **overflow flag** in the status register to detect when this happens
- Programmers must check for overflow and handle it appropriately

---

## Digital storage of graphics

All images on a computer are stored as a collection of **pixels** (picture elements). Each pixel is a single coloured dot, and thousands or millions of pixels together form an image.

### Key terms

| Term | Meaning |
|------|---------|
| **Pixel** | The smallest addressable element of an image — a single coloured dot |
| **Resolution** | The number of pixels in an image, expressed as width x height (e.g. 1920 x 1080) |
| **Colour depth** | The number of bits used to represent the colour of each pixel |

### Colour depth

- **1-bit** colour depth: each pixel is either black or white (2¹ = 2 colours)
- **8-bit** colour depth: 2⁸ = 256 colours per pixel
- **24-bit** colour depth: 2²⁴ = 16,777,216 colours per pixel (true colour — 8 bits each for red, green, blue)

### Calculating image file size

```
File size (bits) = Width (px) x Height (px) x Colour depth (bits)
```

**Example:** A 800 x 600 image at 24-bit colour depth:

800 x 600 x 24 = 11,520,000 bits = 1,440,000 bytes = 1,440 KB = 1.44 MB

### Trade-offs

- **Higher resolution** = more pixels = larger file size but more detail
- **Greater colour depth** = more colours = larger file size but more realistic images
- Compression techniques (lossy and lossless) can reduce file sizes

<div class="exam-tip" markdown="1">
In calculation questions, always state the formula first, substitute your values, then convert the answer into appropriate units (bits to bytes: divide by 8; bytes to KB: divide by 1,000). Show every step of your working.
</div>

### Bitmap graphics

A **bitmap** (also called a raster image) stores an image as a **grid of pixels**. Each pixel holds a binary value representing its colour.

- The file stores colour data for **every individual pixel** in the image
- File size is directly determined by the number of pixels and the colour depth
- Common bitmap formats: BMP, PNG, JPEG, GIF

**Metadata stored with a bitmap file:**
- Image width and height (in pixels)
- Colour depth (bits per pixel)
- File format and compression type

### Vector graphics

A **vector** image stores an image as a collection of **mathematical objects** (lines, shapes, curves) defined by their properties.

- Each object is described by properties such as **coordinates, length, radius, fill colour, stroke colour, stroke width, and layer order**
- The file stores **instructions** for drawing the image, not individual pixels
- Common vector formats: SVG, AI, EPS, WMF

**Metadata stored with a vector file:**
- Canvas dimensions
- List of objects and their mathematical properties
- Layer and grouping information

### Bitmap vs vector comparison

| Feature | Bitmap | Vector |
|---------|--------|--------|
| **Made of** | Pixels (dots) | Mathematical objects (lines, shapes, curves) |
| **Scalability** | Loses quality when enlarged (pixelation) | Scales to any size without losing quality |
| **File size** | Depends on resolution and colour depth; can be very large | Generally smaller for simple images; size depends on number of objects |
| **Editing** | Edit individual pixels; hard to select and move objects | Edit individual objects (move, resize, recolour) easily |
| **Best for** | Photographs, complex images with subtle colour gradients | Logos, diagrams, icons, text, illustrations |
| **Example formats** | BMP, PNG, JPEG, GIF | SVG, AI, EPS |

<div class="key-term" markdown="1">
**Bitmap (raster) image** — an image made up of a grid of pixels, where each pixel stores colour data. **Vector image** — an image made up of mathematical objects defined by properties such as coordinates, fill, and stroke, allowing it to be scaled without loss of quality.
</div>

<div class="exam-tip" markdown="1">
A common exam question asks you to explain why a company logo should be stored as a vector rather than a bitmap. The key points are: logos must be **scaled** to many sizes (business cards to billboards) without losing quality, and vector files are typically **smaller** for simple shapes. Bitmaps would pixelate when enlarged.
</div>

---

## Digital storage and sampling of sound

Sound is an **analogue** signal — a continuous wave. To store sound digitally, it must be converted into binary using a process called **sampling**.

### How sampling works

1. A **microphone** converts sound waves into an electrical signal
2. An **ADC (Analogue-to-Digital Converter)** measures the amplitude of the signal at regular intervals
3. Each measurement is called a **sample** and is stored as a binary number

### Key terms

| Term | Meaning |
|------|---------|
| **Sample rate** | The number of samples taken per second, measured in hertz (Hz). CD quality = 44,100 Hz |
| **Bit depth** | The number of bits used to store each sample. More bits = more possible amplitude values = more accurate |
| **Bit rate** | The amount of data processed per second (sample rate x bit depth x channels) |

### Calculating sound file size

```
File size (bits) = Sample rate (Hz) x Bit depth (bits) x Duration (s) x Channels
```

**Example:** A 30-second stereo clip at 44,100 Hz and 16-bit depth:

44,100 x 16 x 30 x 2 = 42,336,000 bits = 5,292,000 bytes = 5,292 KB = 5.29 MB

### Trade-offs

- **Higher sample rate** = more accurate reproduction of the original sound, but larger file
- **Greater bit depth** = more precise amplitude values (less quantisation noise), but larger file
- Mono (1 channel) uses half the storage of stereo (2 channels)

<div class="key-term" markdown="1">
**Sampling** — the process of measuring an analogue sound wave at regular intervals and converting each measurement into a digital value. Higher sample rate and bit depth produce better quality but larger files.
</div>

---

## Use of metadata in files

**Metadata** is data that describes other data. It provides information **about** a file but is not part of the file's main content.

### Examples of metadata

| File Type | Example Metadata |
|-----------|-----------------|
| **Image** | Width, height, colour depth, file format, date taken, camera model, GPS location |
| **Sound** | Sample rate, bit depth, duration, number of channels, artist, album, genre |
| **Document** | Author, date created, date modified, file size, word count |
| **Video** | Resolution, frame rate, codec, duration, file size |

### Why metadata is important

- Helps the computer **correctly open and display** the file (e.g. knowing the resolution and colour depth of an image)
- Allows files to be **searched and organised** (e.g. sorting photos by date or music by artist)
- Provides information about the file **without opening it**
- Used by the operating system for file management

<div class="exam-tip" markdown="1">
If asked what metadata is, remember: it is "data about data." Always give **specific examples** relevant to the file type mentioned in the question — don't just give a generic definition.
</div>

---

## Character storage as binary; Unicode and ASCII

All characters (letters, numbers, symbols) are stored as **binary numbers** using a character encoding standard.

### ASCII (American Standard Code for Information Interchange)

- Uses **7 bits** per character (extended ASCII uses 8 bits)
- Can represent **128 characters** (or 256 in extended ASCII)
- Includes uppercase and lowercase letters, digits 0–9, punctuation, and control characters
- 'A' = 65, 'B' = 66, 'a' = 97, '0' = 48

| Character | Denary | Binary (7-bit) |
|-----------|--------|----------------|
| A | 65 | 1000001 |
| B | 66 | 1000010 |
| a | 97 | 1100001 |
| 0 | 48 | 0110000 |
| Space | 32 | 0100000 |

### Unicode

- A much larger character set designed to represent **every character from every language** in the world
- Can use **8, 16, or 32 bits** per character depending on the encoding (UTF-8, UTF-16, UTF-32)
- Supports over **143,000 characters** including Chinese, Arabic, emoji, and mathematical symbols
- The first 128 Unicode characters are identical to ASCII, so ASCII text is compatible with Unicode

| Feature | ASCII | Unicode |
|---------|-------|---------|
| Bits per character | 7 (or 8 extended) | 8, 16, or 32 |
| Number of characters | 128 (or 256) | Over 143,000 |
| Languages supported | English only | All languages |
| File size | Smaller | Larger |

<div class="key-term" markdown="1">
**ASCII** — a 7-bit character encoding standard representing 128 characters, primarily English letters, digits, and symbols. **Unicode** — a universal character encoding standard that can represent characters from all of the world's writing systems.
</div>

---

## Data types: Integer, Boolean, real, character, string

A **data type** defines what kind of value a variable can hold and what operations can be performed on it.

| Data Type | Description | Examples |
|-----------|-------------|----------|
| **Integer** | A whole number (positive, negative, or zero) — no decimal point | 42, -7, 0, 1000 |
| **Real** (float) | A number with a decimal point (fractional values) | 3.14, -0.5, 99.99 |
| **Boolean** | A value that is either **TRUE** or **FALSE** | TRUE, FALSE |
| **Character** | A single letter, digit, or symbol | 'A', '7', '!' |
| **String** | A sequence of characters (text) | "Hello", "CS2026", "" |

### Choosing the right data type

- Use **integer** for counting items, ages, scores — anything that is always a whole number
- Use **real** for measurements, prices, percentages — anything that may have decimal places
- Use **Boolean** for yes/no decisions, on/off states, true/false conditions
- Use **character** when you only need a single character (e.g. a grade: 'A', 'B', 'C')
- Use **string** for names, addresses, sentences — any text

<div class="exam-tip" markdown="1">
A common exam mistake is saying a phone number should be an integer. Phone numbers often start with 0, so they should be stored as a **string** to preserve the leading zero. Always think about whether arithmetic is needed — if not, use a string.
</div>

---

## Data structures: Records, 1D and 2D arrays

A **data structure** is a way of organising and storing data so it can be accessed and modified efficiently.

### Arrays

An **array** is an ordered collection of elements of the **same data type**, accessed using an **index** (position number).

**1D Array (one-dimensional):** A simple list of values.

```
students = ["Ali", "Beth", "Carl", "Dana"]
```

| Index | 0 | 1 | 2 | 3 |
|-------|---|---|---|---|
| Value | Ali | Beth | Carl | Dana |

- Access an element by its index: `students[0]` returns `"Ali"`

**2D Array (two-dimensional):** A table of values with rows and columns — like a grid or spreadsheet.

```
grades = [["Ali", 85, 72],
          ["Beth", 91, 68],
          ["Carl", 76, 80]]
```

| | Col 0 | Col 1 | Col 2 |
|---|-------|-------|-------|
| Row 0 | Ali | 85 | 72 |
| Row 1 | Beth | 91 | 68 |
| Row 2 | Carl | 76 | 80 |

- Access an element by row and column: `grades[1][2]` returns `68`

### Records

A **record** is a collection of related data items (fields) of **different data types** that describe one entity.

```
Student Record:
  Name: "Ali"        (string)
  Age: 15            (integer)
  Average: 78.5      (real)
  Prefect: TRUE      (Boolean)
```

- Each item in a record is called a **field**
- Each field can have a **different data type**
- A collection of records forms a **file** (like a database table)

<div class="key-term" markdown="1">
**Array** — an ordered collection of elements of the same data type, accessed by index. **Record** — a collection of related fields of potentially different data types, representing a single entity.
</div>

---

## Select and justify appropriate data structures

When designing a solution, you need to choose the **right data structure** for the task.

### How to choose

| Scenario | Best Structure | Justification |
|----------|----------------|---------------|
| Storing a list of 30 student names | 1D array | Same data type (strings), accessed by position |
| Storing a timetable with days and periods | 2D array | Tabular data with rows (days) and columns (periods) |
| Storing details about one student (name, age, grade) | Record | Different data types grouped together for one entity |
| Storing details about many students | File of records | Multiple records, each with the same set of fields |
| Storing a single yes/no answer | Boolean variable | Only two possible values |

### Justifying your choice

When the exam asks you to justify a data structure, your answer should:

1. **Name** the data structure
2. **Explain why** it suits the data (e.g. same data type, different data types, tabular layout)
3. **Explain the benefit** (e.g. efficient access by index, keeps related data together)

<div class="exam-tip" markdown="1">
Always link your justification to the specific scenario in the question. Do not just say "an array is good" — explain **why** it fits. For example: "A 1D array is suitable because all 20 temperatures are real numbers of the same type and can be accessed by index for efficient processing."
</div>

---

## File design for particular applications

When designing a file to store data for a particular application, you need to define:

### Fields

- Each piece of data to be stored is a **field** (e.g. Surname, DateOfBirth, Email)
- Choose a **meaningful field name** that clearly describes the data
- Select the correct **data type** for each field
- Define the **field length** — the maximum number of characters allowed

### Example file design: Library book system

| Field Name | Data Type | Field Length | Example Data |
|------------|-----------|-------------|--------------|
| BookID | String | 10 | "LIB0001" |
| Title | String | 50 | "Great Expectations" |
| Author | String | 40 | "Charles Dickens" |
| YearPublished | Integer | 4 | 1861 |
| Available | Boolean | — | TRUE |
| Price | Real | 5 | 12.99 |

### Key file

- One field should be a **primary key** — a unique identifier for each record (e.g. BookID)
- The primary key ensures no two records are identical and allows individual records to be found

<div class="key-term" markdown="1">
**Primary key** — a field (or combination of fields) that uniquely identifies each record in a file. No two records can share the same primary key value.
</div>

---

## Data validation and verification techniques

**Validation** and **verification** are two different techniques for ensuring data is accurate and reasonable.

### Validation

Validation checks that data is **reasonable, sensible, and within acceptable limits**. It does **not** check that data is correct — only that it is plausible.

| Validation Check | Description | Example |
|------------------|-------------|---------|
| **Range check** | Data falls within a specified range | Age must be between 0 and 120 |
| **Type check** | Data is the correct data type | Age must be an integer, not text |
| **Length check** | Data is the correct number of characters | Password must be 8–20 characters |
| **Presence check** | A required field is not left empty | Email field must be completed |
| **Format check** | Data matches a required pattern | Date must be DD/MM/YYYY |
| **Lookup check** | Data matches an entry in a predefined list | Title must be Mr, Mrs, Miss, Ms, Dr |
| **Check digit** | A calculated digit added to a number to detect errors | Last digit of a barcode ISBN |

#### Lookup table validation

A **lookup check** (or lookup table) compares the entered data against a **predefined list of acceptable values**. If the input is not in the list, it is rejected.

- Often implemented as a **dropdown menu**, combo box, or list box so the user can only choose from valid options
- Can also be implemented in code by checking input against an array of allowed values
- Prevents typing errors because the user selects rather than types

**Example:** A "Country" field could use a lookup table containing all valid country names. The user selects from the list, ensuring only a recognised country can be entered.

```
validTitles = ["Mr", "Mrs", "Miss", "Ms", "Dr"]

OUTPUT "Select a title: "
INPUT title

IF title NOT IN validTitles THEN
    OUTPUT "Invalid title. Please choose from the list."
END IF
```

#### Check digit verification

A **check digit** is an extra digit appended to a number, calculated from the other digits using a specific **algorithm**. It is used to detect errors in data entry or transmission.

- Used on **barcodes** (EAN), **ISBN numbers** (books), credit card numbers, and other numeric codes
- The receiving system recalculates the check digit from the other digits and compares it to the one supplied
- If they do not match, an **error is detected** — the number has been entered or transmitted incorrectly
- Check digits can detect common errors such as a single wrong digit or two adjacent digits being swapped

**Example — ISBN-13 check digit:**

1. Multiply each of the first 12 digits alternately by 1 and 3
2. Add all the results together
3. Divide by 10 and find the remainder
4. Subtract the remainder from 10 to get the check digit (if the result is 10, the check digit is 0)

<div class="key-term" markdown="1">
**Lookup table** — a validation technique that compares input against a predefined list of acceptable values, often presented as a dropdown menu. **Check digit** — an extra digit calculated from other digits using an algorithm, appended to a code (such as a barcode or ISBN) to detect data entry or transmission errors.
</div>

### Verification

Verification checks that data has been **accurately transferred** or entered — that what was intended is what was actually input.

| Verification Method | Description |
|---------------------|-------------|
| **Double entry** | Data is entered twice and the two entries are compared; any differences are flagged |
| **Visual check / proofreading** | A human visually checks the data on screen against the original source |
| **Parity check** | An extra bit is added to each byte to detect transmission errors |
| **Checksum** | A calculated value sent with data; the receiver recalculates and compares |

<div class="exam-tip" markdown="1">
Remember the difference: **Validation** = "is this data reasonable?" **Verification** = "is this data what the user actually intended?" Validation can be automated; verification often involves the user or comparison of two copies. Data can pass validation but still be wrong (e.g. an age of 25 passes a range check even if the real age is 52).
</div>

---

## Design algorithms for validation and verification

You may be asked to write **pseudocode** or **flowcharts** that implement validation and verification checks.

### Example 1: Range check for age

```
REPEAT
    OUTPUT "Enter your age: "
    INPUT age
    IF age < 0 OR age > 120 THEN
        OUTPUT "Invalid age. Must be between 0 and 120."
    END IF
UNTIL age >= 0 AND age <= 120
```

### Example 2: Length check for password

```
REPEAT
    OUTPUT "Enter a password (8-20 characters): "
    INPUT password
    IF LENGTH(password) < 8 OR LENGTH(password) > 20 THEN
        OUTPUT "Password must be between 8 and 20 characters."
    END IF
UNTIL LENGTH(password) >= 8 AND LENGTH(password) <= 20
```

### Example 3: Double entry verification for email

```
OUTPUT "Enter your email: "
INPUT email1
OUTPUT "Re-enter your email: "
INPUT email2

IF email1 = email2 THEN
    OUTPUT "Email confirmed."
ELSE
    OUTPUT "Emails do not match. Please try again."
END IF
```

### Example 4: Presence check and type check combined

```
REPEAT
    OUTPUT "Enter the quantity (whole number): "
    INPUT quantity
    IF quantity = "" THEN
        OUTPUT "This field cannot be empty."
    ELSE IF NOT IS_INTEGER(quantity) THEN
        OUTPUT "Please enter a whole number."
    ELSE IF quantity < 1 THEN
        OUTPUT "Quantity must be at least 1."
    END IF
UNTIL IS_INTEGER(quantity) AND quantity >= 1
```

<div class="exam-tip" markdown="1">
When writing validation algorithms, use a **REPEAT...UNTIL** loop so the user is asked again if the data fails the check. Always include a clear **error message** that tells the user what went wrong and what is expected. Combine multiple checks where appropriate (e.g. presence check first, then type check, then range check).
</div>
