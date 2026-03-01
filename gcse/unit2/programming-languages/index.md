---
layout: topic
title: "Programming Languages"
level: "GCSE"
level_url: "/gcse/"
unit_name: "Unit 2: Computational Thinking & Programming"
unit_url: "/gcse/unit2/"
prev_topic: "/gcse/unit2/algorithms-and-constructs/"
next_topic: "/gcse/unit2/data-structures-types/"
---

## HTML: Design, write, test and refine HTML pages

**HTML (HyperText Markup Language)** is used to create the structure and content of web pages. It is not a programming language — it is a **markup language** that uses **tags** to define elements on a page.

<div class="key-term" markdown="1">
**HTML** — a markup language used to structure content on web pages. Browsers read HTML files and render them as formatted pages.
</div>

### The development process

When building a web page, you follow a cycle:

1. **Design** — plan the layout, content and purpose of the page (sketches or wireframes)
2. **Write** — create the HTML code using a text editor
3. **Test** — open the page in a browser and check it displays correctly
4. **Refine** — fix errors, improve layout and add missing content

### A minimal HTML page

```html
<!DOCTYPE html>
<html>
  <head>
    <title>My First Page</title>
  </head>
  <body>
    <h1>Welcome</h1>
    <p>This is a simple web page.</p>
  </body>
</html>
```

### Testing your page

- Open the `.html` file in **multiple browsers** (Chrome, Firefox, Edge) to check it looks correct in each
- **Validate** your HTML using an online validator to catch errors such as missing closing tags
- Ask others to **review** the page for readability and usability

<div class="exam-tip" markdown="1">
In the exam you may be asked to write or correct HTML. Always check for matching opening and closing tags, and remember that tags are **nested** — inner tags must close before outer tags.
</div>

---

## HTML tags: html, head, title, body, headings, paragraph

These are the **structural tags** that form the skeleton of every web page.

| Tag | Purpose |
|-----|---------|
| `<html>` | Root element — wraps the entire page |
| `<head>` | Contains metadata (not visible on the page itself) |
| `<title>` | Sets the text shown in the browser tab |
| `<body>` | Contains all the visible content of the page |
| `<h1>` to `<h6>` | Headings, where `<h1>` is the largest and `<h6>` the smallest |
| `<p>` | A paragraph of text |

### Example

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Structural Tags</title>
  </head>
  <body>
    <h1>Main Heading</h1>
    <h2>Sub Heading</h2>
    <h3>Smaller Heading</h3>
    <p>This is a paragraph of text. It will wrap to fill the width of the browser window.</p>
    <p>This is a second paragraph. Each paragraph has space above and below it.</p>
  </body>
</html>
```

<div class="key-term" markdown="1">
**Tag** — an HTML keyword surrounded by angle brackets, e.g. `<p>`. Most tags come in pairs: an **opening tag** (`<p>`) and a **closing tag** (`</p>`).
</div>

<div class="exam-tip" markdown="1">
Remember the difference between `<head>` and `<body>`. The `<head>` holds information *about* the page (title, character set). The `<body>` holds everything the user actually *sees*.
</div>

---

## HTML tags: italic, bold, center, anchor, mailto

These tags control **text formatting** and **links**.

| Tag | Purpose | Example |
|-----|---------|---------|
| `<i>` | Italic text | `<i>slanted text</i>` |
| `<b>` | Bold text | `<b>strong text</b>` |
| `<center>` | Centres content on the page | `<center>centred text</center>` |
| `<a>` | Anchor — creates a hyperlink | `<a href="url">link text</a>` |
| `mailto:` | Used inside an anchor to create an email link | `<a href="mailto:name@example.com">Email us</a>` |

### Example: formatting and links

```html
<body>
  <p>This word is <b>bold</b> and this word is <i>italic</i>.</p>

  <center>
    <p>This paragraph is centred on the page.</p>
  </center>

  <p>Visit <a href="https://www.bbc.co.uk">BBC News</a> for the latest stories.</p>

  <p>Contact us: <a href="mailto:info@school.co.uk">info@school.co.uk</a></p>
