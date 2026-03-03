---
layout: topic
title: "Hardware & Communication"
level: "A2 Level"
level_url: "/a2/"
unit_name: "Unit 4: Architecture, Data, Communication & Applications"
unit_url: "/a2/unit4/"
subtopics:
  - "Architecture: Main components of contemporary computer architecture"
  - "Limiting factors to parallelisation in parallel processing"
  - "Calculate runtime of tasks as result of parallelisation"
  - "Evaluate the effect of parallelisation"
  - "Assembly language programming: Write simple programs"
  - "Demonstrate how assembly programs could be executed"
  - "Input/output: Voice input for command and control systems"
  - "Vocabulary dictation systems for general input"
  - "Voice print recognition for security"
  - "Suitability of each voice system in different situations"
  - "Networking: Applications requiring portable device network connection"
  - "Hardware required for wireless connection"
  - "Contemporary wireless technologies"
---

## Contemporary Computer Architecture

Modern processors are built upon foundational architectural models, each with distinct design philosophies that affect performance, power consumption, and suitability for different tasks.

### Von Neumann vs Harvard Architecture

<div class="key-term" markdown="1">
**Von Neumann Architecture** stores both program instructions and data in the same memory space, accessed via a single shared bus. This creates the **Von Neumann bottleneck** where the CPU must wait for either data or instructions because only one can be fetched at a time.
</div>

<div class="key-term" markdown="1">
**Harvard Architecture** uses physically separate memory stores and buses for instructions and data, allowing both to be fetched simultaneously. This removes the Von Neumann bottleneck and increases throughput.
</div>

| Feature | Von Neumann | Harvard |
|---|---|---|
| Memory | Single shared memory for data and instructions | Separate memory for data and instructions |
| Buses | Single shared bus | Separate data bus and instruction bus |
| Fetch speed | Slower (sequential access) | Faster (simultaneous access) |
| Flexibility | Programs can modify themselves (self-modifying code) | Instructions and data are strictly separated |
| Complexity | Simpler, cheaper to manufacture | More complex, more expensive |
| Common use | General-purpose PCs, laptops | DSPs, microcontrollers, embedded systems |

Most modern desktop processors use a **modified Harvard architecture**: they maintain separate Level 1 caches for instructions and data (Harvard-style) but share a unified main memory (Von Neumann-style). This combines the speed benefits of Harvard with the flexibility of Von Neumann.

### CISC vs RISC

<div class="key-term" markdown="1">
**CISC (Complex Instruction Set Computer)** provides a large number of complex instructions, some of which can perform multi-step operations in a single instruction. Each instruction may take multiple clock cycles to execute.
</div>

<div class="key-term" markdown="1">
**RISC (Reduced Instruction Set Computer)** uses a small, highly optimised set of simple instructions, each typically executing in a single clock cycle. Complex operations are built by combining multiple simple instructions.
</div>

| Feature | CISC | RISC |
|---|---|---|
| Instruction set | Large, complex (hundreds of instructions) | Small, simple (typically under 100) |
| Clock cycles per instruction | Variable (1 to many) | Usually 1 cycle per instruction |
| Instruction length | Variable length | Fixed length |
| Addressing modes | Many | Few |
| Hardware complexity | Complex decoding hardware | Simpler hardware, relies on compiler |
| Pipelining | Harder to implement efficiently | Easier to pipeline due to fixed-length instructions |
| Power consumption | Generally higher | Generally lower |
| Example processors | Intel x86, AMD | ARM, MIPS |
| Typical use | Desktop PCs, servers | Mobile devices, tablets, embedded systems |

<div class="exam-tip" markdown="1">
In exam questions comparing CISC and RISC, always link the architectural features to practical consequences. For example: RISC's fixed-length instructions make pipelining more efficient, which leads to higher throughput. CISC's complex instructions mean fewer lines of assembly code are needed, reducing program memory requirements.
</div>

### Multi-Core Processors

<div class="key-term" markdown="1">
A **multi-core processor** contains two or more independent processing units (cores) on a single chip. Each core can fetch, decode, and execute instructions independently, allowing genuine parallel execution of multiple threads or processes.
</div>

Key characteristics of multi-core processors:

- Each core has its own Level 1 cache, but cores typically share Level 2/Level 3 cache and main memory
- The operating system's scheduler assigns threads and processes to available cores
- Doubling the number of cores does **not** double the performance, because not all tasks can be parallelised and there is overhead in coordinating between cores
- Software must be written to take advantage of multiple cores (multi-threaded programming)

Common configurations include dual-core (2), quad-core (4), hexa-core (6), octa-core (8), and beyond.

### GPU Computing

<div class="key-term" markdown="1">
**GPU (Graphics Processing Unit) computing** uses the massively parallel architecture of a graphics card for general-purpose computation. GPUs contain thousands of small, simple cores optimised for performing the same operation on many data points simultaneously.
</div>

GPUs are designed for **data parallelism**: applying the same instruction to large datasets. This makes them ideal for:

- Graphics rendering (their original purpose)
- Machine learning and neural network training
- Scientific simulations and modelling
- Cryptocurrency mining
- Image and video processing

The programming model used for GPU computing is called **GPGPU (General-Purpose computing on Graphics Processing Units)**, often implemented through frameworks such as CUDA (NVIDIA) or OpenCL.

| Feature | CPU | GPU |
|---|---|---|
| Number of cores | Few (2-64 typically) | Thousands (hundreds to tens of thousands) |
| Core complexity | Complex, powerful cores | Simple, lightweight cores |
| Best for | Sequential, branching logic | Repetitive parallel operations on large data |
| Clock speed per core | Higher | Lower |
| Memory access | Large caches, optimised for latency | High bandwidth, optimised for throughput |

### Co-processors

<div class="key-term" markdown="1">
A **co-processor** is a supplementary processor designed to handle specific types of computation, offloading work from the main CPU to improve overall system performance.
</div>

Examples of co-processors include:

- **Floating Point Unit (FPU)**: handles floating point arithmetic (historically separate, now integrated into modern CPUs)
- **GPU**: handles graphics rendering and parallel computation
- **Digital Signal Processor (DSP)**: optimised for processing audio, video, and sensor signals in real time
- **Neural Processing Unit (NPU)**: accelerates machine learning inference tasks
- **Cryptographic co-processor**: handles encryption and decryption operations

Co-processors improve performance by allowing the CPU to delegate specialised tasks while continuing with other work.

---

## Parallel Processing

<div class="key-term" markdown="1">
**Parallel processing** is the simultaneous execution of multiple instructions or tasks by dividing a problem into parts that can be solved concurrently across multiple processors or cores.
</div>

### Flynn's Taxonomy

Flynn's taxonomy classifies computer architectures based on the number of concurrent instruction streams and data streams they can handle.

| Classification | Instruction Streams | Data Streams | Description | Example |
|---|---|---|---|---|
| **SISD** | Single | Single | One instruction operates on one data item at a time | Traditional single-core Von Neumann processor |
| **SIMD** | Single | Multiple | One instruction operates on multiple data items simultaneously | GPU cores, vector processors, multimedia extensions (SSE/AVX) |
| **MISD** | Multiple | Single | Multiple instructions operate on the same data item | Rare; used in fault-tolerant systems (e.g. space shuttle flight computers running different algorithms on the same input) |
| **MIMD** | Multiple | Multiple | Multiple instructions operate on multiple data items independently | Multi-core processors, networked computer clusters |

<div class="exam-tip" markdown="1">
SIMD is the most commonly examined parallel architecture. A good example is applying a brightness filter to an image: the same "add 10 to pixel value" instruction is applied simultaneously to thousands of different pixels (data items). GPUs are essentially massively parallel SIMD processors.
</div>

**MIMD** can be further divided into:

- **Shared memory MIMD**: all processors access the same memory space (e.g. multi-core processors on one motherboard)
- **Distributed memory MIMD**: each processor has its own local memory and they communicate via message passing (e.g. computer clusters connected by a network)

---

## Limiting Factors to Parallelisation

Not all programs can benefit equally from parallel processing. Several factors limit the achievable speedup.

### Amdahl's Law

<div class="key-term" markdown="1">
**Amdahl's Law** states that the maximum speedup of a program through parallelisation is limited by the proportion of the program that must remain sequential. No matter how many processors are added, the sequential portion creates an upper bound on performance improvement.
</div>

The formula for Amdahl's Law is:

**Speedup = 1 / ((1 - P) + P/N)**

Where:
- **P** = the proportion (fraction) of the program that can be parallelised (0 to 1)
- **N** = the number of processors
- **(1 - P)** = the proportion that must remain sequential

