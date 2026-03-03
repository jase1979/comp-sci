---
layout: topic
title: "System Design"
level: "A2 Level"
level_url: "/a2/"
unit_name: "Unit 3: Programming & System Development"
unit_url: "/a2/unit3/"
subtopics:
  - "Human-computer interaction: Contemporary approaches"
  - "Potential for natural language interface"
  - "Problems of ambiguity with spoken input"
  - "Design validation: Review checking correspondence with specification"
  - "Confirm appropriate techniques used"
  - "Confirm appropriate user interface"
  - "Design evaluation: Criteria for evaluation of computer solutions"
---

## Human-Computer Interaction (HCI): Contemporary Approaches

<div class="key-term" markdown="1">
**Human-Computer Interaction (HCI)** is the study and design of how people interact with computers. It focuses on making interfaces that are effective, efficient, and satisfying for users.
</div>

As technology has advanced, the ways in which humans interact with computers have expanded far beyond the traditional keyboard and mouse. Contemporary HCI approaches include:

### Touch Interfaces

Touch screens allow users to interact directly with what is displayed by tapping, swiping, pinching, and dragging on the screen surface.

**Applications:** Smartphones, tablets, self-service kiosks, point-of-sale terminals, interactive whiteboards

**Advantages:**
- Intuitive and natural -- users directly manipulate on-screen elements
- No need for a separate input device (mouse/keyboard)
- Accessible to a wide range of users, including young children

**Disadvantages:**
- Lack of tactile feedback (no physical sensation of pressing a key)
- Imprecise for detailed work (e.g. fine image editing)
- Screen can become obscured by the user's hand
- Hygiene concerns on shared public touchscreens

### Gesture-Based Interfaces

Gesture recognition systems detect and interpret human body movements -- hand waves, finger pointing, body posture -- as input commands.

**Applications:** Gaming (e.g. Microsoft Kinect), smart TVs, surgical operating theatres (touchless control to maintain sterility), sign language recognition

**Advantages:**
- Hands-free interaction is possible
- Natural and immersive for gaming and entertainment
- Useful in environments where touching a device is impractical or unsafe

**Disadvantages:**
- Can be imprecise and unreliable
- Physically tiring for extended use ("gorilla arm" fatigue)
- Limited vocabulary of gestures compared to keyboard input
- Requires specialised sensors (cameras, depth sensors)

### Voice Interfaces

Voice recognition systems convert spoken language into commands or text. Virtual assistants such as Siri, Alexa, and Google Assistant are prominent examples.

**Applications:** Virtual assistants, dictation software, accessibility tools, smart home control, car infotainment systems

**Advantages:**
- Hands-free and eyes-free operation
- Fast for simple commands and dictation
- Highly beneficial for users with physical disabilities
- Natural interaction for many users

**Disadvantages:**
- Struggles with accents, dialects, and background noise
- Privacy concerns (always-listening devices)
- Ambiguity in natural language (discussed in detail below)
- Difficult for complex or precise instructions
- Socially awkward in public or shared spaces

### Virtual Reality (VR) and Augmented Reality (AR)

**VR** immerses the user in a fully computer-generated environment using a headset and controllers. **AR** overlays digital information on the real world, typically through a smartphone camera or smart glasses.

**VR applications:** Training simulations (surgery, flight, military), gaming, virtual tourism, architectural walkthroughs

**AR applications:** Navigation overlays, maintenance instructions, educational tools, retail (virtual try-on), medical imaging during surgery

**Advantages:**
- Highly immersive and engaging
- Excellent for training in dangerous or expensive real-world scenarios
- AR provides contextual information in real time

**Disadvantages:**
- VR headsets can cause motion sickness and eye strain
- Expensive hardware requirements
- VR isolates the user from the real world
- AR can be distracting and potentially dangerous (e.g. while driving)

### Brain-Computer Interfaces (BCI)

Brain-computer interfaces detect electrical signals from the brain and translate them into computer commands. This is still a largely experimental technology.

**Applications:** Assisting paralysed individuals to control prosthetics or computers, neuroscience research, potential future gaming and productivity applications

**Advantages:**
- Can provide communication for users who cannot speak or move
- No physical input device required at all
- Potential for very direct and fast interaction

**Disadvantages:**
- Currently very limited in accuracy and speed
- Invasive BCIs require surgical implantation
- Non-invasive BCIs (e.g. EEG headsets) are imprecise
- Ethical concerns about brain data privacy
- Very early stage of development for consumer use

