---
layout: topic
title: "Hardware & Communication"
level: "AS Level"
level_url: "/as/"
unit_name: "Unit 1: Fundamentals of Computer Science"
unit_url: "/as/unit1/"
next_topic: "/as/unit1/logical-operations/"
---

## Identify and Describe Hardware and Communication Elements of Computer Systems

A computer system is made up of **hardware** (physical components) and **software** (programs and data). The hardware elements can be broadly categorised into processing components, memory, input/output devices, secondary storage, and communication devices.

<div class="key-term" markdown="1">
**Hardware** refers to the physical, tangible components of a computer system -- the parts you can touch. **Software** refers to the programs and data that instruct the hardware what to do.
</div>

The major hardware subsystems include:

| Subsystem | Purpose | Examples |
|---|---|---|
| **Processor (CPU)** | Fetches, decodes and executes instructions | Intel Core i7, ARM Cortex |
| **Main memory** | Stores data and instructions currently in use | RAM, ROM |
| **Secondary storage** | Long-term, non-volatile data storage | HDD, SSD, optical disc |
| **Input devices** | Allow data to enter the system | Keyboard, mouse, scanner |
| **Output devices** | Present processed data to the user | Monitor, printer, speakers |
| **Communication devices** | Enable data transfer between systems | Network interface card, router, modem |
| **Buses** | Internal pathways that carry data between components | Data bus, address bus, control bus |

Communication elements include the **network interface card (NIC)** which connects a device to a network, **routers** which direct traffic between networks, **switches** which connect devices within a local network, and **modems** which convert between digital and analogue signals.

```python
# Simulating identification of hardware components
hardware = {
    "CPU": "Processing",
    "RAM": "Primary Memory",
    "SSD": "Secondary Storage",
    "Keyboard": "Input",
    "Monitor": "Output",
    "NIC": "Communication"
}

for device, category in hardware.items():
    print(f"{device} -> {category}")
```

```vb
' Simulating identification of hardware components
Module HardwareDemo
    Sub Main()
        Dim hardware As New Dictionary(Of String, String) From {
            {"CPU", "Processing"},
            {"RAM", "Primary Memory"},
            {"SSD", "Secondary Storage"},
            {"Keyboard", "Input"},
            {"Monitor", "Output"},
            {"NIC", "Communication"}
        }

        For Each item In hardware
            Console.WriteLine($"{item.Key} -> {item.Value}")
        Next
    End Sub
End Module
```

---

## Architecture: Main Components Including Von Neumann Architectures

### Von Neumann Architecture

The **Von Neumann architecture** is the foundation of most modern general-purpose computers. Proposed by John von Neumann in 1945, it is based on the **stored program concept** -- both instructions and data are stored together in the same main memory and are accessed via the same bus system.

<div class="key-term" markdown="1">
The **stored program concept** states that instructions (the program) and data are stored together in main memory. Instructions are fetched and executed sequentially unless a branch instruction is encountered.
</div>

The main components of a Von Neumann system are:

**The Central Processing Unit (CPU)** contains:

- **Arithmetic Logic Unit (ALU):** Performs all arithmetic operations (addition, subtraction, multiplication, division) and logical comparisons (AND, OR, NOT, XOR). It receives operands from registers and sends results back.
- **Control Unit (CU):** Coordinates and manages the operation of the entire computer. It fetches instructions from memory, decodes them to determine the operation, and generates control signals to direct other components. It controls the timing of operations using a clock signal.
- **Registers:** Small, extremely fast storage locations within the CPU. Key registers include:

| Register | Full Name | Purpose |
|---|---|---|
| **PC** | Program Counter | Holds the address of the next instruction to be fetched |
| **MAR** | Memory Address Register | Holds the address of the memory location about to be read from or written to |
| **MDR/MBR** | Memory Data Register / Memory Buffer Register | Holds the data that has just been read from or is about to be written to memory |
| **CIR** | Current Instruction Register | Holds the instruction currently being decoded and executed |
| **ACC** | Accumulator | Holds intermediate results of calculations performed by the ALU |

**The Bus System** connects the CPU to main memory and I/O controllers:

- **Data Bus:** Carries data between the CPU, memory and I/O devices. It is **bidirectional** (data flows in both directions).
- **Address Bus:** Carries memory addresses from the CPU to memory. It is **unidirectional** (the CPU sends addresses; memory receives them). The width of the address bus determines the maximum addressable memory (e.g., a 32-bit address bus can address 2^32 = 4 GB of memory).
- **Control Bus:** Carries control signals such as read/write, clock pulses, interrupt requests, and bus request/grant signals. Individual lines are unidirectional but the bus as a whole is bidirectional.

### Harvard Architecture