</body>
```

### How anchors work

The `<a>` tag uses the **href** attribute to specify where the link goes:

- **Web link**: `<a href="https://www.example.com">Click here</a>`
- **Email link**: `<a href="mailto:user@example.com">Send email</a>`
- **Link to another page on the same site**: `<a href="about.html">About Us</a>`

<div class="exam-tip" markdown="1">
You must know the exact syntax for anchor tags. The `href` attribute goes inside the opening `<a>` tag, and the clickable text goes between the opening and closing tags.
</div>

---

## HTML tags: unordered list, list item, blockquote, hr, image

These tags handle **lists**, **quotations**, **dividers** and **images**.

| Tag | Purpose |
|-----|---------|
| `<ul>` | Unordered (bullet point) list |
| `<li>` | A single list item inside `<ul>` |
| `<blockquote>` | Indented block of quoted text |
| `<hr>` | Horizontal rule — a dividing line across the page (self-closing) |
| `<img>` | Displays an image (self-closing) |

### Example

```html
<body>
  <h2>Shopping List</h2>
  <ul>
    <li>Bread</li>
    <li>Milk</li>
    <li>Eggs</li>
  </ul>

  <hr>

  <blockquote>
    "The only way to learn a new programming language is by writing programs in it."
    — Dennis Ritchie
  </blockquote>

  <hr>

  <img src="photo.jpg" alt="A description of the image" width="400">
</body>
```

### The image tag in detail

The `<img>` tag uses attributes rather than wrapping content:

- **src** — the file path or URL of the image
- **alt** — alternative text shown if the image cannot load (also used by screen readers)
- **width** / **height** — optional size control in pixels

```html
<img src="images/logo.png" alt="School logo" width="200" height="100">
```

<div class="key-term" markdown="1">
**Self-closing tag** — a tag that does not need a separate closing tag. Examples include `<img>`, `<hr>` and `<br>` (line break).
</div>

---

## Greenfoot/Java: Create and extend classes

In **object-oriented programming (OOP)**, a **class** is a blueprint for creating objects. In Greenfoot, you build programs by creating classes that extend (inherit from) existing classes.

<div class="key-term" markdown="1">
**Class** — a template that defines the properties (data) and methods (behaviour) that objects of that type will have.
</div>

### Creating a class in Greenfoot/Java

```java
public class Crab extends Actor {
    // This class inherits all the behaviour of Actor
    // and can add its own methods and properties
}
```

- `public` means the class can be accessed from anywhere
- `extends Actor` means `Crab` **inherits** all the features of the `Actor` class
- Greenfoot provides built-in classes: `World`, `Actor`, `GreenfootImage`, `Greenfoot`

### The same concept in Python

In Python, classes work in a similar way:

```python
class Crab(Actor):
    # This class inherits from Actor
    def __init__(self):
        super().__init__()
```

### The same concept in VB.NET

```vb
Public Class Crab
    Inherits Actor

    ' This class inherits from Actor
End Class
```

<div class="exam-tip" markdown="1">
In Greenfoot, every character or item on screen is a subclass of `Actor`, and the background/level is a subclass of `World`. Know this hierarchy for the exam.
</div>

---

## Greenfoot/Java: Create and edit objects and worlds

An **object** is a specific **instance** of a class. A **world** is the environment (screen) where objects are placed and interact.

<div class="key-term" markdown="1">
**Object** — a specific instance created from a class. For example, if `Crab` is the class, then a particular crab on screen is an object.
</div>

### Creating a world

```java
public class CrabWorld extends World {
    public CrabWorld() {
        super(600, 400, 1);  // width, height, cell size
    }
}
```

### Creating objects and adding them to the world

```java
public class CrabWorld extends World {
    public CrabWorld() {
        super(600, 400, 1);

        // Create objects from classes
        Crab myCrab = new Crab();
        Lobster myLobster = new Lobster();

        // Place them in the world at x, y coordinates
        addObject(myCrab, 300, 200);
        addObject(myLobster, 100, 100);
    }
}
```

### Python equivalent

```python
class CrabWorld:
    def __init__(self):
        self.width = 600
        self.height = 400

        # Create objects
        my_crab = Crab()
        my_lobster = Lobster()
