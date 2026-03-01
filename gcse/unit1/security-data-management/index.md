---
layout: topic
title: "Security & Data Management"
level: "GCSE"
level_url: "/gcse/"
unit_name: "Unit 1: Understanding Computer Science"
unit_url: "/gcse/unit1/"
prev_topic: "/gcse/unit1/program-construction/"
next_topic: "/gcse/unit1/ethical-legal-environmental/"
---

## Data security: Dangers of storing personal data on computers

Storing personal data on computer systems brings significant risks. Organisations hold vast amounts of sensitive data — names, addresses, medical records, financial details — and this data can be targeted or misused.

### Key dangers

- **Hacking** — unauthorised individuals may gain access to databases and steal personal information
- **Data breaches** — accidental or deliberate exposure of personal data, which can lead to identity theft
- **Identity theft** — criminals use stolen personal data (name, date of birth, address) to impersonate someone and access their bank accounts, apply for credit, or commit fraud
- **Insider threats** — employees with access to data may misuse it, sell it, or accidentally expose it
- **Loss or corruption** — hardware failure, software bugs, or human error can destroy stored data
- **Lack of consent** — data may be shared with third parties without the knowledge or consent of the data subject

<div class="key-term" markdown="1">
**Personal data** — any information that can be used to identify a living individual, such as name, address, date of birth, email address, medical records, or financial details.
</div>

<div class="exam-tip" markdown="1">
When discussing dangers of storing personal data, always relate your answer to **real-world consequences** — for example, stolen medical records could lead to discrimination, or leaked financial data could result in money being stolen from accounts.
</div>

---

## Protection methods: Access levels, passwords, encryption

Several methods are used to protect data stored on computer systems.

### Access levels

Access levels restrict what different users can do with data:

| Access level | Description | Example |
|-------------|-------------|---------|
| **Full control** | Can read, write, modify, and delete | System administrator |
| **Read and write** | Can view and edit data | Manager |
| **Read only** | Can view but not change data | Standard employee |
| **No access** | Cannot view or interact with data | Unauthorised user |

Access levels follow the principle of **least privilege** — users should only have the minimum access needed to do their job.

### Passwords

- Passwords are the most common form of **authentication** (proving you are who you claim to be)
- Strong passwords should be **long**, contain a **mix of character types** (uppercase, lowercase, numbers, symbols), and be **unique** to each account
- Passwords should be **changed regularly** and never shared
- Systems can enforce password policies such as minimum length and complexity requirements
- **Two-factor authentication (2FA)** adds a second layer of security (e.g. a code sent to a phone)

### Encryption

<div class="key-term" markdown="1">
**Encryption** — the process of converting plain text into an unreadable format (cipher text) using an algorithm and a key. Only someone with the correct key can decrypt the data back to its original form.
</div>

- Data is scrambled using an **encryption algorithm** and a **key**
- Even if encrypted data is intercepted, it cannot be read without the decryption key
- Used for data **in transit** (e.g. HTTPS, email encryption) and data **at rest** (e.g. encrypted hard drives)
- **Symmetric encryption** uses the same key to encrypt and decrypt
- **Asymmetric encryption** uses a pair of keys (public key to encrypt, private key to decrypt)

---

## Data management: Need for file backups and generations

### Why backups are essential

Data can be lost through hardware failure, accidental deletion, malware, natural disasters, or theft. **Backups** are copies of data stored separately so that data can be recovered if the original is lost.

### Backup strategies

| Strategy | Description | Advantages | Disadvantages |
|----------|-------------|------------|---------------|
| **Full backup** | Copies all data every time | Simple to restore | Slow, uses lots of storage |
| **Incremental backup** | Copies only data changed since the last backup | Fast, uses less storage | Slower to restore (needs all increments) |
| **Differential backup** | Copies data changed since the last full backup | Faster to restore than incremental | Uses more storage than incremental |

### Generations of backup (Grandfather-Father-Son)

The **Grandfather-Father-Son (GFS)** method is a common rotation scheme:

- **Son** — daily backup (overwritten each week)
- **Father** — weekly backup (overwritten each month)
- **Grandfather** — monthly backup (kept for long-term storage)

This ensures that multiple points in time are available for recovery, and that recent data loss and older data loss can both be addressed.

<div class="exam-tip" markdown="1">
When asked about backup strategies, consider **how often** data changes, **how quickly** it needs to be restored, and **how much storage** is available. A hospital with constantly changing records needs frequent backups; a small business might manage with weekly ones.
</div>

---