An alternative is the **Harvard architecture**, which uses **separate memory and buses** for instructions and data. This allows instructions and data to be fetched simultaneously, improving throughput. Harvard architecture is commonly used in embedded systems, microcontrollers, and digital signal processors (DSPs).

| Feature | Von Neumann | Harvard |
|---|---|---|
| Memory | Single memory for instructions and data | Separate memories for instructions and data |
| Buses | Shared bus system | Separate bus systems |
| Speed | Slower (bus bottleneck) | Faster (simultaneous access) |
| Flexibility | Programs can modify themselves | Instructions and data strictly separated |
| Usage | General-purpose computers | Embedded systems, DSPs, microcontrollers |

<div class="exam-tip" markdown="1">
The **Von Neumann bottleneck** is the limitation caused by having a single bus system shared between instructions and data. This means the CPU cannot fetch an instruction and read/write data at the same time. Harvard architecture avoids this bottleneck.
</div>

### CISC vs RISC

- **CISC (Complex Instruction Set Computer):** Has a large set of complex instructions, where a single instruction can perform multiple low-level operations. Requires fewer lines of assembly code but each instruction takes more clock cycles. Used in desktop/laptop processors (Intel x86, AMD).
- **RISC (Reduced Instruction Set Computer):** Has a smaller set of simple instructions, each executing in a single clock cycle. Requires more lines of assembly code but achieves high throughput through pipelining. Used in mobile devices and embedded systems (ARM).

---

## Different Types of Memory and Caching

### Primary Memory

Primary memory is directly accessible by the CPU and is essential for the system to operate.

**RAM (Random Access Memory):**
- **Volatile** -- loses its contents when power is switched off
- Stores the currently running programs and data the CPU needs
- Can be read from and written to
- Two main types:
  - **DRAM (Dynamic RAM):** Must be constantly refreshed; cheaper and denser; used for main memory
  - **SRAM (Static RAM):** Does not need refreshing; faster but more expensive; used for cache memory

**ROM (Read Only Memory):**
- **Non-volatile** -- retains its contents when power is switched off
- Stores the boot-up instructions (BIOS/UEFI) that initialise the hardware when the computer is first switched on
- Contents are typically written during manufacture and cannot be easily modified
- Variants include PROM (programmable once), EPROM (erasable with UV light), and EEPROM/Flash (electrically erasable)

<div class="key-term" markdown="1">
**Volatile** memory loses its contents when the power supply is removed. **Non-volatile** memory retains its contents without power.
</div>

### Cache Memory

**Cache** is a small amount of very fast SRAM located on or near the CPU. It stores copies of frequently and recently accessed data and instructions from main memory, reducing the time the CPU spends waiting for data.

Cache operates on the **principle of locality:**

- **Temporal locality:** Data accessed recently is likely to be accessed again soon
- **Spatial locality:** Data stored near recently accessed data is likely to be needed soon

Modern CPUs typically have multiple levels of cache:

| Level | Size | Speed | Location |
|---|---|---|---|
| **L1** | 32-64 KB per core | Fastest | Built into CPU core |
| **L2** | 256 KB - 1 MB per core | Fast | On the CPU die, per core |
| **L3** | 4-64 MB shared | Slower than L1/L2 | On the CPU die, shared between cores |

When the CPU requests data, it checks L1 first, then L2, then L3, then main memory. A **cache hit** occurs when the data is found in cache; a **cache miss** occurs when it must be fetched from slower main memory.

```python
# Simulating cache lookup behaviour
cache = {"addr_100": 42, "addr_200": 17, "addr_300": 89}

def fetch_data(address, cache, main_memory):
    if address in cache:
        print(f"Cache HIT for {address}: {cache[address]}")
        return cache[address]
    else:
        print(f"Cache MISS for {address} - fetching from main memory")
        value = main_memory.get(address, 0)
        cache[address] = value  # Store in cache for next time
        return value

main_memory = {"addr_100": 42, "addr_200": 17, "addr_300": 89, "addr_400": 55}
fetch_data("addr_400", cache, main_memory)
fetch_data("addr_100", cache, main_memory)
```

```vb
' Simulating cache lookup behaviour
Module CacheDemo
    Dim cache As New Dictionary(Of String, Integer) From {
        {"addr_100", 42}, {"addr_200", 17}, {"addr_300", 89}
    }

    Function FetchData(address As String, mainMemory As Dictionary(Of String, Integer)) As Integer
        If cache.ContainsKey(address) Then
            Console.WriteLine($"Cache HIT for {address}: {cache(address)}")
            Return cache(address)
        Else
            Console.WriteLine($"Cache MISS for {address} - fetching from main memory")
            Dim value As Integer = mainMemory(address)
            cache(address) = value
            Return value
        End If
    End Function

    Sub Main()
        Dim mainMemory As New Dictionary(Of String, Integer) From {
            {"addr_100", 42}, {"addr_200", 17}, {"addr_300", 89}, {"addr_400", 55}
        }
        FetchData("addr_400", mainMemory)
        FetchData("addr_100", mainMemory)
    End Sub
End Module
```