```

### VB.NET equivalent

```vb
Public Class CrabWorld
    Public Sub New()
        Dim myCrab As New Crab()
        Dim myLobster As New Lobster()
    End Sub
End Class
```

<div class="exam-tip" markdown="1">
When creating an object in Java, the keyword `new` is required: `Crab myCrab = new Crab();`. Forgetting `new` is a common error.
</div>

---

## Greenfoot/Java: Write and invoke methods

A **method** is a block of code inside a class that performs a specific task. You **invoke** (call) a method to run its code.

<div class="key-term" markdown="1">
**Method** — a named block of code that belongs to a class. Methods define what an object can *do*.
</div>

### Writing a method

```java
public class Crab extends Actor {

    public void act() {
        move(5);
        turn(2);
    }

    public void eatWorm() {
        Actor worm = getOneIntersectingObject(Worm.class);
        if (worm != null) {
            getWorld().removeObject(worm);
        }
    }
}
```

- `public void act()` — the `act()` method runs repeatedly in Greenfoot
- `void` means the method does not return a value
- `eatWorm()` is a custom method that checks for a collision with a worm

### Invoking (calling) a method

```java
public void act() {
    move(5);       // calls the built-in move method
    eatWorm();     // calls our custom method
}
```

### Python equivalent

```python
class Crab:
    def act(self):
        self.move(5)
        self.turn(2)

    def eat_worm(self):
        worm = self.get_intersecting("Worm")
        if worm is not None:
            self.world.remove(worm)
```

### VB.NET equivalent

```vb
Public Class Crab
    Public Sub Act()
        Move(5)
        Turn(2)
    End Sub

    Public Sub EatWorm()
        Dim worm As Actor = GetOneIntersectingObject(GetType(Worm))
        If worm IsNot Nothing Then
            GetWorld().RemoveObject(worm)
        End If
    End Sub
End Class
```

---

## Greenfoot/Java: Properties (public, private, static)

**Properties** (also called **fields** or **attributes**) store data inside a class. **Access modifiers** control which parts of the program can see and change them.

| Modifier | Meaning |
|----------|---------|
| `public` | Accessible from **any** class |
| `private` | Accessible only from **within the same class** |
| `static` | Belongs to the **class itself**, not to individual objects — shared by all instances |

### Example in Java

```java
public class Crab extends Actor {
    private int speed = 5;         // only this class can access speed
    public String name = "Crabby"; // any class can access name
    static int crabCount = 0;      // shared across all Crab objects

    public Crab() {
        crabCount++;  // every time a new Crab is made, the count goes up
    }
}
```

### Python equivalent

Python uses naming conventions instead of strict access modifiers:

```python
class Crab:
    crab_count = 0  # class variable (like static)

    def __init__(self):
        self._speed = 5         # _ prefix suggests private by convention
        self.name = "Crabby"    # public attribute
        Crab.crab_count += 1
```

### VB.NET equivalent

```vb
Public Class Crab
    Private speed As Integer = 5
    Public name As String = "Crabby"
    Shared crabCount As Integer = 0   ' Shared is VB.NET's static

    Public Sub New()
        crabCount += 1
    End Sub
End Class
```

<div class="key-term" markdown="1">
**Private** properties enforce **data hiding** — other classes cannot directly change the data, which protects it from accidental modification. This is a key part of **encapsulation**.
</div>

<div class="exam-tip" markdown="1">
Use `private` for properties and provide `public` methods to get or set them (getters/setters). This is good programming practice and is often tested in the exam.
</div>

---

## Greenfoot/Java: Add/remove objects, use actors, move objects

In Greenfoot, you manage the objects in the world by adding, removing and moving them.

### Adding objects

```java
// Inside a World subclass
Crab crab = new Crab();
addObject(crab, 300, 200);  // adds crab at position (300, 200)
```

### Removing objects

```java
// Remove a specific object from the world
getWorld().removeObject(this);  // removes the current actor

