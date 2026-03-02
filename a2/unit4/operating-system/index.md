---
layout: topic
title: "The Operating System"
level: "A2"
level_url: "/a2/"
unit_name: "Unit 4: Architecture, Data, Communication & Applications"
unit_url: "/a2/unit4/"
---

## Types of Operating System

At A2 level, you need to understand how different OS types are suited to different computing environments.

### Batch Processing OS

A **batch OS** collects jobs together into a **batch** and processes them sequentially **without user interaction**. Jobs are submitted, queued, and executed when resources are available.

- **Example:** Payroll processing, bank statement generation, utility billing
- **Advantage:** Efficient — the CPU is kept busy processing jobs continuously
- **Disadvantage:** No user interaction during processing; errors are only discovered after the batch completes; turnaround time can be long

### Single-User OS

A **single-user OS** allows only **one user** to use the computer at a time. There may be one task (single-user, single-task, e.g. early MS-DOS) or multiple tasks (single-user, multi-task, e.g. Windows, macOS).

### Multi-User OS

A **multi-user OS** allows **many users** to access the same system simultaneously, each via their own terminal. The OS allocates resources (CPU time, memory, storage) fairly between users.

- **Example:** University mainframe, corporate server
- Each user gets a **time slice** of CPU time; rapid switching between users gives the illusion of simultaneous access
- Requires careful **security management** (user accounts, access permissions)

### Multi-Tasking OS

A **multi-tasking OS** allows a single user to run **multiple programs** at the same time. The OS uses **context switching** to rapidly alternate between processes.

- **Preemptive multi-tasking** — the OS can interrupt a running process to give CPU time to another (used by modern OSes)
- **Cooperative multi-tasking** — each process voluntarily yields CPU time (older approach, less reliable)

### Multi-Programming OS

**Multi-programming** keeps multiple programs loaded in memory simultaneously so the CPU always has a job to execute. When one program is waiting for I/O, the CPU switches to another.

- The key difference from multi-tasking: multi-programming focuses on **maximising CPU utilisation** by ensuring the CPU is never idle due to I/O waits
- Multi-tasking focuses on **user responsiveness** by switching between tasks frequently

<div class="exam-tip" markdown="1">
The terms multi-tasking and multi-programming are often confused. **Multi-programming** is about keeping the CPU busy (switching to another job during I/O waits). **Multi-tasking** is about giving the user the ability to run several applications simultaneously with rapid context switching.
</div>

---

## Interrupts

### What is an Interrupt?

An **interrupt** is a signal to the CPU indicating that an event has occurred that requires attention. Interrupts are fundamental to how modern computers handle I/O, errors, and multi-tasking.

### Conditions and Events That Generate Interrupts

| Interrupt Type | Source | Examples |
|---------------|--------|---------|
| **Hardware interrupt** | External devices | Keyboard key press, mouse movement, printer ready, disk read complete, network packet received, USB device connected |
| **Software interrupt** | Running programs | System call (requesting OS service), division by zero, invalid memory access, breakpoint (debugging) |
| **Timer interrupt** | System clock | Time slice expired (for scheduling), real-time clock tick, watchdog timer |
| **I/O interrupt** | I/O devices | Data transfer complete, device error, device ready |
| **Error interrupt** | Hardware/software | Memory parity error, bus error, power failure warning |

### Interrupt Handling Process (7 Steps)

1. An interrupt signal is **generated** by a device, timer, or software event
2. The CPU **completes the current instruction** in the fetch-decode-execute cycle
3. The CPU **checks the interrupt priority** against the current process priority
4. If the interrupt has **sufficient priority**, the CPU saves the **current state** (all register contents, including the Program Counter) onto the **system stack**
5. The CPU looks up the interrupt type in the **interrupt vector table** to find the memory address of the appropriate **Interrupt Service Routine (ISR)**
6. The CPU loads the ISR address into the PC and **executes the ISR** to handle the interrupt
7. When the ISR completes, the CPU **restores the saved state** from the stack and **resumes** the interrupted process from where it left off

<div class="key-term" markdown="1">
An **Interrupt Service Routine (ISR)** is a special routine stored in memory that handles a specific type of interrupt. The **interrupt vector table** maps each interrupt type to the memory address of its ISR.
</div>

### Interrupt Priorities

Not all interrupts are equally urgent. The OS assigns **priority levels** to different interrupt types:

- **Highest:** Power failure, hardware errors (must be handled immediately)
- **High:** Timer interrupts (essential for scheduling)
- **Medium:** I/O device interrupts (disk, network)
- **Low:** Software interrupts, user requests

**Rules for interrupt priorities:**
- A higher-priority interrupt can **interrupt** a lower-priority ISR (nested interrupts)
- A lower-priority interrupt **cannot** interrupt a higher-priority ISR — it must wait
- When a nested interrupt occurs, the state of the current ISR is saved to the stack, and it resumes after the higher-priority ISR completes
- The **stack** handles nesting naturally using LIFO — each interrupted routine's state is pushed on and popped off in reverse order

### Factors in Allocating Priorities

