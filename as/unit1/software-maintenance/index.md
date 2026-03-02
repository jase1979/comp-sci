---
layout: topic
title: "Software Maintenance"
level: "AS"
level_url: "/as/"
unit_name: "Unit 1: Fundamentals of Computer Science"
unit_url: "/as/unit1/"
prev_topic: "/as/unit1/software-testing/"
next_topic: "/as/unit1/choosing-software/"
---

## The Need for Software Maintenance

Software maintenance is the process of modifying a software system **after it has been delivered** to the customer. It is an ongoing and essential part of the software development life cycle.

### Why Software Needs Maintenance

- **Bugs are discovered** after release that were not found during testing. No testing process can guarantee that all defects have been found.
- **User requirements change** over time. Businesses evolve, and the software must adapt to meet new needs.
- **The operating environment changes**. New operating systems, hardware, browsers, or regulations may require the software to be updated.
- **Users request improvements**. As users become familiar with the software, they often identify features they would like added or enhanced.
- **Security vulnerabilities** are discovered that must be patched to protect users and data.
- **Performance issues** become apparent under real-world usage patterns that were not anticipated during development.

### The Cost of Maintenance

Maintenance typically accounts for **60--80% of the total cost** of a software system over its entire lifetime. This is far more than the cost of initial development. This makes it critical to write maintainable code from the outset using good programming practices (modularity, meaningful variable names, comments, documentation).

<div class="key-term" markdown="1">
**Software maintenance** is the modification of a software product after delivery to correct faults, improve performance, or adapt the software to a changed environment. It is the longest and most expensive phase of the software development life cycle.
</div>

---

## Corrective Maintenance

**Corrective maintenance** involves diagnosing and fixing **errors (bugs)** that are discovered after the software has been released. These are faults that were not detected during the testing phase.

### Characteristics

- It is a **reactive** process -- it happens in response to a problem being reported.
- The trigger is a **bug report** from a user or an error log from the system.
- It may involve fixing crashes, incorrect calculations, data corruption, or security vulnerabilities.
- Fixes are often released as **patches** or **hotfixes**.

### Examples

- A user reports that the program crashes when they enter a date in a certain format. The developer identifies a parsing error and releases a patch.
- An online store calculates the wrong total when a discount code is applied to an order with more than 10 items. The logic error in the discount calculation is found and corrected.
- A security researcher discovers that the login system is vulnerable to SQL injection. A corrective patch is released urgently.
- The system fails to send email notifications when a user's subscription is about to expire due to an incorrect date comparison.

<div class="exam-tip" markdown="1">
Corrective maintenance is about fixing things that are **broken**. The key word is "error" or "bug". If a scenario describes a program not working correctly, the maintenance required is corrective.
</div>

---

## Adaptive Maintenance

**Adaptive maintenance** involves modifying the software to keep it working correctly in a **changing environment**. The software itself is not faulty -- but the world around it has changed.

### Characteristics

- It is a **proactive or reactive** process depending on whether the environmental change is anticipated.
- The trigger is a **change in the external environment**, not a bug in the software.
- The software's functionality does not change -- it is adapted so that the same functionality continues to work in the new environment.

### Examples

- A new version of Windows is released and the software needs to be updated to maintain compatibility.
- The government changes the VAT rate from 20% to 25%. The software must be updated to use the new rate.
- A company migrates from on-premises servers to cloud-based infrastructure, and the software must be adapted to work in the new hosting environment.
- A web application must be updated to work with a new version of a web browser.
- New data protection legislation (e.g. GDPR) requires changes to how the software handles personal data.
- The hardware platform changes (e.g. from 32-bit to 64-bit processors) and the software must be recompiled or modified.

<div class="exam-tip" markdown="1">
Adaptive maintenance is about **adapting to change** in the environment. The key words are "new operating system", "new hardware", "change in regulations", or "new platform". The software is not broken -- it just needs to work in a changed environment.
</div>

---

## Perfective Maintenance

