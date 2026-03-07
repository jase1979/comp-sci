# Past Paper Question Extraction Guide

This file explains how to extract WJEC past paper questions into structured JSON for the revision site.

## Overview

The site at `/past-papers/` renders questions from two JSON data files:
- `_data/past_papers.json` — GCSE questions (currently 85 questions, 3 papers)
- `_data/as_past_papers.json` — AS-level questions (currently 181 questions, 7 papers)

Each paper has a **question paper PDF** and a **mark scheme PDF**. Both are needed to create the JSON entries.

## Step 1: Extract text from PDFs

The `Read` tool can't reliably render PDF text. Use `pdftotext` instead:

```bash
pdftotext "/Users/jason/comp_sci/Past Papers/extracted/as-level/s24-2505-01.pdf" /tmp/s24-as-qp.txt
pdftotext "/Users/jason/comp_sci/Past Papers/extracted/as-level/S24-2500U10-1-ms.pdf" /tmp/s24-as-ms.txt
```

Then read the resulting text files with the Read tool.

## Step 2: Create JSON entries

Read both the question paper and mark scheme text. For each question, create a JSON object. The `type` field determines what other fields are needed.

### Common fields (all question types)

```json
{
  "id": "as-s24-q2a",
  "paper": "S24-2500U10-1",
  "year": 2024,
  "session": "Summer",
  "level": "as",
  "question_number": "2a",
  "marks": 5,
  "topic": "communication",
  "type": "short-answer"
}
```

- **id**: `{level prefix}-{session+year}-q{number}`. GCSE has no prefix (e.g. `s24-q1`), AS uses `as-` prefix (e.g. `as-s24-q1`).
- **paper**: The paper code from the PDF header (e.g. `S24-2500U10-1` for AS, `S24-3500U10-1` for GCSE).
- **year**: Integer year.
- **session**: `"Summer"` for S papers, `"Winter"` for W papers, `"Autumn"` for Z papers (the COVID-era resit).
- **level**: `"as"` for AS-level. GCSE questions omit this field (defaults to `"gcse"` in the template).
- **question_number**: String. Use `"2a"`, `"2b"`, `"6d-ii"` etc. for sub-parts.
- **marks**: Integer.
- **topic**: One of the standard topics (see list below).
- **type**: One of the standard types (see list below).

### Topics

GCSE topics:
`hardware`, `communication`, `data-organisation`, `logical-operations`, `system-software`, `software-engineering`, `program-construction`, `principles-of-programming`, `security-data-management`, `ethical-legal-environmental`

AS topics (same set minus ethical-legal-environmental, plus algorithms):
`hardware`, `communication`, `data-organisation`, `logical-operations`, `system-software`, `software-engineering`, `program-construction`, `principles-of-programming`, `security-data-management`, `algorithms`

### Question types and their specific fields

#### `short-answer` and `written`

Use `short-answer` for questions worth 1-6 marks. Use `written` for extended response questions (typically 8-12 marks with banded marking).

```json
{
  "type": "short-answer",
  "question": "Describe the purpose of a router.",
  "answer": "A router forwards data packets between networks.\nIt reads the destination IP address in each packet.\nIt uses a routing table to determine the best path.\nIt connects a LAN to a WAN / the internet."
}
```

- **question**: The full question text. Use `\n` for line breaks.
- **answer**: The mark scheme answer. Include all acceptable answers. Use `\n` to separate bullet points.

#### `true-false`

```json
{
  "type": "true-false",
  "question": "Show if each statement about CPUs is TRUE or FALSE.",
  "statements": [
    { "text": "The CU decodes instructions in the CIR.", "answer": true },
    { "text": "The PC holds the current instruction.", "answer": false }
  ]
}
```

#### `matching`

```json
{
  "type": "matching",
  "question": "Match the network hardware with the correct description.",
  "options": ["Hub", "Router", "Switch", "Bridge"],
  "items": [
    { "description": "Joins together two networks that use the same base protocols.", "answer": "Bridge" },
    { "description": "Copies all incoming data to every port.", "answer": "Hub" }
  ]
}
```

