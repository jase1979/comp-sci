---
layout: topic
title: "Logical Operations"
level: "GCSE"
level_url: "/gcse/"
unit_name: "Unit 1: Understanding Computer Science"
unit_url: "/gcse/unit1/"
prev_topic: "/gcse/unit1/hardware/"
next_topic: "/gcse/unit1/communication/"
---

## Logical operators: AND, OR, NOT, XOR

Computers use **logic gates** to make decisions. Every decision inside a processor comes down to combinations of simple logical operations on binary values (1 = TRUE, 0 = FALSE).

There are four logical operators you need to know:

### AND

The output is **1 only if both inputs are 1**.

| A | B | A AND B |
|---|---|---------|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

Think of it as: "both conditions must be true." For example, a door opens only if a valid keycard is presented **AND** the correct PIN is entered.

### OR

The output is **1 if at least one input is 1**.

| A | B | A OR B |
|---|---|--------|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

Think of it as: "at least one condition must be true." For example, a fire alarm sounds if smoke is detected **OR** a manual button is pressed.

### NOT

The output is the **opposite** of the input. NOT only takes **one input**.

| A | NOT A |
|---|-------|
| 0 | 1 |
| 1 | 0 |

Think of it as: "flip the value." If a light switch is on, NOT turns it off, and vice versa.

### XOR (Exclusive OR)

The output is **1 if the inputs are different** (one is 1 and the other is 0).

| A | B | A XOR B |
|---|---|---------|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

Think of it as: "one or the other, but not both." XOR differs from OR only on the last row — when both inputs are 1, XOR gives 0 while OR gives 1.

<div class="key-term" markdown="1">
**Logic gate** — an electronic circuit that performs a logical operation on one or more binary inputs to produce a single binary output. The four gates at GCSE are AND, OR, NOT, and XOR.
</div>

<div class="exam-tip" markdown="1">
Learn the truth tables by heart. A quick way to remember: **AND** is strict (both must be 1), **OR** is generous (any 1 will do), **XOR** is exclusive (only one can be 1), and **NOT** simply flips.
</div>

---

## Combinations of operators in truth tables

Real-world logic often requires **combining** two or more operators in a single expression. To work these out, you build a truth table with **intermediate columns** — one for each sub-expression — and evaluate them step by step.

### Example 1: NOT A AND B

This means: first apply NOT to A, then AND the result with B.

| A | B | NOT A | NOT A AND B |
|---|---|-------|-------------|
| 0 | 0 | 1 | 0 |
| 0 | 1 | 1 | 1 |
| 1 | 0 | 0 | 0 |
| 1 | 1 | 0 | 0 |

### Example 2: (A OR B) AND (NOT C)

With three inputs, the truth table has 2³ = **8 rows**. Work through each sub-expression in turn:

| A | B | C | A OR B | NOT C | (A OR B) AND (NOT C) |
|---|---|---|--------|-------|----------------------|
| 0 | 0 | 0 | 0 | 1 | 0 |
| 0 | 0 | 1 | 0 | 0 | 0 |
| 0 | 1 | 0 | 1 | 1 | 1 |
| 0 | 1 | 1 | 1 | 0 | 0 |
| 1 | 0 | 0 | 1 | 1 | 1 |
| 1 | 0 | 1 | 1 | 0 | 0 |
| 1 | 1 | 0 | 1 | 1 | 1 |
| 1 | 1 | 1 | 1 | 0 | 0 |

### How to build a combined truth table

1. **List all inputs** — with *n* inputs you need 2ⁿ rows
2. **Fill in all possible input combinations** systematically (count in binary)
3. **Add a column for each sub-expression**, working from the innermost brackets outward
4. **Evaluate the final expression** using the intermediate results

<div class="exam-tip" markdown="1">
Always add intermediate columns for each step. This earns method marks even if your final answer has an error, and it helps you avoid mistakes. Use brackets to make the order of operations clear.
</div>

---

## Simplify Boolean expressions using identities and rules

Boolean algebra lets us **simplify** complex logical expressions into shorter, equivalent ones. Simpler expressions need fewer logic gates, which means cheaper and faster circuits.

### Key Boolean identities

| Identity | Rule | Explanation |
|----------|------|-------------|
| **Identity law** | A AND 1 = A | ANDing with 1 leaves A unchanged |
| | A OR 0 = A | ORing with 0 leaves A unchanged |
| **Null law** | A AND 0 = 0 | ANDing with 0 always gives 0 |
| | A OR 1 = 1 | ORing with 1 always gives 1 |
| **Idempotent law** | A AND A = A | ANDing something with itself gives itself |
| | A OR A = A | ORing something with itself gives itself |
| **Complement law** | A AND (NOT A) = 0 | A value and its opposite can never both be 1 |
| | A OR (NOT A) = 1 | A value or its opposite is always 1 |
| **Double negation** | NOT (NOT A) = A | Two NOTs cancel out |
| **Commutative law** | A AND B = B AND A | Order does not matter |
| | A OR B = B OR A | Order does not matter |
| **Absorption law** | A OR (A AND B) = A | The second term is absorbed by the first |
| | A AND (A OR B) = A | The second term is absorbed by the first |

### De Morgan's Laws

These are especially useful for simplifying expressions involving NOT applied to compound expressions:

- **NOT (A AND B) = (NOT A) OR (NOT B)**
- **NOT (A OR B) = (NOT A) AND (NOT B)**

In words: when you "break open" a NOT over a bracketed expression, you flip the operator (AND becomes OR, OR becomes AND) and negate each term.

<div class="key-term" markdown="1">
**De Morgan's Laws** — rules that describe how NOT distributes over AND and OR. They are essential for simplifying Boolean expressions: NOT (A AND B) = (NOT A) OR (NOT B), and NOT (A OR B) = (NOT A) AND (NOT B).
</div>

### Simplification example

Simplify: **(A AND B) OR (A AND NOT B)**

1. Factor out the common term A: **A AND (B OR NOT B)**
2. Apply the complement law — B OR NOT B = 1: **A AND 1**
3. Apply the identity law — A AND 1 = A: **A**

So the expression simplifies to just **A**.

### Verifying with a truth table

You can always check a simplification is correct by building truth tables for both the original and simplified expressions — they should produce identical outputs for every input combination.

| A | B | NOT B | A AND B | A AND NOT B | (A AND B) OR (A AND NOT B) | Simplified: A |
|---|---|-------|---------|-------------|----------------------------|---------------|
| 0 | 0 | 1 | 0 | 0 | 0 | 0 |
| 0 | 1 | 0 | 0 | 0 | 0 | 0 |
| 1 | 0 | 1 | 0 | 1 | 1 | 1 |
| 1 | 1 | 0 | 1 | 0 | 1 | 1 |

The last two columns match, confirming the simplification is correct.

<div class="exam-tip" markdown="1">
In the exam, always **state which identity or rule** you are applying at each step. Simply jumping to the answer without showing working will not earn full marks. If unsure, draw truth tables for both the original and simplified versions to verify your answer.
</div>
