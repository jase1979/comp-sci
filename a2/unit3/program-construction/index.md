---
layout: topic
title: "Program Construction"
level: "A2 Level"
level_url: "/a2/"
unit_name: "Unit 3: Programming & System Development"
unit_url: "/a2/unit3/"
subtopics:
  - "Translation programs: Making source programs executable"
  - "Compilers, interpreters and assemblers"
  - "Purpose and examples of each translator type"
  - "Distinguish between translation and execution errors"
---

## Translation Programs

A **translator** converts source code written in one language into another form — typically machine code that can be executed by the CPU. There are three main types of translator.

<div class="key-term" markdown="1">
A **translation program** takes source code as input and produces executable code (or an intermediate form) as output. The three types are **compilers**, **interpreters**, and **assemblers**.
</div>

---

## Compilers

A **compiler** translates an entire high-level language source program into machine code (object code) **before** execution. The resulting executable file can be run independently without the compiler.

### Stages of Compilation

| Stage | Purpose |
|-------|---------|
| **Lexical analysis** | Reads source code character by character. Removes whitespace and comments. Identifies **tokens** (keywords, identifiers, operators, literals). Produces a **token stream** and populates the **symbol table**. |
| **Syntax analysis (parsing)** | Checks the token stream against the language's grammar rules. Builds a **parse tree** (abstract syntax tree). Reports **syntax errors** with line numbers. |
| **Semantic analysis** | Checks for meaning errors: type mismatches, undeclared variables, incorrect function arguments. Annotates the parse tree with type information. |
| **Code generation** | Converts the parse tree into machine code or intermediate code. Allocates registers and memory addresses. |
| **Code optimisation** | Improves the generated code for speed or memory usage without changing behaviour. Examples: removing dead code, constant folding, loop unrolling. |

### Lexical Analysis in Detail

The lexer (scanner) processes the source code:

1. Reads the source file character by character
2. Groups characters into **lexemes** (meaningful sequences)
3. Classifies each lexeme as a **token** (keyword, identifier, literal, operator, separator)
4. Adds identifiers to the **symbol table** (stores name, type, scope, memory address)
5. Removes comments and whitespace
6. Replaces each token with a numeric code for efficiency

**Example:** The statement `total = price * 1.2` produces tokens:

| Lexeme | Token Type |
|--------|-----------|
| `total` | Identifier |
| `=` | Assignment operator |
| `price` | Identifier |
| `*` | Arithmetic operator |
| `1.2` | Numeric literal |

### Syntax Analysis in Detail

The parser checks the token stream against **grammar rules** (often defined in BNF):

1. Takes the token stream from the lexer
2. Applies grammar rules to build a **parse tree**
3. Detects **syntax errors** (missing brackets, invalid statements)
4. Each node in the tree represents a grammatical construct

For `total = price * 1.2`, the parse tree would show:

```
        Assignment
       /          \
   total       Multiply
              /        \
          price        1.2
```

### Advantages and Disadvantages of Compilers

| Advantage | Disadvantage |
|-----------|-------------|
| Compiled code runs **faster** — no translation overhead at runtime | **Slower development** — entire program must be recompiled after changes |
| Object code can be **distributed** without the source code (protects IP) | **Platform-specific** — compiled code only runs on the target architecture |
| Errors are reported **all at once** before execution | Error messages can be **harder to trace** back to the original source |
| Optimisation produces **efficient** machine code | Compilation can be **time-consuming** for large programs |

**Examples:** C, C++, Rust, Go, Pascal

---

## Interpreters

An **interpreter** translates and executes source code **one line (or statement) at a time**. No separate object code file is produced.

### How an Interpreter Works

1. Reads the next statement from the source code
2. **Analyses** it (lexical and syntax analysis)
3. **Translates** it into an intermediate form or machine code
4. **Executes** it immediately
5. Moves to the next statement
6. If an error is found, execution **stops** at that point with an error message

### Advantages and Disadvantages of Interpreters

| Advantage | Disadvantage |
|-----------|-------------|
| **Faster development** — changes can be tested immediately without recompilation | **Slower execution** — translation happens every time the program runs |
| **Easier debugging** — stops at the exact line where an error occurs | **Source code must be present** to run the program (no IP protection) |
| **Platform independent** — same source can run on any platform with the interpreter | A loop executed 1000 times is **translated 1000 times** |
| Good for **prototyping** and scripting | Requires the interpreter to be **installed** on the target machine |

**Examples:** Python (CPython interpreter), JavaScript (in browsers), Ruby, PHP

<div class="exam-tip" markdown="1">
Some languages use **both** compilation and interpretation. Java compiles to **bytecode** (an intermediate form), which is then interpreted or JIT-compiled by the **Java Virtual Machine (JVM)**. Python compiles to bytecode (`.pyc` files) which is executed by the Python interpreter. This hybrid approach combines portability with improved performance.
</div>

---

## Assemblers

