---
layout: topic
title: "Systems Analysis"
level: "A2 Level"
level_url: "/a2/"
unit_name: "Unit 3: Programming & System Development"
unit_url: "/a2/unit3/"
subtopics:
  - "Approaches to analysis and design: Waterfall and Agile"
  - "Documentation at each stage of development"
---

## The Waterfall Model

<div class="key-term" markdown="1">
The **Waterfall model** is a sequential, linear approach to software development where each stage must be completed before the next begins. Progress flows in one direction -- like a waterfall -- through a fixed sequence of stages.
</div>

### Stages of the Waterfall Model

The Waterfall model consists of five main stages, each producing defined outputs before work proceeds to the next.

#### 1. Requirements Analysis

The development team works with the client and stakeholders to gather, document, and agree on a complete set of requirements. The output is a **requirements specification** that describes everything the system must do.

**Activities include:**
- Interviewing stakeholders and end users
- Analysing existing systems and processes
- Documenting functional requirements (what the system must do) and non-functional requirements (performance, security, usability constraints)
- Agreeing acceptance criteria with the client
- Producing a formal requirements specification document

#### 2. System Design

The requirements are translated into a detailed technical design. This covers the overall architecture, data structures, user interfaces, and algorithms.

**Activities include:**
- Creating system architecture diagrams
- Designing database schemas (entity-relationship diagrams, normalisation)
- Designing user interfaces (wireframes, screen layouts)
- Specifying algorithms and data structures
- Producing a detailed design document

#### 3. Implementation (Coding)

The system is built according to the design specification. Programmers write, test, and integrate code modules.

**Activities include:**
- Writing source code in the chosen programming language(s)
- Unit testing individual modules
- Integrating modules together
- Following coding standards and conventions
- Code reviews

#### 4. Testing

The completed system is formally tested against the requirements specification to ensure it works correctly and meets all agreed criteria.

**Activities include:**
- System testing (testing the complete integrated system)
- Acceptance testing (the client verifies the system meets their requirements)
- Performance testing and stress testing
- Documenting test results and any defects found
- Regression testing after defect fixes

#### 5. Maintenance

After deployment, the system enters the maintenance phase where bugs are fixed, improvements are made, and the system is adapted to changing requirements.

**Types of maintenance:**

| Type | Description | Example |
|---|---|---|
| **Corrective** | Fixing bugs discovered after deployment | Patching a calculation error |
| **Adaptive** | Modifying the system for changes in the environment | Updating for a new operating system |
| **Perfective** | Improving performance or adding minor enhancements | Optimising a slow database query |
| **Preventive** | Making changes to prevent future problems | Refactoring code to reduce technical debt |

### Advantages of the Waterfall Model

- **Simple and easy to understand** -- the linear structure is straightforward for teams to follow
- **Well-documented** -- each stage produces thorough documentation before the next begins
- **Clear milestones** -- progress is easy to measure against defined stages
- **Suitable for stable requirements** -- works well when requirements are unlikely to change
- **Easier project management** -- fixed stages make budgeting and scheduling more predictable
- **Appropriate for regulated industries** -- the thorough documentation satisfies audit requirements (e.g. medical, defence)

### Disadvantages of the Waterfall Model

- **Inflexible** -- it is very difficult and expensive to go back to a previous stage once it is complete
- **Late delivery of working software** -- the client does not see a working system until very late in the process
- **Assumes requirements are complete at the start** -- in practice, requirements often change or are poorly understood initially
- **High risk** -- problems may not be discovered until the testing stage, when they are expensive to fix
- **No user feedback during development** -- the client is largely excluded after the requirements stage until acceptance testing
- **Poor fit for complex, evolving projects** -- not suitable when the end product is not well-defined from the outset

### When to Use the Waterfall Model

- Requirements are **well-understood, stable, and unlikely to change**
- The project is **relatively small and simple**
- The technology is **well-established** and the team has experience with it
- **Strict documentation** is required (e.g. regulatory or contractual obligations)
- The client is **not available** for regular feedback sessions
- The project has a **fixed budget and timeline** with clearly defined deliverables

