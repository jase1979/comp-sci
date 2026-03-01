---
layout: topic
title: "Security & Authentication"
level: "GCSE"
level_url: "/gcse/"
unit_name: "Unit 2: Computational Thinking & Programming"
unit_url: "/gcse/unit2/"
prev_topic: "/gcse/unit2/data-structures-types/"
---

## Security techniques: Validation and authentication

Security in programming means ensuring that data is **correct**, **safe**, and that only **authorised users** can access the system. Two key techniques are **validation** and **authentication**.

---

### Validation

<div class="key-term" markdown="1">
**Validation** — an automatic check performed by a program to ensure that data entered is **reasonable and sensible** before it is processed. Validation does **not** check if data is correct — only that it is plausible.
</div>

#### Types of validation check

| Check | Description | Example |
|-------|-------------|---------|
| **Range check** | Ensures data falls within a specified range | Age must be between 0 and 120 |
| **Type check** | Ensures data is the correct data type | Age must be an integer, not text |
| **Length check** | Ensures data is the correct number of characters | Password must be at least 8 characters |
| **Presence check** | Ensures a field is not left blank | Username must be entered |
| **Format check** | Ensures data matches a required pattern | Email must contain @ and a domain |
| **Lookup check** | Ensures data matches a value in a predefined list | Country must be in a list of valid countries |

#### Range check example

```python
# Python - Range check
while True:
    age = int(input("Enter your age: "))
    if 0 <= age <= 120:
        print("Valid age entered.")
        break
    else:
        print("Error: Age must be between 0 and 120.")
```

```vb
' VB.NET - Range check
Dim age As Integer
Do
    Console.Write("Enter your age: ")
    age = CInt(Console.ReadLine())
    If age < 0 Or age > 120 Then
        Console.WriteLine("Error: Age must be between 0 and 120.")
    End If
Loop Until age >= 0 And age <= 120
Console.WriteLine("Valid age entered.")
```

#### Length check example

```python
# Python - Length check
while True:
    password = input("Enter a password (min 8 characters): ")
    if len(password) >= 8:
        print("Password accepted.")
        break
    else:
        print("Error: Password must be at least 8 characters.")
```

```vb
' VB.NET - Length check
Dim password As String
Do
    Console.Write("Enter a password (min 8 characters): ")
    password = Console.ReadLine()
    If Len(password) < 8 Then
        Console.WriteLine("Error: Password must be at least 8 characters.")
    End If
Loop Until Len(password) >= 8
Console.WriteLine("Password accepted.")
```

#### Presence check example

```python
# Python - Presence check
while True:
    username = input("Enter your username: ")
    if username != "":
        print("Username accepted.")
        break
    else:
        print("Error: Username cannot be blank.")
```

```vb
' VB.NET - Presence check
Dim username As String
Do
    Console.Write("Enter your username: ")
    username = Console.ReadLine()
    If username = "" Then
        Console.WriteLine("Error: Username cannot be blank.")
    End If
Loop Until username <> ""
Console.WriteLine("Username accepted.")
```

#### Type check example

```python
# Python - Type check
while True:
    user_input = input("Enter a whole number: ")
    if user_input.isdigit():
        number = int(user_input)
        print("Valid number entered:", number)
        break
    else:
        print("Error: You must enter a whole number.")
```

```vb
' VB.NET - Type check
Dim number As Integer
Dim valid As Boolean = False
Do
    Console.Write("Enter a whole number: ")
    valid = Integer.TryParse(Console.ReadLine(), number)
    If Not valid Then
        Console.WriteLine("Error: You must enter a whole number.")
    End If
Loop Until valid
Console.WriteLine("Valid number entered: " & number)
```

#### Lookup check example

```python
# Python - Lookup check
valid_colours = ["red", "green", "blue", "yellow"]
while True:
    colour = input("Enter a colour (red/green/blue/yellow): ").lower()
    if colour in valid_colours:
        print("Valid colour selected:", colour)
        break
    else:
        print("Error: Must be one of", valid_colours)
```

