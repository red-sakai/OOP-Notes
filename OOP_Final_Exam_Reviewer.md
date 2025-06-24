# OOP Final Exam Reviewer

## 1. String Manipulation

String manipulation is the process of handling and modifying strings (sequences of characters). Mastery of string operations is essential for parsing input, formatting output, and data processing.

- **Concatenation:** Combine two or more strings into one. In Python, use `+` or `''.join(list_of_strings)`. `join()` is more efficient for combining many strings.
- **Substring:** Extract a portion of a string using slicing (`s[start:end]`). Negative indices count from the end. Slicing does not modify the original string (strings are immutable).
- **Searching:** Use `find()` to get the index of a substring, or `in` to check for existence. `find()` returns `-1` if not found.
- **Replacing:** Use `replace(old, new)` to substitute substrings. Returns a new string.
- **Case Conversion:** `upper()`, `lower()`, `capitalize()`, `title()`, and `swapcase()` change the case of characters.
- **Trimming:** Remove whitespace with `strip()` (both ends), `lstrip()` (left), `rstrip()` (right).
- **Splitting:** Use `split(delimiter)` to break a string into a list. Use `partition()` to split at the first occurrence of a separator.
- **Joining:** Use `join()` to combine a list of strings into a single string with a separator.
- **Formatting:** Use f-strings (`f"{var}"`), `format()`, or `%` formatting for readable output.
- **Immutability:** Strings cannot be changed in place; all operations return new strings.

**Example (Python):**
```python
s = "Hello World"
sub = s[0:5]           # "Hello"
upper = s.upper()      # "HELLO WORLD"
found = "World" in s   # True
replaced = s.replace("World", "Python")  # "Hello Python"
parts = s.split()      # ["Hello", "World"]
trimmed = "  hi  ".strip()  # "hi"
```

**Advanced Examples:**
```python
sentence = "  The quick brown fox jumps over the lazy dog.  "
words = sentence.strip().split()  # ['The', 'quick', 'brown', ...]
new_sentence = '-'.join(words)    # 'The-quick-brown-fox-jumps-over-the-lazy-dog.'
index = sentence.find("fox")      # 16
formatted = f"Animal: {words[3].capitalize()}"  # 'Animal: Fox'
```

**Best Practices:**
- Prefer `join()` over repeated `+` for concatenating many strings.
- Use string methods for safe and readable code.
- Be aware of Unicode and encoding issues when handling non-ASCII text.

---

## 2. File Handling

File handling allows programs to read from and write to files on disk. This is crucial for data persistence, configuration, and logging.

- **Opening Files:** Use `open(filename, mode)` where mode is `'r'` (read), `'w'` (write), `'a'` (append), `'b'` (binary), or combinations like `'rb'`.
- **Closing Files:** Always close files to free resources. Use `with` statement to handle this automatically.
- **Reading Files:** Use `read()`, `readline()`, or `readlines()` for different reading needs. Iterating over a file object yields lines.
- **Writing Files:** Use `write()` or `writelines()`. Writing in `'w'` mode overwrites the file; `'a'` appends.
- **Exception Handling:** Always handle exceptions (e.g., `FileNotFoundError`, `IOError`) to avoid crashes.
- **Binary Files:** Use `'rb'` or `'wb'` for non-text files (images, etc.).
- **File Paths:** Use `os.path` for cross-platform path handling.

**Example (Python):**
```python
# Reading a file
with open("file.txt", "r") as reader:
    for line in reader:
        print(line.strip())

# Writing to a file
with open("file.txt", "w") as writer:
    writer.write("Hello, file!")
```

**Advanced Examples:**
```python
import os

# Check if file exists before reading
if os.path.exists("data.txt"):
    with open("data.txt", "r") as f:
        data = f.read()
else:
    print("File not found.")

# Appending to a file
with open("log.txt", "a") as log:
    log.write("New log entry\n")
```

**Best Practices:**
- Always use `with` to open files.
- Handle exceptions for robust code.
- Avoid hardcoding file paths; use variables or configuration.

---

## 3. Exception Handling

Exception handling is the process of responding to runtime errors, allowing programs to continue or fail gracefully.

- **try-except:** Wrap code that may fail in a `try` block, and handle errors in `except`.
- **Multiple excepts:** Catch different exception types separately for specific handling.
- **else:** Runs if no exception occurs.
- **finally:** Runs regardless of exceptions (useful for cleanup).
- **Raising Exceptions:** Use `raise` to trigger exceptions intentionally.
- **Custom Exceptions:** Define your own exception classes by inheriting from `Exception`.

**Example (Python):**
```python
try:
    num = int(input("Enter a number: "))
    result = 10 / num
except ValueError:
    print("Invalid input! Please enter a number.")
except ZeroDivisionError:
    print("Cannot divide by zero.")
else:
    print(f"Result is {result}")
finally:
    print("This block always executes.")
```

**Advanced Examples:**
```python
def divide(a, b):
    try:
        return a / b
    except ZeroDivisionError as e:
        print("Error:", e)
        return None

# Custom exception
class NegativeNumberError(Exception):
    pass

def check_positive(num):
    if num < 0:
        raise NegativeNumberError("Number must be positive")
```