An **assembler** translates **assembly language** (low-level, human-readable mnemonics) into **machine code** on a **one-to-one basis** — each assembly instruction maps to exactly one machine code instruction.

### Two-Pass Assembly

Most assemblers make **two passes** over the source code:

**First pass:**
1. Reads each instruction
2. Assigns **memory addresses** to each instruction (using a location counter)
3. Builds the **symbol table** — records labels and their memory addresses
4. Identifies any forward references (labels used before they are defined)

**Second pass:**
1. Reads each instruction again
2. Converts mnemonics to **opcodes** (binary machine code)
3. Resolves forward references using the symbol table
4. Replaces labels with their actual memory addresses
5. Produces the final **machine code** output

### Why Two Passes?

A single pass cannot resolve **forward references** — instructions that jump to labels defined later in the program. The first pass discovers all labels; the second pass can then replace them with addresses.

**Example:**

```
        BRZ end      ; Jump to 'end' — but where is it?
        ADD total
        ...
end:    HLT          ; First pass records: end = address 15
```

On the second pass, `BRZ end` is translated with the now-known address of `end`.

### Advantages and Disadvantages of Assemblers

| Advantage | Disadvantage |
|-----------|-------------|
| Produces **very efficient** machine code | **Platform-specific** — tied to one processor architecture |
| Programmer has **direct hardware control** | **Difficult to write and maintain** — very low level |
| One-to-one mapping makes translation **fast and simple** | Programs are **longer** and harder to read than HLL code |
| Useful for **embedded systems** and device drivers | **No portability** — must be rewritten for different CPUs |

---

## Comparing Translator Types

| Feature | Compiler | Interpreter | Assembler |
|---------|----------|-------------|-----------|
| **Input** | High-level source code | High-level source code | Assembly language |
| **Output** | Machine code (object file) | No output file — executes directly | Machine code |
| **Translation** | Whole program at once | One statement at a time | One-to-one (mnemonic → opcode) |
| **Speed of execution** | Fast (pre-compiled) | Slow (translated each run) | Fast (native machine code) |
| **Error reporting** | All errors after compilation | Stops at first error | All errors after assembly |
| **Source code needed at runtime?** | No | Yes | No |
| **Portability** | Low (platform-specific) | High (any platform with interpreter) | Very low (CPU-specific) |
| **Passes** | Multiple (lexical, syntax, semantic, code gen) | Single pass per statement | Two passes |

---

## Linkers and Loaders

After compilation, the object code may need to be combined with other modules before it can be executed.

### Linker

A **linker** combines multiple object code modules (including library routines) into a single executable file.

- **Static linking** — library code is copied into the executable at link time. Produces a larger file but runs independently.
- **Dynamic linking** — the executable contains references to shared libraries (DLLs on Windows, `.so` on Linux) that are loaded at runtime. Produces smaller files but requires the libraries to be present.

### Loader

A **loader** places the executable program into main memory and prepares it for execution.

1. Allocates memory for the program
2. Loads the machine code from disk into RAM
3. Sets up the **program counter** to the entry point
4. Resolves any remaining addresses (relocation)
5. Hands control to the program

---

## Translation Errors vs Execution Errors

### Translation Errors (Compile-Time Errors)

Detected **during translation** before the program runs:

| Error Type | Example |
|-----------|---------|
| **Syntax error** | Missing bracket: `print("hello"` |
| **Type error** | Assigning a string to an integer variable (in statically typed languages) |
| **Undeclared variable** | Using a variable name that hasn't been defined |
| **Missing semicolon** | `int x = 5` (in languages that require `;`) |

### Execution Errors (Runtime Errors)

Occur **during program execution** — the code is syntactically valid but encounters a problem at runtime:

| Error Type | Example |
|-----------|---------|
| **Division by zero** | `result = 10 / 0` |
| **Stack overflow** | Infinite recursion with no base case |
| **Array index out of bounds** | Accessing `arr[100]` when the array has 50 elements |
| **Null pointer / None reference** | Trying to access an attribute of a null object |
| **File not found** | Attempting to open a file that doesn't exist |
| **Out of memory** | Allocating more memory than is available |

### Logical Errors

A third category — **logical errors** — produce incorrect results but no error messages. The program runs without crashing but produces wrong output.

| Error Type | Example |
|-----------|---------|
| **Wrong operator** | Using `+` instead of `-` |
| **Off-by-one error** | Loop runs one too many or one too few times |
| **Incorrect condition** | Using `>` instead of `>=` |
| **Wrong variable** | Comparing `x > x` instead of `x > y` |

<div class="exam-tip" markdown="1">
Exam questions often ask you to **classify** errors. Remember: **syntax errors** are caught at translation time, **runtime errors** crash the program during execution, and **logical errors** produce wrong results without crashing. A compiler catches syntax and type errors; an interpreter catches them as it reaches each line. Neither can detect logical errors — only thorough **testing** reveals those.
</div>