---

## Agile Methodology

<div class="key-term" markdown="1">
**Agile** is an iterative and incremental approach to software development that delivers working software in short cycles called **sprints** (typically 1--4 weeks). It embraces change, values collaboration, and prioritises working software over comprehensive documentation.
</div>

### Agile Principles

The Agile Manifesto (2001) established four core values:

1. **Individuals and interactions** over processes and tools
2. **Working software** over comprehensive documentation
3. **Customer collaboration** over contract negotiation
4. **Responding to change** over following a plan

### Key Agile Practices

#### Sprints

A **sprint** is a fixed-length iteration (usually 1--4 weeks) during which the team designs, builds, tests, and delivers a working increment of the software. At the end of each sprint, the client can review the product and provide feedback.

#### User Stories

<div class="key-term" markdown="1">
A **user story** is a short, informal description of a feature written from the perspective of an end user. It follows the format: "As a [type of user], I want [some feature] so that [some benefit]."
</div>

**Examples:**
- "As a **customer**, I want to **search for products by category** so that I can **find what I need quickly**."
- "As an **administrator**, I want to **generate monthly sales reports** so that I can **track business performance**."

User stories are prioritised in a **product backlog** and selected for each sprint.

#### Stand-up Meetings

A **daily stand-up** (or daily scrum) is a short meeting (typically 15 minutes) where each team member answers three questions:

1. What did I accomplish yesterday?
2. What will I work on today?
3. Are there any blockers or impediments?

#### Iterative Development

Each sprint builds on the previous one, progressively adding functionality. The system grows incrementally, with each iteration producing a working, tested product that can be demonstrated to the client.

#### Sprint Review and Retrospective

At the end of each sprint:
- The **sprint review** demonstrates the completed work to the client and gathers feedback
- The **sprint retrospective** is an internal team meeting to reflect on what went well, what did not, and how to improve the process

### Advantages of Agile

- **Flexible and adaptive** -- changes in requirements can be accommodated at any sprint boundary
- **Early and continuous delivery** -- the client sees working software from the first sprint
- **Regular feedback** -- client involvement throughout ensures the product meets their actual needs
- **Reduced risk** -- problems are identified and resolved quickly in short iterations
- **Higher client satisfaction** -- the client feels involved and can steer the direction of the product
- **Improved team morale** -- self-organising teams with regular communication and collaboration

### Disadvantages of Agile

- **Difficult to predict cost and timeline** -- the scope may change frequently, making budgeting harder
- **Requires active client involvement** -- if the client cannot attend reviews and provide feedback, the process suffers
- **Less comprehensive documentation** -- the focus on working software can mean documentation is less thorough
- **Can lead to scope creep** -- without a fixed specification, the project may grow beyond the original intent
- **Not ideal for very large teams** -- coordination becomes difficult with many developers
- **Difficult for fixed-price contracts** -- the evolving scope does not fit well with traditional procurement
- **Relies on skilled, experienced team members** -- self-organising teams need experienced developers

### When to Use Agile

- Requirements are **uncertain, incomplete, or likely to change**
- The client is **available and willing** to participate regularly
- The project benefits from **early delivery** of working software
- The team is **small, experienced, and co-located** (or well-connected remotely)
- The project is **complex and innovative** where the solution is not fully understood at the outset
- **Rapid response** to market changes or user feedback is important

---

## Comparison: Waterfall vs Agile

| Feature | Waterfall | Agile |
|---|---|---|
| **Approach** | Sequential, linear | Iterative, incremental |
| **Requirements** | Fixed at the start | Evolving throughout |
| **Client involvement** | Mainly at start and end | Continuous throughout |
| **Flexibility** | Rigid; changes are costly | Embraces change |
| **Delivery** | Single delivery at the end | Regular working increments |
| **Documentation** | Comprehensive at each stage | Lighter; focuses on working software |
| **Testing** | After implementation | Continuous; each sprint includes testing |
| **Risk** | High; problems found late | Lower; problems found early |
| **Project size** | Better for small, well-defined projects | Better for complex, evolving projects |
| **Budget/timeline** | Easier to estimate upfront | Harder to predict overall cost |
| **Team structure** | Hierarchical, managed | Self-organising, collaborative |
| **Best suited for** | Stable requirements, regulated industries | Innovative products, startups, evolving needs |