<div class="exam-tip" markdown="1">
Remember the memory hierarchy from fastest/smallest/most expensive to slowest/largest/cheapest: **Registers > L1 Cache > L2 Cache > L3 Cache > RAM > Secondary Storage**. Each level acts as a buffer for the level below it.
</div>

---

## Parallel Processing

Traditional Von Neumann processors execute instructions sequentially, one at a time. **Parallel processing** improves performance by executing multiple instructions or tasks simultaneously.

### Forms of Parallel Processing

**Pipelining:** The fetch-decode-execute cycle is broken into stages, and multiple instructions are in different stages at the same time (like a factory assembly line). While one instruction is being executed, the next is being decoded, and a third is being fetched.

**Multi-core processing:** A CPU contains multiple independent processing cores, each capable of executing its own instruction stream. A quad-core processor can theoretically execute four instructions simultaneously.

**Multi-processor systems:** Multiple separate CPUs work together on a shared task, connected via a high-speed interconnect.

**GPU computing:** Graphics Processing Units contain thousands of small cores optimised for performing the same operation on many data items simultaneously (SIMD -- Single Instruction, Multiple Data). Used for graphics rendering, machine learning and scientific computing.

| Approach | Description | Best For |
|---|---|---|
| Pipelining | Overlapping stages of different instructions | General instruction throughput |
| Multi-core | Multiple independent cores on one chip | Multitasking, threaded applications |
| GPU computing | Thousands of simple cores | Massively parallel data-level tasks |

<div class="key-term" markdown="1">
**Parallel processing** is the simultaneous execution of multiple instructions or tasks. It can be achieved through pipelining, multiple cores, multiple processors, or GPU computing.
</div>

Not all tasks benefit equally from parallelism. **Amdahl's Law** states that the speedup from parallelism is limited by the fraction of the task that must be performed sequentially. If 25% of a task is sequential, no amount of parallelism can give more than a 4x speedup.

```python
# Demonstrating the concept of parallel vs sequential execution time
import time

# Sequential processing simulation
def sequential_tasks(tasks):
    results = []
    for task in tasks:
        results.append(task * 2)  # Simulate processing
    return results

# In real parallel processing, these would run on separate cores
tasks = list(range(1, 9))
results = sequential_tasks(tasks)
print(f"Tasks: {tasks}")
print(f"Results: {results}")
print(f"Sequential: {len(tasks)} steps")
print(f"Parallel (4 cores): {len(tasks) // 4} steps")
```

```vb
' Demonstrating the concept of parallel vs sequential execution time
Module ParallelDemo
    Sub Main()
        Dim tasks() As Integer = {1, 2, 3, 4, 5, 6, 7, 8}
        Dim results(tasks.Length - 1) As Integer

        ' Sequential processing simulation
        For i As Integer = 0 To tasks.Length - 1
            results(i) = tasks(i) * 2
        Next

        Console.WriteLine("Tasks: " & String.Join(", ", tasks))
        Console.WriteLine("Results: " & String.Join(", ", results))
        Console.WriteLine($"Sequential: {tasks.Length} steps")
        Console.WriteLine($"Parallel (4 cores): {tasks.Length \ 4} steps")
    End Sub
End Module
```

---

## Fetch-Execute Cycle: How Data Is Read from RAM into Registers

The **fetch-decode-execute cycle** (also called the fetch-execute cycle or instruction cycle) is the fundamental process by which the CPU processes each instruction. It repeats continuously from the moment the computer is switched on until it is shut down.

### The Stages in Detail

**1. Fetch:**
1. The **Program Counter (PC)** holds the address of the next instruction to fetch.
2. The contents of the PC are copied to the **Memory Address Register (MAR)**.
3. The PC is incremented by 1, so it now points to the next instruction.
4. The address in the MAR is sent along the **address bus** to main memory.
5. A **read** signal is sent along the **control bus**.
6. The data at that memory location is sent along the **data bus** to the **Memory Data Register (MDR)**.
7. The contents of the MDR are copied to the **Current Instruction Register (CIR)**.

**2. Decode:**
1. The control unit examines the instruction in the CIR.
2. The instruction is split into the **opcode** (the operation to perform) and the **operand** (the data or address the operation acts on).
3. The control unit determines what signals need to be sent and to which components.