---

## Natural Language Interfaces: Potential and Limitations

<div class="key-term" markdown="1">
A **natural language interface** allows users to interact with a computer using everyday human language (spoken or typed) rather than a formal command syntax or graphical controls.
</div>

### Potential of Natural Language Interfaces

Natural language interfaces represent one of the most intuitive forms of HCI because they allow users to communicate with computers in the same way they communicate with other people.

**Potential benefits:**
- **No training required** -- users already know how to speak or type in their native language
- **Accessibility** -- benefits users who struggle with traditional interfaces, including those with physical disabilities or limited computer literacy
- **Speed** -- spoken commands can be faster than navigating menus or typing formal commands
- **Versatility** -- can handle a very wide range of requests without the user needing to learn specific commands
- **Multilingual support** -- systems can potentially support many different languages

### Current Limitations

Despite significant advances in natural language processing (NLP), current systems have important limitations:

- **Ambiguity** -- natural language is inherently ambiguous (see detailed analysis below)
- **Context understanding** -- systems struggle with implied meaning, sarcasm, irony, and cultural references
- **Complex queries** -- multi-step or conditional requests are often misinterpreted
- **Domain knowledge** -- systems may lack specialist vocabulary for technical fields
- **Conversational memory** -- maintaining context over a long conversation remains challenging
- **Error recovery** -- when the system misunderstands, correcting the error can be frustrating

---

## Problems of Ambiguity with Spoken Input

Spoken natural language input introduces additional layers of ambiguity beyond those present in written text.

### Homophones

<div class="key-term" markdown="1">
**Homophones** are words that sound identical when spoken but have different meanings and often different spellings.
</div>

| Spoken Word | Possible Interpretations |
|---|---|
| "there" / "their" / "they're" | A place / belonging to them / they are |
| "to" / "too" / "two" | Preposition / also / the number 2 |
| "write" / "right" | To compose text / correct or a direction |
| "flower" / "flour" | A plant / a baking ingredient |
| "sea" / "see" | A body of water / to perceive visually |
| "knight" / "night" | A medieval warrior / the time after sunset |

A voice recognition system hearing "I want to book a flight to/two/too Nice/nice" must use context to resolve multiple ambiguities simultaneously.

### Accent and Dialect Variation

Different accents and dialects can cause the same word to sound very different, or can make different words sound the same.

**Problems include:**
- Regional pronunciation differences (e.g. "bath" with a long or short 'a')
- Different vowel sounds across dialects
- Systems trained primarily on one accent may perform poorly with others
- Non-native speakers may have pronunciation patterns unfamiliar to the system
- Speed and rhythm of speech vary significantly between speakers

### Background Noise

Real-world environments introduce noise that interferes with speech recognition:

- **Office noise** -- other people talking, phone calls, keyboard typing
- **Outdoor noise** -- traffic, wind, crowds
- **Domestic noise** -- television, music, appliances
- **Echo and reverberation** -- in large rooms or spaces with hard surfaces
- **Multiple speakers** -- the system must identify which voice to listen to (the "cocktail party problem")

### Context Dependence

The meaning of spoken sentences often depends on context that the computer may not have:

- **Conversational context** -- "Book that one" requires knowing what was previously discussed
- **Situational context** -- "It's cold in here" might be a request to adjust heating, or simply a statement
- **Cultural context** -- idioms and colloquialisms vary between cultures and may not translate literally
- **Emotional context** -- tone of voice, stress, and intonation carry meaning that is difficult for systems to interpret

<div class="exam-tip" markdown="1">
When discussing ambiguity in spoken input, remember to cover all four categories: **homophones**, **accent/dialect**, **background noise**, and **context**. An exam answer that only discusses one or two of these will not achieve full marks.
</div>

---

## Design Validation

<div class="key-term" markdown="1">
**Design validation** is the process of reviewing a system design to confirm it correctly and completely addresses the requirements specification. It answers the question: "Are we building the right system?"
</div>

Design validation involves several complementary checks:

### Reviewing the Design Against the Specification

The design must be checked systematically against every requirement in the specification to ensure nothing has been missed or misinterpreted.

