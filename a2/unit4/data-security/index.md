---
layout: topic
title: "Data Security & Integrity Processes"
level: "A2 Level"
level_url: "/a2/"
unit_name: "Unit 4: Architecture, Data, Communication & Applications"
unit_url: "/a2/unit4/"
subtopics:
  - "Security and integrity problems during online file updating"
  - "Need for and purpose of cryptography"
  - "Techniques of cryptography and their role"
  - "Follow algorithms and programs used in cryptography"
---

## Security and Integrity Problems During Online File Updating

When multiple users or processes update the same data simultaneously, several problems can arise.

### Concurrent Access Problems

| Problem | Description | Example |
|---------|-------------|---------|
| **Lost update** | Two users read the same record, both modify it, and the second write overwrites the first — the first update is lost | User A reads stock = 100, User B reads stock = 100. A sets stock = 95. B sets stock = 90. A's update is lost — stock should be 85. |
| **Uncommitted dependency** | A user reads data that another user has modified but not yet committed. If the modification is rolled back, the first user has acted on invalid data. | User A updates a price to £20 (not committed). User B reads £20 and bills a customer. User A rolls back — the price was never £20. |
| **Inconsistent analysis** | A user reads data while another user is partway through updating related records, seeing a mix of old and new values | A report totals account balances while a transfer is moving £500 between accounts — the total appears £500 short or over. |

### Solutions to Concurrent Access Problems

#### Record Locking

When a user accesses a record, the system places a **lock** on it to prevent other users from modifying it simultaneously.

| Lock Type | Description |
|-----------|-------------|
| **Exclusive lock (write lock)** | Only one user can read or write the record. All other users are blocked until the lock is released. |
| **Shared lock (read lock)** | Multiple users can read the record, but no one can write to it until all shared locks are released. |
| **Record-level locking** | Locks only the specific record being accessed — other records remain available |
| **Table-level locking** | Locks the entire table — simpler but reduces concurrency |

#### Timestamps

Each transaction is assigned a **timestamp** when it begins. If two transactions conflict, the system compares timestamps:

- The **older transaction** (earlier timestamp) takes priority
- The **younger transaction** is rolled back and restarted
- Ensures transactions are processed in chronological order

#### Serialisation

Ensures that the **effect** of executing transactions concurrently is the same as if they were executed one after another (serially). The actual execution may be interleaved, but the result must be equivalent to some serial ordering.

### Deadlock

**Deadlock** occurs when two or more transactions are each waiting for the other to release a lock, creating a circular dependency where none can proceed.

**Example:**
1. Transaction A locks Record 1 and requests Record 2
2. Transaction B locks Record 2 and requests Record 1
3. Neither can proceed — both are waiting for the other

**Prevention and detection:**

| Approach | Description |
|----------|-------------|
| **Timeout** | If a transaction waits longer than a set time for a lock, it is automatically rolled back and restarted |
| **Lock ordering** | All transactions must request locks in the same predefined order — prevents circular dependencies |
| **Wait-die / wound-wait** | Timestamp-based schemes that decide whether a transaction should wait or be rolled back |
| **Deadlock detection** | The system periodically checks for circular dependencies in the lock graph and rolls back one transaction to break the cycle |

<div class="exam-tip" markdown="1">
Exam questions often describe a scenario with two users updating the same data and ask you to identify the problem and suggest solutions. Always identify the specific problem (lost update, uncommitted dependency, or inconsistent analysis) and then explain how **locking** or **timestamps** would prevent it.
</div>

---

## Need for and Purpose of Cryptography

### Why Cryptography is Needed

| Purpose | Description |
|---------|-------------|
| **Confidentiality** | Ensures that only authorised parties can read the data. Even if intercepted, encrypted data is meaningless without the key. |
| **Integrity** | Detects whether data has been tampered with during transmission or storage. |
| **Authentication** | Verifies the identity of the sender — confirms the message genuinely comes from who it claims. |
| **Non-repudiation** | Prevents the sender from denying they sent a message. Digital signatures provide evidence of origin. |

<div class="key-term" markdown="1">
**Cryptography** is the science of securing information by transforming it into an unreadable format (**ciphertext**) that can only be converted back to readable form (**plaintext**) by someone with the correct key. **Encryption** is the process of converting plaintext to ciphertext; **decryption** is the reverse.
</div>