#### `fill-blank`

```json
{
  "type": "fill-blank",
  "question": "Complete the following sentences about compilation.",
  "word_bank": ["Symbol", "Lexical", "Code", "Syntax"],
  "sentences": [
    { "text": "During ________ analysis, whitespace is removed.", "answer": "Lexical" },
    { "text": "A ________ table stores identifiers.", "answer": "Symbol" }
  ]
}
```

The `________` placeholder in the text becomes a dropdown in the UI populated from the word bank.

#### `multiple-choice`

```json
{
  "type": "multiple-choice",
  "question": "Which expression represents this truth table?",
  "options": ["C = A AND B", "C = A OR B", "C = A XOR B", "C = NOT A"],
  "answer": "C = A XOR B"
}
```

#### `truth-table`

```json
{
  "type": "truth-table",
  "question": "Draw a truth table for the following Boolean expression:",
  "expression": "X = A + B.C",
  "headers": ["A", "B", "C", "B.C", "X"],
  "given_columns": 3,
  "rows": [
    [0, 0, 0, 0, 0],
    [0, 0, 1, 0, 0],
    [0, 1, 0, 0, 0],
    [0, 1, 1, 1, 1],
    [1, 0, 0, 0, 1],
    [1, 0, 1, 0, 1],
    [1, 1, 0, 0, 1],
    [1, 1, 1, 1, 1]
  ]
}
```

- **given_columns**: Number of columns pre-filled (inputs). Columns from this index onward become interactive text inputs.
- **rows**: Array of arrays. Each inner array has values for every column (inputs + outputs). Use 0 and 1 (integers).

#### `code-error`

```json
{
  "type": "code-error",
  "question": "This pseudo code includes errors. Identify the errors and corrections.",
  "language": "python",
  "code": "def CalcPay():\n    Gross = input\n    Tax = Gross * 0.2\n    Net == Gross - Tax\n    return Net",
  "errors": [
    { "type": "Syntax error", "line": "Net == Gross - Tax", "correction": "Net = Gross - Tax (single equals for assignment)" },
    { "type": "Logic error", "line": "Gross = input", "correction": "Gross = float(input()) — needs to call input() and convert to number" }
  ]
}
```

## Step 3: Append to the JSON file

Edit the JSON file to append new entries. The easiest approach:
1. Read the file to find the closing `]`
2. Replace `]` with `,\n{new entries}\n]`
3. Validate with: `python3 -c "import json; json.load(open('_data/as_past_papers.json')); print('OK')"`

## Step 4: Choosing the right type

Most AS-level questions are `short-answer` or `written` since they require free-text responses. Use interactive types only when the question format naturally fits:

- Truth table completion -> `truth-table`
- "State whether each is true or false" -> `true-false`
- "Match X to Y" -> `matching`
- Fill in blanks from a word bank -> `fill-blank`
- Multiple choice with fixed options -> `multiple-choice`
- Find errors in code -> `code-error`
- Everything else -> `short-answer` (1-6 marks) or `written` (7+ marks)

## PDF locations

- GCSE papers: `/Users/jason/comp_sci/Past Papers/GCSE/`
- AS papers: `/Users/jason/comp_sci/Past Papers/extracted/as-level/`

## Papers already processed

**GCSE** (3 papers):
- S19: `s19-3500-01`
- Z22: `Z22-3500U10-1`
- S23: `s23-3500u10-1`
- S24: `S24-3500U10-1`

**AS** (7 papers):
- S16: `S16-2500U10-1`
- S17: `S17-2500U10-1`
- S18: `S18-2500U10-1`
- S19: `S19-2500U10-1`
- Z22: `Z22-2500U10-1`
- S23: `S23-2500U10-1`
- S24: `S24-2500U10-1`
