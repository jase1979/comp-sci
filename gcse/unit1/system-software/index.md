---
layout: topic
title: "System Software"
level: "GCSE"
level_url: "/gcse/"
unit_name: "Unit 1: Understanding Computer Science"
unit_url: "/gcse/unit1/"
prev_topic: "/gcse/unit1/data-organisation/"
next_topic: "/gcse/unit1/principles-of-programming/"
---

## OS purpose: Managing resources (peripherals, processes, memory, backing store)

The **operating system (OS)** is the most important piece of system software on a computer. It acts as an intermediary between the user and the hardware, managing all of the computer's resources so that application software can run smoothly.

<div class="key-term" markdown="1">
**Operating System (OS)** — system software that manages hardware resources, provides a user interface, and allows application software to run. Examples include Windows, macOS, Linux, iOS and Android.
</div>

The OS manages four key types of resource:

### Peripheral Management

- The OS controls all **input and output devices** (peripherals) connected to the computer
- It uses **device drivers** — small programs that translate general OS commands into specific instructions for each device
- When a peripheral needs attention (e.g. a key is pressed), it sends an **interrupt** to the CPU, and the OS handles it
- The OS maintains a **queue** of print jobs and other I/O requests, sending them to the correct device in order

<div class="key-term" markdown="1">
**Device driver** — a program that allows the operating system to communicate with a specific hardware device. Each device needs its own driver so the OS can send it the correct instructions.
</div>

### Process Management

- A **process** is a program that is currently being executed
- The OS allocates **CPU time** to each process so that multiple programs appear to run simultaneously
- On a single-core processor, the OS uses **time slicing** — rapidly switching between processes so each gets a share of the CPU
- The OS decides the order using **scheduling algorithms**, which consider priority, waiting time, and fairness
- It also handles starting, pausing, resuming and terminating processes

### Memory Management

- The OS allocates **RAM** to each running process and keeps track of which memory locations are in use
- When a program is opened, the OS loads it into an available section of RAM
- When a program closes, the OS frees that memory for other processes
- If RAM becomes full, the OS may use **virtual memory** — a section of the hard drive that temporarily acts as extra RAM
- Virtual memory is much slower than RAM, so heavy use causes the system to slow down (known as **disk thrashing**)

<div class="key-term" markdown="1">
**Virtual memory** — a technique where a section of the hard drive is used as if it were additional RAM. This allows more programs to run than physical RAM would normally permit, but at a significant speed cost.
</div>

### Backing Store Management

- The OS manages how files are stored on secondary storage (hard drives, SSDs)
- It uses a **file system** (e.g. NTFS, FAT32, ext4) to organise files into folders and keep track of where each file's data is physically located on the disk
- The OS handles file operations: **creating, reading, writing, deleting, copying and moving** files
- It manages **access rights** — controlling which users can read, write or execute particular files
- The OS also keeps a **directory structure** so the user can navigate and find files easily

<div class="exam-tip" markdown="1">
A common exam question asks you to describe how the OS manages resources. Structure your answer around the four areas — peripherals, processes, memory and backing store — and give a specific example for each.
</div>

---

## OS purpose: Providing a user interface

The OS provides a **user interface** that allows people to interact with the computer. Different types of interface suit different users and tasks.

### Types of User Interface

| Interface Type | Description | Advantages | Disadvantages |
|----------------|-------------|------------|---------------|
| **GUI (Graphical User Interface)** | Uses windows, icons, menus and pointers (WIMP) | Intuitive, easy to learn, visually clear | Uses more system resources, slower for experts |
| **CLI (Command Line Interface)** | User types text commands | Powerful, fast for experts, uses fewer resources | Steep learning curve, must memorise commands |
| **Menu-driven** | Presents numbered or listed options to choose from | Simple, no commands to learn | Limited options, can be slow to navigate |
| **Natural language** | User speaks or types in everyday language | Very accessible, no training needed | Can misinterpret input, limited functionality |
| **Touch-sensitive** | User taps, swipes and pinches directly on a touchscreen | Intuitive, no extra peripherals needed, portable | Less precise than a mouse, prone to fingerprints, limited for complex tasks |
| **Voice-driven** | User speaks commands interpreted by voice recognition | Hands-free, accessible for users with disabilities | Affected by background noise, accents can cause errors, limited command set |

### GUI (Graphical User Interface)

- The most common interface on desktop and laptop computers
- Users interact by clicking icons, dragging files, and selecting from menus
- Uses a **WIMP** system — Windows, Icons, Menus, Pointers
- Allows **multitasking** by showing multiple windows on screen at once
- Examples: Windows desktop, macOS Finder, smartphone home screens

