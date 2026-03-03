---
layout: topic
title: "Software Engineering"
level: "A2 Level"
level_url: "/a2/"
unit_name: "Unit 3: Programming & System Development"
unit_url: "/a2/unit3/"
subtopics:
  - "Types of software tools for software engineering"
  - "Role of software packages in analysis, specification, design, testing"
  - "Program version management"
---

## Types of Software Tools

Professional software engineering relies on a wide range of tools that support every stage of development.

### Integrated Development Environments (IDEs)

An **IDE** combines multiple development tools into a single application:

| Feature | Purpose |
|---------|---------|
| **Code editor** | Syntax highlighting, auto-completion, code folding, bracket matching |
| **Compiler/interpreter** | Translates source code within the IDE |
| **Debugger** | Step-through execution, breakpoints, variable inspection, watch windows, call stack viewer |
| **Build automation** | Compiles, links, and packages the project with one command |
| **Project management** | Organises source files, resources, and configurations |
| **Version control integration** | Commit, push, pull, and view diffs without leaving the IDE |

**Examples:** Visual Studio, IntelliJ IDEA, Eclipse, PyCharm, VS Code

### Debugging Tools

| Tool | Purpose |
|------|---------|
| **Breakpoints** | Pause execution at a specific line to examine program state |
| **Step-through** | Execute one line at a time (step into, step over, step out) |
| **Watch window** | Monitor the values of selected variables as the program runs |
| **Call stack viewer** | Shows the chain of function calls that led to the current point |
| **Memory inspector** | View raw memory contents and detect memory leaks |
| **Profiler** | Measures execution time of each function to find performance bottlenecks |

### Profiling Tools

A **profiler** analyses a running program to identify performance issues:

- **CPU profiling** — which functions consume the most processor time
- **Memory profiling** — how much memory each part of the program uses, detecting memory leaks
- **I/O profiling** — identifying slow file or network operations
- **Call graph** — visualises which functions call which, and how often

### Automated Testing Tools

| Tool Type | Description |
|-----------|------------|
| **Unit testing frameworks** | Test individual functions/methods in isolation (e.g. JUnit, pytest, NUnit) |
| **Integration testing tools** | Test how modules work together |
| **Test harness** | Automates running multiple tests and reporting results |
| **Code coverage tools** | Measure what percentage of code is executed by tests (statement, branch, path coverage) |
| **Regression testing** | Re-runs previous tests after changes to ensure nothing is broken |

### Build Tools and CI/CD

| Tool | Purpose |
|------|---------|
| **Build tools** | Automate compilation, linking, and packaging (e.g. Make, Gradle, Maven) |
| **Continuous Integration (CI)** | Automatically builds and tests the project whenever code is committed |
| **Continuous Deployment (CD)** | Automatically deploys tested code to production environments |
| **CI/CD pipelines** | Defined sequences of build, test, and deploy stages (e.g. GitHub Actions, Jenkins) |

<div class="exam-tip" markdown="1">
When asked about software tools, categorise them by **stage of development** they support: analysis tools help understand requirements, design tools help plan the solution, coding tools (IDE, editor) help write code, testing tools verify correctness, and deployment tools deliver the product.
</div>

---

## Role of Software Packages in Development

### Analysis and Specification

| Tool | Role |
|------|------|
| **CASE tools** (Computer-Aided Software Engineering) | Support the entire development lifecycle — generate diagrams, manage requirements, produce documentation |
| **Requirements management tools** | Track and organise requirements, link them to tests and designs |
| **Data modelling tools** | Create ER diagrams, normalise database designs |
| **Process modelling tools** | Create DFDs (data flow diagrams), use case diagrams |

### Design

| Tool | Role |
|------|------|
| **UML tools** | Create class diagrams, sequence diagrams, state diagrams, activity diagrams |
| **Prototyping tools** | Build interactive mockups of user interfaces before coding |
| **Wireframing tools** | Design page layouts and user flows |
| **Architecture tools** | Model system components and their interactions |

### Implementation