#### Worked Example 1

A program takes 100 seconds to run on a single processor. 80% of the code can be parallelised. What is the speedup with 4 processors?

- P = 0.8
- N = 4
- Speedup = 1 / ((1 - 0.8) + 0.8/4)
- Speedup = 1 / (0.2 + 0.2)
- Speedup = 1 / 0.4
- **Speedup = 2.5x**
- New runtime = 100 / 2.5 = **40 seconds**

#### Worked Example 2

A program takes 200 seconds on one processor. 90% can be parallelised. Calculate the speedup and new runtime with 8 processors.

- P = 0.9
- N = 8
- Speedup = 1 / ((1 - 0.9) + 0.9/8)
- Speedup = 1 / (0.1 + 0.1125)
- Speedup = 1 / 0.2125
- **Speedup = 4.71x** (to 2 d.p.)
- New runtime = 200 / 4.71 = **42.46 seconds**

#### Worked Example 3

What is the theoretical maximum speedup if 75% of a program can be parallelised, using an infinite number of processors?

- P = 0.75
- As N approaches infinity, P/N approaches 0
- Speedup = 1 / ((1 - 0.75) + 0)
- Speedup = 1 / 0.25
- **Maximum speedup = 4x**

This demonstrates that even with unlimited processors, the sequential 25% limits the speedup to 4x.

<div class="exam-tip" markdown="1">
In exam calculations, always show your working clearly. State the values of P and N, substitute into the formula, and simplify step by step. For the "theoretical maximum" question, set N to infinity so that P/N becomes 0. Remember: speedup is a multiplier (e.g. 2.5x means 2.5 times faster), not a time.
</div>

### Data Dependencies

<div class="key-term" markdown="1">
A **data dependency** occurs when an instruction requires the result of a previous instruction before it can execute. Data dependencies force sequential execution and prevent parallelisation of those instructions.
</div>

For example:
```
A = B + C
D = A * 2
```
The second instruction depends on the result of the first (it needs the value of A), so they cannot run in parallel.

Types of data dependency:

- **Read After Write (RAW)**: an instruction must read a value that a previous instruction has written (most common)
- **Write After Read (WAR)**: an instruction must write to a location that a previous instruction has not yet finished reading
- **Write After Write (WAW)**: two instructions write to the same location and the order matters

### Communication Overhead

When multiple processors work together, they must communicate to share data and coordinate. This communication takes time and introduces overhead that reduces the benefit of parallelisation. As more processors are added:

- More data must be transferred between processors
- Network latency increases if processors are distributed
- Bus contention occurs when multiple processors compete for shared resources
- The overhead can eventually outweigh the benefit of adding more processors

### Synchronisation

<div class="key-term" markdown="1">
**Synchronisation** is the coordination of parallel processes to ensure they execute in the correct order and produce consistent results, particularly when accessing shared resources.
</div>

Synchronisation issues include:

- **Race conditions**: when the outcome depends on the unpredictable timing of processes
- **Deadlock**: when two or more processes are each waiting for the other to release a resource
- **Barriers**: points where all processes must wait until every process has reached that point before any can proceed

Synchronisation mechanisms add waiting time and reduce the effective parallelism.

---

## Assembly Language Programming

<div class="key-term" markdown="1">
**Assembly language** is a low-level programming language that uses mnemonics to represent machine code instructions. Each assembly instruction corresponds to a single machine code operation. An **assembler** translates assembly language into machine code.
</div>

### Registers

Registers are small, fast storage locations within the CPU. The basic assembly language model used at A2 level typically includes:

- **Accumulator (ACC)**: the main working register where arithmetic and logic results are stored
- **Program Counter (PC)**: holds the address of the next instruction to be executed
- **Memory Address Register (MAR)**: holds the address of the memory location being accessed
- **Memory Data Register (MDR)**: holds the data being transferred to or from memory
- **Current Instruction Register (CIR)**: holds the instruction currently being decoded and executed

### Instruction Set

The A2 level assembly language uses the following instruction set:

| Mnemonic | Operand | Description |
|---|---|---|
| `INP` | None | Input: reads a value from the user and stores it in the accumulator |
| `OUT` | None | Output: displays the current value in the accumulator |
| `MOV` | Register | Moves data from one register to another |
| `ADD` | Value/Address | Adds the value (or value at address) to the accumulator |
| `SUB` | Value/Address | Subtracts the value (or value at address) from the accumulator |
| `CMP` | Value/Address | Compares the accumulator with a value (sets flags for branching) |
| `BRZ` | Label | Branch if Zero: jumps to label if the result of the last comparison was zero |
| `BRP` | Label | Branch if Positive: jumps to label if the result was positive (or zero) |
| `BRA` | Label | Branch Always: unconditional jump to label |
| `HLT` | None | Halt: stops program execution |
| `DAT` | Value | Data: reserves a memory location and optionally initialises it with a value |

### Writing and Tracing Assembly Programs

#### Example 1: Add Two Numbers

This program inputs two numbers, adds them, and outputs the result.

```
        INP         // Input first number into ACC
        MOV R1      // Store first number in register R1
        INP         // Input second number into ACC
        ADD R1      // Add R1 to ACC
        OUT         // Output the result
        HLT         // Stop
```

**Trace** (inputs: 5 and 3):

| Step | Instruction | ACC | R1 | Output |
|---|---|---|---|---|
| 1 | INP | 5 | - | |
| 2 | MOV R1 | 5 | 5 | |
| 3 | INP | 3 | 5 | |
| 4 | ADD R1 | 8 | 5 | |
| 5 | OUT | 8 | 5 | 8 |
| 6 | HLT | 8 | 5 | |

#### Example 2: Countdown from Input to Zero

This program inputs a number and counts down to zero, outputting each value.

```
        INP         // Input the starting number
LOOP    OUT         // Output current value
        SUB ONE     // Subtract 1
        BRZ DONE    // If zero, branch to DONE
        BRA LOOP    // Otherwise, loop back
DONE    OUT         // Output the final zero
        HLT         // Stop
ONE     DAT 1       // Constant: 1
```

**Trace** (input: 3):

| Step | Instruction | ACC | Output | Branch Taken? |
|---|---|---|---|---|
| 1 | INP | 3 | | |
| 2 | OUT | 3 | 3 | |
| 3 | SUB ONE | 2 | | |
| 4 | BRZ DONE | 2 | | No (ACC != 0) |
| 5 | BRA LOOP | 2 | | Yes |
| 6 | OUT | 2 | 2 | |
| 7 | SUB ONE | 1 | | |
| 8 | BRZ DONE | 1 | | No (ACC != 0) |
| 9 | BRA LOOP | 1 | | Yes |
| 10 | OUT | 1 | 1 | |
| 11 | SUB ONE | 0 | | |
| 12 | BRZ DONE | 0 | | Yes (ACC == 0) |
| 13 | OUT | 0 | 0 | |
| 14 | HLT | 0 | | |

#### Example 3: Find the Larger of Two Numbers

```
        INP         // Input first number
        MOV R1      // Store in R1
        INP         // Input second number
        MOV R2      // Store in R2
        SUB R1      // ACC = second - first
        BRP SECBIG  // If positive, second is bigger
        MOV ACC R1  // Otherwise load first into ACC
        BRA FINISH
SECBIG  MOV ACC R2  // Load second into ACC
FINISH  OUT         // Output the larger number
        HLT
```

<div class="exam-tip" markdown="1">
When tracing assembly programs in the exam, draw a clear table showing each instruction executed, the state of the accumulator and any registers, and any output produced. Pay careful attention to branch instructions: check whether the condition is met and clearly show which instruction executes next. Use `DAT` at the end of your programs to define constants and variables.
</div>

---

## Voice Input Systems

Voice input systems convert spoken language into a form that a computer can process. There are three distinct types, each suited to different purposes.

### Command and Control Systems

<div class="key-term" markdown="1">
**Command and control** voice systems recognise a limited set of short, predefined spoken commands to control a device or application. They use a restricted vocabulary matched against stored templates.
</div>

Characteristics:

- **Small, fixed vocabulary** (typically tens to hundreds of words)
- Recognises **short, isolated commands** (e.g. "call home", "play music", "turn left")
- Uses **pattern matching** against pre-stored voice templates
- Fast response time due to limited search space
- Works well in **noisy environments** because commands are distinct and short
- Does **not** need to understand continuous speech or natural language

Examples: smart home devices ("Hey Siri, turn off the lights"), satellite navigation voice commands, hands-free phone dialling, industrial machinery control.

