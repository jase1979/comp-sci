---
layout: topic
title: "Hardware"
level: "GCSE"
level_url: "/gcse/"
unit_name: "Unit 1: Understanding Computer Science"
unit_url: "/gcse/unit1/"
subtopics:
  - "Architecture: CPU characteristics including Von Neumann"
  - "Components of CPU in fetch-decode-execute cycle"
  - "Performance factors: Cache size, clock speed, number of cores"
  - "Difference between RISC and CISC processors"
  - "Input/output: Use and characteristics of I/O devices"
  - "Primary storage: RAM, ROM, flash memory, cache memory"
  - "Secondary storage: Magnetic, optical and solid state technologies"
  - "Functional characteristics: Suitability, durability, portability, speed"
  - "Storage requirements: Bit, nybble, byte, kilobyte, prefix multipliers"
  - "Data capacity and calculating data capacity requirements"
  - "Other hardware: GPU, sound cards, motherboards"
  - "Embedded systems: Use and examples"
next_topic: "/gcse/unit1/logical-operations/"
---

## CPU Architecture

The **Central Processing Unit (CPU)** is the main processor in a computer. It carries out instructions from programs by performing basic arithmetic, logic, control and input/output operations.

### Von Neumann Architecture

Most modern computers are based on the **Von Neumann architecture**, proposed by John von Neumann in 1945. Its key principle is that **data and instructions are stored together in the same memory** and are accessed using the same bus system.

<div class="diagram">
┌─────────────────────────────────────────────┐
│                    CPU                       │
│  ┌───────────┐  ┌──────────────────────┐    │
│  │  Control   │  │         ALU          │    │
│  │   Unit     │  │  (Arithmetic Logic   │    │
│  │   (CU)     │  │       Unit)          │    │
│  └─────┬─────┘  └──────────┬───────────┘    │
│        │                    │                │
│  ┌─────┴────────────────────┴───────────┐   │
│  │           Registers                   │   │
│  │  ┌─────┐ ┌─────┐ ┌─────┐ ┌────────┐ │   │
│  │  │ PC  │ │ MAR │ │ MDR │ │  ACC   │ │   │
│  │  └─────┘ └─────┘ └─────┘ └────────┘ │   │
│  └──────────────────────────────────────┘   │
└──────────────────┬──────────────────────────┘
                   │
            ┌──────┴──────┐
            │  System Bus  │
            │ (Address,    │
            │  Data,       │
            │  Control)    │
            └──────┬──────┘
                   │
          ┌────────┴────────┐
          │   Main Memory   │
          │   (RAM / ROM)   │
          └─────────────────┘
</div>

#### Key components

<div class="key-term" markdown="1">
**ALU (Arithmetic Logic Unit)** — performs all arithmetic calculations (add, subtract) and logical comparisons (greater than, equal to, AND, OR, NOT).
</div>

<div class="key-term" markdown="1">
**Control Unit (CU)** — directs the operation of the processor. It fetches instructions from memory, decodes them, and coordinates the ALU, registers and memory to execute them.
</div>

<div class="key-term" markdown="1">
**Registers** — tiny, extremely fast storage locations inside the CPU used to hold data and addresses during processing.
</div>

#### Important registers

| Register | Full Name | Purpose |
|----------|-----------|---------|
| **PC** | Program Counter | Holds the address of the **next** instruction to be fetched |
| **MAR** | Memory Address Register | Holds the address of the memory location being read from or written to |
| **MDR** | Memory Data Register | Holds the data that has been fetched from memory or is about to be written to memory |
| **ACC** | Accumulator | Stores the result of calculations performed by the ALU |
| **CIR** | Current Instruction Register | Holds the instruction currently being decoded and executed |

### The Fetch-Decode-Execute Cycle

The CPU continuously repeats three steps to process every instruction:

**1. Fetch**
- The address in the **PC** is copied to the **MAR**
- The instruction at that address is fetched from **RAM** into the **MDR**
- The instruction is then copied from the MDR to the **CIR**
- The **PC** is incremented by 1 (to point to the next instruction)

**2. Decode**
- The **Control Unit** decodes the instruction in the CIR
- It identifies what operation to perform and what data is needed

**3. Execute**
- The instruction is carried out — this could be a calculation (ALU), data movement, or a control operation
- Results are stored in the **ACC** or written back to memory

<div class="exam-tip" markdown="1">
You may be asked to walk through the fetch-decode-execute cycle step by step. Always mention the specific registers by name (PC, MAR, MDR, CIR) and describe what happens at each stage.
</div>

---

## CPU Performance Factors

Three main factors affect how fast a CPU can process instructions:

### Clock Speed