**Methods include:**
- **Requirements traceability matrix** -- a table that maps each requirement to the corresponding design element, ensuring complete coverage
- **Formal design reviews** -- meetings where the design team presents the design to stakeholders, who verify it meets their expectations
- **Walkthroughs** -- step-by-step examination of the design, often using scenarios or use cases to check that the design handles them correctly
- **Sign-off** -- stakeholders formally approve the design before implementation begins

**Key questions:**
- Does the design address every functional requirement?
- Does the design meet all non-functional requirements (performance, security, usability)?
- Are there any requirements that have been overlooked or misunderstood?
- Are there any design elements that do not map to any requirement (unnecessary complexity)?

### Checking Appropriate Techniques Were Used

The design should use techniques and technologies that are appropriate for the type of system being built.

**Considerations include:**
- Has the appropriate development methodology been chosen (Waterfall, Agile, or a hybrid)?
- Is the chosen programming paradigm suitable (e.g. OOP for a system with many interacting entities)?
- Are the data structures and algorithms efficient for the expected data volumes?
- Is the database design normalised appropriately?
- Are appropriate security measures designed in from the start?
- Is the architecture scalable for future growth?

### Checking User Interface Appropriateness

The user interface design must be appropriate for the intended users and their context of use.

**Factors to consider:**

| Factor | Questions to Ask |
|---|---|
| **Target audience** | Who will use the system? What is their technical ability? |
| **Accessibility** | Does the interface meet accessibility standards (e.g. screen reader support, colour contrast)? |
| **Platform** | Is the interface appropriate for the target device (desktop, mobile, tablet, kiosk)? |
| **Consistency** | Does the interface follow established conventions and maintain internal consistency? |
| **Error handling** | Does the interface provide clear, helpful error messages? |
| **Navigation** | Can users find the features they need without difficulty? |
| **Responsiveness** | Does the interface adapt to different screen sizes and orientations? |

---

## Design Evaluation Criteria

Once a system has been built (or during design), it must be evaluated against a range of criteria to judge its quality and fitness for purpose.

### Functionality

<div class="key-term" markdown="1">
**Functionality** measures whether the system does what it is supposed to do -- whether it correctly implements all the features specified in the requirements.
</div>

- Does the system perform all required functions?
- Are calculations and outputs correct?
- Does it handle all specified input types, including edge cases?
- Are all user roles and permissions implemented correctly?

### Usability

**Usability** measures how easy and pleasant the system is to use.

- Can users learn to use the system quickly?
- Can experienced users complete tasks efficiently?
- Is the interface intuitive and consistent?
- Are error messages clear and helpful?
- Does the system meet accessibility requirements?
- Is user satisfaction high?

### Performance

**Performance** measures how quickly and efficiently the system responds under various conditions.

- Does the system respond within acceptable time limits?
- Can it handle the expected number of concurrent users?
- Does it use system resources (CPU, memory, storage) efficiently?
- How does it perform under peak load conditions?
- Are response times consistent?

### Reliability

**Reliability** measures how consistently the system operates without failure.

- How often does the system crash or produce errors?
- Can it recover gracefully from failures?
- Is data integrity maintained at all times?
- Does it include appropriate backup and recovery mechanisms?
- What is the mean time between failures (MTBF)?

### Maintainability

**Maintainability** measures how easy it is to modify the system after deployment -- fixing bugs, adding features, or adapting to changes.

- Is the code well-structured, commented, and documented?
- Are modules loosely coupled and highly cohesive?
- Can individual components be modified without affecting others?
- Is the system built using standard technologies and patterns?
- Is there comprehensive technical documentation?

### Portability

**Portability** measures how easily the system can be transferred to a different environment (hardware, operating system, or platform).

- Can the system run on different operating systems?
- Is it dependent on specific hardware?
- Are external dependencies well-managed?
- Is the data stored in standard, transferable formats?
- How much effort is required to migrate to a new platform?

### Cost-effectiveness

**Cost-effectiveness** evaluates whether the system provides good value relative to its cost.

- Does the system deliver the expected benefits?
- Are the development costs proportional to the value it provides?
- Are ongoing maintenance and operational costs reasonable?
- Does the system reduce costs or increase revenue as expected?
- How does the total cost of ownership compare with alternative solutions?

<div class="exam-tip" markdown="1">
When evaluating a system in an exam scenario, use these criteria as a checklist. You do not need to address every criterion in depth -- focus on the ones most relevant to the scenario. For example, for a safety-critical medical system, **reliability** and **functionality** are paramount. For a consumer mobile app, **usability** and **performance** may be more important.
</div>