**3. Execute:**
1. The appropriate operation is carried out. This may involve:
   - Performing an arithmetic or logical calculation in the **ALU**
   - Loading data from memory into a register
   - Storing data from a register to memory
   - Changing the PC to a different address (a branch/jump instruction)

<div class="key-term" markdown="1">
The **fetch-decode-execute cycle** is the continuous process by which the CPU fetches an instruction from memory, decodes it to understand what operation is required, and then executes the operation.
</div>

### Interrupts

An **interrupt** is a signal sent to the CPU that requires immediate attention. At the end of each fetch-decode-execute cycle, the CPU checks for interrupts. If an interrupt is detected:

1. The CPU saves its current state (registers, PC) onto the **stack**.
2. The CPU loads the address of the appropriate **Interrupt Service Routine (ISR)** into the PC.
3. The ISR is executed to handle the interrupt.
4. Once complete, the CPU restores its previous state from the stack and resumes the original program.

Examples of interrupts include: a key being pressed, a hardware error, a timer expiring, or I/O completion.

<div class="exam-tip" markdown="1">
Be prepared to trace through the fetch-decode-execute cycle step by step, naming the registers and buses involved at each stage. Questions often ask you to describe how a specific instruction (such as "LOAD 50") would be processed.
</div>

---

## Input/Output: Contemporary Methods and Devices

### Contemporary Input Devices

| Device | Method of Input | Typical Use |
|---|---|---|
| **Touchscreen** | Capacitive or resistive sensor detects finger contact | Smartphones, tablets, kiosks |
| **Digital camera/webcam** | Light is captured by a CCD/CMOS sensor and converted to digital data | Photography, video calls |
| **Microphone** | Sound waves converted to electrical signals then digitised by an ADC | Voice input, recording |
| **Barcode/QR scanner** | Laser or camera reads patterns of light and dark | Retail, logistics |
| **Biometric scanner** | Reads unique biological characteristics (fingerprint, iris, face) | Security authentication |
| **RFID/NFC reader** | Radio waves read data from an RFID tag | Contactless payments, access control |
| **Sensor (temperature, pressure, light)** | Converts physical quantities into electrical signals | Monitoring systems, IoT |

### Contemporary Output Devices

| Device | Method of Output | Typical Use |
|---|---|---|
| **LCD/OLED monitor** | Pixels emit or filter light to display images | Desktop computing, smartphones |
| **Laser/inkjet printer** | Toner or ink deposited onto paper | Document printing |
| **3D printer** | Layers of material built up to create a physical object | Prototyping, manufacturing |
| **Speakers/headphones** | Electrical signals converted to sound waves by a DAC and driver | Audio output |
| **Actuator** | Converts electrical signals into physical movement | Robotics, control systems |
| **Projector** | Light projected through or reflected off a display element | Presentations, cinema |

<div class="key-term" markdown="1">
An **ADC (Analogue-to-Digital Converter)** converts continuous analogue signals into discrete digital data. A **DAC (Digital-to-Analogue Converter)** does the reverse. These are essential for interfacing between the analogue real world and digital computers.
</div>

---

## Suitability of I/O Methods in Different Situations

Choosing the right I/O device depends on the **context** of the application:

| Situation | Suitable I/O | Reason |
|---|---|---|
| **Supermarket checkout** | Barcode scanner (input), receipt printer (output) | Fast item identification; printed record for customer |
| **Disabled user** | Voice recognition (input), screen reader (output) | Allows hands-free interaction with the system |
| **Warehouse inventory** | RFID reader (input), handheld display (output) | Bulk scanning without line-of-sight; portable display |
| **Hospital patient monitoring** | Sensors (input), monitor display and alarm (output) | Continuous automatic data collection; immediate alerts |
| **Graphic design studio** | Graphics tablet (input), high-resolution monitor (output) | Precise drawing input; accurate colour output |
| **ATM machine** | Touchscreen and card reader (input), screen and cash dispenser (output) | User-friendly interface; secure transaction |

Factors to consider when selecting I/O methods:

- **Speed:** How quickly must data be entered or presented?
- **Accuracy:** How precise does the input/output need to be?
- **Volume of data:** Is it a single item or thousands?
- **Environment:** Is it indoors, outdoors, noisy, or hazardous?
- **User capability:** Does the user have physical limitations?
- **Cost:** Is the investment justified for the application?
- **Automation:** Should the process be manual or automatic?

<div class="exam-tip" markdown="1">
In exam questions about I/O suitability, always link the **characteristics of the device** to the **specific requirements of the situation**. Do not just name a device -- explain *why* it is appropriate.
</div>

---

## Secondary Storage: Functional Characteristics of Storage Devices

Secondary storage is **non-volatile** storage used to hold data and programs long-term, even when the computer is switched off. There are three main types.