---

## Techniques of Cryptography

### Symmetric Encryption

In **symmetric encryption**, the **same key** is used for both encryption and decryption. Both the sender and receiver must possess this shared secret key.

| Feature | Detail |
|---------|--------|
| **How it works** | Plaintext + Key → Ciphertext (encryption). Ciphertext + Same Key → Plaintext (decryption). |
| **Key distribution** | The key must be shared securely between parties **before** communication. This is the main weakness. |
| **Speed** | Fast — suitable for encrypting large amounts of data |
| **Examples** | AES (Advanced Encryption Standard — 128/192/256-bit keys), DES (Data Encryption Standard — 56-bit, now insecure), 3DES (Triple DES) |

**Advantages:**
- Fast encryption and decryption
- Simpler algorithms
- Efficient for bulk data encryption

**Disadvantages:**
- Key distribution problem — how do you securely share the key?
- Each pair of communicating parties needs a unique key
- Does not provide non-repudiation (both parties have the same key)

### Asymmetric Encryption

In **asymmetric encryption**, two mathematically related keys are used: a **public key** (shared openly) and a **private key** (kept secret).

| Operation | Keys Used |
|-----------|-----------|
| **Encryption** | Sender encrypts with the recipient's **public key** |
| **Decryption** | Recipient decrypts with their own **private key** |
| **Digital signature** | Sender signs with their own **private key** |
| **Signature verification** | Recipient verifies with the sender's **public key** |

**Key principle:** Data encrypted with a public key can **only** be decrypted with the corresponding private key, and vice versa.

| Feature | Detail |
|---------|--------|
| **Key distribution** | No need to share secret keys — public keys are freely distributed |
| **Speed** | Slower than symmetric — not practical for large data volumes |
| **Examples** | RSA (Rivest-Shamir-Adleman), ECC (Elliptic Curve Cryptography) |

**Advantages:**
- No key distribution problem
- Provides digital signatures (non-repudiation)
- Scales well — N users need only N key pairs, not N(N-1)/2 shared keys

**Disadvantages:**
- Much slower than symmetric encryption
- Key sizes must be larger for equivalent security
- Computationally intensive

### Hybrid Approach

In practice, most secure communication uses **both** types:

1. Asymmetric encryption securely exchanges a **session key**
2. The session key is then used for **symmetric encryption** of the actual data
3. This combines the key distribution advantage of asymmetric with the speed of symmetric

This is exactly how **TLS/SSL** (used in HTTPS) works.

---

## Hashing

A **hash function** takes input of any size and produces a fixed-size output (the **hash** or **message digest**). Hashing is a **one-way** function — you cannot recover the original input from the hash.

| Property | Description |
|----------|-------------|
| **Deterministic** | The same input always produces the same hash |
| **Fixed output size** | Regardless of input size, the output is always the same length (e.g. SHA-256 produces 256 bits) |
| **One-way** | Cannot reverse the hash to find the input |
| **Collision-resistant** | It should be extremely difficult to find two different inputs with the same hash |
| **Avalanche effect** | A tiny change in input (even one bit) produces a completely different hash |

### Uses of Hashing

| Use | How It Works |
|-----|-------------|
| **Password storage** | Store the hash of the password, not the password itself. To verify a login, hash the entered password and compare hashes. |
| **Data integrity** | Send data with its hash. The receiver hashes the received data and compares — if the hashes match, the data is unchanged. |
| **Digital signatures** | Hash the message, then encrypt the hash with the sender's private key. The recipient decrypts with the sender's public key and compares hashes. |
| **File verification** | Software downloads include checksums (hashes) so users can verify the file is complete and unaltered. |

### Salting Passwords

A **salt** is a random value added to each password **before** hashing:

1. Generate a unique random salt for each user
2. Concatenate: `salt + password`
3. Hash the combined value: `hash(salt + password)`
4. Store both the **salt** and the **hash** (the salt is not secret)

**Why salting is necessary:**
- Without salts, identical passwords produce identical hashes — an attacker who cracks one password cracks all accounts with that password
- Prevents **rainbow table attacks** (precomputed tables of hash-to-password mappings)
- Each password has a unique salt, so each must be attacked individually

