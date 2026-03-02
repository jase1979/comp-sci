---
layout: topic
title: "Hardware"
level: "GCSE"
level_url: "/gcse/"
unit_name: "Unit 1: Understanding Computer Science"
unit_url: "/gcse/unit1/"
next_topic: "/gcse/unit1/logical-operations/"
---

## Architecture: CPU characteristics including Von Neumann

The **Central Processing Unit (CPU)** is the main processor in a computer. It carries out instructions from programs by performing basic arithmetic, logic, control and input/output operations.

Most modern computers are based on the **Von Neumann architecture**, proposed by John von Neumann in 1945. Its key principle is that **data and instructions are stored together in the same memory** and are accessed using the same bus system.

<div class="key-term" markdown="1">
**Von Neumann architecture** — a computer design where program instructions and data share the same memory and bus system. This means only one instruction or data item can be fetched at a time.
</div>

The CPU contains three main components:

- **ALU (Arithmetic Logic Unit)** — performs all arithmetic calculations (add, subtract) and logical comparisons (greater than, equal to, AND, OR, NOT)
- **Control Unit (CU)** — directs the operation of the processor. It fetches instructions from memory, decodes them, and coordinates the ALU, registers and memory to execute them
- **Registers** — tiny, extremely fast storage locations inside the CPU used to hold data and addresses during processing