// Remove another object
getWorld().removeObject(worm);
```

### Using actors

Every object placed in the world is an **Actor**. Actors have built-in methods:

| Method | Purpose |
|--------|---------|
| `move(int distance)` | Moves the actor forward by the given number of pixels |
| `turn(int degrees)` | Rotates the actor by the given angle |
| `setLocation(int x, int y)` | Places the actor at a specific position |
| `getX()` / `getY()` | Returns the actor's current x or y coordinate |
| `setRotation(int angle)` | Sets the direction the actor faces |

### Moving objects

```java
public class Crab extends Actor {
    public void act() {
        move(3);  // move 3 pixels in the current direction

        // Wrap around: if the crab reaches the edge, appear on the other side
        if (getX() >= getWorld().getWidth() - 1) {
            setLocation(0, getY());
        }
    }
}
```

<div class="exam-tip" markdown="1">
The `act()` method is called repeatedly by Greenfoot — roughly 60 times per second at normal speed. This is what creates animation and interactivity.
</div>

---

## Greenfoot/Java: Keyboard input, sounds

### Keyboard input

Greenfoot provides the `Greenfoot.isKeyDown()` method to detect when a key is pressed:

```java
public class Player extends Actor {
    public void act() {
        if (Greenfoot.isKeyDown("left")) {
            move(-5);
        }
        if (Greenfoot.isKeyDown("right")) {
            move(5);
        }
        if (Greenfoot.isKeyDown("up")) {
            setLocation(getX(), getY() - 5);
        }
        if (Greenfoot.isKeyDown("down")) {
            setLocation(getX(), getY() + 5);
        }
    }
}
```

You can also check for a single key press (rather than holding the key down):

```java
String key = Greenfoot.getKey();  // returns the key pressed, or null
if ("space".equals(key)) {
    fire();
}
```

### Playing sounds

Greenfoot can play sound files stored in the project's `sounds` folder:

```java
Greenfoot.playSound("crunch.wav");  // plays the sound once
```

Place the sound file (`.wav` or `.mp3`) in the `sounds` folder of your Greenfoot project.

```java
public void eatWorm() {
    Actor worm = getOneIntersectingObject(Worm.class);
    if (worm != null) {
        Greenfoot.playSound("chomp.wav");
        getWorld().removeObject(worm);
    }
}
```

<div class="exam-tip" markdown="1">
Remember: `Greenfoot.isKeyDown()` checks if a key is currently held down (returns `true`/`false`). `Greenfoot.getKey()` returns the name of the last key pressed as a `String`, or `null` if no key was pressed.
</div>

---

## Greenfoot/Java: Parameter passing (by value and reference)

When you call a method and pass data to it, the data is called a **parameter** (or **argument**). There are two ways parameters can be passed.

<div class="key-term" markdown="1">
**Parameter passing by value** — a **copy** of the data is sent to the method. Changes inside the method do **not** affect the original variable.

**Parameter passing by reference** — a **reference (address)** to the original data is sent. Changes inside the method **do** affect the original data.
</div>

### By value — Java (primitives)

In Java, **primitive types** (int, double, boolean, char) are passed **by value**:

```java
public void doubleSpeed(int speed) {
    speed = speed * 2;  // only changes the local copy
}

// Calling code
int mySpeed = 5;
doubleSpeed(mySpeed);
// mySpeed is still 5 — the original was not changed
```

### By reference — Java (objects)

In Java, **objects** are passed **by reference** (technically, the reference itself is passed by value, but the effect is the same — the original object can be modified):

```java
public void resetCrab(Crab c) {
    c.setLocation(0, 0);  // this changes the actual Crab object
}
```

### Python equivalent

Python passes all arguments by **object reference**. Immutable types (int, str, tuple) behave like by value; mutable types (list, dict) behave like by reference:

```python
# Behaves like by value (int is immutable)
def double_speed(speed):
    speed = speed * 2  # local change only

my_speed = 5
double_speed(my_speed)
# my_speed is still 5