<div class="exam-tip" markdown="1">
In exam questions that present a scenario and ask which methodology is more appropriate, look for clues: if requirements are "well-defined" and "unlikely to change," lean towards Waterfall. If the client wants "regular feedback" or requirements are "not yet fully understood," lean towards Agile. Always justify your answer with specific features of the methodology.
</div>

---

## Documentation at Each Stage

Regardless of the development methodology used, documentation plays a vital role in ensuring a system is built correctly, can be maintained, and is usable. The type and depth of documentation varies between Waterfall (more formal and comprehensive) and Agile (lighter, but still necessary).

### Requirements Specification

The requirements specification is produced during the analysis phase and records **what the system must do**.

**Contents typically include:**

- **Functional requirements** -- specific features and capabilities (e.g. "The system shall allow users to search products by keyword")
- **Non-functional requirements** -- quality attributes (e.g. performance targets, security requirements, usability standards)
- **Constraints** -- limitations on the solution (e.g. must run on Windows, budget limit, deadline)
- **Acceptance criteria** -- measurable conditions that must be met for the client to accept the system
- **Use case diagrams** -- visual representation of how different users interact with the system
- **Data requirements** -- what data the system must store and process

### Design Documents

Design documents translate the requirements into a technical blueprint for the system.

**Contents typically include:**

- **System architecture diagrams** -- showing the overall structure, components, and how they interact
- **Database design** -- entity-relationship diagrams, table structures, normalisation to third normal form
- **User interface designs** -- wireframes, mockups, navigation flow diagrams
- **Algorithm specifications** -- pseudocode or flowcharts for key processes
- **Class diagrams** (for OOP) -- showing classes, attributes, methods, and relationships
- **Data flow diagrams** -- showing how data moves through the system
- **Input/output specifications** -- formats, validation rules, expected outputs

### Test Plans

Test plans define **how the system will be tested** to verify it meets the requirements.

**Contents typically include:**

| Component | Description |
|---|---|
| **Test strategy** | Overall approach to testing (unit, integration, system, acceptance) |
| **Test cases** | Specific inputs, expected outputs, and pass/fail criteria |
| **Test data** | Normal, boundary, and erroneous data to be used |
| **Test schedule** | When each type of testing will take place |
| **Responsibilities** | Who is responsible for each area of testing |
| **Environment** | Hardware, software, and configuration needed for testing |
| **Defect tracking** | How bugs will be recorded, prioritised, and resolved |

### User Manuals

User documentation helps end users operate the system effectively.

**Contents typically include:**

- **Installation guide** -- how to set up the system
- **Getting started tutorial** -- a walkthrough for new users
- **Feature reference** -- detailed description of each function
- **Screenshots and annotated diagrams** -- visual guidance
- **FAQ and troubleshooting** -- common problems and solutions
- **Glossary** -- definitions of technical terms

### Technical Documentation

Technical documentation is aimed at developers and system administrators who will maintain and extend the system.

**Contents typically include:**

- **Source code comments** -- inline explanations within the code
- **API documentation** -- specifications for programmatic interfaces
- **Database documentation** -- schema descriptions, stored procedures, data dictionary
- **Deployment guide** -- how to build, configure, and deploy the system
- **Change log** -- record of all modifications made to the system
- **System administration guide** -- backup procedures, monitoring, security configuration

<div class="exam-tip" markdown="1">
Exam questions may ask you to identify **which documents are produced at which stage**. Remember: requirements specification comes from analysis, design documents from design, test plans are prepared during design but executed during testing, and user manuals and technical documentation are finalised during or after implementation. In Agile, these documents are produced and updated incrementally throughout the sprints.
</div>
