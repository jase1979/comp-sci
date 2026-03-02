---
layout: topic
title: "Systems Analysis"
level: "AS"
level_url: "/as/"
unit_name: "Unit 1: Fundamentals of Computer Science"
unit_url: "/as/unit1/"
prev_topic: "/as/unit1/principles-programming/"
next_topic: "/as/unit1/software-design/"
---

## The Systems Development Life Cycle (SDLC)

<div class="key-term" markdown="1">
The **Systems Development Life Cycle (SDLC)** is a structured framework that defines the stages involved in developing an information system, from initial investigation through to maintenance. It provides a systematic approach to planning, creating, testing, and deploying software.
</div>

### Stages of the SDLC

The SDLC is typically described as having six main stages. Different sources may group or name them slightly differently, but the core activities remain the same.

### 1. Feasibility Study and Analysis

This is the investigation phase. The purpose is to understand the current system, identify its problems, and determine the requirements for the new system.

Activities include:
- **Investigating the current system** -- understanding how it works, who uses it, what data it processes, and what its shortcomings are.
- **Gathering requirements** -- determining what the new system must do (functional requirements) and how well it must perform (non-functional requirements such as speed, security, usability).
- **Conducting a feasibility study** -- assessing whether the project is viable (see the detailed section below).
- **Producing a requirements specification** -- a formal document that precisely describes what the system must do.
- **Fact-finding** -- using techniques such as interviews, questionnaires, observation, and document analysis to gather information.

### 2. Design

The design phase translates the requirements into a detailed plan for the new system. Designers create specifications for:

- **Data structures and database design** -- what data will be stored and how it will be organised (e.g., entity-relationship diagrams, table structures).
- **User interface (UI) design** -- screen layouts, menus, navigation, forms, and reports.
- **System architecture** -- hardware requirements, network configuration, and how components interact.
- **Algorithm design** -- the logic for processing data (using pseudocode or flowcharts).
- **Security design** -- authentication, access levels, encryption, and backup procedures.
- **Testing plan** -- what tests will be carried out and what results are expected.

### 3. Implementation (Development)

The system is built according to the design specifications:

- Programmers write the code using an appropriate programming language.
- Databases are created and populated.
- The user interface is built.
- Individual modules are developed and then integrated.
- Code is documented with comments and technical documentation.

### 4. Testing

The system is tested to ensure it works correctly and meets the requirements:

- **Unit testing** -- individual modules or functions are tested in isolation.
- **Integration testing** -- modules are combined and tested together to check they work as a system.
- **System testing** -- the entire system is tested end-to-end against the requirements specification.
- **User acceptance testing (UAT)** -- end users test the system to confirm it meets their needs and is fit for purpose.
- **Test data** includes **normal data** (typical valid inputs), **boundary data** (values at the edge of valid ranges), and **erroneous data** (invalid inputs that should be rejected).

### 5. Installation (Deployment)

The new system is deployed and replaces the old system. This involves:

- Choosing and executing an appropriate changeover method (direct, parallel, phased, or pilot).
- Migrating data from the old system to the new system.
- Training users on the new system.
- Providing user documentation (user guides, help files).

### 6. Maintenance

After deployment, the system must be maintained to keep it operational and up to date:

- **Corrective maintenance** -- fixing bugs and errors discovered after deployment.
- **Adaptive maintenance** -- modifying the system to work with changes in its environment (e.g., new operating systems, new hardware, new legislation).
- **Perfective maintenance** -- improving the system by adding new features or enhancing performance based on user feedback.

<div class="exam-tip" markdown="1">
The SDLC is a cycle, not a one-off process. After maintenance, the system may eventually need to be replaced, starting the cycle again. Be prepared to describe each stage and explain what happens during it.
</div>

---

## Software Development Methodologies

The SDLC stages can be organised in different ways depending on the chosen development methodology. Each methodology has different strengths and suits different types of project.

### Waterfall Model

The **waterfall model** is the most traditional approach. Each stage is completed fully before the next stage begins, and there is no going back to a previous stage.