---

## Cryptographic Algorithms — Worked Examples

### Caesar Cipher

The **Caesar cipher** is a simple substitution cipher that shifts each letter by a fixed number of positions in the alphabet.

**Encryption:** Replace each letter with the letter `k` positions later in the alphabet (wrapping around).

**Example with shift of 3:**

| Plaintext | A | B | C | D | E | F | ... | X | Y | Z |
|-----------|---|---|---|---|---|---|-----|---|---|---|
| Ciphertext | D | E | F | G | H | I | ... | A | B | C |

**Encrypt "HELLO" with shift 3:**

| H | E | L | L | O |
|---|---|---|---|---|
| K | H | O | O | R |

Ciphertext: **KHORR**

**Decryption:** Shift each letter back by `k` positions.

```python
def caesar_encrypt(plaintext, shift):
    result = ""
    for char in plaintext:
        if char.isalpha():
            base = ord('A') if char.isupper() else ord('a')
            result += chr((ord(char) - base + shift) % 26 + base)
        else:
            result += char
    return result

def caesar_decrypt(ciphertext, shift):
    return caesar_encrypt(ciphertext, -shift)

# Example
encrypted = caesar_encrypt("HELLO", 3)
print(encrypted)  # KHORR
print(caesar_decrypt(encrypted, 3))  # HELLO
```

```vb
Function CaesarEncrypt(plaintext As String, shift As Integer) As String
    Dim result As String = ""
    For Each ch As Char In plaintext
        If Char.IsLetter(ch) Then
            Dim base As Integer = If(Char.IsUpper(ch), Asc("A"c), Asc("a"c))
            Dim shifted As Integer = ((Asc(ch) - base + shift) Mod 26 + 26) Mod 26
            result &= Chr(shifted + base)
        Else
            result &= ch
        End If
    Next
    Return result
End Function

Function CaesarDecrypt(ciphertext As String, shift As Integer) As String
    Return CaesarEncrypt(ciphertext, 26 - shift)
End Function

' Example
Dim encrypted As String = CaesarEncrypt("HELLO", 3)
Console.WriteLine(encrypted)  ' KHORR
Console.WriteLine(CaesarDecrypt(encrypted, 3))  ' HELLO
```

**Weakness:** Only 25 possible keys — easily broken by **brute force** (trying all shifts) or **frequency analysis** (comparing letter frequencies to known language patterns).

### Vigenère Cipher

The **Vigenère cipher** uses a **keyword** to determine different shifts for each letter, making it much harder to crack than a simple Caesar cipher.

**How it works:**
1. Choose a keyword (e.g. "KEY")
2. Repeat the keyword to match the length of the plaintext
3. Each letter of the keyword determines the shift for the corresponding plaintext letter (A=0, B=1, C=2, ... Z=25)

**Example — encrypt "HELLO WORLD" with keyword "KEY":**

| Plaintext  | H | E | L | L | O | W | O | R | L | D |
|------------|---|---|---|---|---|---|---|---|---|---|
| Key letter | K | E | Y | K | E | Y | K | E | Y | K |
| Shift      | 10| 4 | 24| 10| 4 | 24| 10| 4 | 24| 10|
| Ciphertext | R | I | J | V | S | U | Y | V | J | N |

Ciphertext: **RIJVS UYVJN**

```python
def vigenere_encrypt(plaintext, keyword):
    result = ""
    key_index = 0
    keyword = keyword.upper()
    for char in plaintext:
        if char.isalpha():
            shift = ord(keyword[key_index % len(keyword)]) - ord('A')
            base = ord('A') if char.isupper() else ord('a')
            result += chr((ord(char) - base + shift) % 26 + base)
            key_index += 1
        else:
            result += char
    return result

def vigenere_decrypt(ciphertext, keyword):
    result = ""
    key_index = 0
    keyword = keyword.upper()
    for char in ciphertext:
        if char.isalpha():
            shift = ord(keyword[key_index % len(keyword)]) - ord('A')
            base = ord('A') if char.isupper() else ord('a')
            result += chr((ord(char) - base - shift) % 26 + base)
            key_index += 1
        else:
            result += char
    return result

print(vigenere_encrypt("HELLO WORLD", "KEY"))  # RIJVS UYVJN
print(vigenere_decrypt("RIJVS UYVJN", "KEY"))  # HELLO WORLD
```