- Measured in **hertz (Hz)** — typically **gigahertz (GHz)** for modern processors
- Each "tick" of the clock is one cycle; simple instructions take one cycle, complex ones take more
- A 3.5 GHz processor can perform 3.5 billion cycles per second
- **Higher clock speed = more instructions processed per second**
- Increasing clock speed generates more heat, requiring better cooling

### Cache Size

- **Cache** is a small amount of very fast memory **inside the CPU**
- It stores frequently used data and instructions so the CPU doesn't have to fetch them from slower RAM
- Levels of cache: **L1** (smallest, fastest), **L2**, **L3** (largest, slowest of the three)
- **Larger cache = fewer trips to RAM = faster performance**

### Number of Cores

- A **core** is an independent processing unit within the CPU
- A **dual-core** processor has 2 cores; a **quad-core** has 4
- Multiple cores can process different instructions **simultaneously** (parallel processing)
- **More cores = more tasks handled at once**
- Not all software can use multiple cores effectively

<div class="exam-tip" markdown="1">
If asked to recommend a CPU upgrade, consider the use case. Gaming benefits from clock speed; video editing benefits from more cores; general speed improvements come from more cache.
</div>

---

## RISC vs CISC Processors

| Feature | RISC | CISC |
|---------|------|------|
| **Full name** | Reduced Instruction Set Computer | Complex Instruction Set Computer |
| **Instructions** | Small set of simple instructions | Large set of complex instructions |
| **Cycles per instruction** | Usually 1 cycle | Multiple cycles |
| **Clock speed** | Generally faster | Generally slower |
| **Code length** | More lines of code needed | Fewer lines of code needed |
| **Power consumption** | Lower (used in mobile devices) | Higher (used in desktops/laptops) |
| **Example** | ARM processors (phones, tablets) | Intel x86 processors (PCs) |

<div class="key-term" markdown="1">
**RISC** uses many simple instructions that each execute in one clock cycle. **CISC** uses fewer, more powerful instructions that may take several cycles each. RISC is more power-efficient; CISC can do more per instruction.
</div>

---

## Input/Output Devices

**Input devices** send data into the computer. **Output devices** present data from the computer to the user.

### Common Input Devices

| Device | Use | Characteristics |
|--------|-----|-----------------|
| Keyboard | Typing text and commands | Familiar, accurate for text, slow for large data |
| Mouse | Pointing and selecting on screen | Intuitive, requires flat surface |
| Touchscreen | Direct interaction with display | Intuitive, less precise, fingerprint smudges |
| Microphone | Voice input, recording audio | Hands-free, affected by background noise |
| Scanner | Digitising physical documents | High quality, slow, bulky |
| Barcode reader | Reading product codes | Fast, accurate, limited to barcodes |
| Webcam | Capturing video/images | Real-time, lower quality than dedicated cameras |

### Common Output Devices

| Device | Use | Characteristics |
|--------|-----|-----------------|
| Monitor | Displaying visual output | High resolution, various sizes |
| Printer | Producing hard copies | Permanent output, slow, costs per page |
| Speaker | Audio output | Range of quality, requires amplification |
| Projector | Large-screen display | Good for presentations, needs dark room |

---

## Primary Storage

Primary storage is **directly accessible by the CPU** and holds data currently in use.

### RAM (Random Access Memory)

- **Volatile** — loses all data when power is turned off
- Stores the **operating system**, running **programs**, and **data currently in use**
- Can be **read from and written to**
- More RAM allows more programs to run simultaneously

### ROM (Read Only Memory)

- **Non-volatile** — retains data when power is turned off
- Stores the **BIOS/boot-up instructions** that start the computer
- Can only be **read from** (not written to in normal use)
- Contents set during manufacture

### Cache Memory

- Extremely fast, small, expensive memory **inside the CPU**
- Stores copies of frequently accessed data from RAM
- Operates in levels: **L1 > L2 > L3** (speed vs size trade-off)

### Flash Memory

- **Non-volatile** — retains data without power
- Can be **read from and written to** electronically
- Used in USB drives, SSDs, SD cards
- No moving parts, durable, but limited write cycles

| Type | Volatile? | Read/Write? | Speed | Typical Use |
|------|-----------|-------------|-------|-------------|
| RAM | Yes | Read & Write | Fast | Running programs |
| ROM | No | Read only | Fast | Boot-up instructions |
| Cache | Yes | Read & Write | Very fast | Frequently used data |
| Flash | No | Read & Write | Medium | Portable storage |

---

## Secondary Storage

Secondary storage is **non-volatile** and used for long-term data storage. It is not directly accessible by the CPU — data must be loaded into RAM first.

### Magnetic Storage

- **Hard Disk Drive (HDD)**: spinning platters with a read/write head
- **Magnetic tape**: sequential access, used for backups and archiving
- High capacity, low cost per GB, but moving parts make it fragile and slower