**Stages flow downward like a waterfall:**

1. Requirements/Analysis
2. Design
3. Implementation
4. Testing
5. Deployment
6. Maintenance

| Advantages | Disadvantages |
|---|---|
| Simple and easy to understand | No going back -- errors found late are expensive to fix |
| Well-documented at each stage | The client does not see the product until late in the process |
| Clear milestones and deliverables | Requirements must be fully known at the start |
| Good for small, well-defined projects | Not suitable for projects where requirements may change |
| Easy to manage due to rigid structure | Testing only happens after implementation |

**Best suited for:** Projects with clear, fixed requirements that are unlikely to change, such as safety-critical systems or government contracts.

### Agile / Iterative Development

<div class="key-term" markdown="1">
**Agile development** is an iterative approach where the system is developed in short cycles called **iterations** (or **sprints**, typically 2-4 weeks). Each iteration produces a working increment of the software that can be reviewed and tested by the client.
</div>

Key principles:
- Working software is delivered frequently and incrementally.
- Requirements can change and evolve throughout the project.
- Close collaboration between developers and clients.
- Regular feedback and adaptation.
- Small, self-organising teams.

| Advantages | Disadvantages |
|---|---|
| Flexible -- adapts to changing requirements | Can be difficult to estimate total time and cost |
| Client sees working software early and often | Requires continuous client involvement |
| Bugs are found and fixed early | Less documentation may cause issues later |
| Higher client satisfaction due to involvement | Scope can expand uncontrollably ("scope creep") |
| Reduced risk -- problems are caught each iteration | Not ideal for very large, complex systems |

**Best suited for:** Projects where requirements are uncertain or likely to change, such as web applications, mobile apps, and startup products.

### Spiral Model

The **spiral model** combines elements of both waterfall and iterative approaches, with a strong emphasis on **risk analysis**. Development proceeds in spirals (cycles), and each spiral has four phases:

1. **Planning** -- determine objectives, alternatives, and constraints.
2. **Risk analysis** -- identify and evaluate risks; build prototypes to address uncertainties.
3. **Development and testing** -- build and test the product increment.
4. **Evaluation** -- review the results with the client and plan the next spiral.

| Advantages | Disadvantages |
|---|---|
| Explicit risk management at every cycle | Complex and expensive to manage |
| Flexible to changing requirements | Requires expertise in risk assessment |
| Suitable for large, high-risk projects | Not suitable for small, low-risk projects |
| Prototyping reduces uncertainty | Can be slow due to repeated risk analysis |

**Best suited for:** Large, complex, high-risk projects where requirements are unclear, such as military systems or large enterprise software.

### RAD (Rapid Application Development)

<div class="key-term" markdown="1">
**RAD** is a methodology that prioritises rapid prototyping and quick feedback over lengthy planning and documentation. The goal is to produce a working system as quickly as possible.
</div>

Key features:
- Heavy use of **prototyping** -- quick, rough versions of the system are built and shown to the client.
- Client feedback drives each iteration of the prototype.
- Minimal planning and documentation compared to waterfall.
- Uses tools such as GUI builders and code generators to speed development.
- The final system evolves from the prototype.

| Advantages | Disadvantages |
|---|---|
| Very fast development | Final product may be lower quality due to speed |
| Client is heavily involved and gives continuous feedback | Requires skilled and experienced developers |
| Reduced risk of building the wrong system | Not suitable for large or complex systems |
| Prototypes help clarify requirements | Poor documentation may cause maintenance difficulties |
| Flexible and adaptable | Relies heavily on client availability |

**Best suited for:** Small to medium projects with tight deadlines where requirements are not fully defined, such as business applications and user interface design.

### V-Model (Verification and Validation Model)

The **V-model** is an extension of the waterfall model that emphasises **testing** at each stage. Each development stage on the left side of the "V" has a corresponding testing stage on the right side.

```
Requirements Analysis  <----------->  User Acceptance Testing
    System Design      <----------->  System Testing
      Module Design    <----------->  Integration Testing
        Coding         <----------->  Unit Testing
```