**Perfective maintenance** involves making changes to **improve** the software or to **add new features** that were not part of the original specification. The software is working correctly, and the environment has not changed -- the goal is to make the software better.

### Characteristics

- It is a **proactive** process, often driven by user feedback or competitive pressure.
- The trigger is a **user request** for new functionality or an internal decision to improve performance.
- Can involve adding new features, improving the user interface, optimising performance, or improving code quality (refactoring).

### Examples

- Users request a "dark mode" option for the interface. The developers add this feature.
- A report that previously took 30 seconds to generate is optimised to run in 2 seconds.
- An "export to PDF" feature is added to a word processing application.
- The user interface is redesigned to be more intuitive based on user feedback.
- A mobile app originally designed for phones is updated to support tablets with an optimised layout.
- Search functionality is enhanced to support filters and sorting options.

<div class="exam-tip" markdown="1">
Perfective maintenance is about making something **better** or **adding new features**. The key words are "improve", "enhance", "new feature", "optimise", or "user requested". The software is not broken and the environment has not changed -- it is simply being improved.
</div>

---

## Comparison of Maintenance Types

| Feature | Corrective | Adaptive | Perfective |
|---------|-----------|----------|------------|
| **Purpose** | Fix bugs and errors | Adapt to environmental changes | Improve or enhance functionality |
| **Trigger** | Bug report / error detected | New OS, hardware, regulations, etc. | User request / business decision |
| **Is the software faulty?** | Yes | No | No |
| **Has the environment changed?** | No | Yes | No |
| **Nature** | Reactive | Reactive or proactive | Proactive |
| **Urgency** | Often high (especially for critical bugs) | Moderate (depends on deadline for change) | Low to moderate |
| **Example** | Fixing a crash when printing | Updating for Windows 12 | Adding an export feature |
| **Another example** | Correcting a wrong calculation | Adapting to new tax rates | Improving report loading speed |

### Decision Flowchart for Identifying Maintenance Type

1. Is the software producing incorrect results or crashing? **Yes** -> **Corrective**
2. Has something outside the software changed (OS, hardware, laws)? **Yes** -> **Adaptive**
3. Is the change to add a feature or improve performance? **Yes** -> **Perfective**

<div class="key-term" markdown="1">
The three types of software maintenance are: **Corrective** (fixing bugs), **Adaptive** (adapting to environmental changes), and **Perfective** (improving or enhancing the software). In exam scenarios, identify the trigger to determine the type.
</div>

---

## Factors Affecting Maintainability

**Maintainability** is a measure of how easy it is to modify, update, or fix a piece of software. Poorly written software is expensive and time-consuming to maintain.

### Factors That Make Software Easier to Maintain

| Factor | How it Helps Maintainability |
|--------|------------------------------|
| **Modular design** | Each module can be understood, tested, and modified independently without affecting other parts of the system |
| **Meaningful variable names** | Makes the code self-documenting -- a maintenance programmer can quickly understand what each variable represents |
| **Use of constants** | Changing a value that appears in many places only requires one edit (e.g. changing `VAT_RATE`) |
| **Comments and documentation** | Internal comments explain the purpose of code sections; external documentation explains the overall system |
| **Consistent coding style** | Consistent indentation, naming conventions, and formatting make the code predictable and easier to read |
| **Low coupling** | Modules are independent -- changing one module does not require changes to many others |
| **High cohesion** | Each module does one thing well, making it easier to understand and modify |
| **Version control** | Tracking changes allows maintainers to understand what was changed, when, and why |
| **Proper testing** | A comprehensive test suite means changes can be verified quickly (regression testing) |
| **Avoiding global variables** | Using local variables and parameters reduces unexpected side effects when code is changed |

### Factors That Make Software Harder to Maintain