# Behaves like by reference (list is mutable)
def add_item(items):
    items.append("new")  # changes the original list

my_list = ["a", "b"]
add_item(my_list)
# my_list is now ["a", "b", "new"]
```

### VB.NET equivalent

VB.NET lets you explicitly choose using **ByVal** and **ByRef**:

```vb
' By value — original not changed
Sub DoubleSpeed(ByVal speed As Integer)
    speed = speed * 2
End Sub

' By reference — original IS changed
Sub DoubleSpeed(ByRef speed As Integer)
    speed = speed * 2
End Sub

Dim mySpeed As Integer = 5
DoubleSpeed(mySpeed)
' With ByVal: mySpeed is still 5
' With ByRef: mySpeed is now 10
```

<div class="exam-tip" markdown="1">
This is a commonly tested concept. Remember: **by value = copy** (original unchanged), **by reference = address** (original can change). In VB.NET, `ByVal` and `ByRef` make this explicit.
</div>

---

## Greenfoot/Java: Access objects, collision detection, random numbers

### Accessing other objects

In Greenfoot, actors can find and interact with other actors in the world:

```java
// Get a list of all Worm objects in the world
java.util.List<Worm> worms = getWorld().getObjects(Worm.class);

// Get the world reference
World world = getWorld();
```

### Collision detection

Greenfoot provides built-in methods for detecting when actors touch or overlap:

| Method | Returns | Purpose |
|--------|---------|---------|
| `isTouching(Class cls)` | `boolean` | True if this actor is touching any object of the given class |
| `getOneIntersectingObject(Class cls)` | `Actor` | Returns one overlapping object, or `null` |
| `getIntersectingObjects(Class cls)` | `List` | Returns all overlapping objects of the given class |
| `removeTouching(Class cls)` | `void` | Removes one touching object of the given class |

```java
public void act() {
    if (isTouching(Worm.class)) {
        removeTouching(Worm.class);
        Greenfoot.playSound("slurp.wav");
    }
}
```

A more detailed approach:

```java
public void checkCollision() {
    Actor worm = getOneIntersectingObject(Worm.class);
    if (worm != null) {
        // A collision has occurred
        getWorld().removeObject(worm);
        score++;
    }
}
```

### Random numbers

The `Greenfoot.getRandomNumber(int limit)` method returns a random integer from 0 up to (but not including) the limit:

```java
int random = Greenfoot.getRandomNumber(100);  // 0 to 99

// Random direction change
if (Greenfoot.getRandomNumber(100) < 10) {
    turn(Greenfoot.getRandomNumber(90) - 45);  // turn between -45 and +44 degrees
}
```

### Python equivalent

```python
import random

value = random.randint(0, 99)  # 0 to 99 inclusive

# Random direction change
if random.randint(0, 99) < 10:
    turn(random.randint(-45, 44))
```

### VB.NET equivalent

```vb
Dim rng As New Random()
Dim value As Integer = rng.Next(0, 100)  ' 0 to 99

If rng.Next(0, 100) < 10 Then
    Turn(rng.Next(-45, 45))
End If
```

---

## Greenfoot/Java: Inheritance and encapsulation

### Inheritance

**Inheritance** allows a new class to take on (inherit) the properties and methods of an existing class, then add or override them.

<div class="key-term" markdown="1">
**Inheritance** — when a **subclass** (child class) inherits all the properties and methods of a **superclass** (parent class). The subclass can add new behaviour or override existing behaviour.
</div>

```java
// Superclass
public class Animal extends Actor {
    public void move(int distance) {
        setLocation(getX() + distance, getY());
    }

    public void makeSound() {
        // default: no sound
    }
}

// Subclass — inherits from Animal
public class Crab extends Animal {
    @Override
    public void makeSound() {
        Greenfoot.playSound("click.wav");  // overrides parent method
    }

    public void pinch() {
        // new method only Crab has
    }
}
```

#### Python equivalent

```python
class Animal:
    def move(self, distance):
        self.x += distance

    def make_sound(self):
        pass  # default: no sound