### Magnetic Storage (e.g., Hard Disk Drive -- HDD)

- Data is stored as magnetic patterns on rotating metal platters
- A read/write head moves across the spinning platters to access data
- **Capacity:** Very high (up to several terabytes)
- **Speed:** Moderate (limited by physical spinning and head movement -- typical 5400-7200 RPM)
- **Cost:** Low cost per gigabyte
- **Durability:** Susceptible to damage from physical shock (moving parts)
- **Best for:** Bulk storage, file servers, backups where cost and capacity matter more than speed

### Solid-State Storage (e.g., SSD, USB Flash Drive)

- Data is stored in NAND flash memory chips using electrical charges in floating-gate transistors
- No moving parts
- **Capacity:** Moderate to high (up to several terabytes for SSDs)
- **Speed:** Very fast (no mechanical latency; near-instant access times)
- **Cost:** Higher cost per gigabyte than magnetic
- **Durability:** Very robust -- resistant to shock and vibration
- **Lifespan:** Limited number of write cycles per cell (though modern SSDs have wear-levelling algorithms)
- **Best for:** Operating system drives, laptops, portable storage, any application needing fast access

### Optical Storage (e.g., CD, DVD, Blu-ray)

- Data is stored as pits and lands on a reflective disc surface, read by a laser
- **Capacity:** Low to moderate (CD: 700 MB; DVD: 4.7 GB; Blu-ray: 25-50 GB)
- **Speed:** Slow compared to HDD and SSD
- **Cost:** Very cheap per disc
- **Durability:** Resistant to magnetic interference but can be scratched
- **Best for:** Software distribution, media playback, archival storage

| Feature | HDD | SSD | Optical |
|---|---|---|---|
| **Capacity** | Very high | High | Low-Moderate |
| **Speed** | Moderate | Very fast | Slow |
| **Cost per GB** | Low | Medium | Very low |
| **Durability** | Low (moving parts) | High | Moderate |
| **Portability** | Low | High | High |
| **Power usage** | Higher | Lower | Low |

<div class="key-term" markdown="1">
**Secondary storage** is non-volatile storage used for the long-term retention of data and programs. Unlike primary memory (RAM), it retains data when the computer is powered off.
</div>

---

## Data Storage on Disc: Fragmentation and Defragmentation

### How Data Is Stored on a Magnetic Disc

A hard disk platter is divided into concentric **tracks**, which are further divided into **sectors**. A group of sectors is called a **cluster** (or allocation unit), and this is the smallest unit of storage the operating system can manage.

When a file is saved, the operating system allocates enough clusters to hold it. Ideally, the clusters are **contiguous** (next to each other), allowing the read/write head to read the file sequentially without moving.

### Fragmentation

**Fragmentation** occurs when files are stored in non-contiguous clusters scattered across the disk. This happens over time as files are created, modified, resized, and deleted, leaving gaps between occupied clusters.

Effects of fragmentation:

- The read/write head must move to multiple locations to read a single file
- This increases **seek time** (the time taken for the head to move to the correct track)
- Overall system performance degrades as file access becomes slower
- More mechanical wear on the drive

### Defragmentation

**Defragmentation** is the process of reorganising the data on a disk so that files are stored in contiguous clusters.

- The defragmentation tool reads fragmented files and rewrites them in consecutive sectors
- Free space is consolidated into larger contiguous blocks
- After defragmentation, file access is faster because the head moves less
- Defragmentation should be performed periodically on HDDs

<div class="exam-tip" markdown="1">
**SSDs should NOT be defragmented.** Because SSDs have no moving read/write head, fragmentation does not affect their access times. Defragmenting an SSD wastes write cycles and reduces its lifespan. SSDs use a different optimisation called **TRIM** instead.
</div>

```python
# Simulating fragmentation on a disk
disk = [None] * 20  # 20 empty clusters

# Write file A (4 clusters)
for i in range(4):
    disk[i] = "A"

# Write file B (3 clusters)
for i in range(4, 7):
    disk[i] = "B"

# Delete file A - leaves a gap
for i in range(4):
    disk[i] = None

# Write file C (6 clusters) - has to split across the gap and end
cluster_index = 0
clusters_needed = 6
for i in range(len(disk)):
    if clusters_needed == 0:
        break
    if disk[i] is None:
        disk[i] = "C"
        clusters_needed -= 1

print("Fragmented disk:", disk)
# File C is split: some before B, some after B = fragmented
```