```vb
Function VigenereEncrypt(plaintext As String, keyword As String) As String
    Dim result As String = ""
    Dim keyIndex As Integer = 0
    keyword = keyword.ToUpper()
    For Each ch As Char In plaintext
        If Char.IsLetter(ch) Then
            Dim shift As Integer = Asc(keyword(keyIndex Mod keyword.Length)) - Asc("A"c)
            Dim base As Integer = If(Char.IsUpper(ch), Asc("A"c), Asc("a"c))
            Dim encrypted As Integer = ((Asc(ch) - base + shift) Mod 26 + 26) Mod 26
            result &= Chr(encrypted + base)
            keyIndex += 1
        Else
            result &= ch
        End If
    Next
    Return result
End Function

Function VigenereDecrypt(ciphertext As String, keyword As String) As String
    Dim result As String = ""
    Dim keyIndex As Integer = 0
    keyword = keyword.ToUpper()
    For Each ch As Char In ciphertext
        If Char.IsLetter(ch) Then
            Dim shift As Integer = Asc(keyword(keyIndex Mod keyword.Length)) - Asc("A"c)
            Dim base As Integer = If(Char.IsUpper(ch), Asc("A"c), Asc("a"c))
            Dim decrypted As Integer = ((Asc(ch) - base - shift) Mod 26 + 26) Mod 26
            result &= Chr(decrypted + base)
            keyIndex += 1
        Else
            result &= ch
        End If
    Next
    Return result
End Function

Console.WriteLine(VigenereEncrypt("HELLO WORLD", "KEY"))  ' RIJVS UYVJN
Console.WriteLine(VigenereDecrypt("RIJVS UYVJN", "KEY"))  ' HELLO WORLD
```

**Strength:** The repeating key means simple frequency analysis does not work (the same plaintext letter maps to different ciphertext letters). However, if the key length is discovered, the cipher can be broken as multiple Caesar ciphers.

---

## Digital Certificates and PKI

### Digital Certificates

A **digital certificate** is an electronic document that binds a public key to an identity (person, organisation, or server). It is issued by a trusted **Certificate Authority (CA)**.

A certificate contains:
- The **subject's identity** (name, organisation, domain name)
- The subject's **public key**
- The **CA's digital signature** (proving the certificate is genuine)
- **Validity period** (issue date and expiry date)
- **Serial number** (unique identifier)

### Public Key Infrastructure (PKI)

**PKI** is the framework of policies, procedures, and technologies that manages digital certificates and public keys:

| Component | Role |
|-----------|------|
| **Certificate Authority (CA)** | Issues, signs, and revokes certificates. The trusted third party. |
| **Registration Authority (RA)** | Verifies the identity of certificate applicants before the CA issues a certificate |
| **Certificate Revocation List (CRL)** | A list of certificates that have been revoked before their expiry date |
| **Certificate store** | Where certificates are stored on a device (browsers have built-in stores of trusted CAs) |

### How HTTPS Works (TLS Handshake)

When a browser connects to an HTTPS website:

1. **Client Hello** — the browser sends its supported encryption algorithms and a random number
2. **Server Hello** — the server responds with its chosen algorithm, a random number, and its **digital certificate**
3. **Certificate verification** — the browser checks the certificate against its trusted CA list, verifies the digital signature, and checks the expiry date
4. **Key exchange** — the browser generates a **pre-master secret**, encrypts it with the server's **public key** (from the certificate), and sends it
5. **Session keys** — both sides derive identical **symmetric session keys** from the pre-master secret and random numbers
6. **Secure communication** — all subsequent data is encrypted using the **symmetric session key** (fast encryption for the actual data transfer)

<div class="exam-tip" markdown="1">
The HTTPS handshake combines **asymmetric** and **symmetric** encryption. Asymmetric encryption is used only for the initial key exchange (slow but solves the key distribution problem). Once both sides have the shared session key, they switch to **symmetric encryption** for speed. This hybrid approach is the foundation of secure Internet communication.
</div>