```vb
' VB.NET - Lookup check
Dim validColours() As String = {"red", "green", "blue", "yellow"}
Dim colour As String
Do
    Console.Write("Enter a colour (red/green/blue/yellow): ")
    colour = Console.ReadLine().ToLower()
    If Not validColours.Contains(colour) Then
        Console.WriteLine("Error: Must be red, green, blue or yellow.")
    End If
Loop Until validColours.Contains(colour)
Console.WriteLine("Valid colour selected: " & colour)
```

#### Combining multiple validation checks

In a real program you would typically combine several checks. For example, a registration form might validate a username with a **presence check** and a **length check**, and validate an age with a **type check** and a **range check**.

```python
# Python - Combined validation
def get_valid_username():
    while True:
        username = input("Enter username (3-20 characters): ")
        if username == "":
            print("Error: Username cannot be blank.")
        elif len(username) < 3 or len(username) > 20:
            print("Error: Username must be 3-20 characters.")
        else:
            return username

def get_valid_age():
    while True:
        user_input = input("Enter your age: ")
        if not user_input.isdigit():
            print("Error: Age must be a whole number.")
        elif int(user_input) < 0 or int(user_input) > 120:
            print("Error: Age must be between 0 and 120.")
        else:
            return int(user_input)

username = get_valid_username()
age = get_valid_age()
print(f"Welcome {username}, age {age}")
```

```vb
' VB.NET - Combined validation
Function GetValidUsername() As String
    Dim username As String
    Do
        Console.Write("Enter username (3-20 characters): ")
        username = Console.ReadLine()
        If username = "" Then
            Console.WriteLine("Error: Username cannot be blank.")
        ElseIf Len(username) < 3 Or Len(username) > 20 Then
            Console.WriteLine("Error: Username must be 3-20 characters.")
        End If
    Loop Until username <> "" And Len(username) >= 3 And Len(username) <= 20
    Return username
End Function

Function GetValidAge() As Integer
    Dim age As Integer
    Dim valid As Boolean = False
    Do
        Console.Write("Enter your age: ")
        valid = Integer.TryParse(Console.ReadLine(), age)
        If Not valid Then
            Console.WriteLine("Error: Age must be a whole number.")
        ElseIf age < 0 Or age > 120 Then
            Console.WriteLine("Error: Age must be between 0 and 120.")
            valid = False
        End If
    Loop Until valid
    Return age
End Function

Dim username As String = GetValidUsername()
Dim age As Integer = GetValidAge()
Console.WriteLine("Welcome " & username & ", age " & age)
```

<div class="exam-tip" markdown="1">
Validation checks that data is **reasonable**, not that it is **correct**. For example, a range check can confirm an age is between 0 and 120, but it cannot tell if the user actually entered their real age. You may also be asked to write pseudocode or a program that implements a specific validation check — always use a **loop** so the user can re-enter data if it fails.
</div>

---

### Authentication

<div class="key-term" markdown="1">
**Authentication** — the process of verifying a user's identity to confirm they are who they claim to be. This prevents unauthorised access to a system or its data.
</div>

#### Common authentication methods

| Method | How it works | Strengths | Weaknesses |
|--------|-------------|-----------|------------|
| **Username & password** | User enters credentials matched against stored records | Simple to implement, familiar | Passwords can be guessed, stolen, or shared |
| **Two-factor authentication (2FA)** | Requires two different types of proof (e.g. password + SMS code) | Much harder to bypass | Slower, relies on second device |
| **Biometric** | Uses unique physical features (fingerprint, face, iris) | Very hard to fake, convenient | Expensive hardware, privacy concerns |
| **Email/SMS verification** | A one-time code is sent to a registered device | Confirms ownership of device | Delays, relies on network access |

#### Simple password authentication

