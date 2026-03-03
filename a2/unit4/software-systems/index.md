---
layout: topic
title: "Different Types of Software Systems"
level: "A2 Level"
level_url: "/a2/"
unit_name: "Unit 4: Architecture, Data, Communication & Applications"
unit_url: "/a2/unit4/"
subtopics:
  - "Types: Safety related, control, expert, information exchange systems"
  - "Safety related systems: High level of dependability"
  - "Development of safety critical systems as specialised field"
  - "Control systems: Nature and scope of computer control"
  - "Benefits and implications of automation"
  - "Expert systems: Effects on professional groups and wider community"
  - "Internet and Intranet: Use of search engines"
  - "Common contemporary applications"
  - "Effects of internet on professional groups and wider community"
---

## Types of Software Systems

Software systems can be classified by their purpose and the environment in which they operate. At A2 level, you need to understand four main categories.

| Type | Purpose | Examples |
|------|---------|---------|
| **Safety-related systems** | Systems where failure could endanger life or cause significant damage | Aircraft autopilot, medical devices, nuclear reactor control |
| **Control systems** | Systems that manage physical processes using sensors and actuators | Central heating, traffic lights, industrial robots |
| **Expert systems** | Systems that emulate human expert decision-making in a specific domain | Medical diagnosis, financial planning, fault diagnosis |
| **Information exchange systems** | Systems for sharing and accessing information | The Internet, intranets, search engines, email |

---

## Safety-Related Systems

### Safety-Critical vs Safety-Related

| Term | Definition |
|------|-----------|
| **Safety-critical** | Failure could **directly** cause death, serious injury, or major environmental damage. The system **must** work correctly. |
| **Safety-related** | The system contributes to safety but is not the sole means of protection. Failure increases risk but other safeguards may exist. |

**Examples of safety-critical systems:**
- Aircraft flight control systems
- Medical infusion pumps and ventilators
- Railway signalling systems
- Nuclear reactor shutdown systems
- Automotive braking systems (ABS, autonomous emergency braking)

### High Dependability Requirements

Safety-critical systems must meet exceptionally high standards across several properties:

| Property | Description |
|----------|-------------|
| **Reliability** | The system must operate correctly for extended periods without failure. Often measured as Mean Time Between Failures (MTBF). |
| **Availability** | The system must be operational and accessible whenever needed. Expressed as a percentage (e.g. 99.999% uptime = ~5 minutes downtime per year). |
| **Safety** | The system must not cause harm to people or the environment, even in the event of failure. |
| **Security** | The system must resist deliberate attacks and unauthorised access. |
| **Maintainability** | The system must be easy to repair and update without compromising safety. |

### Techniques for Achieving Dependability

| Technique | Description |
|-----------|-------------|
| **Redundancy** | Duplicate critical components so that if one fails, another takes over. Triple modular redundancy (TMR) uses three systems and a voting mechanism. |
| **Fail-safe design** | If the system fails, it defaults to a safe state (e.g. traffic lights go to all-red, not all-green). |
| **Formal methods** | Use mathematical models and proofs to verify that the system meets its specification. Eliminates ambiguity. |
| **Diversity** | Use different hardware, software, or algorithms for redundant components so a single bug cannot affect all copies. |
| **Watchdog timers** | A hardware timer that resets the system if the software stops responding (indicating a crash or hang). |
| **Defensive programming** | Extensive input validation, error handling, and assertions in the code. |

### Development of Safety-Critical Systems

Developing safety-critical systems is a **specialised field** with requirements beyond standard software engineering:

| Aspect | Requirement |
|--------|-------------|
| **Standards** | Must comply with domain-specific standards (e.g. DO-178C for aviation, IEC 61508 for industrial, ISO 26262 for automotive) |
| **Certification** | Independent third-party assessment and certification before deployment |
| **Documentation** | Extensive documentation of requirements, design decisions, test results, and risk assessments |
| **Testing** | Exhaustive testing including formal verification, simulation, and real-world testing. 100% code coverage may be required. |
| **Traceability** | Every requirement must be traceable through design, implementation, and testing |
| **Review** | Multiple levels of peer review, including independent safety assessment |
| **Lifecycle** | Strict adherence to development lifecycle models with defined review gates |