class Crab(Animal):
    def make_sound(self):
        play_sound("click.wav")  # overrides parent method

    def pinch(self):
        pass  # new method only Crab has
```

#### VB.NET equivalent

```vb
Public Class Animal
    Public Overridable Sub MakeSound()
        ' default: no sound
    End Sub
End Class

Public Class Crab
    Inherits Animal

    Public Overrides Sub MakeSound()
        PlaySound("click.wav")
    End Sub

    Public Sub Pinch()
        ' new method only Crab has
    End Sub
End Class
```

### Encapsulation

**Encapsulation** means bundling data (properties) and the methods that operate on that data inside a single class, and **hiding the internal details** from outside code.

<div class="key-term" markdown="1">
**Encapsulation** — the principle of keeping an object's data **private** and only allowing access through **public methods** (getters and setters). This protects the data from being changed in unexpected ways.
</div>

```java
public class Player extends Actor {
    private int score = 0;    // hidden from other classes
    private int lives = 3;

    // Public getter — allows reading the score
    public int getScore() {
        return score;
    }

    // Public setter — controls how the score changes
    public void addScore(int points) {
        if (points > 0) {
            score += points;
        }
    }

    // Public getter for lives
    public int getLives() {
        return lives;
    }
}
```

#### Python equivalent

```python
class Player:
    def __init__(self):
        self.__score = 0   # name mangling makes it harder to access directly
        self.__lives = 3

    def get_score(self):
        return self.__score

    def add_score(self, points):
        if points > 0:
            self.__score += points

    def get_lives(self):
        return self.__lives
```

#### VB.NET equivalent

```vb
Public Class Player
    Private _score As Integer = 0
    Private _lives As Integer = 3

    Public ReadOnly Property Score As Integer
        Get
            Return _score
        End Get
    End Property

    Public Sub AddScore(points As Integer)
        If points > 0 Then
            _score += points
        End If
    End Sub

    Public ReadOnly Property Lives As Integer
        Get
            Return _lives
        End Get
    End Property
End Class
```

### Why encapsulation matters

| Without Encapsulation | With Encapsulation |
|-----------------------|--------------------|
| Any code can directly change `score` to any value | Only the `addScore()` method can change the score |
| Bugs are hard to track down | Changes are controlled and validated |
| Changing the internal structure breaks other code | Internal changes don't affect other classes |

<div class="exam-tip" markdown="1">
Inheritance and encapsulation are two of the four pillars of OOP (along with **abstraction** and **polymorphism**). You should be able to explain what each one means and give an example. In Greenfoot, inheritance is visible in the class hierarchy on the right side of the screen.
</div>

---

## Assembly language: INP, OUT, STA, LDA

**Assembly language** is a **low-level programming language** that uses short **mnemonics** (abbreviations) to represent machine code instructions. The exam uses the **Little Man Computer (LMC)** instruction set.

<div class="key-term" markdown="1">
**Assembly language** — a low-level language where each instruction corresponds to a single machine code operation. It is specific to a particular type of CPU.

**LMC (Little Man Computer)** — a simplified model of a computer used to teach assembly language. It has an accumulator, memory (mailboxes), an input tray and an output tray.
</div>

### Core instructions

| Mnemonic | Full Name | What it Does |
|----------|-----------|--------------|
| `INP` | Input | Takes a value from the user and stores it in the **accumulator** |
| `OUT` | Output | Outputs the value currently in the **accumulator** |
| `STA` | Store | Copies the value from the accumulator into a **memory location** |
| `LDA` | Load | Copies a value from a **memory location** into the accumulator |

### Example: Input a number and output it

```text
      INP         ; get a number from the user
      STA num     ; store it in memory location 'num'
      LDA num     ; load it back into the accumulator
      OUT         ; display the value
      HLT         ; stop the program
num   DAT         ; reserve a memory location called 'num'
```

### Example: Input two numbers and output the first

```text
      INP         ; input the first number
      STA first   ; store in 'first'
      INP         ; input the second number
      STA second  ; store in 'second'
      LDA first   ; load the first number back
      OUT         ; output it
      HLT