**Best Practices:**
- Catch only exceptions you can handle.
- Avoid bare `except:`; always specify the exception type.
- Use exceptions for exceptional cases, not for normal control flow.

---

## 4. Inheritance

Inheritance allows a class (child/subclass) to acquire properties and methods from another class (parent/superclass).

- **Single Inheritance:** One parent class.
- **Multiple Inheritance:** A class inherits from multiple parents (use with care).
- **Method Overriding:** Subclass can redefine parent methods.
- **super():** Call parent methods from child class.
- **isinstance() and issubclass():** Check object/class relationships.

**Example (Python):**
```python
class Animal:
    def eat(self):
        print("Eating")

class Dog(Animal):
    def bark(self):
        print("Bark!")
```

**Advanced Examples:**
```python
class Vehicle:
    def start(self):
        print("Vehicle starting")

class Car(Vehicle):
    def start(self):
        super().start()
        print("Car ready to go!")

my_car = Car()
my_car.start()
```

**Best Practices:**
- Use inheritance for "is-a" relationships.
- Prefer composition over inheritance for code reuse when possible.
- Avoid deep inheritance hierarchies.

---

## 5. Encapsulation

Encapsulation restricts direct access to some of an object's components, which is critical for data hiding and integrity.

- **Private Attributes:** Prefix with `__` (name mangling).
- **Protected Attributes:** Prefix with `_` (convention only).
- **Public Attributes:** No prefix.
- **Getters/Setters:** Use `@property` and setter decorators for controlled access.
- **Benefits:** Prevents unintended interference, enables validation, and hides implementation details.

**Example (Python):**
```python
class Person:
    def __init__(self, name):
        self.__name = name  # private attribute

    @property
    def name(self):
        return self.__name

    @name.setter
    def name(self, n):
        self.__name = n
```

**Advanced Examples:**
```python
class Account:
    def __init__(self, balance):
        self.__balance = balance

    @property
    def balance(self):
        return self.__balance

    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount

    def withdraw(self, amount):
        if 0 < amount <= self.__balance:
            self.__balance -= amount
```

**Best Practices:**
- Use encapsulation to protect object state.
- Expose only necessary methods and properties.

---

## 6. Abstraction

Abstraction means exposing only relevant information and hiding the internal details.

- **Abstract Classes:** Use `abc.ABC` as a base class.
- **Abstract Methods:** Use `@abstractmethod` decorator; must be implemented by subclasses.
- **Interfaces:** Python does not have interfaces, but abstract base classes serve a similar purpose.
- **Benefits:** Simplifies complex systems, enforces method implementation in subclasses.

**Example (Python):**
```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def draw(self):
        pass

class Circle(Shape):
    def draw(self):
        print("Drawing Circle")
```

**Advanced Examples:**
```python
class Animal(ABC):
    @abstractmethod
    def make_sound(self):
        pass

class Cat(Animal):
    def make_sound(self):
        print("Meow")
```

**Best Practices:**
- Use abstraction to define templates for classes.
- Hide implementation details from users of your class.

---

## 7. Polymorphism

Polymorphism allows objects of different classes to be treated as objects of a common superclass.

- **Duck Typing:** In Python, if an object implements the needed method, it can be used (regardless of its class).
- **Method Overriding:** Subclasses provide specific implementations.
- **Operator Overloading:** Define special methods like `__add__`, `__str__` for custom behavior.
- **Benefits:** Enables flexible and reusable code.

**Example (Python):**
```python
def animal_sound(animal):
    animal.eat()

a = Dog()
animal_sound(a)  # Dog is-an Animal
```

**Advanced Examples:**
```python
class Cat:
    def speak(self):
        print("Meow")

class Dog:
    def speak(self):
        print("Woof")

def animal_speak(animal):
    animal.speak()

animals = [Cat(), Dog()]
for a in animals:
    animal_speak(a)
```

**Best Practices:**
- Use polymorphism to write generic, reusable code.
- Rely on interfaces/abstract base classes for consistency.

---

## 8. Classes and Objects

A class is a blueprint for creating objects. An object is an instance of a class, containing data and behavior.

- **Defining Classes:** Use the `class` keyword.
- **Constructors:** `__init__` method initializes object state.
- **Instance Attributes:** Belong to each object.
- **Class Attributes:** Shared across all instances.
- **Methods:** Functions defined inside a class.
- **Self:** Refers to the instance itself.

**Example (Python):**
```python
class Car:
    def __init__(self, brand, model):
        self.brand = brand
        self.model = model

    def drive(self):
        print(f"{self.brand} {self.model} is driving.")

my_car = Car("Toyota", "Corolla")
my_car.drive()  # Output: Toyota Corolla is driving.
```

**Advanced Examples:**
```python
class Student:
    school = "ABC University"  # class attribute

    def __init__(self, name):
        self.name = name  # instance attribute

    def greet(self):
        print(f"Hello, my name is {self.name} and I study at {Student.school}.")

s1 = Student("Alice")
s2 = Student("Bob")
s1.greet()
s2.greet()
```

**Best Practices:**
- Use classes to model real-world entities.
- Use instance attributes for unique data, class attributes for shared data.

---