<div class="exam-tip" markdown="1">
When discussing safety-critical systems, always mention **redundancy**, **formal methods**, **fail-safe design**, and the need for **certification** to domain-specific standards. These are the key distinguishing factors from standard software development.
</div>

---

## Control Systems

### Nature and Scope of Computer Control

A **control system** uses computers to manage and regulate physical processes. The basic structure involves:

1. **Sensors** measure the current state of the physical process (temperature, pressure, speed, position)
2. **Processor** compares the measured value against the **desired value** (set point)
3. **Actuators** make physical adjustments based on the processor's output (open valves, adjust motors, switch heaters)

### Open-Loop vs Closed-Loop Control

| Feature | Open-Loop | Closed-Loop |
|---------|-----------|-------------|
| **Feedback** | No feedback — output is not measured | Uses feedback — output is measured and compared to the set point |
| **Accuracy** | Less accurate — cannot correct for disturbances | More accurate — continuously adjusts based on measured error |
| **Complexity** | Simpler and cheaper | More complex |
| **Example** | A toaster with a timer (runs for set time regardless of toast colour) | A thermostat (measures temperature and adjusts heating) |

### Feedback Loop

The **feedback loop** in a closed-loop control system works as follows:

1. The **sensor** reads the current value of the controlled variable
2. The **comparator** calculates the **error** = set point − measured value
3. The **controller** determines the appropriate response based on the error
4. The **actuator** adjusts the physical process
5. The cycle **repeats continuously**

### Types of Control Systems

| Type | Description | Examples |
|------|-------------|---------|
| **Embedded systems** | Computer built into a device to control its operation | Washing machine, microwave, car engine management |
| **SCADA** | Supervisory Control and Data Acquisition — large-scale industrial control with remote monitoring | Power stations, water treatment, oil pipelines |
| **PLCs** | Programmable Logic Controllers — rugged industrial computers for real-time control | Manufacturing lines, conveyor systems, robotic arms |
| **Real-time systems** | Must respond to inputs within guaranteed time limits | ABS braking, pacemakers, air traffic control |

### Benefits and Implications of Automation

**Benefits:**

| Benefit | Description |
|---------|-------------|
| **Consistency** | Automated processes produce identical results every time, reducing defects |
| **Speed** | Computers operate faster than humans for repetitive tasks |
| **24/7 operation** | Automated systems can run continuously without breaks |
| **Dangerous environments** | Robots can work in hazardous conditions (radiation, extreme heat, toxic chemicals) |
| **Precision** | Computer-controlled machines achieve accuracy beyond human capability |
| **Cost reduction** | Lower long-term labour costs once the initial investment is recovered |

**Implications:**

| Implication | Description |
|-------------|-------------|
| **Job displacement** | Automation replaces human workers in manufacturing, logistics, and service industries |
| **Deskilling** | Remaining workers may need fewer skills as machines handle complex tasks |
| **Dependency** | Over-reliance on automated systems creates vulnerability if they fail |
| **Initial cost** | High capital investment for equipment, installation, and programming |
| **Maintenance** | Requires specialised technical staff to maintain and repair automated systems |
| **Ethical concerns** | Questions about accountability when automated systems cause harm |
| **Retraining** | Workers displaced by automation need retraining for new roles |

---

## Expert Systems

### What is an Expert System?

An **expert system** is a computer program that emulates the decision-making ability of a human expert in a specific, narrow domain.

<div class="key-term" markdown="1">
An **expert system** uses a **knowledge base** of facts and rules, combined with an **inference engine**, to draw conclusions and provide advice in a specialised domain. It aims to replicate the reasoning of a human expert.
</div>

### Components of an Expert System