### CLI (Command Line Interface)

- The user types precise text commands to perform operations
- Provides **direct control** over the system, with no visual overhead
- Commonly used by **system administrators** and **programmers** for tasks such as managing servers, automating scripts, and navigating file systems
- Commands can be combined and saved as **scripts** to automate repetitive tasks
- Examples: Windows Command Prompt, PowerShell, Linux Terminal

### Touch-Sensitive Interface

- The user interacts directly with the screen by **tapping, swiping, pinching and dragging**
- Common on **smartphones, tablets, ATMs, self-service checkouts** and information kiosks
- Very **intuitive** — even young children can use it with no training
- Less suitable for tasks requiring **precise input** (e.g. detailed graphic design) or **large amounts of text**
- Screens can become dirty and difficult to read due to **fingerprints**

### Voice-Driven Interface

- The user speaks commands which are interpreted by **voice recognition software**
- Used in **smart speakers** (Alexa, Google Home), **virtual assistants** (Siri, Cortana), and **accessibility tools**
- Allows **hands-free** operation — useful while driving, cooking, or for users with physical disabilities
- Accuracy can be reduced by **background noise**, strong **accents**, or unusual vocabulary
- Privacy concerns — the device may be **always listening** to detect the wake word

<div class="exam-tip" markdown="1">
If asked to compare a GUI and CLI, always discuss **ease of use** (GUI is easier for beginners), **speed** (CLI is faster for experienced users), **system resources** (GUI uses more), and **power/flexibility** (CLI allows scripting and automation).
</div>

---

## Utility software: Purpose and functionality

**Utility software** is a type of system software designed to help **maintain, optimise and protect** the computer system. Utilities perform specific housekeeping tasks that keep the system running efficiently.

<div class="key-term" markdown="1">
**Utility software** — programs that perform maintenance and housekeeping tasks to keep the computer system running smoothly. They support the operating system rather than the user's direct work.
</div>

### Common Utility Programs

| Utility | Purpose | How it Works |
|---------|---------|--------------|
| **Antivirus** | Protects against malware | Scans files and programs against a database of known virus signatures; quarantines or deletes threats |
| **Disk defragmenter** | Improves HDD performance | Rearranges fragmented file data so that each file is stored in contiguous blocks, reducing read/write times |
| **Backup software** | Protects against data loss | Creates copies of files that can be restored if the originals are lost, corrupted or accidentally deleted |
| **File compression** | Reduces file size | Uses algorithms to reduce the number of bits needed to store a file, saving space and speeding up transfers |
| **Encryption software** | Protects data security | Scrambles data using an algorithm and a key so it cannot be read without the correct decryption key |
| **File manager** | Organises files and folders | Allows users to browse, move, copy, rename and delete files within the file system |
| **Firewall** | Prevents unauthorised network access | Monitors incoming and outgoing traffic and blocks connections that violate security rules |
| **Disk partitioner** | Divides a drive into logical sections | Splits a physical hard drive into separate partitions, each of which can act as an independent drive |
| **Disk checker** | Detects and repairs file system errors | Scans the disk for bad sectors, corrupted files and file system inconsistencies and attempts to repair them |
| **Disk formatter** | Prepares a disk for use | Erases all data and sets up a new file system (e.g. NTFS, FAT32) so the OS can read and write to the disk |
| **Disk compression** | Compresses entire drives to save space | Automatically compresses and decompresses files as they are written to and read from the disk |
| **System profiler** | Displays system information | Shows details about hardware components, installed software, OS version and resource usage |
| **Data recovery** | Recovers lost or deleted files | Scans storage media for remnants of deleted files and attempts to restore them |
| **Clipboard manager** | Extends clipboard functionality | Stores a history of copied items so the user can paste from previous clipboard entries, not just the most recent |
| **Version control** | Tracks changes to files over time | Records every change made to a set of files, allowing users to revert to previous versions and compare changes |
| **Archiver** | Combines and compresses multiple files | Packages multiple files and folders into a single archive file (e.g. .zip, .tar) for easier storage and transfer |

### Antivirus Software

- Runs **real-time scans** in the background to check files as they are opened or downloaded
- Performs **full system scans** on a schedule to check all stored files
- Compares files against a database of known **virus signatures** (patterns of code)
- Uses **heuristic analysis** to detect suspicious behaviour from previously unknown threats
- Must be **regularly updated** so that the signature database includes the latest threats

### Disk Defragmentation