| Factor | Description |
|--------|-------------|
| **Urgency** | How critical is the event? Power failure requires immediate response |
| **Consequences of delay** | Will delayed handling cause data loss or system damage? |
| **Time sensitivity** | Real-time events (e.g. sensor data) need fast response |
| **System stability** | Hardware errors that could crash the system get high priority |
| **User impact** | Events affecting user experience (e.g. keyboard input) get moderate priority |

<div class="exam-tip" markdown="1">
A very common exam question asks you to describe the interrupt handling process step by step. Always mention: (1) completing the current instruction, (2) checking priority, (3) saving state to the stack, (4) looking up the ISR in the interrupt vector table, (5) executing the ISR, (6) restoring state from the stack, (7) resuming the original process. The **stack** and the **interrupt vector table** are key details that examiners look for.
</div>

---

## Memory Management

### Reasons for Partitioning Main Memory

The OS must divide (partition) main memory between multiple programs. Without partitioning:
- Programs could overwrite each other's data
- There would be no protection between processes
- Only one program could be in memory at a time

### Fixed Partitioning

Memory is divided into a set number of **fixed-size partitions** at boot time. Each partition can hold one process.

| Advantage | Disadvantage |
|-----------|-------------|
| Simple to implement | **Internal fragmentation** — if a process is smaller than its partition, the remaining space is wasted |
| Low overhead | Limited number of processes (one per partition) |
| Fast allocation | Large processes may not fit in any partition |

### Dynamic Partitioning

Partitions are created **dynamically** to match the exact size of each process. No predefined partition sizes.

| Advantage | Disadvantage |
|-----------|-------------|
| No internal fragmentation (partition = process size) | **External fragmentation** — as processes are loaded and removed, gaps (holes) of free memory appear between partitions |
| More efficient use of memory | More complex allocation algorithms needed (first-fit, best-fit, worst-fit) |
| No limit on process size (up to total memory) | May need **compaction** (moving processes to consolidate free space), which is time-consuming |

### Internal vs External Fragmentation

| Type | Cause | Effect |
|------|-------|--------|
| **Internal fragmentation** | Process is smaller than its allocated partition (fixed partitioning) | Wasted space **inside** the partition |
| **External fragmentation** | Free memory exists but is scattered in small, non-contiguous gaps (dynamic partitioning) | Enough total free memory exists but no single block is large enough for the next process |

### Virtual Memory and Paging

**Virtual memory** uses secondary storage as an extension of RAM. Programs are divided into **pages** (fixed-size blocks), and RAM is divided into **page frames** of the same size.

**How paging works:**
1. Only the **currently needed pages** are loaded into RAM
2. The rest are stored in a **swap file** on disk
3. A **page table** maps each logical page to its physical frame (or marks it as on disk)
4. When the CPU accesses a page not in RAM, a **page fault** occurs
5. The OS selects a page to **swap out** (write to disk) and loads the required page **in**

### Thrashing

**Thrashing** occurs when the system spends more time **swapping pages** between RAM and disk than executing useful work.

**Causes:**
- Too many processes competing for limited RAM
- Working sets of active processes exceed available physical memory
- Poor page replacement algorithm choosing pages that are needed again immediately

**Symptoms:**
- System becomes extremely slow
- Disk activity is very high (constant read/write to swap file)
- CPU utilisation drops (CPU is waiting for I/O)