- **Monolithic code** -- one large block of code with no modular structure.
- **Poor or no documentation** -- the maintenance programmer has no guide to how the system works.
- **Cryptic variable names** -- names like `x`, `a1`, `temp2` give no clue about their purpose.
- **Hard-coded values** -- "magic numbers" scattered throughout the code are difficult to find and change consistently.
- **Tight coupling** -- modules depend heavily on each other, so changing one module causes a cascade of changes.
- **No version control** -- no history of changes, making it impossible to track or revert modifications.
- **Original developer unavailable** -- if the person who wrote the code has left the organisation, their knowledge is lost.

<div class="exam-tip" markdown="1">
When asked how to make software easier to maintain, always give specific practical examples. Do not just say "use comments" -- say "use comments to explain the purpose of each subroutine and any complex logic, so that a maintenance programmer who did not write the original code can understand it."
</div>

---

## Technical Documentation

**Technical documentation** is written for programmers and IT professionals who need to understand, maintain, or modify the software. It describes the internal workings of the system.

### Contents of Technical Documentation

| Component | Description |
|-----------|-------------|
| **System overview** | A high-level description of what the system does and its architecture |
| **Data flow diagrams** | Show how data moves through the system |
| **Entity-relationship diagrams** | Show the database structure and relationships between tables |
| **Data dictionary** | Lists all data items, their types, sizes, validation rules, and descriptions |
| **Pseudocode / algorithms** | Describes the key algorithms used in the system |
| **Program listings** | The annotated source code |
| **File structures** | Details of file formats, record structures, and field descriptions |
| **Test plans and results** | The test strategy, test data, expected results, and actual results |
| **Installation guide** | How to install and configure the system on new hardware |
| **Known issues** | A list of known bugs or limitations and any workarounds |
| **Change log** | A record of all changes made to the system since its initial release |

### Why Technical Documentation is Important

- Enables **maintenance programmers** (who may not have written the original code) to understand the system.
- Provides a **reference** for debugging -- programmers can look up data structures, algorithms, and expected behaviour.
- Ensures **continuity** -- if the original developer leaves, the documentation preserves their knowledge.
- Supports **adaptive and perfective maintenance** by providing a clear understanding of the current system before changes are made.

<div class="key-term" markdown="1">
**Technical documentation** is aimed at IT professionals and programmers. It describes the internal structure, design, and implementation of the software to support future maintenance and development.
</div>

---

## User Documentation

**User documentation** is written for the end users of the software. It explains how to use the system without requiring any technical knowledge.

### Contents of User Documentation

| Component | Description |
|-----------|-------------|
| **Installation guide** | Step-by-step instructions for installing the software |
| **Getting started / tutorial** | A guided walkthrough for new users to learn the basics |
| **User manual** | Comprehensive reference covering all features and functions |
| **Frequently Asked Questions (FAQ)** | Answers to common questions and problems |
| **Troubleshooting guide** | Solutions to common errors and issues |
| **Glossary** | Definitions of technical terms used in the documentation |
| **System requirements** | The minimum hardware and software needed to run the application |
| **Contact information** | How to reach technical support for further help |

### Forms of User Documentation

- **Printed manuals** -- physical books shipped with the software (less common today).
- **Online help** -- built-in help system accessible from within the application (e.g. pressing F1).
- **Video tutorials** -- recorded demonstrations of how to use features.
- **Interactive guides** -- step-by-step walkthroughs embedded in the software interface.
- **Knowledge bases** -- searchable online databases of help articles.

### Differences Between Technical and User Documentation

| Feature | Technical Documentation | User Documentation |
|---------|------------------------|-------------------|
| **Audience** | Programmers and IT professionals | End users |
| **Purpose** | Support maintenance and development | Help users operate the software |
| **Content** | Code, algorithms, data structures, system design | Instructions, tutorials, screenshots |
| **Language** | Technical, assumes programming knowledge | Non-technical, plain language |
| **Examples include** | Data dictionary, ERD, pseudocode, test plans | User manual, FAQ, tutorial, troubleshooting guide |

<div class="exam-tip" markdown="1">
The exam may give a scenario and ask whether technical or user documentation is more appropriate. Technical documentation is for the IT team maintaining the system. User documentation is for the people using the system day-to-day. Both are important and serve different purposes.
</div>