```vb
' Simulating fragmentation on a disk
Module FragmentationDemo
    Sub Main()
        Dim disk(19) As String  ' 20 empty clusters

        ' Write file A (4 clusters)
        For i As Integer = 0 To 3
            disk(i) = "A"
        Next

        ' Write file B (3 clusters)
        For i As Integer = 4 To 6
            disk(i) = "B"
        Next

        ' Delete file A - leaves a gap
        For i As Integer = 0 To 3
            disk(i) = Nothing
        Next

        ' Write file C (6 clusters) - has to split across the gap and end
        Dim clustersNeeded As Integer = 6
        For i As Integer = 0 To disk.Length - 1
            If clustersNeeded = 0 Then Exit For
            If disk(i) Is Nothing Then
                disk(i) = "C"
                clustersNeeded -= 1
            End If
        Next

        Console.Write("Fragmented disk: ")
        For Each slot In disk
            Console.Write(If(slot, "_") & " ")
        Next
        Console.WriteLine()
    End Sub
End Module
```

---

## Networking: How Networks Communicate

### Types of Network

**LAN (Local Area Network):**
- Covers a small geographical area (single building or campus)
- Hardware is typically owned and managed by the organisation
- High data transfer speeds (typically 100 Mbps to 10 Gbps)
- Connected using Ethernet cables, switches, and wireless access points

**WAN (Wide Area Network):**
- Covers a large geographical area (cities, countries, or the world)
- Uses third-party communication links (leased lines, telephone networks, satellite links)
- Lower data transfer speeds than LAN (varies widely)
- The Internet is the largest WAN

**Other network types:**
- **MAN (Metropolitan Area Network):** Spans a city or large campus
- **PAN (Personal Area Network):** Very short range, connecting personal devices (e.g., Bluetooth)
- **WLAN (Wireless LAN):** A LAN using Wi-Fi instead of cables

### Network Topologies

A **topology** describes how devices (nodes) in a network are arranged and connected.

**Star topology:**
- All devices connect to a central switch or hub
- If one device fails, the rest of the network is unaffected
- If the central switch fails, the entire network goes down
- Easy to add new devices
- Most common topology in modern LANs

**Bus topology:**
- All devices share a single backbone cable (the bus)
- Data travels in both directions along the bus
- If the backbone cable fails, the entire network goes down
- Prone to collisions as all devices share the medium
- Cheap to install but difficult to troubleshoot

**Ring topology:**
- Devices are connected in a circular loop
- Data travels in one direction around the ring
- Each device receives data and passes it to the next
- A break in the ring can disable the whole network (unless a dual ring is used)

**Mesh topology:**
- Every device is connected to every other device (full mesh) or to several devices (partial mesh)
- Very resilient -- multiple paths between devices
- Expensive due to the number of connections required
- Used in critical infrastructure (e.g., the Internet backbone)

<div class="key-term" markdown="1">
A **network topology** describes the physical or logical arrangement of devices in a network. The choice of topology affects performance, fault tolerance, and cost.
</div>

### Client-Server vs Peer-to-Peer

**Client-server model:**
- A central server provides services (file storage, authentication, email) to client devices
- Easier to manage, back up, and secure centrally
- Server failure disrupts the entire network
- Used in most business environments

**Peer-to-peer model:**
- All devices are equal and share resources directly with each other
- No central server required
- Harder to manage security and backups
- Used in small home networks and file-sharing applications

---

## Importance of Networking Standards

**Networking standards** are agreed-upon rules and specifications that ensure devices from different manufacturers can communicate with each other. Without standards, a computer from one manufacturer would not be able to communicate with a printer from another.

Key reasons standards are important:

- **Interoperability:** Devices from different vendors can work together on the same network
- **Competition:** Multiple manufacturers can produce compatible products, driving innovation and lowering prices
- **Reliability:** Standardised protocols are thoroughly tested and widely understood
- **Scalability:** Networks can grow by adding any standards-compliant device

Important standards bodies include:

| Organisation | Role |
|---|---|
| **IEEE (Institute of Electrical and Electronics Engineers)** | Defines standards such as IEEE 802.3 (Ethernet) and IEEE 802.11 (Wi-Fi) |
| **IETF (Internet Engineering Task Force)** | Develops and maintains Internet protocols (TCP/IP, HTTP) through RFCs |
| **ISO (International Organization for Standardization)** | Developed the OSI 7-layer reference model |
| **W3C (World Wide Web Consortium)** | Develops web standards (HTML, CSS, HTTP) |

<div class="exam-tip" markdown="1">
If asked why standards are important, focus on **interoperability** (devices can communicate regardless of manufacturer) and **competition** (consumers benefit from choice and lower prices because vendors must all follow the same rules).
</div>

---

## Protocols: HTTP, FTP, SMTP, TCP/IP, IMAP, DHCP, UDP, Wireless

A **protocol** is a set of rules that governs how data is formatted, transmitted, and received over a network. Different protocols serve different purposes.

### The TCP/IP Protocol Suite

