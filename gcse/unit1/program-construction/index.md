---
layout: topic
title: "Program Construction"
level: "GCSE"
level_url: "/gcse/"
unit_name: "Unit 1: Understanding Computer Science"
unit_url: "/gcse/unit1/"
prev_topic: "/gcse/unit1/software-engineering/"
next_topic: "/gcse/unit1/security-data-management/"
---

## Compilers, interpreters and assemblers: Purpose and examples

Before a program written in a high-level or assembly language can be executed by a computer, it must be **translated** into machine code (binary). There are three types of translator.

<div class="key-term" markdown="1">
**Source code** — the original program written by the programmer in a high-level or assembly language. **Object code** (or machine code) — the translated binary version that the CPU can execute directly.
</div>

### Compiler

A compiler translates the **entire** source code into machine code **in one go**, before the program is run.

- Produces a **standalone executable file** that can be run without the compiler
- Reports **all errors at the end** of compilation, making debugging harder at first
- Once compiled, the program runs **very quickly** because no translation is needed at runtime
- The compiled program can be **distributed without revealing the source code**
- Examples: C, C++, Java (compiled to bytecode)

### Interpreter

An interpreter translates and executes the source code **one line at a time**.

- **No executable file** is produced — the interpreter must be present every time the program runs
- Stops at the **first error** it finds, making it easier to debug during development
- Runs **more slowly** than compiled code because translation happens every time
- The source code is always visible, which is a disadvantage for commercial software
- Examples: Python, JavaScript, Ruby

### Assembler

An assembler translates **assembly language** into machine code.

- Assembly language uses **mnemonics** (short codes like `LDA`, `ADD`, `STO`) that correspond directly to machine code instructions
- There is a **one-to-one relationship** between each assembly instruction and its machine code equivalent
- The resulting machine code is specific to a particular **processor architecture**

| Feature | Compiler | Interpreter | Assembler |
|---------|----------|-------------|-----------|
| **Translates** | Entire program at once | One line at a time | Assembly to machine code |
| **Speed of execution** | Fast (pre-translated) | Slow (translates each run) | Fast (direct mapping) |
| **Error reporting** | All errors after compilation | Stops at first error | Reports errors on assembly |
| **Output** | Executable file | No separate file | Machine code file |
| **Source code visible?** | No (only executable shared) | Yes (source needed to run) | No (only machine code shared) |

<div class="exam-tip" markdown="1">
A common exam question asks you to compare compilers and interpreters. Remember: compilers are better for **distributing finished software** (faster, source hidden), while interpreters are better for **developing and testing** programs (immediate error feedback).
</div>

---

## Compilation stages: Lexical analysis, symbol table, syntax analysis

The compilation process has several distinct stages. This section covers the first three.

### Lexical analysis

Lexical analysis is the **first stage** of compilation. The lexer (or scanner) reads through the source code character by character and:

1. **Removes whitespace and comments** — these are not needed for the machine code
2. **Breaks the code into tokens** — individual meaningful units such as keywords, identifiers, operators, and literals
3. **Replaces identifiers with references** to entries in the **symbol table**
4. Produces a **stream of tokens** that is passed to the next stage

For example, the line `total = price + tax` would be broken into tokens: `total`, `=`, `price`, `+`, `tax`.

### Symbol table

The **symbol table** is a data structure created and maintained during compilation. It stores information about every identifier (variable name, function name, etc.) used in the program.

| Information stored | Example |
|--------------------|---------|
| **Identifier name** | `total` |
| **Data type** | Integer, Real, String |
| **Memory address** | Location where the value is stored |
| **Scope** | Where in the program it can be accessed |
| **Value** (if constant) | `100` |

The symbol table is **built up during lexical analysis** and **used throughout** the remaining stages of compilation. If an identifier is used but never declared, the compiler can detect this using the symbol table.

### Syntax analysis (parsing)

Syntax analysis checks whether the stream of tokens follows the **grammar rules** of the programming language.

- The tokens are compared against the language's syntax rules (often defined in a format called **BNF** — Backus-Naur Form)
- A **parse tree** (or syntax tree) is built, representing the structure of the program
- If a token sequence does not match any valid rule, a **syntax error** is reported
- Examples of syntax errors: missing brackets, missing semicolons, incorrect keyword spelling

<div class="key-term" markdown="1">
**Syntax analysis** — the stage of compilation that checks the token stream against the grammar rules of the language and builds a parse tree. If the structure is invalid, syntax errors are reported.
</div>