first DAT
second DAT
```

### How it works step by step

1. `INP` — the user types a number, which goes into the **accumulator**
2. `STA first` — the accumulator value is **copied** to the memory location labelled `first`
3. The accumulator still holds the value — `STA` copies, it does not move
4. `LDA first` — the value at memory location `first` is **loaded** into the accumulator (overwriting whatever was there)
5. `OUT` — the accumulator value is displayed to the user

<div class="exam-tip" markdown="1">
Remember that the accumulator can only hold **one value** at a time. If you need to keep a value for later, you must `STA` it to a named memory location before the accumulator is overwritten.
</div>

---

## Assembly language: ADD, SUB, BRA, HLT, DAT

These instructions handle **arithmetic**, **branching** (jumping to different parts of the program) and **program control**.

| Mnemonic | Full Name | What it Does |
|----------|-----------|--------------|
| `ADD` | Add | Adds the value at a memory location to the accumulator |
| `SUB` | Subtract | Subtracts the value at a memory location from the accumulator |
| `BRA` | Branch Always | Jumps to a labelled instruction (unconditional) |
| `BRZ` | Branch if Zero | Jumps to a labelled instruction **only if** the accumulator is zero |
| `BRP` | Branch if Positive | Jumps to a labelled instruction **only if** the accumulator is zero or positive |
| `HLT` | Halt | Stops the program |
| `DAT` | Data | Reserves a memory location, optionally with an initial value |

### Example: Add two numbers

```text
      INP         ; input first number
      STA num1    ; store it
      INP         ; input second number
      STA num2    ; store it
      LDA num1    ; load first number
      ADD num2    ; add second number to it
      OUT         ; output the result
      HLT
num1  DAT
num2  DAT
```

### Example: Subtract two numbers

```text
      INP         ; input first number
      STA num1
      INP         ; input second number
      STA num2
      LDA num1
      SUB num2    ; subtract second from first
      OUT         ; output the result
      HLT
num1  DAT
num2  DAT
```

### Example: Countdown from a number using branching

```text
      INP         ; input the starting number
      STA count
loop  LDA count   ; load the current count
      OUT         ; output it
      SUB one     ; subtract 1
      STA count   ; store the new count
      BRP loop    ; if count >= 0, go back to 'loop'
      HLT
count DAT
one   DAT 1       ; a constant with value 1
```

### How branching works

- `BRA loop` — **always** jumps to the line labelled `loop` (like a `while True` loop)
- `BRZ done` — jumps to `done` **only if** the accumulator equals zero (like `if x == 0`)
- `BRP loop` — jumps to `loop` **only if** the accumulator is zero or positive (like `if x >= 0`)

### Example: Compare two numbers and output the larger

```text
        INP
        STA num1
        INP
        STA num2
        LDA num1
        SUB num2     ; num1 - num2
        BRP first    ; if result >= 0, num1 is larger
        LDA num2     ; otherwise load num2
        OUT
        BRA done
first   LDA num1
        OUT
done    HLT
num1    DAT
num2    DAT
```

### Summary of LMC instruction set

| Instruction | Code | Purpose |
|-------------|------|---------|
| `INP` | 901 | Input to accumulator |
| `OUT` | 902 | Output from accumulator |
| `LDA` | 5xx | Load from memory |
| `STA` | 3xx | Store to memory |
| `ADD` | 1xx | Add to accumulator |
| `SUB` | 2xx | Subtract from accumulator |
| `BRA` | 6xx | Branch always |
| `BRZ` | 7xx | Branch if zero |
| `BRP` | 8xx | Branch if positive/zero |
| `HLT` | 000 | Halt program |
| `DAT` | — | Define a data location |

<div class="key-term" markdown="1">
**DAT** — used at the end of an LMC program to reserve named memory locations. `DAT` on its own reserves empty space; `DAT 1` reserves space and sets the initial value to 1.
</div>

<div class="exam-tip" markdown="1">
In exam questions, you may be asked to **trace** through an LMC program. Write out a table with columns for each memory location and the accumulator, then work through line by line updating values. Always check the branching conditions carefully.
</div>