The **TCP/IP model** is the layered model that underpins the Internet. It has four layers:

| Layer | Purpose | Example Protocols |
|---|---|---|
| **Application** | Provides network services to user applications | HTTP, FTP, SMTP, IMAP, DHCP, DNS |
| **Transport** | Provides reliable or unreliable end-to-end data delivery | TCP, UDP |
| **Internet** | Handles addressing and routing of packets across networks | IP (IPv4, IPv6) |
| **Network Access** | Handles physical transmission of data over the network medium | Ethernet, Wi-Fi |

### Key Protocols Explained

**HTTP (HyperText Transfer Protocol):**
- Used by web browsers to request and receive web pages from web servers
- Uses a request-response model (client sends a request, server sends a response)
- **HTTPS** adds encryption using TLS/SSL for secure communication
- Uses TCP port 80 (HTTP) or 443 (HTTPS)

**FTP (File Transfer Protocol):**
- Used to transfer files between a client and a server
- Supports uploading and downloading files, directory listing, renaming and deleting
- Uses two connections: a control connection (port 21) and a data connection (port 20)
- Credentials are sent in plain text (SFTP or FTPS should be used for security)

**SMTP (Simple Mail Transfer Protocol):**
- Used to **send** emails from a client to a mail server or between mail servers
- Uses TCP port 25 (or 587 for authenticated submission)
- Only handles sending -- not retrieving email

**IMAP (Internet Message Access Protocol):**
- Used to **retrieve** emails from a mail server
- Emails remain on the server and can be accessed from multiple devices
- Supports folders, search, and partial message download
- Uses TCP port 143 (or 993 with encryption)
- Alternative: POP3 (downloads emails and typically deletes them from the server)

**TCP (Transmission Control Protocol):**
- A **connection-oriented** transport protocol
- Guarantees delivery, correct ordering, and error checking
- Uses a three-way handshake (SYN, SYN-ACK, ACK) to establish a connection
- Slower than UDP due to overhead
- Used when reliability is essential: web browsing, email, file transfer

**UDP (User Datagram Protocol):**
- A **connectionless** transport protocol
- Does NOT guarantee delivery, ordering, or error correction
- Much faster and lower overhead than TCP
- Used when speed matters more than reliability: live video/audio streaming, online gaming, DNS queries, VoIP

| Feature | TCP | UDP |
|---|---|---|
| Connection | Connection-oriented | Connectionless |
| Reliability | Guaranteed delivery | No guarantee |
| Ordering | Maintains order | No ordering |
| Speed | Slower (overhead) | Faster |
| Error checking | Yes, with retransmission | Basic checksum only |
| Use cases | Web, email, file transfer | Streaming, gaming, DNS |

**DHCP (Dynamic Host Configuration Protocol):**
- Automatically assigns IP addresses and other network configuration to devices when they join a network
- Eliminates the need for manual IP configuration
- A DHCP server maintains a pool of available addresses
- Addresses are leased for a set period and can be renewed

**Wireless Protocols (IEEE 802.11 / Wi-Fi):**
- Define how wireless devices communicate over radio frequencies
- Different standards offer different speeds and ranges (e.g., 802.11ac, 802.11ax/Wi-Fi 6)
- Use CSMA/CA (Carrier Sense Multiple Access with Collision Avoidance) to manage access to the shared wireless medium
- Security protocols: WPA2, WPA3 for encryption and authentication

<div class="key-term" markdown="1">
A **protocol** is a standardised set of rules governing the format, timing, and error handling of data communication between devices on a network.
</div>

```python
# Demonstrating a simple HTTP request concept
# In practice you would use the requests library
protocol_ports = {
    "HTTP": 80,
    "HTTPS": 443,
    "FTP": 21,
    "SMTP": 25,
    "IMAP": 143,
    "DHCP": 67,
    "DNS": 53
}

for protocol, port in protocol_ports.items():
    print(f"{protocol} uses port {port}")

# Choosing TCP vs UDP
def choose_protocol(application):
    unreliable_ok = ["streaming", "gaming", "VoIP", "DNS"]
    if application in unreliable_ok:
        return "UDP (speed over reliability)"
    else:
        return "TCP (reliability required)"

print(choose_protocol("email"))       # TCP
print(choose_protocol("streaming"))   # UDP
```

