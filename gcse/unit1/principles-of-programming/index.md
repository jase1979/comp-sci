---
layout: topic
title: "Principles of Programming"
level: "GCSE"
level_url: "/gcse/"
unit_name: "Unit 1: Understanding Computer Science"
unit_url: "/gcse/unit1/"
prev_topic: "/gcse/unit1/system-software/"
next_topic: "/gcse/unit1/software-engineering/"
---

## Characteristics of high-level and low-level languages

Programming languages are divided into two broad categories: **high-level** and **low-level**. The level refers to how close the language is to human language (high) or machine code (low).

### High-Level Languages

High-level languages are designed to be **easy for humans to read and write**. They use English-like keywords and mathematical notation.

- Each statement typically carries out **multiple** low-level operations
- Code is **portable** — the same source code can run on different types of hardware with the appropriate translator
- Must be translated into machine code before the CPU can execute it, using a **compiler** or **interpreter**
- Examples include **Python**, **Java**, **C#**, **Visual Basic** and **JavaScript**

```
total = 0
for i in range(10):
    total = total + i
print(total)
```

<div class="key-term" markdown="1">
**High-level language** — a programming language that uses English-like syntax and abstracts away hardware details. It must be translated into machine code before execution.
</div>

### Low-Level Languages

Low-level languages are much closer to the **binary instructions** that the CPU directly understands. There are two types:

**Machine Code**
- The **only** language the CPU can execute directly — no translation needed
- Written entirely in **binary** (1s and 0s)
- Extremely difficult for humans to read, write and debug
- Specific to a particular **processor architecture** (not portable)

**Assembly Language**
- Uses short **mnemonics** (e.g. `LDA`, `ADD`, `STO`, `OUT`) to represent machine code instructions
- Each mnemonic corresponds to **one** machine code instruction
- Must be translated into machine code by an **assembler**
- Still specific to a particular processor architecture

```
LDA 5
ADD 6
STO 7
OUT
```

<div class="key-term" markdown="1">
**Assembly language** — a low-level language that uses short mnemonic codes to represent individual machine code instructions. It requires an assembler to translate it into executable machine code.
</div>

### Comparison Table

| Feature | High-Level Language | Low-Level Language |
|---------|--------------------|--------------------|
| **Readability** | Easy to read and write | Difficult to read and write |
| **Portability** | Portable across platforms | Tied to specific processor |
| **Translation** | Needs compiler or interpreter | Needs assembler (or none for machine code) |
| **Speed of execution** | Generally slower (translation overhead) | Very fast (close to or is machine code) |
| **Lines of code** | Fewer lines needed | Many more lines needed |
| **Debugging** | Easier to find and fix errors | Much harder to debug |
| **Hardware access** | Limited direct hardware control | Direct access to hardware and memory |
| **Abstraction** | High — hides hardware details | Low — programmer manages hardware details |

<div class="exam-tip" markdown="1">
Remember that "low-level" does **not** mean low quality. It means the language is close to the machine. Low-level languages are extremely powerful for tasks that need direct hardware control.
</div>

---

## Situations requiring high-level or low-level language

Different programming tasks call for different types of language. The choice depends on what the software needs to achieve.

### When to Use a High-Level Language

High-level languages are the best choice for **most** software development because they are faster to write, easier to maintain, and portable.

| Situation | Why High-Level is Suitable |
|-----------|---------------------------|
| **Developing desktop applications** (e.g. word processor, spreadsheet) | Large, complex programs benefit from readable, maintainable code |
| **Web development** (e.g. websites, web apps) | Languages like JavaScript and Python are designed for rapid development |
| **Mobile apps** | Frameworks in high-level languages enable cross-platform development |
| **School/educational projects** | Easier syntax allows students to focus on problem-solving rather than hardware details |
| **Rapid prototyping** | Quicker to write and test ideas before committing to a full build |
| **Working in a team** | Readable code is easier for multiple programmers to understand and collaborate on |

### When to Use a Low-Level Language

Low-level languages are used when **performance**, **hardware control** or **resource efficiency** is critical.

| Situation | Why Low-Level is Suitable |
|-----------|--------------------------|
| **Writing device drivers** | Drivers need to communicate directly with specific hardware components |
| **Programming embedded systems** | Embedded devices (e.g. washing machine controllers) have very limited memory and processing power |
| **Operating system development** | OS kernels need direct access to CPU registers, memory and hardware |
| **Real-time systems** (e.g. aircraft control, medical devices) | Execution speed and predictable timing are critical for safety |
| **Game engine optimisation** | Performance-critical sections benefit from fine-tuned low-level code |
| **Security-sensitive code** (e.g. encryption routines) | Precise control over memory and execution prevents vulnerabilities |

<div class="exam-tip" markdown="1">
Exam questions often present a **scenario** and ask you to recommend a high-level or low-level language. Always **justify** your choice by linking the language characteristics to the requirements of the scenario. For example: "A low-level language is appropriate for programming the embedded system in a heart rate monitor because it needs to run on a processor with very limited memory and must respond in real time."
</div>

### Key Decision Factors

When deciding which type of language to use, consider these questions:

- **Does the program need direct access to hardware?** If yes, use a low-level language.
- **Is memory extremely limited?** If yes, low-level gives finer control over memory usage.
- **Does the program need to run on multiple platforms?** If yes, a high-level language offers portability.
- **Is development speed important?** If yes, high-level languages are much faster to code in.
- **Will the code need to be maintained or updated by others?** If yes, high-level code is easier to read and modify.
- **Is execution speed absolutely critical?** If yes, low-level code runs faster because it is closer to machine code.

<div class="key-term" markdown="1">
**Portability** — the ability of source code to be run on different types of hardware or operating systems without modification. High-level languages are portable; low-level languages are not.
</div>

---

## Little Man Computer (LMC)

The **Little Man Computer (LMC)** is a simplified model of a computer, used to teach the fundamental concepts of how a CPU executes machine code instructions. It was designed as an educational tool to demonstrate the **fetch-decode-execute cycle**, **assembly language**, and how data moves between memory and registers.

<div class="key-term" markdown="1">
The **Little Man Computer (LMC)** is an instructional model of a simple computer. It has a limited instruction set, a single accumulator register, an input tray, an output tray, and 100 mailboxes (memory locations numbered 00–99).
</div>

In the LMC model, a "little man" inside the computer reads instructions from mailboxes one at a time, performs the operation, and moves to the next instruction. This mirrors how a real CPU fetches, decodes, and executes instructions.

### LMC Instruction Set

The LMC uses **mnemonics** (short codes) to represent instructions, just like real assembly language. Each instruction has a three-digit numeric machine code equivalent.

| Mnemonic | Numeric Code | Instruction | Description |
|----------|-------------|-------------|-------------|
| **INP** | 901 | Input | Takes a value from the input tray and stores it in the accumulator |
| **OUT** | 902 | Output | Outputs the value in the accumulator to the output tray |
| **STA** | 3xx | Store | Stores the value in the accumulator into mailbox address xx |
| **LDA** | 5xx | Load | Loads the value from mailbox address xx into the accumulator |
| **ADD** | 1xx | Add | Adds the value in mailbox address xx to the accumulator |
| **SUB** | 2xx | Subtract | Subtracts the value in mailbox address xx from the accumulator |
| **BRA** | 6xx | Branch always | Unconditionally jumps to the instruction at address xx |
| **BRZ** | 7xx | Branch if zero | Jumps to address xx only if the accumulator value is zero |
| **BRP** | 8xx | Branch if positive | Jumps to address xx only if the accumulator value is zero or positive |
| **HLT** | 000 | Halt | Stops the program |
| **DAT** | — | Data | Defines a named memory location for storing data (used as a label) |

<div class="exam-tip" markdown="1">
You must memorise all the LMC mnemonics and what they do. In the exam, you may be asked to **trace** an LMC program (showing the accumulator value and outputs at each step), **write** an LMC program for a given task, or **explain** what an existing LMC program does.
</div>

### Worked Example: Add Two Numbers

**Task:** Take two numbers as input, add them together, and output the result.

```
        INP         // Read first number into accumulator
        STA FIRST   // Store it in mailbox labelled FIRST
        INP         // Read second number into accumulator
        ADD FIRST   // Add the value stored in FIRST to the accumulator
        OUT         // Output the result
        HLT         // Stop the program
FIRST   DAT         // Reserve a mailbox labelled FIRST
```

**Step-by-step trace (inputs: 25, 17):**

| Step | Instruction | Accumulator | Output | Notes |
|------|-------------|-------------|--------|-------|
| 1 | INP | 25 | — | User inputs 25 |
| 2 | STA FIRST | 25 | — | Stores 25 in FIRST |
| 3 | INP | 17 | — | User inputs 17 |
| 4 | ADD FIRST | 42 | — | 17 + 25 = 42 |
| 5 | OUT | 42 | 42 | Outputs 42 |
| 6 | HLT | 42 | — | Program stops |

### Worked Example: Subtract Two Numbers and Output

**Task:** Input two numbers, subtract the second from the first, and output the result.

```
        INP         // Read first number into accumulator
        STA FIRST   // Store it in FIRST
        INP         // Read second number into accumulator
        STA SECOND  // Store it in SECOND
        LDA FIRST   // Load FIRST back into accumulator
        SUB SECOND  // Subtract SECOND from accumulator
        OUT         // Output the result
        HLT         // Stop the program
FIRST   DAT         // Reserve mailbox for first number
SECOND  DAT         // Reserve mailbox for second number
```

### Worked Example: Countdown from Input to Zero

**Task:** Input a number, output a countdown from that number to zero.

```
        INP         // Read the starting number
LOOP    OUT         // Output the current value
        STA COUNT   // Store current value
        SUB ONE     // Subtract 1
        BRP LOOP    // If result >= 0, branch back to LOOP
        HLT         // Stop when negative
ONE     DAT 1       // Constant value 1
COUNT   DAT         // Storage for current count
```

<div class="exam-tip" markdown="1">
When writing LMC programs, always put your `DAT` labels at the **end** of the program. If you place them in the middle, the CPU will try to execute them as instructions and the program will not work correctly. Remember that `BRZ` and `BRP` are used to create loops and conditional behaviour.
</div>