| Tool | Role |
|------|------|
| **Code editors and IDEs** | Write, compile, and debug source code |
| **Code generators** | Automatically produce code from models or specifications |
| **Refactoring tools** | Restructure existing code without changing behaviour (rename, extract method, move class) |
| **Linting tools** | Check code for style violations, potential bugs, and best practice adherence |

### Testing

| Tool | Role |
|------|------|
| **Test harnesses** | Provide a controlled environment for running automated tests |
| **Coverage tools** | Report which lines/branches of code are exercised by tests |
| **Performance testing tools** | Simulate load and measure response times (e.g. stress testing, load testing) |
| **Static analysis tools** | Analyse code without running it to find potential bugs, security vulnerabilities, and code smells |

---

## Program Version Management

### What is Version Control?

**Version control** (also called **source control**) is a system that records changes to files over time, allowing developers to track history, collaborate, and revert to previous versions.

<div class="key-term" markdown="1">
A **version control system (VCS)** tracks every change made to source code files, recording who made each change, when, and why. It enables multiple developers to work on the same project simultaneously without overwriting each other's work.
</div>

### Key Concepts

| Concept | Description |
|---------|-------------|
| **Repository** | The central store of all project files and their complete history |
| **Commit** | A snapshot of the project at a point in time, with a descriptive message |
| **Branch** | An independent line of development. The main branch (often called `main` or `master`) holds the stable code |
| **Merge** | Combining changes from one branch into another |
| **Conflict** | When two developers change the same lines — must be manually resolved |
| **Pull/Push** | Download changes from (pull) or upload changes to (push) the remote repository |
| **Clone** | Create a complete local copy of a remote repository |
| **Diff** | Shows the exact lines that changed between two versions |
| **Tag** | A named marker on a specific commit (often used for releases) |

### Version Numbering

**Semantic versioning** (SemVer) uses three numbers: **MAJOR.MINOR.PATCH**

| Component | When to Increment | Example |
|-----------|-------------------|---------|
| **MAJOR** | Incompatible changes that break backward compatibility | 1.0.0 → **2**.0.0 |
| **MINOR** | New features added in a backward-compatible way | 2.0.0 → 2.**1**.0 |
| **PATCH** | Bug fixes that don't add features or break compatibility | 2.1.0 → 2.1.**1** |

Pre-release versions may include labels: `2.0.0-beta.1`, `3.0.0-rc.2`

### Branching Strategies

| Strategy | Description |
|----------|-------------|
| **Feature branching** | Each new feature is developed in its own branch, then merged when complete |
| **Release branching** | A branch is created for each release version, allowing bug fixes without disrupting new development |
| **Hotfix branching** | Emergency fixes are made on a branch from the release, merged back to both release and main |

### Centralised vs Distributed VCS

| Feature | Centralised (e.g. SVN) | Distributed (e.g. Git) |
|---------|------------------------|----------------------|
| **Repository** | Single central server | Every developer has a full local copy |
| **Working offline** | Not possible — requires server connection | Full functionality offline |
| **Speed** | Slower — operations require network access | Faster — most operations are local |
| **Single point of failure** | Yes — if the server goes down, no one can work | No — any copy can restore the project |
| **Branching** | Heavyweight and slow | Lightweight and fast |
| **Collaboration** | Lock-based or merge-based | Always merge-based with pull requests |

### Rollback and History

Version control allows **rollback** — reverting the project to any previous commit:

- **Undo a single change** — revert one commit without affecting later work
- **Restore a previous version** — reset the entire project to an earlier state
- **Blame/annotate** — see who last changed each line of a file and when
- **Bisect** — binary search through commit history to find which commit introduced a bug

<div class="exam-tip" markdown="1">
Questions on version management often ask **why** it is needed in professional software development. Key points: it enables **collaboration** (multiple developers working simultaneously), provides a **complete audit trail** of changes, allows **rollback** if a change introduces bugs, supports **branching** for parallel development of features, and facilitates **code review** through pull/merge requests.
</div>