### Optical Storage

- Uses a **laser** to read/write data on a reflective disc
- Types: **CD** (~700 MB), **DVD** (~4.7 GB), **Blu-ray** (~25 GB)
- Portable, cheap, but low capacity compared to other media and easily scratched

### Solid State Storage

- **Solid State Drive (SSD)**: uses flash memory with no moving parts
- **USB flash drives**, **SD cards**
- Very fast, durable, silent, lightweight — but more expensive per GB than HDD

### Comparison

| Feature | HDD | SSD | Optical | Magnetic Tape |
|---------|-----|-----|---------|---------------|
| Speed | Medium | Fast | Slow | Very slow |
| Capacity | Very high | High | Low | Very high |
| Cost per GB | Low | Medium | Very low | Very low |
| Durability | Fragile (moving parts) | Durable | Scratches easily | Durable |
| Portability | Low | High | High | Low |
| Best for | Desktop storage | OS drive, laptops | Software distribution | Backups, archives |

---

## Storage Requirements

### Units of Storage

| Unit | Size | Equivalent |
|------|------|------------|
| **Bit** | 1 or 0 | Smallest unit of data |
| **Nybble** | 4 bits | Half a byte |
| **Byte (B)** | 8 bits | One character |
| **Kilobyte (KB)** | 1,000 bytes | Short text document |
| **Megabyte (MB)** | 1,000 KB | A photo or song |
| **Gigabyte (GB)** | 1,000 MB | A movie |
| **Terabyte (TB)** | 1,000 GB | Large hard drive |
| **Petabyte (PB)** | 1,000 TB | Data centre scale |

> Note: In computing, 1 KB is sometimes treated as 1,024 bytes (using binary prefixes: KiB, MiB, GiB). The WJEC spec uses the 1,000 convention above for simplicity.

### Calculating Data Capacity

#### Image file size

```
File size = Width (px) × Height (px) × Colour depth (bits)
```

- **Colour depth** is the number of bits per pixel (e.g. 24-bit colour = 16.7 million colours)
- A 1920×1080 image at 24-bit colour: `1920 × 1080 × 24 = 49,766,400 bits ≈ 5.93 MB`

#### Sound file size

```
File size = Sample rate (Hz) × Bit depth × Duration (s) × Channels
```

- **Sample rate**: how many samples per second (e.g. 44,100 Hz for CD quality)
- **Bit depth**: bits per sample (e.g. 16-bit)
- A 3-minute stereo track at CD quality: `44,100 × 16 × 180 × 2 = 254,016,000 bits ≈ 30.2 MB`

<div class="exam-tip" markdown="1">
Always show your working in calculation questions. Convert your final answer to sensible units (bits → bytes → KB → MB) by dividing by 8, then by 1,000 as needed. State the formula first.
</div>

---

## Other Hardware

### GPU (Graphics Processing Unit)

- Specialised processor designed for **rendering images and video**
- Contains thousands of small cores optimised for **parallel processing**
- Used for gaming, video editing, 3D modelling, and increasingly for AI workloads
- Can be integrated (built into CPU) or dedicated (separate card)

### Sound Card

- Processes **audio input and output**
- Converts digital signals to analogue (for speakers) and analogue to digital (from microphones)
- Built-in sound is sufficient for most users; dedicated cards offer higher quality for music production

### Motherboard

- The **main circuit board** that connects all components together
- Contains the CPU socket, RAM slots, expansion slots, and connectors for storage and peripherals
- Houses the **chipset** that manages data flow between the CPU, memory, and peripherals
- Determines what components are compatible with the system

---

## Embedded Systems

<div class="key-term" markdown="1">
An **embedded system** is a computer system built into a larger device to perform a **dedicated function**. It is not a general-purpose computer — it is designed for one specific task.
</div>

### Characteristics

- **Dedicated purpose** — performs one specific function
- **Built into** a larger device
- Often operates in **real time**
- Usually has **limited resources** (memory, processing power)
- Typically **no user interface** (or a very simple one)
- Often uses **ROM** to store its program (firmware)

### Examples

| Device | Embedded System Function |
|--------|--------------------------|
| Washing machine | Controls water temperature, spin speed, cycle timing |
| Traffic lights | Manages signal timing and sequences |
| Central heating thermostat | Monitors and regulates temperature |
| Car engine management | Controls fuel injection, emissions, engine timing |
| Digital watch | Keeps time, manages alarms and display |
| Smart TV remote | Processes button presses, sends IR/Bluetooth signals |
| Microwave oven | Controls power levels, timing, and safety interlocks |

<div class="exam-tip" markdown="1">
When asked for examples of embedded systems, choose devices that clearly have a **single dedicated purpose**. Explain both what the device is and what the embedded system within it controls.
</div>