| Component | Function |
|-----------|----------|
| **Knowledge base** | Stores facts about the domain and **IF-THEN rules** that represent expert knowledge. For example: `IF temperature > 38°C AND cough = persistent THEN suggest = pneumonia (confidence 0.7)` |
| **Inference engine** | The reasoning mechanism. Applies rules to known facts to derive new conclusions. Uses **forward chaining** (data-driven: start with facts, apply rules to reach a conclusion) or **backward chaining** (goal-driven: start with a hypothesis, work backwards to find supporting facts). |
| **User interface** | Allows users to input information (answer questions) and receive advice. Should be clear and accessible to non-experts. |
| **Explanation facility** | Explains **how** and **why** the system reached its conclusion. Essential for user trust and for verifying correctness. |
| **Knowledge acquisition facility** | Tools for domain experts to add, modify, and validate rules in the knowledge base. |

### Expert System Shell

An **expert system shell** is a generic framework that provides the inference engine, user interface, and explanation facility without any domain-specific knowledge. A knowledge base is then added to create a complete expert system for a particular domain.

### Knowledge Acquisition

The process of extracting knowledge from human experts is the **knowledge engineering bottleneck**:

- **Interviews** with domain experts
- **Observation** of experts at work
- **Analysis** of case studies and documentation
- The **knowledge engineer** translates expert knowledge into IF-THEN rules
- Challenge: experts often cannot explicitly articulate their reasoning (tacit knowledge)

### Effects on Professional Groups

| Professional Group | Effects |
|-------------------|---------|
| **Doctors** | Expert systems can assist with diagnosis, suggest treatments, and flag drug interactions. May improve accuracy but raises concerns about liability and over-reliance. Does not replace clinical judgement. |
| **Lawyers** | Legal expert systems can search case law, assess case strength, and suggest relevant precedents. Makes legal advice more accessible but cannot handle nuanced interpretation. |
| **Financial advisers** | Can assess risk profiles and recommend investment portfolios. Democratises financial advice but may not account for unusual circumstances. |
| **Engineers** | Fault diagnosis systems help identify problems in complex equipment. Speeds up maintenance but requires accurate knowledge base. |

### Effects on Wider Community

| Effect | Description |
|--------|-------------|
| **Accessibility** | Makes expert-level advice available in areas with few human experts (rural healthcare, developing countries) |
| **Consistency** | Always applies rules the same way — no bad days, bias, or fatigue |
| **Cost reduction** | Cheaper than consulting a human expert for routine decisions |
| **Limitations** | Cannot handle situations outside its knowledge base, lacks common sense, cannot learn from experience (traditional systems) |
| **Trust** | People may over-trust or under-trust automated advice |

<div class="exam-tip" markdown="1">
When comparing expert systems to human experts, discuss both advantages (consistency, availability, speed, no fatigue) and disadvantages (limited domain, no common sense, difficulty acquiring knowledge, cannot handle novel situations). Always mention the **explanation facility** — it distinguishes expert systems from black-box AI.
</div>

---

## Internet and Intranet

### Internet vs Intranet

| Feature | Internet | Intranet |
|---------|----------|----------|
| **Access** | Public — anyone can connect | Private — restricted to an organisation's members |
| **Scope** | Global | Local (within one organisation) |
| **Security** | Varies widely | Protected by firewalls and access controls |
| **Content** | General public information | Organisation-specific resources (policies, internal tools, documents) |
| **Protocols** | TCP/IP, HTTP/HTTPS | Same protocols but within a private network |

### How Search Engines Work

Search engines use three main processes to index and retrieve web content:

**1. Web Crawling (Spidering)**
- Automated programs called **web crawlers** (or spiders/bots) systematically browse the web
- They follow **hyperlinks** from page to page, discovering new and updated content
- Crawlers respect `robots.txt` files that tell them which pages not to crawl
- They periodically **re-crawl** pages to detect changes

**2. Indexing**
- The crawler sends discovered pages to the **indexer**
- The indexer analyses the content: words, their positions, headings, links, images, metadata
- An **inverted index** is built — mapping each word to the list of pages containing it
- This allows fast lookup: given a search term, instantly find all pages containing it