The left side represents development (verification -- "are we building the product right?"), and the right side represents testing (validation -- "are we building the right product?").

| Advantages | Disadvantages |
|---|---|
| Testing is planned from the very start | Rigid -- no going back once a stage is complete |
| Clear relationship between development and testing stages | Requirements must be fully known upfront |
| Defects are found early due to early test planning | Not flexible for changing requirements |
| Higher quality and reliability | Expensive for small projects |
| Well-suited for safety-critical systems | No prototypes are produced |

**Best suited for:** Projects where quality and reliability are critical and requirements are well understood, such as medical devices, avionics, and financial systems.

### Prototyping

<div class="key-term" markdown="1">
**Prototyping** involves building a preliminary version (a **prototype**) of the system to explore requirements, test ideas, and gather user feedback before building the final product.
</div>

Types of prototyping:
- **Throwaway (disposable) prototyping** -- the prototype is built quickly to explore an idea, shown to the client, and then discarded. The final system is built from scratch using the lessons learned.
- **Evolutionary prototyping** -- the prototype is continuously refined based on feedback until it becomes the final system.

| Advantages | Disadvantages |
|---|---|
| Helps clarify vague or uncertain requirements | Can raise unrealistic client expectations |
| Users can see and interact with a working model early | Time spent on prototypes may be wasted (throwaway) |
| Reduces risk of building the wrong system | May lead to poorly structured final code (evolutionary) |
| Encourages user involvement | Can be difficult to know when to stop refining |

### Methodology Comparison Summary

| Methodology | Flexibility | Risk Management | Client Involvement | Best For |
|---|---|---|---|---|
| **Waterfall** | Low | Low | Low (only at start/end) | Fixed, well-defined requirements |
| **Agile** | High | Medium | High (continuous) | Evolving requirements |
| **Spiral** | High | High (explicit) | Medium | Large, high-risk projects |
| **RAD** | High | Low | High (continuous) | Fast delivery, small projects |
| **V-Model** | Low | Medium (via testing) | Low | Safety-critical, quality-focused |
| **Prototyping** | High | Medium | High | Unclear requirements |

<div class="exam-tip" markdown="1">
A common exam question gives you a scenario and asks you to recommend and justify a development methodology. Consider: How well are the requirements defined? Is the project large or small? Is it safety-critical? How involved can the client be? How much risk is involved? Match the methodology to the scenario's characteristics.
</div>

---

## Fact-Finding Techniques

During the analysis stage, the systems analyst must gather information about the current system and the requirements for the new system. There are several techniques for doing this.

### Interviews

Face-to-face (or virtual) conversations with stakeholders, users, and managers.

- **Structured interviews** have a pre-set list of questions asked in a fixed order.
- **Unstructured interviews** are more like conversations, allowing the interviewer to follow up on interesting points.
- **Semi-structured interviews** combine both approaches.

| Advantages | Disadvantages |
|---|---|
| Can ask follow-up questions and probe deeper | Time-consuming to conduct and analyse |
| Body language and tone provide additional information | Interviewee may be biased or tell you what they think you want to hear |
| Can clarify misunderstandings immediately | Difficult to interview large numbers of people |
| Builds rapport with stakeholders | Responses may be subjective |

### Questionnaires

Written sets of questions distributed to a large number of people.

- Can include **closed questions** (yes/no, multiple choice, rating scales) for quantitative data.
- Can include **open questions** (free text) for qualitative data.
- Can be distributed on paper or electronically.

| Advantages | Disadvantages |
|---|---|
| Can reach a large number of people quickly | No opportunity to ask follow-up questions |
| Inexpensive to distribute and collect | Questions may be misunderstood |
| Responses can be analysed statistically | Low response rates are common |
| Respondents can remain anonymous (encouraging honesty) | Cannot observe body language or tone |
| Consistent -- everyone gets the same questions | Poorly designed questions lead to unreliable data |

### Observation

Watching users as they perform their tasks in the current system.