- Over time, files are saved in **non-contiguous** (fragmented) blocks across a hard drive
- The read/write head must jump between scattered blocks, **slowing down** file access
- Defragmentation rearranges data so that files are stored in **adjacent blocks**
- This reduces seek time and improves performance
- Only needed for **HDDs** — SSDs should **not** be defragmented as it wears out the flash memory unnecessarily

### Backup Software

- Creates copies of data that can be used for **recovery** after data loss
- **Full backup**: copies all selected files — thorough but time-consuming and storage-heavy
- **Incremental backup**: only copies files that have **changed since the last backup** — faster and uses less space
- Good practice is to follow the **3-2-1 rule**: 3 copies of data, on 2 different types of media, with 1 stored off-site

### File Compression

- **Lossy compression** permanently removes some data to achieve smaller file sizes (e.g. JPEG images, MP3 audio) — the original cannot be perfectly restored
- **Lossless compression** reduces file size without any loss of data (e.g. ZIP, PNG) — the original can be perfectly restored
- Compressed files take up less storage space and can be **transferred faster** over a network

<div class="exam-tip" markdown="1">
Know the difference between **lossy** and **lossless** compression. Lossy is suitable when a slight reduction in quality is acceptable (photos, music). Lossless is essential when the data must be perfectly preserved (text documents, program files).
</div>

### Firewall

- Monitors all **incoming and outgoing network traffic** and checks it against a set of security rules
- **Blocks unauthorised access** — prevents external users or programs from connecting to the computer without permission
- Can be **software-based** (a program installed on the computer) or **hardware-based** (a dedicated device between the network and the internet)
- Protects against **hackers and malicious connections** by filtering traffic based on IP addresses, port numbers and protocols
- Works alongside antivirus software to provide a layered approach to security

<div class="key-term" markdown="1">
**Firewall** — a security utility that monitors network traffic and blocks unauthorised access based on a set of predefined rules. It acts as a barrier between a trusted internal network and untrusted external networks such as the internet.
</div>

### Disk Partitioner

- Divides a single **physical hard drive** into separate **logical sections** called partitions
- Each partition can act as a **separate drive**, with its own drive letter and file system
- Useful for **running multiple operating systems** on the same machine (e.g. Windows on one partition, Linux on another)
- Allows users to **separate OS files from user data**, making it easier to reinstall the operating system without losing personal files
- Can **resize, create or delete** partitions as needed

<div class="key-term" markdown="1">
**Disk partitioner** — a utility that divides a physical storage device into separate logical sections (partitions). Each partition is treated as an independent drive by the operating system.
</div>

<div class="exam-tip" markdown="1">
Remember that a firewall does **not** remove viruses — it prevents unauthorised access. Antivirus software handles detection and removal of malware. They serve different but complementary roles in system security.
</div>

---

## Hierarchical File Structure

The OS organises files into a **hierarchical (tree) structure** of folders (directories) and subfolders. This makes it possible to locate and manage files efficiently.

### Key Concepts

- **Root directory** — the top-level folder on a drive (e.g. `C:\` on Windows, `/` on Linux/macOS)
- **Directory (folder)** — a container that holds files and other subdirectories
- **Subdirectory** — a folder inside another folder
- **File path** — the route from the root to a specific file, e.g. `C:\Users\Alex\Documents\homework.docx`

### Example Structure

```
C:\
├── Program Files
│   ├── Browser
│   └── Office
├── Users
│   └── Alex
│       ├── Documents
│       │   └── homework.docx
│       ├── Pictures
│       └── Music
└── Windows
    └── System32
```

### File Attributes

Every file stored by the OS has **attributes** — properties that describe and control the file.

| Attribute | Description |
|-----------|-------------|
| **Filename** | The name given to the file by the user |
| **Extension** | Indicates the file type (e.g. `.docx`, `.jpg`, `.py`) |
| **File size** | The amount of storage the file occupies (in bytes, KB, MB, etc.) |
| **Date created** | When the file was first created |
| **Date modified** | When the file was last changed |
| **Read-only** | If set, the file can be viewed but not edited or deleted |
| **Hidden** | If set, the file is not displayed in normal folder views |
| **System** | Marks a file as part of the OS — should not be modified by the user |
| **Archive** | Indicates whether the file has changed since the last backup |
| **Permissions** | Controls which users can read, write or execute the file |

<div class="exam-tip" markdown="1">
You may be asked to explain why a hierarchical file structure is used. Key reasons: it keeps files **organised**, makes files **easy to locate**, allows different folders to have different **access permissions**, and prevents **name conflicts** (two files can have the same name if they are in different folders).
</div>