```python
# Python - Username and password authentication
stored_username = "admin"
stored_password = "SecurePass123"
max_attempts = 3

for attempt in range(max_attempts):
    username = input("Username: ")
    password = input("Password: ")
    if username == stored_username and password == stored_password:
        print("Access granted. Welcome!")
        break
    else:
        remaining = max_attempts - attempt - 1
        print(f"Incorrect. {remaining} attempts remaining.")
else:
    print("Account locked. Too many failed attempts.")
```

```vb
' VB.NET - Username and password authentication
Dim storedUsername As String = "admin"
Dim storedPassword As String = "SecurePass123"
Dim maxAttempts As Integer = 3
Dim authenticated As Boolean = False

For attempt As Integer = 1 To maxAttempts
    Console.Write("Username: ")
    Dim username As String = Console.ReadLine()
    Console.Write("Password: ")
    Dim password As String = Console.ReadLine()
    If username = storedUsername And password = storedPassword Then
        Console.WriteLine("Access granted. Welcome!")
        authenticated = True
        Exit For
    Else
        Console.WriteLine("Incorrect. " & (maxAttempts - attempt) & " attempts remaining.")
    End If
Next
If Not authenticated Then
    Console.WriteLine("Account locked. Too many failed attempts.")
End If
```

#### Password strength requirements

A secure authentication system should enforce strong passwords:

- **Minimum length** (e.g. 8 characters)
- **Mix of character types** — uppercase, lowercase, numbers, symbols
- **No common words** — dictionary words or "password123" should be rejected
- **Limited attempts** — lock the account after a number of failed attempts

```python
# Python - Password strength checker
def check_password_strength(password):
    if len(password) < 8:
        return "Too short - must be at least 8 characters"
    has_upper = any(c.isupper() for c in password)
    has_lower = any(c.islower() for c in password)
    has_digit = any(c.isdigit() for c in password)
    has_symbol = any(not c.isalnum() for c in password)
    if not (has_upper and has_lower and has_digit and has_symbol):
        return "Must contain uppercase, lowercase, digit and symbol"
    return "Strong password"

password = input("Choose a password: ")
result = check_password_strength(password)
print(result)
```

```vb
' VB.NET - Password strength checker
Function CheckPasswordStrength(password As String) As String
    If Len(password) < 8 Then
        Return "Too short - must be at least 8 characters"
    End If
    Dim hasUpper As Boolean = False
    Dim hasLower As Boolean = False
    Dim hasDigit As Boolean = False
    Dim hasSymbol As Boolean = False
    For Each c As Char In password
        If Char.IsUpper(c) Then hasUpper = True
        If Char.IsLower(c) Then hasLower = True
        If Char.IsDigit(c) Then hasDigit = True
        If Not Char.IsLetterOrDigit(c) Then hasSymbol = True
    Next
    If Not (hasUpper And hasLower And hasDigit And hasSymbol) Then
        Return "Must contain uppercase, lowercase, digit and symbol"
    End If
    Return "Strong password"
End Function

Console.Write("Choose a password: ")
Dim password As String = Console.ReadLine()
Console.WriteLine(CheckPasswordStrength(password))
```

<div class="exam-tip" markdown="1">
Know the difference between **validation** and **authentication**. Validation checks that **data** is reasonable. Authentication checks that a **user** is who they say they are. You may be asked to write a program that combines both — for example, validating the format of a password before using it to authenticate a user.
</div>

---

### Verification vs validation

It's important to distinguish validation from **verification**:

| | Validation | Verification |
|---|-----------|-------------|
| **Purpose** | Checks data is reasonable and within rules | Checks data has been entered or transferred correctly |
| **When** | Before data is processed | During or after data entry/transfer |
| **How** | Automated checks (range, type, length, etc.) | Human checks (proofreading) or system checks (double entry, checksums) |
| **Example** | Checking age is between 0-120 | Asking user to type their email twice to confirm |

<div class="key-term" markdown="1">
**Verification** — the process of checking that data has been accurately entered or transferred. Methods include **double entry** (entering data twice and comparing), **proofreading** (visually checking), and **check digits** (calculated values appended to data for error detection).
</div>