---

## Compilation stages: Semantic analysis, code generation, optimisation

### Semantic analysis

Semantic analysis checks that the program **makes logical sense**, even if the syntax is correct.

- **Type checking** — ensuring you don't try to add a string to an integer, for example
- **Undeclared variables** — checking that all variables have been declared before use
- **Scope checking** — ensuring variables are used within their valid scope
- **Type compatibility** — checking that assignments and operations involve compatible data types

A program can be syntactically correct but semantically wrong. For example, `"hello" + 5` may follow syntax rules but is a semantic error because you cannot add a string and a number.

### Code generation

Code generation is the stage where the compiler converts the parse tree into **machine code** (or an intermediate code).

- The parse tree is walked through, and corresponding machine code instructions are produced for each node
- The output is often initially in an **intermediate form** before final machine code is generated
- Memory addresses from the symbol table are used to allocate storage for variables

### Code optimisation

Optimisation improves the generated code to make it **run faster** or **use less memory**, without changing what the program does.

- **Removing redundant instructions** — for example, removing a variable that is assigned but never used
- **Simplifying calculations** — replacing `x * 2` with `x + x` if it is faster on the target processor
- **Loop optimisation** — moving calculations that produce the same result every iteration outside of the loop
- **Dead code elimination** — removing code that can never be reached or executed

<div class="exam-tip" markdown="1">
In exam questions about compilation stages, remember the order: **lexical analysis** (tokenisation) then **syntax analysis** (grammar check) then **semantic analysis** (logic/meaning check) then **code generation** then **optimisation**. You may be asked to identify which stage detects a particular type of error.
</div>

| Stage | Purpose | Type of error detected |
|-------|---------|----------------------|
| Lexical analysis | Tokenises code, removes comments | Illegal characters, invalid tokens |
| Syntax analysis | Checks grammar rules | Missing brackets, wrong structure |
| Semantic analysis | Checks logical meaning | Type mismatches, undeclared variables |
| Code generation | Produces machine code | — |
| Optimisation | Improves efficiency | — |

---

## Programming errors: Description and examples

Errors in programs fall into three main categories. Understanding the differences is essential for debugging.

### Syntax errors

A **syntax error** occurs when the code **breaks the grammar rules** of the programming language. The program **will not compile or run** until all syntax errors are fixed.

Examples:
- Missing a closing bracket: `print("hello"`
- Misspelling a keyword: `pritn("hello")`
- Missing a colon at the end of an `if` statement (in Python): `if x > 5`
- Forgetting to declare a variable (in languages that require it)

Syntax errors are detected at **compile time** (by a compiler) or immediately when the line is reached (by an interpreter).

### Logic errors

A **logic error** occurs when the program runs without crashing but **produces incorrect results**. The code is syntactically valid, but the algorithm is wrong.

Examples:
- Using `+` instead of `-` in a calculation
- Using `>` instead of `>=` in a condition, causing an off-by-one error
- An infinite loop caused by forgetting to update the loop counter
- Calculating an average by dividing by the wrong number

Logic errors are the **hardest to find** because the program does not crash or display an error message. They require careful **testing and tracing** to identify.

### Runtime errors

A **runtime error** occurs when the program crashes or stops unexpectedly **while running**. The syntax is correct, but something goes wrong during execution.

Examples:
- **Division by zero** — attempting to divide a number by 0
- **File not found** — trying to open a file that does not exist
- **Stack overflow** — infinite recursion that uses up all available memory
- **Out of range** — accessing an array index that does not exist
- **Type error** — attempting an operation on the wrong data type at runtime

<div class="key-term" markdown="1">
**Syntax error** — code breaks the language's grammar rules and will not run. **Logic error** — code runs but produces the wrong output. **Runtime error** — code compiles but crashes during execution due to an unexpected condition.
</div>

| Error type | When detected | Program runs? | Example |
|------------|---------------|---------------|---------|
| **Syntax** | Compile time / interpretation | No | Missing bracket |
| **Logic** | During testing (by the programmer) | Yes, but wrong output | Wrong operator used |
| **Runtime** | During execution | Starts, then crashes | Division by zero |

<div class="exam-tip" markdown="1">
Exam questions may give you a code snippet and ask you to identify the type of error. If the code would not run at all, it is a syntax error. If it runs but gives the wrong answer, it is a logic error. If it runs but crashes on certain inputs, it is a runtime error.
</div>