### Vocabulary Dictation Systems

<div class="key-term" markdown="1">
**Vocabulary dictation** systems convert continuous, natural speech into text. They must handle a large vocabulary, varied sentence structures, and connected words spoken at normal speed.
</div>

Characteristics:

- **Large vocabulary** (tens of thousands to hundreds of thousands of words)
- Handles **continuous speech** (words spoken naturally without pauses between them)
- Uses **language models** and context to disambiguate similar-sounding words (e.g. "there", "their", "they're")
- Requires **training** to adapt to individual speakers for better accuracy
- More computationally intensive than command and control
- Accuracy improves with user-specific training and context awareness

Examples: dictation software for writing documents, live captioning, medical transcription, legal transcription.

### Voice Print Recognition

<div class="key-term" markdown="1">
**Voice print recognition** (speaker verification) is a biometric security system that identifies or verifies a person based on the unique physical characteristics of their voice, rather than understanding what they say.
</div>

Characteristics:

- Analyses **voice characteristics**: pitch, tone, cadence, frequency patterns, vocal tract shape
- Creates a **voice print** (a mathematical model of the speaker's voice)
- Used for **authentication and identification**, not for understanding speech content
- Can be **text-dependent** (user speaks a specific passphrase) or **text-independent** (any speech can be analysed)
- Vulnerable to **spoofing** (recordings, voice synthesis) so often combined with other security factors
- Affected by illness, emotional state, or background noise

Examples: telephone banking authentication, secure facility access, forensic speaker identification.

### Suitability of Each System

| Situation | Best System | Reason |
|---|---|---|
| Controlling a smart home device | Command and control | Limited set of known commands; fast response needed |
| Dictating an essay | Vocabulary dictation | Continuous speech; large vocabulary; natural language |
| Unlocking a secure phone | Voice print recognition | Biometric verification of identity |
| Surgical theatre (hands-free operation) | Command and control | Short, precise commands in a controlled environment |
| Creating meeting minutes | Vocabulary dictation | Long-form continuous speech needs accurate transcription |
| Bank telephone authentication | Voice print recognition | Verifying the caller's identity |
| In-car navigation commands | Command and control | Simple commands; driver must keep eyes on road |
| Accessibility for visually impaired users | Vocabulary dictation | Full text input via speech for extended interaction |
| Prison visitor verification | Voice print recognition | Biometric check to confirm identity against records |

<div class="exam-tip" markdown="1">
When asked to evaluate the suitability of a voice system for a given scenario, consider: (1) the size of vocabulary needed, (2) whether continuous speech or isolated commands are used, (3) whether the goal is to understand content or verify identity, (4) the environment (noisy or quiet), and (5) the response time requirements. Always justify your choice by linking features of the system to the requirements of the scenario.
</div>

---

## Wireless Networking

### Wi-Fi (IEEE 802.11 Standards)

<div class="key-term" markdown="1">
**Wi-Fi** is a family of wireless networking protocols based on the IEEE 802.11 standards. Wi-Fi allows devices to connect to a local area network (LAN) wirelessly using radio waves.
</div>

| Standard | Frequency Band | Maximum Theoretical Speed | Typical Range (Indoors) | Year |
|---|---|---|---|---|
| 802.11a | 5 GHz | 54 Mbps | ~35 m | 1999 |
| 802.11b | 2.4 GHz | 11 Mbps | ~35 m | 1999 |
| 802.11g | 2.4 GHz | 54 Mbps | ~38 m | 2003 |
| 802.11n (Wi-Fi 4) | 2.4 GHz / 5 GHz | 600 Mbps | ~70 m | 2009 |
| 802.11ac (Wi-Fi 5) | 5 GHz | 6.9 Gbps | ~35 m | 2013 |
| 802.11ax (Wi-Fi 6) | 2.4 GHz / 5 GHz / 6 GHz | 9.6 Gbps | ~30 m | 2020 |

Key points about Wi-Fi:

- **2.4 GHz** band: longer range, better wall penetration, but more congestion (shared with microwaves, Bluetooth, etc.) and fewer non-overlapping channels
- **5 GHz** band: faster speeds, less congestion, but shorter range and poorer wall penetration
- Wi-Fi uses **CSMA/CA** (Carrier Sense Multiple Access with Collision Avoidance) to manage shared access to the wireless medium

### Bluetooth

<div class="key-term" markdown="1">
**Bluetooth** is a short-range wireless technology for exchanging data between devices over short distances using the 2.4 GHz ISM band. It is designed for low-power, low-cost personal area networks (PANs).
</div>

| Feature | Detail |
|---|---|
| Range | Typically 10 m (Class 2), up to 100 m (Class 1) |
| Speed | Up to 3 Mbps (Bluetooth 3.0), 2 Mbps (Bluetooth 5.0 LE) |
| Power consumption | Low (especially Bluetooth Low Energy / BLE) |
| Connection type | Point-to-point or piconet (up to 8 devices) |
| Common uses | Wireless headphones, keyboards, mice, fitness trackers, file transfer between phones |

### NFC (Near Field Communication)

<div class="key-term" markdown="1">
**NFC (Near Field Communication)** is a very short-range wireless technology (up to approximately 10 cm) based on RFID. It enables simple, touch-based communication between devices.
</div>

| Feature | Detail |
|---|---|
| Range | Up to ~10 cm |
| Speed | 424 Kbps |
| Power | Very low; passive NFC tags require no battery |
| Connection setup | Instantaneous (no pairing required) |
| Common uses | Contactless payment (Apple Pay, Google Pay), travel cards (Oyster), access control, pairing Bluetooth devices |

NFC's extremely short range is actually a **security feature**: an attacker would need to be within centimetres to intercept the signal.

### Cellular Networks (4G / 5G)

<div class="key-term" markdown="1">
**Cellular networks** provide wide-area wireless connectivity through a network of base stations (cell towers). Each base station covers a geographical "cell", and devices are handed off between cells as they move.
</div>

| Feature | 4G (LTE) | 5G |
|---|---|---|
| Maximum speed | ~150 Mbps (typical), up to 1 Gbps | ~1-10 Gbps (theoretical) |
| Latency | ~30-50 ms | ~1-10 ms |
| Frequency | 700 MHz - 2.6 GHz | Sub-6 GHz and mmWave (24-100 GHz) |
| Range per cell | Large (several km) | Smaller cells needed for mmWave |
| Key applications | Mobile internet, video streaming | IoT, autonomous vehicles, remote surgery, AR/VR |

5G uses higher frequencies (particularly mmWave) which provide greater bandwidth but have shorter range and poorer building penetration, requiring a denser network of smaller cells.

### Hardware Required for Wireless Connection

To establish a wireless network, the following hardware is required:

| Hardware Component | Purpose |
|---|---|
| **Wireless Network Interface Card (NIC)** | Installed in each device; contains a radio transceiver to send and receive wireless signals. Converts data between digital format and radio waves. |
| **Wireless Access Point (WAP)** | Acts as a central hub for the wireless network; bridges wireless devices to the wired network. Manages connections, authentication, and channel allocation. |
| **Wireless Router** | Combines a WAP, router, and often a modem. Routes traffic between the local network and the internet, assigns IP addresses via DHCP. |
| **Antenna** | Transmits and receives radio signals. Can be omnidirectional (all directions) or directional (focused beam for longer range). Built into NICs and access points, or external for extended range. |
| **Repeater / Range Extender** | Receives the wireless signal and retransmits it to extend coverage area. Useful for large buildings but can reduce throughput. |

### Comparison of Wireless Technologies

| Feature | Wi-Fi | Bluetooth | NFC | Cellular (4G/5G) |
|---|---|---|---|---|
| Range | ~30-70 m (indoors) | ~10-100 m | ~10 cm | Several km |
| Speed | Up to several Gbps | Up to 3 Mbps | 424 Kbps | Up to 10 Gbps (5G) |
| Power usage | Medium-High | Low | Very low | High |
| Setup | Network name/password | Pairing process | Touch/tap | SIM card / eSIM |
| Best for | Local network, internet access | Peripheral devices, short-range data | Payments, access cards | Mobile internet, wide-area connectivity |

<div class="exam-tip" markdown="1">
When comparing wireless technologies in an exam, structure your answer around the key differentiators: range, speed, power consumption, security, and typical use cases. Always match the technology to the scenario. For example, NFC is ideal for contactless payments because the very short range provides inherent security, instant connection, and minimal power use. Wi-Fi would be inappropriate for a contactless payment system because it operates over a much larger range, creating security concerns.
</div>