**Solutions:**
- Add more physical RAM
- Reduce the number of concurrent processes
- Use a better page replacement algorithm
- Increase swap file size (alleviates but doesn't solve the underlying problem)

<div class="exam-tip" markdown="1">
Understand the difference between **internal** and **external** fragmentation, and which partitioning method causes each. Fixed partitioning → internal fragmentation. Dynamic partitioning → external fragmentation. Virtual memory with paging eliminates external fragmentation but can cause **thrashing** if overused.
</div>

---

## Methods of Data Transfer: Buffering

### Why Buffering is Needed

The CPU operates much faster than I/O devices. Without buffering, the CPU would idle while waiting for a slow device (e.g. printer, disk drive) to be ready. A **buffer** is a temporary memory area that holds data being transferred between devices operating at different speeds.

### Single Buffering

- One buffer is used
- The **producer** (e.g. CPU) fills the buffer
- The **consumer** (e.g. printer) reads from the buffer
- The producer must **wait** until the consumer has finished reading before writing new data
- Simple but can leave one device idle

### Double Buffering

- **Two buffers** are used alternately
- While Buffer A is being read by the consumer, Buffer B is being filled by the producer
- When both finish, the buffers **swap roles**
- The producer and consumer can work **simultaneously**, significantly improving throughput

| Feature | Single Buffering | Double Buffering |
|---------|-----------------|------------------|
| **Buffers** | 1 | 2 |
| **Concurrency** | Sequential — producer waits for consumer | Parallel — both work simultaneously |
| **Efficiency** | Lower | Higher |
| **Memory cost** | Less | More (double the buffer memory) |
| **Use case** | Simple I/O | Printing, audio/video streaming, disk I/O |

### Spooling

**Spooling (Simultaneous Peripheral Operations On-Line)** is used specifically for slow output devices like printers:
- Print jobs are written to a **spool queue** on disk
- The **spooler** sends jobs to the printer one at a time
- The CPU and applications are **freed immediately** after writing to the spool
- Multiple users can share a single printer without conflicts

---

## Scheduling

### Principles of High-Level Scheduling

**High-level scheduling** (also called **job scheduling** or **long-term scheduling**) decides which jobs from the **job pool** are admitted into the system (loaded into memory). It controls the **degree of multiprogramming** — how many processes are in memory at once.

Considerations:
- Balancing **I/O-bound** and **CPU-bound** jobs for efficient resource usage
- Ensuring the system is not overloaded (too many processes cause thrashing)
- Prioritising jobs based on urgency, resource requirements, or user priority

### Processor Allocation and Scheduling Algorithms

**Low-level scheduling** (CPU scheduling) decides which process in the ready queue gets the CPU next.

| Algorithm | Type | Description |
|-----------|------|-------------|
| **FCFS** | Non-preemptive | First Come First Served — processes run in arrival order |
| **SJF** | Non-preemptive | Shortest Job First — shortest estimated time runs next |
| **Round Robin** | Preemptive | Each process gets a fixed time slice; cycles through ready queue |
| **Priority** | Either | Highest priority process runs next; can cause starvation |
| **Multilevel Feedback Queue** | Preemptive | Multiple priority queues; processes move between queues based on behaviour |

### Allocation of Devices

The OS must manage access to **shared devices** (printers, disk drives, network interfaces):
- **Dedicated allocation** — a device is assigned exclusively to one process until it finishes
- **Shared allocation** — multiple processes share a device (managed via spooling or time-sharing)
- **Virtual devices** — the OS creates virtual instances of a device (e.g. virtual printers) so multiple processes can "use" it simultaneously

### Significance of Job Priorities

Priorities determine the order in which jobs are processed:
- **System processes** typically have higher priority than user processes
- **Real-time tasks** get the highest priority
- **Interactive tasks** (user typing) get higher priority than batch tasks
- **Ageing** prevents starvation by gradually increasing the priority of long-waiting processes
- Priority can be **static** (set at creation) or **dynamic** (adjusted based on behaviour)

---

## Three States of a Process

At any point, a process is in one of three states:

| State | Description |
|-------|-------------|
| **Running** | Currently being executed by the CPU. Only one process per core can be in this state. |
| **Ready** | In memory, has all resources except CPU time. Waiting to be selected by the scheduler. |
| **Blocked (Waiting)** | Waiting for an event (I/O completion, resource availability, signal from another process). Cannot run even if CPU is free. |

### State Transitions

| Transition | From → To | Cause |
|-----------|-----------|-------|
| **Dispatch** | Ready → Running | Scheduler selects this process |
| **Timeout** | Running → Ready | Time slice expires or higher-priority process arrives |
| **Block** | Running → Blocked | Process requests I/O or waits for a resource |
| **Wake** | Blocked → Ready | I/O completes or resource becomes available |

**Important:** A process **cannot** go directly from Blocked to Running. It must pass through Ready first.

---

## Time-Slicing, Polling and Threading

### Time-Slicing

**Time-slicing** is the technique of dividing CPU time into small intervals (**time slices** or **quanta**) and allocating each slice to a different process in turn (Round Robin scheduling).

- Gives the **illusion of concurrent execution** on a single core
- Each process runs for its time slice, then is preempted and placed back in the ready queue
- The **context switch** (saving and restoring process state) adds overhead
- Time slice too small → excessive context switching overhead
- Time slice too large → poor responsiveness (approaches FCFS behaviour)

### Polling

**Polling** is where the CPU repeatedly checks each I/O device in turn to see if it needs attention.

| Feature | Polling | Interrupts |
|---------|---------|------------|
| **Mechanism** | CPU actively checks devices | Device signals the CPU |
| **CPU usage** | Wastes time checking idle devices | CPU only responds when needed |
| **Simplicity** | Simpler to implement | More complex (ISRs, vector table) |
| **Response time** | Depends on polling frequency | Immediate |
| **Best for** | Simple embedded systems | Complex systems with many devices |

### Threading

A **thread** is the smallest unit of execution that can be scheduled. A single process can contain **multiple threads** that share memory but execute independently.

| Feature | Process | Thread |
|---------|---------|--------|
| **Memory** | Own address space | Shares process memory |
| **Creation** | Heavyweight | Lightweight |
| **Communication** | IPC needed | Shared memory |
| **Context switch** | Expensive | Cheaper |

**Benefits of multithreading:**
- **Responsiveness** — a GUI thread stays responsive while a background thread performs computation
- **Parallelism** — on multi-core CPUs, threads can run on different cores simultaneously
- **Resource sharing** — threads in the same process share memory, reducing overhead
- **Efficiency** — creating and switching threads is faster than creating and switching processes

<div class="exam-tip" markdown="1">
Understand the relationship between these concepts: **time-slicing** is the mechanism that enables multi-tasking by giving each process a turn on the CPU. **Polling** and **interrupts** are two different approaches to handling I/O device communication. **Threading** allows a single process to perform multiple tasks concurrently. These concepts frequently appear together in exam questions about how the OS manages resources.
</div>