| Advantages | Disadvantages |
|---|---|
| See exactly how the current system is used in practice | Time-consuming |
| Can identify inefficiencies and workarounds that users may not mention | Users may behave differently when being observed (Hawthorne effect) |
| Provides first-hand, objective data | Observer may misinterpret what they see |
| No reliance on users accurately describing their own work | Can only observe what is happening now, not what should happen |

### Document Analysis

Examining existing documents such as forms, reports, manuals, procedure guides, and data files from the current system.

| Advantages | Disadvantages |
|---|---|
| Provides concrete, factual information about the current system | Documents may be out of date or incomplete |
| Can be done without disrupting users | Does not capture informal processes or workarounds |
| Reveals the structure of data currently used | Large volumes of documents can be overwhelming |
| No scheduling needed -- documents are available anytime | Cannot ask the document follow-up questions |

<div class="exam-tip" markdown="1">
Exam questions often ask you to recommend a fact-finding technique for a given scenario and justify your choice. Consider the number of people involved, the type of information needed, the time available, and whether you need qualitative or quantitative data.
</div>

---

## Feasibility Study

<div class="key-term" markdown="1">
A **feasibility study** is an investigation carried out early in the SDLC to determine whether a proposed project is viable and worth pursuing. It examines the project from multiple perspectives before significant resources are committed.
</div>

The feasibility study typically examines five areas, sometimes remembered by the acronym **TELOS**:

### Technical Feasibility

Can the system be built with current technology and expertise?

- Is the required hardware and software available?
- Does the organisation have (or can it acquire) the necessary technical skills?
- Is the proposed technology proven and reliable?
- Can the system integrate with existing systems?

### Economic Feasibility (Cost-Benefit Analysis)

Is the system financially worthwhile?

- What are the development costs (hardware, software, staff, training)?
- What are the ongoing running costs (maintenance, hosting, support)?
- What are the expected benefits (cost savings, increased revenue, improved efficiency)?
- Do the benefits outweigh the costs over the system's expected lifetime?
- What is the payback period (how long before the investment is recovered)?

### Legal Feasibility

Will the system comply with all relevant laws and regulations?

- Does it comply with the **Data Protection Act / UK GDPR** (if handling personal data)?
- Does it comply with the **Computer Misuse Act** (security requirements)?
- Are there any **copyright or licensing** issues with the software or data used?
- Does it meet any industry-specific regulations (e.g., health and safety, financial regulations)?
- Are there contractual obligations that affect the project?

### Operational Feasibility

Will the system work in practice within the organisation?

- Will the users accept and adopt the new system?
- Is the system compatible with existing business processes?
- Will sufficient training be provided?
- Is the organisation prepared for the changes the system will bring?
- Will the system actually solve the identified problems?

### Schedule (Time) Feasibility

Can the system be developed within the required timeframe?

- Is the deadline realistic given the scope of the project?
- Are there enough skilled staff available to meet the schedule?
- Are there any external dependencies that could cause delays?
- What is the impact of missing the deadline?

<div class="exam-tip" markdown="1">
Remember **TELOS**: Technical, Economic, Legal, Operational, Schedule. In the exam, you may be asked to discuss the feasibility of a proposed system. Make sure you address multiple aspects of feasibility and relate them specifically to the scenario given.
</div>

---

## Requirements Specification

<div class="key-term" markdown="1">
A **requirements specification** (also called a software requirements specification or SRS) is a formal document that describes exactly what the new system must do. It forms a contract between the client and the developers, and all subsequent design, development, and testing are based on it.
</div>

### Types of Requirements

**Functional requirements** describe **what** the system must do:
- The system must allow users to log in with a username and password.
- The system must generate a monthly sales report.
- The system must calculate VAT at the current rate.
- The system must send email notifications when an order is dispatched.

**Non-functional requirements** describe **how well** the system must perform:
- **Performance** -- the system must respond to user queries within 2 seconds.
- **Security** -- all passwords must be stored using encryption.
- **Usability** -- the system must be usable by non-technical staff with minimal training.
- **Reliability** -- the system must have 99.9% uptime.
- **Scalability** -- the system must handle up to 10,000 concurrent users.
- **Compatibility** -- the system must work on Windows 10 and above.