**3. Ranking**
- When a user searches, the engine retrieves matching pages from the index
- Pages are ranked by **relevance** using algorithms that consider hundreds of factors

**Key ranking factors:**

| Factor | Description |
|--------|-------------|
| **PageRank** | Measures page importance based on the number and quality of links pointing to it. A page linked to by many high-quality pages ranks higher. |
| **Content relevance** | How well the page content matches the search query (keyword frequency, placement in headings) |
| **Freshness** | Recently updated content may rank higher for time-sensitive queries |
| **User signals** | Click-through rates, time spent on page, bounce rate |
| **Mobile-friendliness** | Pages optimised for mobile devices rank higher in mobile searches |
| **Page speed** | Faster-loading pages are preferred |
| **HTTPS** | Secure pages may receive a small ranking boost |

---

## Common Contemporary Applications

| Application | Description | Key Technologies |
|------------|-------------|-----------------|
| **E-commerce** | Online buying and selling of goods and services | HTTPS, payment gateways, databases, recommendation engines |
| **Social media** | Platforms for user-generated content and social interaction | Real-time messaging, content delivery networks, AI moderation |
| **Cloud computing** | On-demand access to computing resources over the Internet | Virtualisation, distributed storage, APIs, pay-as-you-go pricing |
| **Internet of Things (IoT)** | Network of physical devices with embedded sensors and connectivity | Wireless protocols, edge computing, sensor networks |
| **Streaming services** | Real-time delivery of audio/video content | Adaptive bitrate streaming, CDNs, compression codecs |
| **Online banking** | Financial services delivered via the Internet | Encryption, two-factor authentication, secure APIs |
| **Telehealth** | Remote medical consultations and monitoring | Video conferencing, wearable sensors, electronic health records |
| **Remote working** | Working from any location using Internet-connected tools | VPNs, collaboration platforms, cloud storage |

---

## Effects on Professional Groups and the Wider Community

### Effects on Professional Groups

| Group | Positive Effects | Negative Effects |
|-------|-----------------|-----------------|
| **Healthcare** | Telemedicine reaches remote patients, AI assists diagnosis, electronic records improve coordination | Data security concerns, digital literacy requirements, risk of misdiagnosis via remote consultation |
| **Education** | Online learning widens access, digital resources enhance teaching, personalised learning | Digital divide excludes some students, screen fatigue, reduced social interaction |
| **Legal** | Online legal databases speed up research, video conferencing enables remote hearings | Cybercrime creates new legal challenges, jurisdiction issues across borders |
| **Journalism** | Instant news distribution, citizen journalism, data journalism | Fake news, declining revenue from print, information overload |
| **Retail** | E-commerce opens global markets, data analytics improves targeting | High street decline, returns and fraud costs, competitive pressure |

### Effects on Wider Community

| Area | Effects |
|------|--------|
| **Communication** | Instant global communication via email, messaging, and video calls. But risk of isolation from excessive screen time. |
| **Information access** | Vast information freely available. But reliability varies — misinformation spreads easily. |
| **Employment** | New job types created (content creators, app developers). But traditional roles disrupted (retail workers, bank tellers). |
| **Privacy** | Online activity generates vast data trails. Companies and governments can track behaviour. Data protection laws attempt to balance this. |
| **Democracy** | Social media enables political engagement and activism. But also enables manipulation through targeted advertising and echo chambers. |
| **Culture** | Global sharing of cultural content. But risk of cultural homogenisation and dominance of English-language content. |
| **Health** | Health information and fitness tracking empower individuals. But screen addiction, cyberbullying, and mental health impacts are growing concerns. |

<div class="exam-tip" markdown="1">
Questions about the effects of the Internet on society require **balanced** answers. For each positive effect, acknowledge a corresponding concern or drawback. Always consider **multiple stakeholders** — what benefits one group may disadvantage another. Use specific examples to support your points rather than making general statements.
</div>