## Need for archiving files

<div class="key-term" markdown="1">
**Archiving** — moving data that is no longer actively used to a separate, long-term storage medium. The data is preserved but removed from the main system.
</div>

Archiving is different from backing up:

| Feature | Backup | Archive |
|---------|--------|---------|
| **Purpose** | Recovery from data loss | Long-term preservation |
| **Data status** | Copy of active data | Moved from active system |
| **Access frequency** | Restored when needed | Rarely accessed |
| **Storage** | Recent copies kept | Kept indefinitely |

### Reasons for archiving

- **Frees up storage space** on the main system, improving performance
- **Legal requirements** — some industries must retain records for a set number of years (e.g. financial records for 7 years)
- **Historical reference** — old data may be needed for audits, legal cases, or analysis
- **Reduces clutter** — keeping only active data on the main system makes it easier to manage
- Archived data is typically stored on **magnetic tape** or **cloud storage** due to low cost and high capacity

---

## Compression: Lossy and lossless algorithms

Compression reduces the **file size** of data, making it faster to transmit and requiring less storage space.

### Lossy compression

- **Permanently removes** some data from the file to reduce its size
- The original file **cannot be fully reconstructed**
- Works by removing data that humans are unlikely to notice (e.g. sounds outside human hearing range, subtle colour differences)
- Results in **smaller file sizes** than lossless compression
- Used for **media files**: JPEG (images), MP3 (audio), MP4 (video)
- Suitable when **perfect quality is not essential**

### Lossless compression

- Reduces file size **without losing any data**
- The original file can be **perfectly reconstructed** from the compressed version
- Works by finding patterns and representing repeated data more efficiently (e.g. run-length encoding)
- Produces **larger files** than lossy compression
- Used where **data integrity is critical**: PNG (images), FLAC (audio), ZIP (general files), text files, program code

| Feature | Lossy | Lossless |
|---------|-------|----------|
| **Data lost?** | Yes | No |
| **File size** | Smaller | Larger |
| **Reversible?** | No | Yes |
| **Quality** | Reduced (but often acceptable) | Identical to original |
| **Example formats** | JPEG, MP3, MP4 | PNG, FLAC, ZIP |
| **Best for** | Photos, music, video | Text, code, medical images |