<svg viewBox="0 0 520 420" xmlns="http://www.w3.org/2000/svg" style="max-width:520px;width:100%;height:auto;display:block;margin:1.2rem auto;">
  <style>
    .box { fill: #1a1d27; stroke: #6c8aff; stroke-width: 1.5; rx: 8; }
    .box-outer { fill: none; stroke: #2d3148; stroke-width: 1.5; rx: 10; }
    .label { fill: #e1e4ed; font-family: -apple-system, sans-serif; text-anchor: middle; }
    .label-sm { fill: #8b90a5; font-family: -apple-system, sans-serif; font-size: 11px; text-anchor: middle; }
    .label-accent { fill: #6c8aff; font-family: -apple-system, sans-serif; font-size: 12px; text-anchor: middle; font-weight: 600; }
    .connector { stroke: #6c8aff; stroke-width: 1.5; fill: none; }
  </style>
  <rect class="box-outer" x="30" y="10" width="460" height="230"/>
  <text class="label" x="260" y="35" font-size="15" font-weight="700">CPU</text>
  <rect class="box" x="55" y="50" width="150" height="60"/>
  <text class="label" x="130" y="76" font-size="13" font-weight="600">Control Unit</text>
  <text class="label-sm" x="130" y="96">(CU)</text>
  <rect class="box" x="235" y="50" width="230" height="60"/>
  <text class="label" x="350" y="76" font-size="13" font-weight="600">Arithmetic Logic Unit</text>
  <text class="label-sm" x="350" y="96">(ALU)</text>
  <line class="connector" x1="130" y1="110" x2="130" y2="145"/>
  <line class="connector" x1="350" y1="110" x2="350" y2="145"/>
  <rect class="box" x="55" y="145" width="410" height="75"/>
  <text class="label-sm" x="260" y="165">Registers</text>
  <rect x="75" y="175" width="60" height="30" rx="5" fill="#242836" stroke="#6c8aff" stroke-width="1"/>
  <text class="label-accent" x="105" y="195">PC</text>
  <rect x="155" y="175" width="60" height="30" rx="5" fill="#242836" stroke="#6c8aff" stroke-width="1"/>
  <text class="label-accent" x="185" y="195">MAR</text>
  <rect x="235" y="175" width="60" height="30" rx="5" fill="#242836" stroke="#6c8aff" stroke-width="1"/>
  <text class="label-accent" x="265" y="195">MDR</text>
  <rect x="315" y="175" width="60" height="30" rx="5" fill="#242836" stroke="#6c8aff" stroke-width="1"/>
  <text class="label-accent" x="345" y="195">ACC</text>
  <rect x="395" y="175" width="55" height="30" rx="5" fill="#242836" stroke="#6c8aff" stroke-width="1"/>
  <text class="label-accent" x="422" y="195">CIR</text>
  <line class="connector" x1="260" y1="240" x2="260" y2="280"/>
  <rect class="box" x="165" y="280" width="190" height="55"/>
  <text class="label" x="260" y="303" font-size="13" font-weight="600">System Bus</text>
  <text class="label-sm" x="260" y="322">Address / Data / Control</text>
  <line class="connector" x1="260" y1="335" x2="260" y2="360"/>
  <rect class="box" x="165" y="360" width="190" height="48"/>
  <text class="label" x="260" y="381" font-size="13" font-weight="600">Main Memory</text>
  <text class="label-sm" x="260" y="398">RAM / ROM</text>
</svg>

---

## Components of CPU in fetch-decode-execute cycle

The CPU continuously repeats three steps to process every instruction:

### Registers involved

| Register | Full Name | Purpose |
|----------|-----------|---------|
| **PC** | Program Counter | Holds the address of the **next** instruction to be fetched |
| **MAR** | Memory Address Register | Holds the address of the memory location being read from or written to |
| **MDR** | Memory Data Register | Holds the data that has been fetched from memory or is about to be written to memory |
| **ACC** | Accumulator | Stores the result of calculations performed by the ALU |
| **CIR** | Current Instruction Register | Holds the instruction currently being decoded and executed |

### The cycle

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

## Performance factors: Cache size, clock speed, number of cores

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

## Difference between RISC and CISC processors

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

## Input/output: Use and characteristics of I/O devices

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
| Sensor | Detecting physical conditions (temperature, pressure, light, motion) | Used in control systems and IoT, provides real-time data, requires ADC to convert analogue readings to digital |

### Common Output Devices

| Device | Use | Characteristics |
|--------|-----|-----------------|
| Monitor | Displaying visual output | High resolution, various sizes |
| Printer | Producing hard copies | Permanent output, slow, costs per page |
| Speaker | Audio output | Range of quality, requires amplification |
| Projector | Large-screen display | Good for presentations, needs dark room |
| Actuator | Converts electrical signals into physical movement | Used in control systems (motors, valves, servos), essential for robotics and embedded systems |

---

## Primary storage: RAM, ROM, flash memory, cache memory

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

## Secondary storage: Magnetic, optical and solid state technologies

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

---

## Functional characteristics: Suitability, durability, portability, speed

When choosing storage, consider these characteristics:

| Feature | HDD | SSD | Optical | Magnetic Tape |
|---------|-----|-----|---------|---------------|
| Speed | Medium | Fast | Slow | Very slow |
| Capacity | Very high | High | Low | Very high |
| Cost per GB | Low | Medium | Very low | Very low |
| Durability | Fragile (moving parts) | Durable | Scratches easily | Durable |
| Portability | Low | High | High | Low |
| Best for | Desktop storage | OS drive, laptops | Software distribution | Backups, archives |

<div class="exam-tip" markdown="1">
Questions often ask you to **recommend** a storage device for a scenario. Match the characteristics to the requirements — e.g. a photographer on location needs portability and durability (SSD or SD card), while a company archiving old records needs high capacity and low cost (magnetic tape).
</div>

---

## Storage requirements: Bit, nybble, byte, kilobyte, prefix multipliers

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

---

## Data capacity and calculating data capacity requirements

### Image file size

```
File size = Width (px) × Height (px) × Colour depth (bits)
```

- **Colour depth** is the number of bits per pixel (e.g. 24-bit colour = 16.7 million colours)
- A 1920×1080 image at 24-bit colour: `1920 × 1080 × 24 = 49,766,400 bits ≈ 5.93 MB`

### Sound file size

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

## Other hardware: GPU, sound cards, motherboards

### GPU (Graphics Processing Unit)

- Specialised processor designed for **rendering images and video**
- Contains thousands of small cores optimised for **parallel processing**
- Used for gaming, video editing, 3D modelling, and increasingly for AI workloads
- Can be integrated (built into CPU) or dedicated (separate card)

### Sound Card

- Processes **audio input and output**
- Contains a **DAC (Digital-to-Analogue Converter)** which converts digital data into analogue signals for speakers and headphones
- Contains an **ADC (Analogue-to-Digital Converter)** which converts analogue signals from microphones into digital data the computer can process
- Built-in sound is sufficient for most users; dedicated cards offer higher quality for music production

### Motherboard

- The **main circuit board** that connects all components together
- Contains the CPU socket, RAM slots, expansion slots, and connectors for storage and peripherals
- Houses the **chipset** that manages data flow between the CPU, memory, and peripherals
- Determines what components are compatible with the system

---

## Embedded systems: Use and examples

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