```vb
' Demonstrating protocol port numbers and TCP vs UDP selection
Module ProtocolDemo
    Sub Main()
        Dim protocolPorts As New Dictionary(Of String, Integer) From {
            {"HTTP", 80}, {"HTTPS", 443}, {"FTP", 21},
            {"SMTP", 25}, {"IMAP", 143}, {"DHCP", 67}, {"DNS", 53}
        }

        For Each item In protocolPorts
            Console.WriteLine($"{item.Key} uses port {item.Value}")
        Next

        Console.WriteLine(ChooseProtocol("email"))
        Console.WriteLine(ChooseProtocol("streaming"))
    End Sub

    Function ChooseProtocol(application As String) As String
        Dim unreliableOk() As String = {"streaming", "gaming", "VoIP", "DNS"}
        If unreliableOk.Contains(application) Then
            Return "UDP (speed over reliability)"
        Else
            Return "TCP (reliability required)"
        End If
    End Function
End Module
```

---

## Role of Handshaking

**Handshaking** is the automated process of negotiation between two devices before data transfer begins. It establishes the parameters of the communication channel so both sides can communicate successfully.

### The TCP Three-Way Handshake

The most important example at AS Level is the TCP three-way handshake, used to establish a reliable connection:

1. **SYN (Synchronise):** The client sends a SYN packet to the server, requesting a connection. It includes an initial sequence number.
2. **SYN-ACK (Synchronise-Acknowledge):** The server responds with a SYN-ACK packet, acknowledging the client's request and sending its own sequence number.
3. **ACK (Acknowledge):** The client sends an ACK packet back to the server, confirming the connection is established.

After this three-way handshake, data transfer can begin. When the communication is finished, a similar process (FIN, FIN-ACK, ACK) is used to close the connection gracefully.

### What Handshaking Establishes

- Both devices confirm they are ready to communicate
- The **transmission speed** (baud rate) is agreed upon
- **Error-checking method** to be used
- **Packet size** and format
- **Sequence numbers** for ordering packets
- **Flow control** parameters to prevent the sender from overwhelming the receiver

<div class="key-term" markdown="1">
**Handshaking** is the exchange of control signals between two devices to establish the rules and parameters of a communication session before any data is transmitted.
</div>

<div class="exam-tip" markdown="1">
Remember that handshaking happens **before** data is sent. It ensures both devices agree on how the communication will proceed. The TCP three-way handshake (SYN, SYN-ACK, ACK) is the most commonly examined example.
</div>

---

## The Internet as a World-Wide Communications Infrastructure

### What Is the Internet?

The **Internet** is a global network of interconnected networks. It is not a single network but a vast infrastructure that connects millions of private, public, academic, and government networks using the TCP/IP protocol suite.

<div class="key-term" markdown="1">
The **Internet** is a global interconnected network of networks that uses TCP/IP to communicate. The **World Wide Web (WWW)** is a service that runs on top of the Internet, using HTTP to deliver web pages -- it is NOT the same as the Internet.
</div>

### Key Components of the Internet Infrastructure

- **Backbone:** High-capacity fibre-optic cables (often undersea) that carry the majority of Internet traffic between continents and countries
- **Internet Service Providers (ISPs):** Companies that provide access to the Internet for homes and businesses. They connect to the backbone and to each other at Internet Exchange Points (IXPs)
- **Routers:** Direct packets across the Internet, choosing the best path from source to destination
- **DNS (Domain Name System):** Translates human-readable domain names (e.g., www.example.com) into IP addresses (e.g., 93.184.216.34). DNS servers form a distributed hierarchical database
- **IP Addressing:** Every device on the Internet has a unique IP address. **IPv4** uses 32-bit addresses (e.g., 192.168.1.1) providing about 4.3 billion addresses. **IPv6** uses 128-bit addresses to provide a vastly larger address space

### How Data Travels Across the Internet

1. Data is broken into **packets** at the source
2. Each packet is labelled with source and destination **IP addresses**
3. Packets are sent independently across the network -- they may take **different routes**
4. **Routers** at each hop examine the destination IP and forward the packet towards its destination
5. At the destination, packets are **reassembled** in the correct order using sequence numbers
6. If any packets are lost or corrupted, **TCP** requests retransmission

### Internet Services

The Internet supports many services beyond the World Wide Web:

| Service | Protocol | Description |
|---|---|---|
| World Wide Web | HTTP/HTTPS | Web pages and web applications |
| Email | SMTP, IMAP, POP3 | Sending and receiving electronic messages |
| File Transfer | FTP/SFTP | Uploading and downloading files |
| Voice/Video calls | SIP, RTP (over UDP) | Real-time voice and video communication (VoIP) |
| Streaming media | HTTP, DASH, HLS (over TCP/UDP) | On-demand and live audio/video |
| Domain resolution | DNS | Translating domain names to IP addresses |

<div class="exam-tip" markdown="1">
The Internet and the World Wide Web are **not the same thing**. The Internet is the physical infrastructure (cables, routers, protocols). The Web is one of many services that runs on top of the Internet. Email, FTP, and streaming also use the Internet but are not part of the Web.
</div>