<div class="exam-tip" markdown="1">
If asked to recommend a compression type, consider **what the data is used for**. A music streaming service can use lossy compression (listeners won't notice small quality loss). A hospital storing X-ray images must use lossless compression (any data loss could affect diagnosis).
</div>

---

## Calculate compression ratios

The **compression ratio** describes how much a file has been reduced in size.

### Formula

```
Compression ratio = Uncompressed size / Compressed size
```

This can also be expressed as a percentage saving:

```
Space saving (%) = ((Uncompressed size - Compressed size) / Uncompressed size) x 100
```

### Worked example

An image file is 12 MB before compression and 3 MB after compression.

- **Compression ratio** = 12 / 3 = **4:1** (the original is 4 times larger)
- **Space saving** = ((12 - 3) / 12) x 100 = **75%**

### Another example

A sound file is 50 MB before compression and 10 MB after compression.

- **Compression ratio** = 50 / 10 = **5:1**
- **Space saving** = ((50 - 10) / 50) x 100 = **80%**

<div class="exam-tip" markdown="1">
Always show your working in compression ratio questions. State the formula, substitute the values, and express the answer as a ratio (e.g. 4:1) or as a percentage. A higher compression ratio means a greater reduction in file size.
</div>

---

## Network security: Importance and dangers from network use

Connecting computers to a network introduces significant security risks because data is transmitted between devices and can potentially be intercepted or systems can be accessed remotely.

### Why network security is important

- Businesses rely on networks to operate — a security breach can cause **financial loss**, **reputational damage**, and **legal consequences**
- Networks allow **remote access**, which means attackers do not need to be physically present
- A single vulnerability on one device can compromise the **entire network**

### Dangers from network use

- **Interception of data** — data transmitted across a network can be captured using packet sniffing tools
- **Unauthorised access** — hackers may exploit vulnerabilities to gain access to network resources
- **Malware distribution** — viruses and worms can spread rapidly across a network
- **Denial of Service (DoS) attacks** — overwhelming a server with traffic so legitimate users cannot access it
- **Man-in-the-middle attacks** — an attacker intercepts communication between two parties without their knowledge
- **Data theft** — sensitive information can be stolen from networked databases

### Network protection methods

- **Firewalls** — monitor incoming and outgoing network traffic and block unauthorised connections based on predefined rules
- **Encryption** — scrambles data so intercepted traffic cannot be read (e.g. WPA2 for Wi-Fi, HTTPS for web traffic)
- **Authentication** — ensuring users prove their identity before accessing the network (passwords, 2FA)
- **MAC address filtering** — only allowing devices with approved hardware addresses onto the network
- **Intrusion detection systems (IDS)** — monitor network traffic for suspicious activity and alert administrators

---

## Acceptable use policy and disaster recovery policy

### Acceptable use policy (AUP)

An **acceptable use policy** is a document that defines what users are and are not allowed to do on an organisation's computer systems and network.

A typical AUP covers:

- **Permitted use** — using systems only for work-related purposes
- **Prohibited activities** — no illegal downloads, no accessing inappropriate content, no installing unauthorised software
- **Email and internet rules** — guidelines for professional communication
- **Password responsibilities** — users must keep passwords secure and not share them
- **Data handling** — rules about storing and transferring sensitive data
- **Consequences** — what happens if the policy is breached (warnings, dismissal, legal action)

### Disaster recovery policy (DRP)

A **disaster recovery policy** outlines the procedures an organisation will follow to recover its IT systems after a major disruption (fire, flood, cyberattack, hardware failure).

A typical DRP includes:

- **Risk assessment** — identifying potential threats and their likelihood
- **Backup procedures** — what is backed up, how often, and where backups are stored
- **Recovery procedures** — step-by-step instructions for restoring systems
- **Roles and responsibilities** — who is responsible for each part of the recovery process
- **Communication plan** — how staff, customers, and stakeholders will be informed
- **Testing** — the plan should be regularly tested and updated

<div class="key-term" markdown="1">
**Acceptable use policy (AUP)** — a set of rules that users must agree to follow in order to use an organisation's IT systems. **Disaster recovery policy (DRP)** — a documented plan for restoring IT systems and data after a major incident.
</div>

---

## Cybersecurity: Malware (viruses, worms, key loggers)

<div class="key-term" markdown="1">
**Malware** — malicious software designed to damage, disrupt, or gain unauthorised access to a computer system. It is a general term covering all types of harmful programs.
</div>

### Types of malware

| Type | Description | How it spreads |
|------|-------------|----------------|
| **Virus** | Malicious code that attaches itself to a legitimate program or file. It activates when the host file is opened and can replicate itself. | Spread through infected files, email attachments, USB drives |
| **Worm** | A standalone program that replicates itself and spreads across networks without needing a host file. | Exploits network vulnerabilities; spreads automatically |
| **Trojan** | Disguises itself as legitimate software to trick users into installing it. Does not replicate but creates a backdoor. | Downloaded by the user, often disguised as useful software |
| **Spyware** | Secretly monitors user activity and collects information such as browsing habits and personal data. | Bundled with other software, or installed via drive-by downloads |
| **Key logger** | Records every keystroke the user makes, capturing passwords, credit card numbers, and messages. | Installed by trojans, or through physical access to the device |
| **Ransomware** | Encrypts the victim's files and demands payment (ransom) for the decryption key. | Spread through phishing emails, malicious downloads, network exploits |
| **Adware** | Displays unwanted advertisements, often as pop-ups. May also collect data on browsing habits. | Bundled with free software |

<div class="exam-tip" markdown="1">
Know the **differences** between viruses, worms, and trojans. A virus needs a host file and user action to spread. A worm spreads on its own across networks. A trojan tricks the user into installing it and does not replicate.
</div>

---

## Forms of attack: Technical weaknesses and user behaviour

Cyberattacks exploit either **technical weaknesses** in systems or **human behaviour** (social engineering).

### Attacks exploiting technical weaknesses

- **SQL injection** — inserting malicious SQL code into a web form to access or manipulate a database. Exploits poorly validated input fields
- **Denial of Service (DoS)** — flooding a server with so many requests that it cannot respond to legitimate users
- **Distributed Denial of Service (DDoS)** — a DoS attack using many compromised computers (a botnet) simultaneously
- **Brute force attack** — systematically trying every possible password combination until the correct one is found
- **Buffer overflow** — sending more data than a program's buffer can hold, potentially allowing the attacker to execute malicious code
- **Zero-day exploit** — attacking a vulnerability that the software developer does not yet know about, so no patch exists

### Attacks exploiting user behaviour (social engineering)

- **Phishing** — sending fraudulent emails that appear to be from a trusted source, tricking users into revealing passwords or clicking malicious links
- **Spear phishing** — a targeted phishing attack aimed at a specific individual, using personal details to appear convincing
- **Shoulder surfing** — physically looking over someone's shoulder to see their password or sensitive information
- **Blagging (pretexting)** — creating a fabricated scenario to trick someone into providing information (e.g. pretending to be IT support)
- **Pharming** — redirecting users from a legitimate website to a fraudulent one by poisoning DNS records

<div class="key-term" markdown="1">
**Social engineering** — manipulating people into revealing confidential information or performing actions that compromise security, rather than exploiting technical vulnerabilities.
</div>

---

## Methods of identifying vulnerabilities

Organisations use various methods to find security weaknesses before attackers exploit them.

- **Penetration testing** — authorised security experts (ethical hackers) attempt to break into a system to identify weaknesses. They produce a report with recommendations
- **Vulnerability scanning** — automated software scans systems for known vulnerabilities such as outdated software, open ports, or missing patches
- **Code reviews** — experienced programmers manually examine source code to find security flaws, logic errors, and bad practices
- **Network monitoring** — continuously monitoring network traffic for unusual patterns that might indicate an intrusion or vulnerability
- **Audit trails and logs** — reviewing system logs to identify suspicious activity, failed login attempts, or unauthorised access
- **Bug bounty programmes** — organisations pay external researchers to find and report security vulnerabilities

<div class="exam-tip" markdown="1">
Penetration testing is often confused with hacking. The key difference is **authorisation** — penetration testers have **permission** to test the system and follow an agreed scope. Hackers act without permission.
</div>

---

## Protecting software during design, creation, testing, use

Security must be considered at **every stage** of the software development lifecycle, not just after release.

### During design

- **Threat modelling** — identifying potential threats and designing the system to mitigate them from the outset
- **Principle of least privilege** — designing access controls so users and processes only have the minimum permissions needed
- **Input validation planning** — deciding how all user inputs will be checked and sanitised

### During creation (coding)

- **Secure coding practices** — following established guidelines to avoid common vulnerabilities (e.g. avoiding hardcoded passwords)
- **Input validation and sanitisation** — checking all user inputs to prevent injection attacks
- **Code reviews** — having other programmers review code for security flaws before it is merged
- **Using up-to-date libraries** — ensuring third-party code does not contain known vulnerabilities

### During testing

- **Penetration testing** — simulating attacks to find vulnerabilities
- **Unit and integration testing** — testing individual components and how they work together
- **Security testing** — specifically testing for common attack vectors (SQL injection, XSS, buffer overflow)
- **User acceptance testing** — ensuring the system works correctly in real-world conditions

### During use (maintenance)

- **Patching and updates** — regularly releasing fixes for discovered vulnerabilities
- **Monitoring** — watching for unusual activity that could indicate a breach
- **User training** — educating users about phishing, strong passwords, and safe practices
- **Incident response** — having a plan ready for when a security breach occurs

---

## Role of internet cookies

<div class="key-term" markdown="1">
**Cookie** — a small text file stored on a user's computer by a website. It contains data that the website can read the next time the user visits.
</div>

### Types of cookies

| Type | Description | Example |
|------|-------------|---------|
| **Session cookie** | Temporary; deleted when the browser is closed | Keeping items in a shopping basket while browsing |
| **Persistent cookie** | Remains on the device for a set period or until manually deleted | Remembering login details or language preferences |
| **First-party cookie** | Set by the website the user is visiting | Saving user settings on that site |
| **Third-party cookie** | Set by a different domain (usually an advertiser) | Tracking browsing habits across multiple websites for targeted advertising |

### Uses of cookies

- **Session management** — keeping users logged in, maintaining shopping baskets
- **Personalisation** — remembering language preferences, themes, or region settings
- **Tracking and analytics** — monitoring which pages users visit and how long they stay
- **Targeted advertising** — building a profile of user interests to display relevant adverts

### Privacy concerns

- Third-party cookies can **track users across multiple websites** without their explicit knowledge
- Cookie data can be used to build detailed **profiles of browsing behaviour**
- Users have the right to **accept or reject cookies** (required by law in many countries under regulations like GDPR)
- Cookies can be **deleted** by the user through browser settings
- Some browsers now **block third-party cookies** by default

<div class="exam-tip" markdown="1">
Exam questions often ask about the **benefits and drawbacks** of cookies. Benefits include a better user experience (staying logged in, personalised content). Drawbacks include privacy concerns (tracking behaviour, building advertising profiles without full user awareness).
</div>