### Importance of the Requirements Specification

- Provides a **clear and agreed understanding** between client and developer.
- Acts as a **benchmark for testing** -- testers can verify each requirement is met.
- Helps with **project planning** -- developers can estimate time and cost based on the requirements.
- Reduces the risk of **scope creep** -- changes must be formally agreed.
- Forms a **legal basis** -- in case of disputes about what was agreed.

---

## Installation / Changeover Methods

When a new system is ready to replace an old one, the transition must be managed carefully. The choice of changeover method depends on the risk involved, the budget, the size of the organisation, and how critical the system is.

### Direct Changeover

The old system is switched off and the new system is switched on immediately. There is no overlap.

| Advantages | Disadvantages |
|---|---|
| Quickest and cheapest method | Highest risk -- if the new system fails, there is no fallback |
| Benefits of the new system are available immediately | No way to compare outputs between old and new systems |
| No duplication of effort | Data could be lost if migration fails |
| Clean break -- no confusion about which system to use | Users must adapt immediately with no transition period |

**Best suited for:** Non-critical systems, or when the old system has completely failed and there is no alternative.

### Parallel Running

Both the old and new systems run simultaneously for a period of time. Outputs from both systems are compared to ensure the new system is working correctly.

| Advantages | Disadvantages |
|---|---|
| Lowest risk -- the old system is available as a fallback | Most expensive method (double the resources, staff, and effort) |
| Outputs can be compared to verify accuracy | Very demanding on staff who must operate both systems |
| Users can gradually build confidence in the new system | Confusing -- staff may not know which system to trust |
| Data integrity can be verified | Takes longer to complete the changeover |

**Best suited for:** Critical systems where failure would be catastrophic, such as payroll, banking, or air traffic control.

### Phased Implementation

The new system is introduced in stages or modules. One part of the system is replaced at a time, while the rest continues to use the old system.

| Advantages | Disadvantages |
|---|---|
| Lower risk than direct -- only one module is at risk at a time | Takes a long time to fully implement |
| Problems in one module do not affect the whole system | Old and new modules must be compatible and interface correctly |
| Users can learn the new system gradually | Complex to manage the transition between modules |
| Lessons learned from early modules can improve later ones | Some functionality may be temporarily limited |

**Best suited for:** Large systems that can be logically divided into independent modules, such as a company-wide ERP system.

### Pilot Running

The complete new system is implemented in one location, department, or branch of the organisation. If it works well, it is rolled out to the rest of the organisation.

| Advantages | Disadvantages |
|---|---|
| The new system is tested in a real environment on a small scale | The pilot group may not be representative of the whole organisation |
| If it fails, only a small part of the organisation is affected | The pilot group may have different needs or capabilities |
| Feedback from the pilot group can improve the system before wider rollout | Users not in the pilot group must wait for the new system |
| Reduces overall risk compared to a direct changeover across the whole organisation | Requires careful selection of the pilot group |

**Best suited for:** Organisations with multiple branches or departments, such as a retail chain testing a new point-of-sale system in one store before rolling it out nationwide.

### Changeover Methods Comparison Summary

| Method | Risk Level | Cost | Speed | Best For |
|---|---|---|---|---|
| **Direct** | High | Low | Fast | Non-critical systems |
| **Parallel** | Low | High | Slow | Critical, high-risk systems |
| **Phased** | Medium | Medium | Slow | Large, modular systems |
| **Pilot** | Medium-Low | Medium | Medium | Multi-site organisations |

<div class="exam-tip" markdown="1">
For the exam, be prepared to recommend a changeover method for a given scenario and **justify** your choice. Always consider: How critical is the system? What is the budget? How large is the organisation? What would happen if the new system failed? For example, a hospital patient records system would likely require parallel running due to the critical nature of the data, whereas a small business replacing a simple invoicing system might use direct changeover.
</div>
